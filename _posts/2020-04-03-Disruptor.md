---
layout: post
title:  "Disruptor"
date:   2020-04-03 09:26:47 +0800
categories: Java
---

# Disruptor

## demo

```java
 private void initDisruptor() {
    // 必须是 2^n
    int bufferSize = 1024 << 2;
    // 多生产者，生产、消费 CacheEvent，队列满等待
    disruptor = new Disruptor<>(CacheEvent::new, bufferSize, Executors.defaultThreadFactory(),
            ProducerType.MULTI, new BlockingWaitStrategy());
    // 使用 doRefreshCache 消费 cacheEvent
    disruptor.handleEventsWith(this::doRefreshCache);
    // 加上默认的异常处理，因为 Disruptor 自带的会抛出 RunTimeException 杀死消费者线程
    disruptor.setDefaultExceptionHandler(new ExceptionHandler<CacheEvent>() {
        @Override
        public void handleEventException(Throwable ex, long sequence, CacheEvent event) {
            log.error("sequence " + sequence + " error!", ex);
        }

        @Override
        public void handleOnStartException(Throwable ex) {
            log.error("Exception during onStart()", ex);
        }

        @Override
        public void handleOnShutdownException(Throwable ex) {
            log.error("Exception during onShutdown()", ex);
        }
    });
    ringBuffer = disruptor.start();
}
```


## 解读

### start()
```java
public RingBuffer<T> start()
{
    checkOnlyStartedOnce();
    // handleEventsWith(...) 添加到 consumerRepository
    for (final ConsumerInfo consumerInfo : consumerRepository)
    {
        // 开启消费者线程，从 executor 里获得线程
        // Demo 里指定了 ThreadFactory，默认通过其创建 BasicExecutor
        // 而其 execute() 是创建一个新线程
        consumerInfo.start(executor);
    }

    return ringBuffer;
}
```

### handleEventsWith(handlers)

```java
public final EventHandlerGroup<T> handleEventsWith(final EventHandler<? super T>... handlers)
{
    return createEventProcessors(new Sequence[0], handlers);
}

EventHandlerGroup<T> createEventProcessors(
        final Sequence[] barrierSequences,
        final EventHandler<? super T>[] eventHandlers)
{
    checkNotStarted();

    final Sequence[] processorSequences = new Sequence[eventHandlers.length];
    final SequenceBarrier barrier = ringBuffer.newBarrier(barrierSequences);

    for (int i = 0, eventHandlersLength = eventHandlers.length; i < eventHandlersLength; i++)
    {
        final EventHandler<? super T> eventHandler = eventHandlers[i];

        final BatchEventProcessor<T> batchEventProcessor =
            new BatchEventProcessor<>(ringBuffer, barrier, eventHandler);

        if (exceptionHandler != null)
        {
            batchEventProcessor.setExceptionHandler(exceptionHandler);
        }

        consumerRepository.add(batchEventProcessor, eventHandler, barrier);
        processorSequences[i] = batchEventProcessor.getSequence();
    }

    updateGatingSequencesForNextInChain(barrierSequences, processorSequences);

    return new EventHandlerGroup<>(this, consumerRepository, processorSequences);
}
```
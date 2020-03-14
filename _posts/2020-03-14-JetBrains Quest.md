---
layout: post
title: "JetBrains Quest"
date: 2020-03-14 00:03:41 +0800
categories: JetBrains
---

## Quest 1

![qust-1-1]({{ site.url }}/assets/imgs/jetbrains_quest/quest-1-1.png)

`十六进制` 转 `字符串`：

{% highlight javascript %}
"48 61 76 65 20 79 6f 75 20 73 65 65 6e 20 74 68 65 20 73 6f 75 72 63 65 20 63 6f 64 65 20 6f 66 20 74 68 65 20 4a 65 74 42 72 61 69 6e 73 20 77 65 62 73 69 74 65 3f"
    .split(' ')
    .map(ch => String.fromCharCode((parseInt(ch, 16))))
    .join('')
// output: "Have you seen the source code of the JetBrains website?"
{% endhighlight %}

查看 [JetBrains 官网](https://jetbrains.com) 源码：

![qust-1-2]({{ site.url }}/assets/imgs/jetbrains_quest/quest-1-2.png)

全文如下：

{% highlight html %}

        <!--
      O
{o)xxx|===============-
      O

Welcome to the JetBrains Quest.

What awaits ahead is a series of challenges. Each one will require a little initiative, a little thinking, and a whole lot of JetBrains to get to the end. Cheating is allowed and in some places encouraged. You have until the 15th of March at 12:00 CET to finish all the quests.
Getting to the end of each quest will earn you a reward.
Let the quest commence!

JetBrains has a lot of products, but there is one that looks like a joke on our Products page, you should start there... (hint: use Chrome Incognito mode)
It’s dangerous to go alone take this key: Good luck! == Jrrg#oxfn$

                 O
-===============|xxx(o}
                 O
-->
{% endhighlight %}


根据上面提示使用**隐身模式**打开 [JetBrains 产品页](https://jetbrains.com/products)

![qust-1-3]({{ site.url }}/assets/imgs/jetbrains_quest/quest-1-3.png)

进入 `JK Read More`:

![qust-1-4]({{ site.url }}/assets/imgs/jetbrains_quest/quest-1-4.png)


找到 500 - 5000 之间质数的个数：**574**。

打开 [https://jb.gg/574](https://jb.gg/574)

![qust-1-5]({{ site.url }}/assets/imgs/jetbrains_quest/quest-1-5.png)

打开 `youtrack` 中 [MPS-31816](https://youtrack.jetbrains.com/issue/MPS-31816)

![qust-1-6]({{ site.url }}/assets/imgs/jetbrains_quest/quest-1-6.png)

根据网页中 `Good luck! == Jrrg#oxfn$` 再对照 `ASCII` 表可知 `left + 3 = right`。

{% highlight javascript %}
"Qlfh$#Li#|rx#duh#uhdglqj#wklv#|rx#pxvw#kdyh#zrunhg#rxw#krz#wr#ghfu|sw#lw1#Wklv#lv#rxu#lvvxh#wudfnhu#ghvljqhg#iru#djloh#whdpv1#Lw#lv#iuhh#iru#xs#wr#6#xvhuv#lq#Forxg#dqg#iru#43#xvhuv#lq#Vwdqgdorqh/#vr#li#|rx#zdqw#wr#jlyh#lw#d#jr#lq#|rxu#whdp#wkhq#zh#wrwdoo|#uhfrpphqg#lw1#|rx#kdyh#ilqlvkhg#wkh#iluvw#Txhvw/#qrz#lw“v#wlph#wr#uhghhp#|rxu#iluvw#sul}h1#Wkh#frgh#iru#wkh#iluvw#txhvw#lv#‟EhfdxvhFrgh†1#Jr#wr#wkh#Txhvw#Sdjh#dqg#xvh#wkh#frgh#wr#fodlp#|rxu#sul}h1#kwwsv=22zzz1mhweudlqv1frp2surpr2txhvw2"
    .split('')
    .map(s => s.codePointAt(0) - 3)
    .map(i => String.fromCharCode(i))
    .join('')
// output: Nice! If you are reading this you must have worked out how to decrypt it. This is our issue
// tracker designed for agile teams. It is free for up to 3 users in Cloud and for 10 users in Standalone, 
// so if you want to give it a go in your team then we totally recommend it. you have finished the first Quest, 
// now it’s time to redeem your first prize. The code for the first quest is “BecauseCode”. 
// Go to the Quest Page and use the code to claim your prize. https://www.jetbrains.com/promo/quest/
{% endhighlight %}

**获得 3 个月免费全产品线产品。**

---

## Quest 2

![qust-2-1]({{ site.url }}/assets/imgs/jetbrains_quest/quest-2-1.png)

反转字符串：

{% highlight java %}
new StringBuilder(".spleh A+lrtC/dmC .thgis fo tuo si ti semitemos ,etihw si txet nehw sa drah kooL .tseretni wohs dluohs uoy ecalp a si ,dessecorp si xat hctuD erehw esac ehT .sedih tseuq fo txen eht erehw si ,deificeps era segaugnal cificeps-niamod tcudorp ehT")
    .reverse()
    .toString();
// output: The product domain-specific languages are specified, is where the next of quest hides. 
// The case where Dutch tax is processed, is a place you should show interest. 
// Look hard as when text is white, sometimes it is out of sight. Cmd/Ctrl+A helps."
{% endhighlight %}

`MPS` 是其领域语言产品。到其 [Dutch Tax](https://resources.jetbrains.com/storage/products/mps/docs/MPS_DTO_Case_Study.pdf)， `ctrl + A`:

![qust-2-2]({{ site.url }}/assets/imgs/jetbrains_quest/quest-2-2.png)

得到：

```
This is our 20th year as a company,
we have shared numbers in our JetBrains
Annual report, sharing the section with
18,650 numbers will progress your quest.
```

打开其 [2019 年度报告](https://www.jetbrains.com/company/annualreport/2019/)

![qust-2-3]({{ site.url }}/assets/imgs/jetbrains_quest/quest-2-3.png)


这一节的数字加起来正好是 `18650`。点击分享：

![qust-2-4]({{ site.url }}/assets/imgs/jetbrains_quest/quest-2-4.png)

打开 [目标网址](https://blog.jetbrains.com/blog/2019/11/22/jetbrains-7th-annual-hackathon/)

![qust-2-5]({{ site.url }}/assets/imgs/jetbrains_quest/quest-2-5.png)

可以看出右侧 `hiring`，跳转 [JetBrains 招聘](http://jetbrains.com/jobs)

都填 `any`，跳转 [无畏的应聘者](https://www.jetbrains.com/careers/jobs/fearless-quester-356)

![qust-2-6]({{ site.url }}/assets/imgs/jetbrains_quest/quest-2-6.png)

跳转到 [JetBrains 游戏开发招募](https://www.jetbrains.com/gamedev/)

输入 `↑↑↓↓←→←→BA`，打砖块即可：

![qust-2-7]({{ site.url }}/assets/imgs/jetbrains_quest/quest-2-7.png)

**获得 3 个月免费全产品线产品。**

---

## Final Quest

![qust-3-1]({{ site.url }}/assets/imgs/jetbrains_quest/quest-3-1.png)

`Base64` 解码：

{% highlight javascript %}
atob("SGF2ZSB5b3Ugc2VlbiB0aGUgcG9zdCBvbiBvdXIgSW5zdGFncmFtIGFjY291bnQ/")
// output: Have you seen the post on our Instagram account?
{% endhighlight %}

跳转其 `Instagram` 找到最近图片：

![qust-3-2]({{ site.url }}/assets/imgs/jetbrains_quest/quest-3-2.png)

跳转网页 [Kotlin Playground](https://play.kotlinlang.org/?short=o-lDUKP8W)：

![qust-3-3]({{ site.url }}/assets/imgs/jetbrains_quest/quest-3-3.png)

可以看到也是同第一个 quest 一样的题目。`TODO()` 改为 `3`。得到结果：

```
We have been working 22/7 on the video for the first episode of the PhpStorm EAP. 
If we gave you a clue, it would be easy as pi.
```

> Kotlin 确实不错！

跳转到 [PHPStorm 2020.1](https://blog.jetbrains.com/phpstorm/2020/02/whats-coming-in-phpstorm-2020-1-eap-video-series-season-2020-1-episode-1/)

上面提到了 `pi` 应该在 `3 分 14 秒` 附近：

![qust-3-4]({{ site.url }}/assets/imgs/jetbrains_quest/quest-3-4.png)

跳转 [JetBrains Quest Quiz](https://jb.gg/31415926)

> 得知奖金是 **8折优惠券** 后就没继续了。
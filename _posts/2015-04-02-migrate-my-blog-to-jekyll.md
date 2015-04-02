---
layout: post
title: "将博客从Octopress迁移到Jekyll"
description: ""
category: 
---

![](/images/20150402.jpg)

使用Octopress已将近两年,主题换了两三个,也能达到随时随地写博客的基本需求,只是总感觉少了点什么,让人不太自在.最近我想我找到原因了,那便是不够简洁,不够稳定,操作不够方便,同时太过臃肿.当换到新环境后,可能会由于新环境所装Ruby版本或rake版本与clone下来的环境不匹配,出现一些令人意想不到的问题.其臃肿的程度更不必细说,从Octopress作者Brandom Mathis一席话中便能知晓:

> Octopress is released as a single product, but it is a collection of plugins and configurations which are hard to disentangle. if you want to change or remove anything you are leaving the "golden path" and updates will be painful, if not impossible — short of copy and paste. Even I can not remove things from Octopress.

<!-- more -->

通过观察clone下来的源码文件夹也能窥知其臃肿不堪.

我们要时刻具有反思与反问的精神.每做一件事情或一个决定时,问问自己为什么要这样做?当理清思绪明确目的后,便要思考该怎样做才是合适的,至于所选方式是否为最合适,已显得不是很重要,毕竟人生不可能永远走的是最短路径,难免会经历一些曲折.曲折也没什么不好,也许能欣赏到不一样的风景,收获不一样的感受.只有当自己感觉不满意或是了解了更好的方式时,才需要去寻求改变,否则stay
still吧.

这方面自己还有待提高,往往在选择方式时思考太多,瞻前顾后,总试图最开始便找出best
practise.在没找出前,决不会进行下一步工作.后来的一些经历使我改变了之前的看法,逐渐采取先尝试后决策的做法,这样往往有"山重水复疑无路,柳暗花明又一村"的感觉.尝试一种方法进行下去后,整个思路逐渐便的清晰起来,不再有之前一叶障目的困惑.

由Octopress换到Jekyll最大的原因是我无法了解Octopress的整个工作流程,文件太多,文档资料显得有点单薄,理解起来略费劲.而Jekyll刚好弥补了这些缺点,在这里不得不大赞Jekyll的文档,写的实在是太好了!非常容易便能找到自己想看的内容.同时Jekyll可定制化程度相当高,自己写插件也很方便.

此次迁移过程比较顺利,步骤也非常简单,只需如下几步便可完成:

1. 安装Jekyll: `$gem install jekyll`
2. 创建新博客: `$jekyll new Blog`
3. 拷贝Octopress文章到Jekyll

只需将之前Octopress的`source/_posts`目录下的内容和`source/images`目录下的图片拷贝到Jekyll新博客的`_posts`目录和`images`目录(需新建)即可.唯一麻烦的地方可能需要修改之前文章中的代码引用方式,Jekyll中采用liquid的highlight方式,而Octopress采用codeblocks方式.如果类似的文章有多篇需替换,那么最好写正则批量替换,否则真的是要改到手抽筋.

对我来说,Jekyll默认的主题便够用,虽说与我之前Octopress所用主题效果上相差很多,但够用就好.唯一令我不太满意的是字体的显示,对中文支持不太好,看着有点难受.后面再慢慢换,先这样将就着.至于评论、文章分类等,觉着意义不大,也便不花心思在上面了,等哪天有心思觉着有必要再添加吧.

改动地方较大的大致要数首页的显示了,默认首页只显示文章标题列表,我不太习惯这种方式,便修改成摘要预览的方式了.只需对index.html文件稍加修改便可.

{% highlight html %}
{% raw %}
<div>
    {% if post.content contains "<!-- more -->" %}
        {{ post.content | split:"<!-- more -->" | first}}
    {% else %}
        {{ post.content | strip_html | truncatewords:300 }}
    {% endif %}
</div>
{% endraw %}
{% endhighlight %}

然后只需在文章中相应位置添加`<!-- more -->`即可.

有关预览的详细步骤,可参考:

[http://truongtx.me/2013/05/01/jekyll-read-more-feature-without-any-plugin/](http://truongtx.me/2013/05/01/jekyll-read-more-feature-without-any-plugin/)

Jekyll默认不提供创建post和page的模板,所以参考网上资料写了个post和page的task放在Rakefile中.新建post时只需用`rake
post title="xxx"`的方式便能迅速创建一个post.

![](/images/20150402_oldblog.png)
    最后,附上一张之前Octopress博客的截图以示怀念.


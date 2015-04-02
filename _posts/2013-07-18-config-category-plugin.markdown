---
layout: post
title: "配置文章分类插件"
date: 2013-07-18 17:17
comments: true
categories: Octopress 
---
Octopress搭建的博客默认没有文章分类，这肯定让人很不爽，但这个号称Hacker的博客肯定有这功能，便网上搜寻了答案，最终得以解决。方法如下：

###1. 添加category\_list插件

代码如下：

```
    module Jekyll
        class CategoryListTag < Liquid::Tag
            def render(context)
                html = ""
                categories = context.registers[:site].categories.keys
                categories.sort.each do |category|
                    posts_in_category = context.registers[:site].categories[category].size
                    category_dir = context.registers[:site].config['category_dir']
                    category_url = File.join(category_dir, category.gsub(/_|\P{Word}/, '-').gsub(/-{2,}/, '-').downcase)
                    html << "<li class='category'><a href='/#{category_url}/'>#{category} (#{posts_in_category})</a></li>\n"
                end
                html
            end
        end
    end

    Liquid::Template.register_tag('category_list', Jekyll::CategoryListTag)
```

将以上代码保存到plugins/category\_list\_tag.rb中。

这个插件会向liquid注册一个名为category\_list的tag，该tag就是以li的形式将站点所有的category组织起来。如果要将category加入到侧边导航栏，需要增加一个aside

### 2. 添加category到aside中

在source/\_include/custom/asides中新建category\_list.html文件，并且将以下代码复制到其中：

```
    <section>
        <h1>Categories</h1>
        <ul id="categories">
            {\% category_list %}
        </ul>
    </section>
```

其中\是为了显示才添加上的，不然无法正常显示，复制代码时请去掉%前的\。

### 3. 配置侧边栏

在\_config.yml中配置侧边栏，修改其中的default\_asides项：

```
    default_asides: [custom/asides/category_list.html, ...]
```

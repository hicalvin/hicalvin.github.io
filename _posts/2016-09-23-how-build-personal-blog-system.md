---
layout: post
title:  "搭建我的博客系统 GitHub+Jekyll+Flickr"
date:   2016-09-23 14:12:50 +0800
category: tech
---

和同事W在培训的时候闲聊，发现大家都有强烈的吐槽愿望， 苦于没有合适的平台， 而对于自己搭平台又感觉苦难重重， 但是W推荐的GitHub Pages让我觉得似乎困难没有想象的那么大。 用GitHub Pages作为博客站点的好处有那么几个。 首先， 如果你要沾点工程师气质的话， GitHub作为工程师的Facebook， 简直没有第二个可以与它相比。 既然要做个带点工程师气质的博客站点， 我都快舍不得去用自己的域名来替代 github.io 了。 其次， 网站无限流量， 而且长城内外都可以访问， 当初光这两点基本上就已经打动我了。 另外还有， 就是丰富的资源， GitHub上各种主题模版， 框架都随你使用，操作也是如此简单， 只要通用的Git命令就可以快速上传你要发布的内容。 早知如此， 怎么这么久才动呢。 之前自己发布的内容包括了各种论坛， 博客， 微博， 但也导致了自己的分享碎片化。 有个集中的， 自由度又极高的， 又是可以访问的地方实在是不可多得。 

另外说个小插曲。 开始时候在选择Jekyll和Hexo之间又犯难了， 但是在咨询Google Trend 以后就果断选择了Jekyll。 看图可能就很快明白了

![比较图一](/img/timeline/screenshot-jekyll-hexo-1.png)

![比较图二](/img/timeline/screenshot-jekyll-hexo-2.png)



选好了平台和核心组件， 接下来就是 

<code>STOP TALK SHOW ME THE CODE</code>

网上有很多手把手一步步建站的文章，我就不重复写了。 

[发动机的小角落分享的*Jekyll本地搭建开发环境以及Github部署流程*](http://pizida.com/technology/2016/03/03/use-jekyll-create-blog-on-github/)

等到Jekyll好了， 接下来当然是发布博客。 Mac上的工具还是挺多的， 之前一直用Sublime就可以通过安装 MarkdownEditing 和 MarkdownPreview 来编辑和预览， 但是感觉有点不方便， 每次都要用快捷键来预览真的有点烦， 于是就找了[MacDown](http://macdown.uranusjr.com/)来写， 立马就喜欢上了。 即时的预览， 写起来当然舒服多了。 除了文字， 图片当然是少不了的， 那么就得有个提供图片外链的网站， 因为如果把图片放到GitHub上是不合适的， 毕竟GitHub是放代码的， 提供的容量只有300M。 如果放图片一会就爆了， 所以找到了[Flickr](http://flickr.com)， 一个我一直觉得几乎糟蹋在Yahoo手里的非常好的网站，虽然现在也还是非常棒， 但Yahoo并没有太珍惜。 但是如果要拿到Flickr的外链还是有个小技巧，上传过图片后，在所有图片里会看到你刚刚上传的图片，打开后右下角有个选项按钮，点开<code>选择检视所有尺寸</code>，进去后选择好要的大小后，复制图片链接，这个链接就可以做为你的外部链接使用了。

几乎就这么多， 剩下的就是去熟悉MarkDown的语法， 然后就是

<pre><code>
$>git add . 
$>git commit -m "blablabla.."
$>git push
</code></pre>


好了， 开始写吧， 动手比任何方式都学得快！！



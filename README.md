<div class="preview">

          <div class="show-content"><h1>WebPack是什么</h1>
<blockquote><ol>
<li>一个打包工具</li>
<li>一个模块加载工具</li>
<li>各种资源都可以当成模块来处理</li>
<li>网站 <a href="http://webpack.github.io/" target="_blank">http://webpack.github.io/</a>
</li>
</ol></blockquote>
<p>如今，越来越多的JavaScript代码被使用在页面上，我们添加很多的内容在浏览器里。如何去很好的组织这些代码，成为了一个必须要解决的难题。</p>
<p>对于模块的组织，通常有如下几种方法：</p>
<ol>
<li>通过书写在不同文件中，使用script标签进行加载</li>
<li>CommonJS进行加载（NodeJS就使用这种方式）</li>
<li>AMD进行加载（require.js使用这种方式）</li>
<li>ES6模块</li>
</ol>
<p><strong>思考：为什么只有JS需要被模块化管理，前台的很多预编译内容，不需要管理吗？</strong></p>
<p>基于以上的思考，WebPack项目有如下几个目标：</p>
<ul>
<li>将依赖树拆分，保证按需加载</li>
<li>保证初始加载的速度</li>
<li>所有静态资源可以被模块化</li>
<li>可以整合第三方的库和模块</li>
<li>可以构造大系统</li>
</ul>
<p>从下图可以比较清晰的看出WebPack的功能<br></p><div class="image-package imagebubble" widget="ImageBubble">
<img src="http://upload-images.jianshu.io/upload_images/401663-3b68765ce208588f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240" data-original-src="http://upload-images.jianshu.io/upload_images/401663-3b68765ce208588f.png?imageMogr2/auto-orient/strip%7CimageView2/2" class="imagebubble-image"><br><div class="image-caption">这是一个示意图</div>
</div>
<hr>
<h1>WebPack的特点</h1>
<ol>
<li>丰富的插件，方便进行开发工作</li>
<li>大量的加载器，包括加载各种静态资源</li>
<li>代码分割，提供按需加载的能力</li>
<li>发布工具</li>
</ol>
<hr>
<h1>WebPack的优势</h1>
<blockquote>
<ul>
<li>webpack 是以 commonJS 的形式来书写脚本滴，但对 AMD/CMD 的支持也很全面，方便旧项目进行代码迁移。</li>
<li>能被模块化的不仅仅是 JS 了。</li>
<li>开发便捷，能替代部分 grunt/gulp 的工作，比如打包、压缩混淆、图片转base64等。</li>
<li>扩展性强，插件机制完善，特别是支持 React 热插拔（见 react-hot-loader ）的功能让人眼前一亮。</li>
</ul>
<hr>
</blockquote>
<h1>WebPack的安装</h1>
<ol>
<li>安装命令<pre class="hljs sql"><code class="sql">$ npm <span class="hljs-operator"><span class="hljs-keyword">install</span> webpack -<span class="hljs-keyword">g</span></span></code></pre>
</li>
<li>使用webpack<pre class="hljs ruby"><code class="ruby"><span class="hljs-variable">$ </span>npm init  <span class="hljs-comment"># 会自动生成一个package.json文件</span>
<span class="hljs-variable">$ </span>npm install webpack --save-dev <span class="hljs-comment">#将webpack增加到package.json文件中</span></code></pre>
</li>
<li>可以使用不同的版本<pre class="hljs sql"><code class="sql">$ npm <span class="hljs-operator"><span class="hljs-keyword">install</span> webpack@<span class="hljs-number">1.2</span>.x <span class="hljs-comment">--save-dev</span></span></code></pre>
</li>
<li>如果想要安装开发工具<pre class="hljs sql"><code class="sql">$ npm <span class="hljs-operator"><span class="hljs-keyword">install</span> webpack-dev-<span class="hljs-keyword">server</span> <span class="hljs-comment">--save-dev</span></span></code></pre>
</li>
</ol>
<h1>WebPack的配置</h1>
<blockquote><p> 每个项目下都必须配置有一个 webpack.config.js ，它的作用如同常规的 gulpfile.js/Gruntfile.js ，就是一个配置项，告诉 webpack 它需要做什么。</p></blockquote>
<p>下面是一个例子</p>
<pre class="hljs javascript"><code class="javascript"><span class="hljs-keyword">var</span> webpack = <span class="hljs-built_in">require</span>(<span class="hljs-string">'webpack'</span>);
<span class="hljs-keyword">var</span> commonsPlugin = <span class="hljs-keyword">new</span> webpack.optimize.CommonsChunkPlugin(<span class="hljs-string">'common.js'</span>);
<span class="hljs-built_in">module</span>.exports = {
    <span class="hljs-comment">//插件项</span>
    plugins: [commonsPlugin],
    <span class="hljs-comment">//页面入口文件配置</span>
    entry: {
        index : <span class="hljs-string">'./src/js/page/index.js'</span>
    },
    <span class="hljs-comment">//入口文件输出配置</span>
    output: {
        path: <span class="hljs-string">'dist/js/page'</span>,
        filename: <span class="hljs-string">'[name].js'</span>
    },
    <span class="hljs-built_in">module</span>: {
        <span class="hljs-comment">//加载器配置</span>
        loaders: [
            { test: <span class="hljs-regexp">/\.css$/</span>, loader: <span class="hljs-string">'style-loader!css-loader'</span> },
            { test: <span class="hljs-regexp">/\.js$/</span>, loader: <span class="hljs-string">'jsx-loader?harmony'</span> },
            { test: <span class="hljs-regexp">/\.scss$/</span>, loader: <span class="hljs-string">'style!css!sass?sourceMap'</span>},
            { test: <span class="hljs-regexp">/\.(png|jpg)$/</span>, loader: <span class="hljs-string">'url-loader?limit=8192'</span>}
        ]
    },
    <span class="hljs-comment">//其它解决方案配置</span>
    resolve: {
        root: <span class="hljs-string">'E:/github/flux-example/src'</span>, <span class="hljs-comment">//绝对路径</span>
        extensions: [<span class="hljs-string">''</span>, <span class="hljs-string">'.js'</span>, <span class="hljs-string">'.json'</span>, <span class="hljs-string">'.scss'</span>],
        alias: {
            AppStore : <span class="hljs-string">'js/stores/AppStores.js'</span>,
            ActionType : <span class="hljs-string">'js/actions/ActionType.js'</span>,
            AppAction : <span class="hljs-string">'js/actions/AppAction.js'</span>
        }
    }
};</code></pre>
<ol>
<li>plugins 是插件项，这里我们使用了一个 CommonsChunkPlugin的插件，它用于提取多个入口文件的公共脚本部分，然后生成一个 common.js 来方便多页面之间进行复用。</li>
<li>entry 是页面入口文件配置，output 是对应输出项配置 （即入口文件最终要生成什么名字的文件、存放到哪里）</li>
<li>module.loaders 是最关键的一块配置。它告知 webpack 每一种文件都需要使用什么加载器来处理。 <strong>所有加载器需要使用npm来加载</strong>
</li>
<li>最后是 resolve 配置，配置查找模块的路径和扩展名和别名（方便书写）</li>
</ol>
<h1>WebPack开始使用</h1>
<blockquote><p>这里有最基本的使用方法，给大家一个感性的认识</p></blockquote>
<ol>
<li>正确安装了WebPack，方法可以参考上面</li>
<li>书写entry.js文件<pre class="hljs perl"><code class="perl">document.<span class="hljs-keyword">write</span>(<span class="hljs-string">"看看如何让它工作！"</span>);</code></pre>
</li>
<li>书写index.html文件<pre class="hljs xml"><code class="xml"><span class="hljs-tag">&lt;<span class="hljs-title">html</span>&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-title">head</span>&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-title">meta</span> <span class="hljs-attribute">charset</span>=<span class="hljs-value">"utf-8"</span>&gt;</span>
<span class="hljs-tag">&lt;/<span class="hljs-title">head</span>&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-title">body</span>&gt;</span>
<span class="hljs-tag">&lt;<span class="hljs-title">script</span> <span class="hljs-attribute">type</span>=<span class="hljs-value">"text/javascript"</span> <span class="hljs-attribute">src</span>=<span class="hljs-value">"bundle.js"</span> <span class="hljs-attribute">charset</span>=<span class="hljs-value">"utf-8"</span>&gt;</span><span class="undefined"></span><span class="hljs-tag">&lt;/<span class="hljs-title">script</span>&gt;</span>
<span class="hljs-tag">&lt;/<span class="hljs-title">body</span>&gt;</span>
<span class="hljs-tag">&lt;/<span class="hljs-title">html</span>&gt;</span></code></pre>
</li>
<li>执行命令，生成bundle.js文件<pre class="hljs ruby"><code class="ruby"><span class="hljs-variable">$ </span>webpack ./entry.js bundle.js</code></pre>
</li>
<li>在浏览器中打开index.html文件，可以正常显示出预期</li>
<li>增加一个content.js文件<pre class="hljs javascript"><code class="javascript"><span class="hljs-built_in">module</span>.exports = <span class="hljs-string">"现在的内容是来自于content.js文件！"</span>;</code></pre>
</li>
<li>修改entry.js文件<pre class="hljs perl"><code class="perl">document.<span class="hljs-keyword">write</span>(<span class="hljs-keyword">require</span>(<span class="hljs-string">"./content.js"</span>));</code></pre>
</li>
<li>执行第四步的命令</li>
</ol>
<p><strong>进行加载器试验</strong></p>
<ol>
<li>增加style.css文件<pre class="hljs css"><code class="css"><span class="hljs-tag">body</span> <span class="hljs-rules">{
<span class="hljs-rule"><span class="hljs-attribute">background</span>:<span class="hljs-value"> yellow</span></span>;
}</span></code></pre>
</li>
<li>修改entry.js文件<pre class="hljs perl"><code class="perl"><span class="hljs-keyword">require</span>(<span class="hljs-string">"!style!css!./style.css"</span>);
document.<span class="hljs-keyword">write</span>(<span class="hljs-keyword">require</span>(<span class="hljs-string">"./content.js"</span>));</code></pre>
</li>
<li>执行命令，安装加载器<pre class="hljs sql"><code class="sql">$ npm <span class="hljs-operator"><span class="hljs-keyword">install</span> css-loader <span class="hljs-keyword">style</span>-loader   # 安装的时候不使用 -<span class="hljs-keyword">g</span></span></code></pre>
</li>
<li>执行webpack命令，运行看效果</li>
<li>可以在命令行中使用loader <pre class="hljs perl"><code class="perl">$ webpack ./entry.js bundle.js --module-<span class="hljs-keyword">bind</span> <span class="hljs-string">"css=style!css"</span></code></pre>
</li>
</ol>
<p><strong>使用配置文件</strong><br>默认的配置文件为webpack.config.js</p>
<ol>
<li>增加webpack.config.js文件<pre class="hljs javascript"><code class="javascript"><span class="hljs-built_in">module</span>.exports = {
 entry: <span class="hljs-string">"./entry.js"</span>,
 output: {
     path: __dirname,
     filename: <span class="hljs-string">"bundle.js"</span>
 },
 <span class="hljs-built_in">module</span>: {
     loaders: [
         { test: <span class="hljs-regexp">/\.css$/</span>, loader: <span class="hljs-string">"style!css"</span> }
     ]
 }
};</code></pre>
</li>
<li>执行程序<pre class="hljs ruby"><code class="ruby"><span class="hljs-variable">$ </span>webpack</code></pre>
</li>
</ol>
<p><strong>发布服务器</strong></p>
<ol>
<li>安装服务器<pre class="hljs sql"><code class="sql">$ npm <span class="hljs-operator"><span class="hljs-keyword">install</span> webpack-dev-<span class="hljs-keyword">server</span> -<span class="hljs-keyword">g</span>
$ webpack-dev-<span class="hljs-keyword">server</span> <span class="hljs-comment">--progress --colors</span></span></code></pre>
</li>
<li>服务器可以自动生成和刷新，修改代码保存后自动更新画面<pre class="hljs objectivec"><code class="objectivec">http:<span class="hljs-comment">//localhost:8080/webpack-dev-server/bundle</span></code></pre>
</li>
</ol>
</div>
        </div>


## 教程 ##

- [WebPack 简明学习教程](http://www.jianshu.com/p/b95bbcfc590d)
- [官方文档](https://webpack.github.io/docs/tutorials/getting-started/)
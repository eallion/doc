\> 本文由 \[简悦 SimpRead\](http://ksria.com/simpread/) 转码， 原文地址 \[fffou.com\](https://fffou.com/post/2020-05-14/)

站点程序从动态切换到静态已经很久了，而我用的静态程序是 hugo，不得不说 hugo 各方面都比较不错的，就是很难找到称心如意的主题。

今天某个博友问我文章归档页面是怎么样实现页面分页的，才想起去年通过搜索引擎找了好多主题，好不容易才找到这个 hugo 主题 hermit，因为觉得归档页的页面很简洁，所以直接把主题的归档页面当作了站点首页，期间遇到主题在新版本的 hugo 中存在[小问题](https://fffou.com/post/191214/) ，把 hugo 退回到 0.56.3 版本。

直到后面遇到实在不能忍受的问题，就是这款主题归档页面竟然没有分页功能！要知道我这个人是比较追求稳定的，万一哪天文章多起来了，光是归档页面估计都能拉好几个屏幕那么长，这是我不能接受的。得想办法修改主题以实现这个功能，但是我不怎么会修改 hugo 主题，后面还是一咬牙，仔细看了看 hugo 官方文档，紧接着再翻看了十几二十个带翻页功能的 hugo 主题，终于看出了实现归档页面分页功能的可能：那就是为什么不通过查看别的 hugo 主题，文章列表分页功能是怎么实现的，想办法移植到这款主题的归档页面。

事实证明我的想法是对的，后面通过左拼右凑，还真实现了 hermit 主题归档页面的分页功能。期间也给其他没有归档分页功能的 hugo 主题弄上了分页功能，但是跟 hermit 主题实现分页功能在代码上有一点差异，所以本文标题才特意指定 hermit，其他 hugo 主题也可以参考本文，对有差异的地方自行修改实现。

这里就以 hugo 主题 hermit 为例，记录增加归档页面的分页功能的实现步骤：

### 找到归档页面的源码部分，添加分页代码[](#找到归档页面的源码部分-添加分页代码)

hermit 主题的归档页面源码在`layouts/_default/list.html`文件中:

如下代码：

```
{{ define "header" }}
 {{ partialCached "header.html" . }}
 {{ end }}

 {{ define "main" }}
    <main class="site-main section-inner thin animated fadeIn faster">
        <h1>{{ .Title }}</h1>
        {{- if .Content }}
        <div class="content">
            {{ .Content }}
        </div>
        {{- end }}
        {{- range .Data.Pages.GroupByDate "2006" }}
        <div class="posts-group">
            <div class="post-year" id="{{ .Key }}">{{ .Key }}</div>
            <ul class="posts-list">
                {{- range .Pages }}
                <li class="post-item">
                    <a href="{{.Permalink}}">
                        <span class="post-title">{{.Title}}</span>
                        <span class="post-day">{{ .Date.Format .Site.Params.dateformShort }}</span>
                    </a>
                </li>
                {{- end }}
             </ul>
         </div>
        {{- end }}
     </main>
 {{ end }}

 {{ define "footer" }}
 {{ partialCached "footer.html" . }}
 {{ end }}
```

修改以下代码：

```
{{- range .Data.Pages.GroupByDate "2006" }}
```

为

```
{{- range (.Paginate .Pages).Pages.GroupByDate "2006" }}
```

那么修改后的代码就是：

```
{{ define "header" }}
 {{ partialCached "header.html" . }}
 {{ end }}

 {{ define "main" }}
    <main class="site-main section-inner thin animated fadeIn faster">
        <h1>{{ .Title }}</h1>
        {{- if .Content }}
        <div class="content">
            {{ .Content }}
        </div>
        {{- end }}
        {{- range (.Paginate .Pages).Pages.GroupByDate "2006" }}
        <div class="posts-group">
            <div class="post-year" id="{{ .Key }}">{{ .Key }}</div>
            <ul class="posts-list">
                {{- range .Pages }}
                <li class="post-item">
                        <a href="{{.Permalink}}">
                        <span class="post-title">{{.Title}}</span>
                        <span class="post-day">{{ .Date.Format .Site.Params.dateformShort }}</span>
                    </a>
                </li>
                {{- end }}
            </ul>
        </div>
        {{- end }}

     </main>
 {{ end }}

 {{ define "footer" }}
 {{ partialCached "footer.html" . }}
 {{ end }}
```

这时候 hugo 主题 hermit 归档页面已经实现分页功能，而我实现的原理就是在 hermit 这个主题的归档页面中，把展示文章列表的代码部分，也就是上面那行代码，在页面元素中增加了分页，实现了分页展示功能。其他 hugo 主题跟 hermit 主题相比，在修改归档页面增加分页功能这一步中可能有一点差异，而我所说的差异就这一步的代码差异，需要自己去尝试修改。

### 为归档页面增加底部分页按钮[](#为归档页面增加底部分页按钮)

做完上面那一步，大家会发现归档页面的文章已经变少了，说明归档页面分页功能已经实现，所有文章列表被分成了几个页面。我们怎么查看其他分出来的页面呢？又怎么切换到上一页或下一页呢？难道在地址栏手动改动页面地址进行页面切换？当然不是，这一步就是为已经具备分页功能的归档页面增加底部页面切换按钮。

继续查看归档页面的代码：

```
{{ define "header" }}
 {{ partialCached "header.html" . }}
 {{ end }}

 {{ define "main" }}
    <main class="site-main section-inner thin animated fadeIn faster">
        <h1>{{ .Title }}</h1>
        {{- if .Content }}
        <div class="content">
            {{ .Content }}
        </div>
        {{- end }}
        {{- range (.Paginate .Pages).Pages.GroupByDate "2006" }}
        <div class="posts-group">
            <div class="post-year" id="{{ .Key }}">{{ .Key }}</div>
            <ul class="posts-list">
                {{- range .Pages }}
                <li class="post-item">
                        <a href="{{.Permalink}}">
                        <span class="post-title">{{.Title}}</span>
                        <span class="post-day">{{ .Date.Format .Site.Params.dateformShort }}</span>
                    </a>
                </li>
                {{- end }}
            </ul>
        </div>
        {{- end }}

     </main>
 {{ end }}

 {{ define "footer" }}
 {{ partialCached "footer.html" . }}
 {{ end }}
```

增加以下代码到合适的部分，也就是文章列表的下面：

```
{{ partial "pagination.html" . }}
```

那么修改后的代码就是这样：

```
{{ define "header" }}
 {{ partialCached "header.html" . }}
 {{ end }}

 {{ define "main" }}
    <main class="site-main section-inner thin animated fadeIn faster">
        <h1>{{ .Title }}</h1>
        {{- if .Content }}
        <div class="content">
            {{ .Content }}
        </div>
        {{- end }}
        {{- range (.Paginate .Pages).Pages.GroupByDate "2006" }}
        <div class="posts-group">
            <div class="post-year" id="{{ .Key }}">{{ .Key }}</div>
            <ul class="posts-list">
                {{- range .Pages }}
                <li class="post-item">
                        <a href="{{.Permalink}}">
                        <span class="post-title">{{.Title}}</span>
                        <span class="post-day">{{ .Date.Format .Site.Params.dateformShort }}</span>
                    </a>
                </li>
                {{- end }}
            </ul>
        </div>
        {{- end }}
        {{ partial "pagination.html" . }}
     </main>
 {{ end }}

 {{ define "footer" }}
 {{ partialCached "footer.html" . }}
 {{ end }}
```

上面通过引用了`layouts/partials`目录下的 `pagination.html`配置文件，以实现在这个归档页面底部添加可以切换分页的分页按钮功能，那么下面将有两种分页按钮供大家选择，选择自己喜欢的就行了：

#### 精简型分页按钮[](#精简型分页按钮)

下图就是精简型分页按钮：

![](https://src.orro.ro/file/ffcode/img/2020-05-14-1.png)

那么怎么实现精简型分页按钮方式呢？首先进入`layouts/partials`目录新建`pagination.html`文件，添加以下代码：

```
{{ if or (.Paginator.HasPrev) (.Paginator.HasNext) }}
 <div class="pagination">
     {{- if .Paginator.HasPrev }}
     <a class="pagination\_\_item pagination\_\_item--prev btn" href="{{ .Paginator.Prev.URL }}">«</a>
     {{- end }}
     <span class="pagination\_\_item pagination\_\_item--current">{{ .Paginator.PageNumber }}/{{ .Paginator.TotalPages }}</span>
     {{- if .Paginator.HasNext }}
     <a class="pagination\_\_item pagination\_\_item--next btn" href="{{ .Paginator.Next.URL }}">»</a>
     {{- end }}
 </div>
 {{ end }}
```

然后在对应的 css 样式文件中添加以下样式：

```
.pagination {
     margin-top: 20px
 }

 .pagination\_\_item {
    display: inline-block;
    padding: 10px 15px;
     font-weight: 700;
     color: #000;
     background: #c6c6c7
 }

 .pagination\_\_item:hover, .pagination\_\_item--current {
    color: #fff;
    background: #535e75
 }
```

#### 数字型分页按钮[](#数字型分页按钮)

下图就是数字型分页按钮：

![](https://src.orro.ro/file/ffcode/img/2020-05-14-2.png)

上面已经实现精简型分页按钮方式，那么又怎么实现数字型分页按钮方式呢？首先进入`layouts/partials`目录新建`pagination.html`文件，添加以下代码：

```
{{ $pag := $.Paginator }}
 {{ if gt $pag.TotalPages 1 }}
 <ul class="pagination">
     {{ with $pag.First }}
     <!-- <li class="page-item {{ if not $pag.HasPrev }}disabled{{ end }}">
         <span class="page-link">
             <a href="{{ .URL }}" aria-label="First"><span aria-hidden="true">&laquo;&laquo;</span></a>
         </span>
     </li> -->
     {{ end }}
     <!-- <li class="page-item {{ if not $pag.HasPrev }}disabled{{ end }}">
         <span class="page-link">
             <a href="{{ if $pag.HasPrev }}{{ $pag.Prev.URL }}{{ end }}" aria-label="Previous"><span aria-hidden="true">&laquo;</span></a>
         </span>
     </li> -->
     {{ $.Scratch.Set "\_\_paginator.ellipsed" false }}
     {{ range $pag.Pagers }}
     {{ $right := sub .TotalPages .PageNumber }}
     {{ $showNumber := or (le .PageNumber 1) (eq $right 0) }}
     {{ $showNumber := or $showNumber (and (gt .PageNumber (sub $pag.PageNumber 3)) (lt .PageNumber (add $pag.PageNumber 3)))  }}
     {{ if $showNumber }}
         {{ $.Scratch.Set "\_\_paginator.ellipsed" false }}
         {{ $.Scratch.Set "\_\_paginator.shouldEllipse" false }}
     {{ else }}
         {{ $.Scratch.Set "\_\_paginator.shouldEllipse" (not ($.Scratch.Get "\_\_paginator.ellipsed") ) }}
         {{ $.Scratch.Set "\_\_paginator.ellipsed" true }}
     {{ end }}
     {{ if $showNumber }}
     <li class="page-item {{ if eq . $pag }}active{{ end }}">
         <span class="page-link">
             <a href="{{ .URL }}">{{ .PageNumber }}</a></li>
         </span>
     {{ else if ($.Scratch.Get "\_\_paginator.shouldEllipse") }}
     <li class="page-item "><span class="page-link" aria-hidden="true">&hellip;</span></li>
     {{ end }}
     {{ end }}
     <!-- <li class="page-item {{ if not $pag.HasNext }}disabled{{ end }}">
         <span class="page-link">
             <a href="{{ if $pag.HasNext }}{{ $pag.Next.URL }}{{ end }}" aria-label="Next"><span aria-hidden="true">&raquo;</span></a>
         </span>
     </li> -->
     <!-- {{ with $pag.Last }}
     <li class="page-item {{ if not $pag.HasNext }}disabled{{ end }}">
         <span class="page-link">
         <a href="{{ .URL }}" aria-label="Last"><span aria-hidden="true">&raquo;&raquo;</span></a>
     </span>
     </li>
     {{ end }} -->
 </ul>
 {{ end }}
```

然后在对应的 css 样式文件中添加以下样式:

```
.pagination {
     display: flex;
     flex-direction: row;
     justify-content: center;
     list-style: none;
     white-space: nowrap;
     width: 100%;
     padding-top: 2em
 }

 .pagination a {
     -webkit-font-smoothing: antialiased;
     font-size: 12px;
     color: #bfbfbf;
     letter-spacing: .1em;
     font-weight: 700;
     padding: 5px;
     text-decoration: none;
     transition: .3s
 }

 .pagination li {
     padding-bottom: 3px;
     margin: 0 20px;
     box-sizing: border-box;
     position: relative;
     display: inline
 }

 .pagination li.disabled {
     display: none
 }

 .pagination li:hover a {
     color: #000
 }

 .dark-theme .pagination li:hover a {
     color: #fff
 }

 .pagination li:before,.pagination li:after {
     position: absolute;
     content: "";
     width: 0;
     height: 3px;
     background: #000;
     transition: .3s;
     bottom: 0
 }

 .dark-theme .pagination li:before,.dark-theme .pagination li:after {
     background: #fff
 }

 .pagination li:before .active,.pagination li:after .active {
     width: 100%
 }

 .pagination li:before {
     left: 50%
 }

 .pagination li:after {
     right: 50%
 }

 .pagination li:hover:before,.pagination li:hover:after {
     width: 50%
 }

 .pagination li.active a {
     color: #000
 }

 .dark-theme .pagination li.active a {
     color: #fff
 }

 .pagination li.active:before,.pagination li.active:after {
     width: 60%
 }/\*!Color themes for Google Code Prettify | MIT License | github.com/jmblog/color-themes-for-google-code-prettify\*/.prettyprint {
     background: #2d2d2d;
     font-family: Menlo,Bitstream Vera Sans Mono,DejaVu Sans Mono,Monaco,Consolas,monospace;
     border: 0!important
 }
```
原版B站视频：<https://www.bilibili.com/video/BV1yo4y167As/?spm_id_from=333.337.search-card.all.click&vd_source=2210291ff748722b564b45a544036097>



# 0 网页整体

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>哔哩哔哩 (゜-゜)つロ 干杯~-bilibili</title>
    <link rel="stylesheet" href="./css/base.css">
    <link rel="stylesheet" href="./css/index.css">
    <link rel="icon" href="./favicon.ico">
</head>
<body>
	<!-- 头部 -->
    <div class="large-header">
		<!-- 导航 -->
        <div class="bili-nav"></div>
		<!-- banner -->
        <div class="bili-banner"></div>
		<!-- 频道 -->
        <div class="bili-channel"></div>
	</div>
    <!-- 主体 -->
    <div class="main">
		<!-- 推荐列表 -->
        <div class="recommended-container"></div>
		<!-- 滚动按钮 -->
        <div class="sidebar"></div>
	</div>
</body>
</html>
```

> 头部和主体都是div，所以直接划分为上下两个部分。

展示

![image.png](https://note.youdao.com/yws/public/resource/33a7fa38941e62d212173a9426228d0b/WEBRESOURCE24bbe00b11653193d734897b6a2b74e1)

# 1 公共样式

```css
* {
    margin: 0;
    padding: 0;
    /*默认就是normal*/
    font-weight: normal;
}

body {
    /*整体字体大小*/
    font-size: 14px;
}

a {
    /*链接去掉下划线*/
    text-decoration: none;
    color: #000;
    /*鼠标出现小手手*/
    cursor: pointer;
}

ul, ol, li {
    /*去掉原始样式*/
    list-style: none;
}

input {
    /*去掉原始样式*/
    border: 0 none;
    outline-style: none;
}

img {
    vertical-align: middle;
}
```

# 2 导航

```html
<div class="bili-nav">
	<ul class="left-entry"></ul>
	<div class="center-search-container"></div>
	<ul class="right-entry"></ul>
</div>
```

css

```css
.bili-nav {
    /*子元素转成一行排列，且上下居中*/
    display: flex;
    align-items: center;
    
    /*让nav的宽度撑满其父元素的宽度*/
    width: 100%;
    /*上下填充0，左右填充24px*/
    padding: 0 24px;
    /*改为边框盒模型，当使用width100%又设置了padding时必须使用*/
    /*否则元素会超出父元素外*/
    box-sizing: border-box;
}
```

## 2.1 导航-左侧

```html
			<ul class="left-entry">
				<li>
					<a href="/" class="entry-title">
						<svg></svg>
						<span>首页</span>
					</a>
				</li>
				<li><a href="/" class="entry-title"><span>番剧</span></a></li>
				<li><a href="/" class="entry-title"><span>直播</span></a></li>
				...
			</ul>	
```

css

```css
/*左侧入口区域*/
.left-entry {
    /*首页、番剧、直播...转成一行*/
    display: flex;
    /*限制最小宽度，避免换行导致排序所乱*/
    min-width: 474px;
}

.left-entry .entry-title {
    /*有图标的标题，图标和文字同一行，且上下居中*/
    display: flex;
    align-items: center;

    /*每个标题右边有个margin*/
    margin-right: 15px;
    
    /*改变元素高度，可以调整导航栏与上边框的距离*/
    height: 64px;
    
    color: #fff;
}

.left-entry .entry-title svg {
    /*svg图标和文字之间有个margin*/
    margin-right: 6px;
}
```

## 2.2 \*导航-中间(搜索)

```html
			<div class="center-search-container">
				<div class="nav-search-content">
					<label>
						<input type="text" class="nav-search-input">
					</label>
				</div>
				<div class="nav-search-button">
					<svg></svg>
				</div>
			</div>
```

css

非常具有启发作用

```css
/*中间搜索区域*/
.center-search-container {
    /*搜索框和图标转成一行*/
    display: flex;
    align-items: center;
    
    /*根据其父容器中可用的额外空间来弹性撑开*/
    flex: 1;
    
    /*搜索容器(是容器)的高度和填充，右侧给图片按钮留了48的padding*/
    height: 40px;
    padding: 0 48px 0 4px;
    /*搜索容器(是容器)的美化样式*/
    border-radius: 8px;
    border: 1px solid #e3e5e7;
    background-color: #f1f2f3;
    
    /*父相子绝*/
    position: relative;
}
.center-search-container:hover {
    /*鼠标悬浮时，背景色变为白色*/
    background-color: #fff;
}

.center-search-container .nav-search-content {
    height: 20px;
    width: 100%;
    padding: 0 8px;
}
.center-search-container .nav-search-content .nav-search-input {
    /*背景色透明，使用搜索容器的颜色*/
    background-color: transparent;

    /*搜索框的宽度，撑满父容器*/
    width: 100%;
    
    /*内容会被修剪，并且其余内容是不可见的*/
    overflow: hidden;
}

.center-search-container .nav-search-button {
    /*正方形的搜索按钮*/
    width: 32px;
    height: 32px;
    
    /*父相子绝，相对父(搜索容器)右边7px*/
    position: absolute;
    right: 7px;
    
    /*将内部svg图标上中下居中*/
    display: flex;
    align-items: center;
    justify-content: center;
    
    /*样式美化*/
    border-radius: 6px;
    cursor: pointer;
    /*0.3s内平滑过渡背景颜色*/
    transition: background-color .3s;
}
.center-search-container .nav-search-button:hover {
    background-color: #e3e4e5;
}
```

## 2.3 \*导航-右侧

```html
			<ul class="right-entry">
				<li class="header-avatar">
					<a href="/">
						<span>登录</span>
					</a>
				</li>
				<li class="right-entry-item">
					<a href="/">
						<svg></svg>
						<span>大会员</span>
					</a>
				</li>
				...
				<li>
					<a href="/" class="upload">
						<svg></svg>
						<span>投稿</span>
					</a>
				</li>
			</ul>
```

css

```css
/*nav右侧入口*/
.right-entry {
    /*排成一行，且上下居中*/
    display: flex;
    align-items: center;
    
    /*和左边的搜索框保持一定的距离*/
    margin-left: 10px;
}

.right-entry .header-avatar {
    height: 50px;
    width: 50px;
    padding-right: 10px;
    
    /*父相子绝*/
    position: relative;
}
.right-entry .header-avatar a {
    /*形状*/
    width: 36px;
    height: 36px;
    line-height: 36px;

    /*父相子绝*/
    position: absolute;
    top: 6px;
    left: 10px;

    /*让span的登录文字居中*/
    display: flex;
    justify-content: center;
    
    /*美化*/
    border-radius: 50%;
    background-color: #00aeec;
    border: 2px solid #fff;
    color: #fff;
}

.right-entry .right-entry-item {
    min-width: 50px;
    margin-right: 4px;
}
.right-entry .right-entry-item a {
    /*安装列方向排列，在flex排列方向居中*/
    display: flex;
    flex-direction: column;
    align-items: center;
    
    color: #fff;
}
.right-entry .right-entry-item a span {
    font-size: 13px;
}

.right-entry .upload {
    width: 90px;
    height: 34px;
    margin-left: 10px;
    
    /*居中三板斧*/
    display: flex;
    align-items: center;
    justify-content: center;
    
    /*美化*/
    border-radius: 8px;
    color: #fff3cd;
    background-color: #fb7299;
}
.right-entry .upload span {
    margin-left: 5px;
}
```

# 3 \*banner

```html
		<!-- banner -->
        <div class="bili-banner">
			<img src="./img/header-banner.webp" alt="">
			<div class="logo">
				<a href="/">
					<img src="./img/logo.png" alt="">
				</a>
			</div>
			<div class="mask"></div>
		</div>
```

css

```css
/*banner区域*/
/*放到banner上层，压住banner区域*/
.bili-nav {
    /*相对于父元素位置，导航栏将不占用空间，banner图片将从docment开头开始*/
    position: absolute;
    top: 0;
    
    /*整个导航栏置于最顶层*/
    z-index: 1000;
}

.bili-banner {
    /*大小*/
    height: 155px;
    width: 100%;
    
    /*overflow: hidden;*/
    /*父相子绝*/
    position: relative;
}

.bili-banner img {
    /*父相子绝*/
    position: absolute;
    left: 0;
    top: 0;
    
    /*宽高100%当窗口大小改变时，会使图片比例变形*/
    /*cover是填充整个容器，保持图片的宽高比*/
    /*可能会裁剪掉部分图片以适应容器，以图片中轴线对齐网页中轴线*/
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.bili-banner .logo {
    width: 100%;
    height: 100%;
    padding: 0 64px;
    
    /*子元素按底边对齐*/
    display: flex;
    align-items: flex-end;
}
.bili-banner .logo a {
    width: 162px;
    height: 78px;
    
    position: relative;
    margin-bottom: 10px;
}

.bili-banner .mask {
    /*遮罩层*/
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    
    /*渐变色，使banner的文字更清晰*/
    background: linear-gradient(rgba(0,0,0,.4), transparent);
}
```

# 4 频道

```html
		<!-- 频道 -->
        <div class="bili-channel">
			<div class="channel-icons"></div>
			<div class="right-channel-container">
				<div class="channel-items__left"></div>
				<div class="channel-items__right"></div>
			</div>
		</div>
```

css

```css
/*频道区域*/
.bili-channel {
    height: 110px;
    padding: 0 60px;
    
    /*子元素上下居中对齐*/
    display: flex;
    align-items: center;
}
```

## 4.1 频道-左侧图标

```html
			<div class="channel-icons">
				<a href="/">
					<div class="icon-bg icon-bg__dynamic">
						<svg></svg>
					</div>
					<span class="icon-title">动态</span>
				</a>
			</div>
```

css

```css
.bili-channel .channel-icons {
    display: flex;
}
.bili-channel .channel-icons a {
    margin-right: 24px;
    
    /*图片和文字上下居中*/
    display: flex;
    flex-direction: column;
    justify-content: center;
}
.bili-channel .channel-icons a .icon-bg {
    /*大小、位置*/
    width: 46px;
    height: 46px;
    margin-bottom: 6px;

    /*让svg图标三板斧*/
    display: flex;
    align-items: center;
    justify-content: center;

    /*美化*/
    border-radius: 50%;
}
/*不同的频道图标背景颜色不同*/
.bili-channel .icon-bg__dynamic {
    background-color: #ff9212;
}
.bili-channel .icon-bg__popular {
    background-color: #f07775;
}
.bili-channel .icon-bg__channel {
    background-color: #59ca73;
}
.bili-channel .icon-bg svg {
    width: 25px;
    height: 25px;
}
.bili-channel span {
    text-align: center;
}
```

## 4.2 \*频道-右侧的左部分

```html
			<div class="right-channel-container">
				<div class="channel-items__left">
					<a href="/">番剧剧</a>
					<a href="/">国创</a>
					<a href="/">综艺</a>
					...
				</div>
			</div>
```

css

```css
/*左侧频道项列表*/
.bili-channel  .right-channel-container {
    width: 100%;
    display: flex;
}

.bili-channel .channel-items__left {
    /*保证样式宽度，并且充满*/
    min-width: 640px;
    width: 100%;
    
    /*子元素按照grid布局，11列，比例1fr*/
    display: grid;
    grid-template-columns: repeat(11, 1fr);
    grid-gap: 10px;
}

.bili-channel .channel-items__left a {
    height: 26px;
    
    /*文字上下居中*/
    line-height: 26px;
    /*文字左右居中*/
    text-align: center;
    color: #61666d;
    
    border: 1px solid #f1f2f3;
    border-radius: 6px;
    background-color: #f6f7f8;
}
```

## 4.3 \*频道-右侧的右部分

```html
			<div class="right-channel-container">
				<div class="channel-items__left"></div>
				<div class="channel-items__right">
					<a href="/">
						<svg></svg>
						<span>专栏</span>
					</a>
				</div>
			</div>
```

css

```css
/*右侧频道项列表*/
.bili-channel .channel-items__right {
    /* 使右侧频道项列表不收缩 */
    width: 240px;
    flex-shrink: 0;

    margin-left: 30px;
    
    /*grid纵向布局，2行，比例1fr*/
    display: grid;
    grid-auto-flow: column;
    grid-template-rows: repeat(2, 1fr);
    row-gap: 10px;
    
    border-left: 1px solid #e2e5e7;
}

.bili-channel .channel-items__right a {
    width: 100%;
    height: 28px;
    /*增加文本的间距*/
    letter-spacing: 2px;
    
    display: flex;
    align-items: center;
    justify-content: flex-end;
}

.bili-channel .channel-items__right a svg {
    width: 20px;
    height: 20px;
    margin-right: 4px;
    
    fill: #61666d
}

.bili-channel .channel-items__right span {
    color: #61666d;
}
```



# 5 主体

```html
	<!-- 主体 -->
    <div class="main">
        <!-- 推荐列表 -->
        <div class="recommended-container"></div>
		<!-- 滚动按钮 -->
        <div class="sidebar"></div>
	</div>
```

css

```css
/*推荐列表*/
.main {
    width: 100%;
    padding: 0 60px;
    box-sizing: border-box;
}
```

## 5.1 推荐列表

```html
		<!-- 推荐列表 -->
        <div class="recommended-container">
			<!-- 大推荐一个 -->
			<div class="carousel-area">
				<img src="./img/carousel1.avif" alt="">
				<div class="mask"></div>
				<div class="tools">
					<a href="/">顶流原来是只三角饭团</a>
					<ul>
						<li class="active"></li>
						<li></li>
						...
					</ul>
					<div class="buttons">
						<button>
							<svg></svg>
						</button>
						<button>
							<svg></svg>
						</button>
					</div>
				</div>
			</div>
			<!-- 多个小推荐 -->
			<div class="recommended-card">
				<a href="/">
					<div class="card-image">
						<img src="./img/rcmd-1.png@672w_378h_1c_!web-home-common-cover" alt="">
						<!-- 遮罩层 -->
						<div class="image-mask">
							<!-- 遮罩层左侧，播放量和弹幕数 -->
							<div class="stats-left">
								<span class="stats-item">
									<!-- 播放量 -->
									<svg></svg>
									<span>10.5万</span>
								</span>
								<span class="stats-item">
									<!-- 弹幕数 -->
									<svg></svg>
									<span>128</span>
								</span>
							</div>
							<!-- 时长 -->
							<div class="stats-duration">01:08</div>
						</div>
					</div>
				</a>
				<!-- 底部信息 -->
				<div class="card-info">
					<h3 class="info-title">
						<a href="/">十块钱，十分钟...</a>
					</h3>
					<!-- up主链接 -->
					<div class="info-bottom">
						<a href="/">
							<svg></svg>
							<span class="info-author">午夜老渔夫</span>
							<span class="info-date">· 2-28</span>
						</a>
					</div>
				</div>
			</div>
			...
		</div>
```

css

```css
.recommended-container {
    width: 100%;
    min-width: 1125px;
    
    /*5列的grid*/
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    gap: 20px;
}

.recommended-card .card-image {
    border-radius: 6px;
    overflow: hidden;

    /*给子元素(图片底部的遮罩层)定位*/
    position: relative;
}
.recommended-card .card-image img {
    width: 100%;
    height: 100%;
    /*vertical-align: middle;*/
}
/*视频底部的遮罩层*/
.recommended-card .card-image .image-mask {
    /*贴近底部*/
    position: absolute;
    bottom: 0;
    left: 0;

    height: 38px;
    padding: 16px 8px 6px;
    width: 100%;
    box-sizing: border-box;
    
    background: linear-gradient(180deg, rgba(0,0,0,0) 0% , rgba(0,0,0,.8) 100%);
    color: #fff;
    font-size: 13px;
    
    display: flex;
    align-items: center;
}
/*遮罩层左侧，播放量和弹幕数*/
.recommended-card .card-image .image-mask .stats-left {
    flex: 1;
    display: flex;
    align-items: center;
}
.recommended-card .card-image .image-mask .stats-left .stats-item {
    display: flex;
    align-items: center;
    margin-right: 12px;
}
.recommended-card .card-image .image-mask svg {
    width: 18px;
    height: 18px;
    margin-right: 2px;
    
    color: #fff;
}

/*底部信息*/
.card-info h3 {
    line-height: 22px;
    padding-right: 16px;
    font-size: 15px;
    
    /*固定写法即可，缩为2行，最后用...代替*/
    overflow: hidden;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    line-break: anywhere;
    -webkit-line-clamp: 2;
}

.card-info .info-bottom {
    margin-top: 4px;
    font-size: 13px;
    display: flex;
}
.card-info .info-bottom a {
    color: #9499a0;

    display: flex;
    align-items: center;
}
.card-info .info-bottom svg {
    width: 17px;
    height: 17px;
    margin-right: 2px;
}
.card-info .info-bottom .info-date {
    margin-left: 4px;
}

/*轮播图*/
.recommended-container .carousel-area {
    /*元素将占用第1行第2行和第1列第2列，左闭右开*/
    /*通过这种方式，可以让大块的元素占据指定的位置*/
    grid-row: 1/3;
    grid-column: 1/3;
    
    border-radius: 6px;
    overflow: hidden;
    
    position: relative;
}
.carousel-area img {
    width: 100%;
}
.carousel-area .mask {
    position: absolute;
    top: 0;

    height: 360px;
    width: 100%;

    border-radius: 6px;
    background: linear-gradient(0, #524c46 30%, transparent 60%);
}
.carousel-area .tools {
    position: absolute;
    bottom: 80px;
    left: 0;

    width: 100%;
    padding: 0 15px;
    box-sizing: border-box;
}

.carousel-area .tools a {
    font-size: 18px;
    color: #fff;
}
.carousel-area .tools ul {
    display: flex;
}
.carousel-area .tools li {
    width: 8px;
    height: 8px;
    margin: 4px;
    
    border-radius: 50%;
    background-color: #fff6;
    cursor: pointer;
}
.carousel-area .tools li.active {
    width: 14px;
    height: 14px;
    margin: 1px;
    background-color: #fff;
}
.carousel-area .tools .buttons {
    position: absolute;
    bottom: 10px;
    right: 15px;
}
.tools button {
    width: 28px;
    height: 28px;
    margin-right: 8px;
    
    /*也可以在父元素使用flex居中*/
    display: inline-flex;
    align-items: center;
    justify-content: center;

    border: 0;
    border-radius: 8px;
    background-color: #ffffff1a;
}
.tools button:last-child {
    margin-right: 0;
}
.tools button:hover {
    background-color: #ffffff4d;
}
.tools button svg {
    width: 12px;
    height: 12px;
    color: #fff;
}
```

## 5.2 滚动按钮

```html
		<div class="sidebar">
			<div class="primary-btn">
				<svg></svg>
				<span class="primary-btn-text">分区</span>
			</div>
			<div class="primary-btn go-back">回到旧版</div>
			<div class="primary-btn">
				<svg></svg>
				<span class="primary-btn-text">客服</span>
			</div> 
			<div class="primary-btn go-back">前往内测</div>
			<div class="primary-btn top-btn">
				<svg></svg>
				<span class="primary-btn-text">顶部</span>
			</div>
		</div>
```

css

```css
/*侧边栏*/
.sidebar {
    /*固定定位*/
    position: fixed;
    bottom: 40px;
    right: 12px;
}

.sidebar .primary-btn {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    
    width: 40px;
    margin-top: 6px;
    padding: 8px 0 6px;
    box-sizing: border-box;
    
    text-align: center;
    font-size: 12px;

    border: 1px solid #e3e5e7;
    border-radius: 8px;
    background-color: #fff;
    cursor: pointer;
}
.sidebar .primary-btn svg {
    width: 24px;
    height: 24px;
}
.sidebar .primary-btn .primary-btn-text {
    margin-top: 2px;
}
.sidebar .primary-btn.go-back {
    padding: 4px;
}
.sidebar .primary-btn.top-btn {
    margin-top: 12px;
}
.sidebar .primary-btn.top-btn svg {
    width: 15px;
    height: 8px;
}
```

# 套路整理

```css
.main {
    width: 100%;
    padding: 0 60px;
	/*固定用法*/	
    box-sizing: border-box;
}

.ttt {
	/*居中三板斧*/
    /*将内部svg图标上中下居中*/
    display: flex;
    align-items: center;
    justify-content: center;
}

.card-info h3 {
    /*固定写法即可，缩为2行，最后用...代替*/
	overflow: hidden;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    line-break: anywhere;
    -webkit-line-clamp: 2;
}

.bili-banner img {
    /*宽高100%当窗口大小改变时，会使图片比例变形*/
    /*cover是填充整个容器，保持图片的宽高比*/
    /*可能会裁剪掉部分图片以适应容器，以图片中轴线对齐网页中轴线*/
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.bili-banner .mask {
    /*遮罩层*/
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    
    /*渐变色，使banner的文字更清晰*/
    background: linear-gradient(rgba(0,0,0,.4), transparent);
}
```



# 总结

1.  位置(相对、填充)
2.  大小
3.  内部
4.  美化(包括hover)：圆角、背景色
5.  过渡

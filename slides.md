---
theme: seriph
background: https://images.unsplash.com/photo-1538131052268-1af52c1db73d?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1770&q=80&w=1920
fonts:
  sans: "PingFang SC"
  local: "PingFang SC"
class: 'text-center'
highlighter: shiki
lineNumbers: false
info: |
  Presentation slides for developers.
drawings:
  persist: false
transition: slide-left
css: unocss
---
# 打造一个追剧 App


[//]: # (---)

[//]: # (transition: slide-left)

[//]: # (layout: cover)

[//]: # (background: https://images.unsplash.com/photo-1619560820102-31f5b04c049a?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1770&q=80&w=1920)

[//]: # (---)

[//]: # (# App 介绍)


---
transition: slide-left
layout: image-right
image: https://images.unsplash.com/photo-1619560820102-31f5b04c049a?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1770&q=80&w=1920
---
# 视频网站现状

- 超前点播/点映礼
- 各种独播资源，需要买购买多个平台视频会员
- 会员专属广告
- 限制多设备登录
- 普通会员涨价
- 手机端会员和电视端会员不能通用
- 普通 VIP 无法投屏/限制投屏清晰度

---
transition: slide-left
layout: center
---
<img src="/bullets_fly.png" width="500"/>


---
transition: slide-left
---
# App 展示

<div class="flex">
  <div class="flex-1">
    <img src="/app_home.jpeg"  width="200">
  </div>
  <div class="flex-1">
    <img src="/app_detail.jpeg" width="200">
  </div>
  <div class="flex-1">
    <img src="/app_favorite.jpeg" width="200">
  </div>
</div>


---
transition: slide-left
layout: two-cols
---
# 计算机软件保护条例

> 第十七条　为了学习和研究软件内含的设计思想和原理，通过安装、显示、传输或者存储软件等方式使用软件的，可以不经软件著作权人许可，不向其支付报酬。

::right::

<v-clicks>
  <ul class="ml10 mt12">
    <li>工具是合法的，是否合法取决于你使用什么数据源（韩剧 TV/人人视频）</li>
    <li>不再内置数据源，未来考虑只提供工具，由用户侧进行数据源配置</li>
  </ul>
</v-clicks>


---
transition: slide-left
layout: image-left
image: https://images.unsplash.com/photo-1619560820102-31f5b04c049a?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1770&q=80&w=1920
---
# 技术栈

- Flutter & Dart
- GraphQL

---
transition: slide-left
layout: image-right
image: https://images.unsplash.com/photo-1538131052268-1af52c1db73d?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1770&q=80&w=1920
---
# Overview

| 章节 | 内容      | 
|----|---------|
| 1  | 静态资源抓取  | 
| 2  | 视频播放    |
| 3  | 投屏      |

---
transition: slide-left
layout: cover
background: https://images.unsplash.com/photo-1588153191435-c890d9adbb99?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2370&q=80
---
# 静态资源抓取

---
transition: slide-left
---
# 寻找资源
[示例网站](https://www.dm530p.net/list/?region=%E4%B8%AD%E5%9B%BD)
```shell
curl https://www.dm530p.net/list/\?region\=%E4%B8%AD%E5%9B%BD --output demo.html
```

<v-clicks>
<img src="/ssr.svg">
    <li>对 SEO 有的强烈的需求，一般会采用 SSR</li>
    <li>数据并非通过 JS 请求 API 所获得，而是被隐藏在 HTML</li>
</v-clicks>

---
transition: slide-left
---
# 抓取数据
将数据从 HTML 中提取出来，恢复成「API」

```dart {0|all}
List<Video> getVideos(String page, String cateId, String orderBy)
```


<v-clicks>
    <ul class="mt10">
        <li>Step1: 定义配置</li>
        <li>Step2: 找到 HTML</li>
        <li>Step3: 操作 DOM 获得数据</li>
    </ul>
</v-clicks>


---
transition: slide-left
---
# Crawler 配置
<div flex gap-2 m="-t-2" h-110>

  ```graphql
 # 类型（Describe what you want）
  schema {
    query: Query
  }
  
  type Query {
    init(
      siteName: String!
      siteUrl: String!
      listOptions: ListOptions!
    ): Resources
  }
  
  type Resources {
    getVideos(path: String!): VideoListData
  }

  type VideoListData {
    videos: [VideoData]!
    totalPage: Int!
  }
  
  type VideoData {
    title: String!
    detailUrl: String!
    imageUrl: String
  }
  
  directive @_dom_attr(name: String!) repeatable on FIELD
  directive @_dom_query(
    selector: String!
    fromDocument: Boolean
  ) repeatable on FIELD
  ```


  ```graphql
# 配置（Ask for what you need）
  query {
    init(
      siteName: "爱看影视"
      siteUrl: "https://ikan6.vip"
      listOptions: {
        sortBy: "sortBy"
        pageBy: "catePg"
        groups: [
          { name: "国产剧", values: [{ value: "2", key: "cateId" }] }
          { name: "动漫", values: [{ value: "4", key: "cateId" }] }
        ]
      }
    ) {
      getVideos(
        path: "/vodshow/{cateId:2}--{sortBy:time}-----{catePg}---/"
      ) {
        videos @_dom_query(selector: ".myui-vodlist") {
          title @_dom_attr(name: "title")
          imageUrl @_dom_attr(name: "data-original")
          detailUrl @_dom_attr(name: "href")
        }
      }
    }
  }
  ```

</div>

---
transition: slide-left
---
# GraphQL
GraphQL 是一种用于构建 API 的查询语言和运行时。「请求你所要的数据，不多不少」


<div class="flex mt20" style="height: 150px">
<v-clicks>
  <img src="/graph_ql_1.png" class="mr4">
  <img src="/graph_ql_2.png" class="mr4">
  <img src="/graph_ql_3.png">
</v-clicks>
</div>



---
transition: slide-left
layout: two-cols
---
# 指令集
- @_dom_query
- @_dom_query_all
- @_dom_attr
- @_string_replace
- @_def
- ...

```graphql
{
  videos @_dom_query(selector: ".myui-vodlist") {
    title @_dom_attr(name: "title")
    imageUrl @_dom_attr(name: "data-original")
    detailUrl @_dom_attr(name: "href")
  }
}
```

::right::
# Directives

- 通过指令来标记如何获取该数据
- 每个指令对应一个函数
- 通过组合 directives，应对复杂业务场景
- 通过扩展 directives，应对需求变化

---
transition: slide-left
---
# 配置解析

<div flex gap-2 m="-t-2" h-110>

```graphql {all} {maxHeight:'420px'}
query {
  init(
    siteName: "爱看影视"
    siteUrl: "https://ikan6.vip"
    listOptions: {
      sortBy: "sortBy"
      pageBy: "catePg"
      groups: [
        { name: "国产剧", values: [{ value: "2", key: "cateId" }] }
        { name: "动漫", values: [{ value: "4", key: "cateId" }] }
      ]
    }
  ) {
    getVideos(
      path: "/vodshow/{cateId:2}--{sortBy:time}-----{catePg}---/"
    ) {
      videos @_dom_query(selector: ".myui-vodlist") {
        title @_dom_attr(name: "title")
        imageUrl @_dom_attr(name: "data-original")
        detailUrl @_dom_attr(name: "href")
      }
    }
  }
}
```

```json {all} {maxHeight:'420px'}
{
  "siteName": "爱看影视",
  "siteUrl": "https://ikan6.vip",
  "resources": {
    "getVideos": {
      "path": "/vodshow/{cateId}-{area}-{by}-{class}-----{catePg}---{year}/",
      "params": [
        {
          "name": "cateId",
          "defaultValue": "2",
          "enums": [
            "0",
            "1",
            "2",
            "3",
            "4"
          ]
        },
        {
          "name": "area",
          "defaultValue": ""
        },
        {
          "name": "by",
          "defaultValue": ""
        },
        {
          "name": "class",
          "defaultValue": ""
        },
        {
          "name": "catePg",
          "defaultValue": ""
        },
        {
          "name": "year",
          "defaultValue": ""
        }
      ],
      "response": {
        "__type": "Videos",
        "videos": {
          "__type": "[Video]",
          "directives": [
            {
              "_domGetAll": {
                "selector": "div>a[href^='/voddetail']"
              }
            }
          ],
          "__items": {
            "__props": {
              "title": {
                "__type": "String",
                "directives": [
                  {
                    "_domAttr": {
                      "name": "title"
                    }
                  }
                ]
              },
              "imageUrl": {
                "__type": "String",
                "directives": [
                  {
                    "_domAttr": {
                      "name": "data-original"
                    }
                  }
                ]
              },
              "detailUrl": {
                "__type": "String",
                "directives": [
                  {
                    "_domAttr": {
                      "name": "href"
                    }
                  }
                ]
              }
            }
          }
        },
        "page": {
          "__type": "Page",
          "total": {
            "__type": "Int",
            "directives": [
              {
                "_domGetByText": {
                  "selector": ".myui-page li a",
                  "text": "尾页"
                }
              },
              {
                "_domAttr": {
                  "name": "href"
                }
              }
            ]
          }
        }
      }
    }
  }
}
```

</div>


---
transition: slide-left
---
# Why GraphQL

<v-clicks>
<ul>
    <li>相较 JSON 而言，表达更简洁，方便后期维护配置</li>
    <li>拥有类型系统，避免配置出错</li>
    <li>可扩展性，可以使用自定义指令扩展查询语言</li>
    <li>被多种语言支持，如 Dart/JavaScript/Kotlin，能够快速迁移到其他地方</li>
</ul>
</v-clicks>

---
transition: slide-left
---
# 如何解析
GraphQL AST(对源代码语法的抽象解释) 

<img src="/ast.png">


---
transition: slide-left
---
# 静态资源抓取流程
<img src="/data_crawl.png">



---
transition: slide-left
layout: cover
background: https://images.unsplash.com/photo-1619075120156-f5729c752edf?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2671&q=80
---
# 视频播放

---
transition: slide-left
---
# 视频嗅探
播放地址不是静态的，并不存在于 HTML 中。如何抓取播放链接？

<v-clicks :every='1'>
  <div class="center middle mt20">
    <img src="/web_view.png" width="822">
  </div>
</v-clicks>

---
transition: slide-left
---
# M3U8 (HLS 索引文件) 

HLS（HTTP Live Streaming）协议是由苹果公司提出的基于 HTTP 的流媒体传输协议，用于音频和视频的实时传输。

<div class="flex items-center gap-16">
<v-clicks :every='1'>
  <div class="flex-1">
      <img src="/hls.png" width="460">
    </div>
  </v-clicks>
  <div class="flex-1">
    <v-clicks :every='1'>
      <div>
        原理：将媒体文件拆分成一系列小的片段，并使用 HTTP 协议来传输这些片段。这些媒体段可以被独立地请求和下载。
      </div>
      <div class="mt-4">
          组成：
          <div>- HTTP: 传输协议</div>
          <div>- M3U8: 索引文件</div>
          <div>- TS(Transport Stream): 音视频的媒体信息</div>
      </div>
    </v-clicks>
  </div>
</div>

---
transition: slide-left
layout: two-cols
---
# HLS 的应用场景
- 直播
- 在线教育
- 各大视频平台

::right::
# 为什么选择 HLS？
<v-clicks>
    <li>适应不同网络状况：可以根据当前网络情况自动调整码率和分辨率</li>
    <li>支持多平台：包括手机/电脑/电视等，可以在不同的平台上提供一致的视频体验。</li>
    <li>可以实现直播和点播：为视频网站提供了更多应用场景</li>
</v-clicks>


---
transition: slide-left
layout: cover
background: https://images.unsplash.com/photo-1650968163166-da7e87ab4e8c?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1770&q=80
---
# 投屏

---
transition: slide-left
---
# 投屏
投屏技术是一种将移动设备或电脑屏幕内容「无线传输」到大屏幕设备上显示的技术

<div class="flex mt-20 space-around">
<div class="flex-1 mr-4">
  <div>
    <img src="/mirror_recreation.jpeg" width="300" >
  </div>
  <p class="text-center">家庭娱乐</p>
</div>
<div class="flex-1 mr-4">
  <div>
    <img src="/mirror_meeting.jpeg" width="300" >
  </div>
  <p class="text-center">商务会议</p>
</div>
<div class="flex-1 mr-4">
  <div>
    <img src="/mirror_teaching.jpeg" width="300" >
  </div>
  <p class="text-center">教育培训</p>
</div>
</div>

---
transition: slide-left
---
# DLNA vs AirPlay
| 特征 | DLNA协议                           | AirPlay |
| --- |----------------------------------| --- |
| 设备兼容性 | 跨平台，支持 Android/IOS/Windows 等各种设备 | 仅限于苹果设备之间的连接和交互 |
| 支持的媒体格式和协议 | 支持多种不同的媒体格式和流媒体协议                | 仅支持特定的媒体格式和协议，如H.264和AAC等 |
| 控制选项 | 提供更多的控制选项，如播放控制、音量控制、暂停和跳过等功能    | 提供更简单、更直接的传输体验，但控制选项更少 |
| 连接方式 | 可以通过有线或无线网络连接设备                  | 仅能通过无线网络连接设备 |


---
transition: slide-left
---
# DLNA 原理

<div class="flex justify-center">
<img src="/dlna.svg" width="600">
</div>


---
transition: slide-left
layout: two-cols
---

# 设备发现
<div class="flex justify-center">
  <img src="/ssdp_devices.png" width="200">
</div>

::right::
# SSDP
简单服务发现（Simple Service Discovery Protocol，SSDP）允许设备在同一网络上发现彼此的存在，从而实现设备间的通信和协作。

<img src="/ssdp.svg" width="480">

---
transition: slide-left
---
# 总有一些坑
<div class="flex center">
  <img src="/cache_pool.svg">
</div>

<v-clicks>
<li class="mt10">m3u8 地址单次消费，无法同时给手机播放器和投屏使用</li>
<li>文件系统: 
    <ul class="ml8">
        <li>temp 文件夹：用于存放临时文件。这个文件夹里面的文件会被手机管家清理掉。</li>
        <li>doc 文件夹：用于存储应用程序文档和资源的文件夹。比如图片、音频、视频等。</li>
    </ul>
</li>
</v-clicks>

---
transition: slide-left
---
# 总结

<v-clicks>
      <h3>静态资源的抓取</h3>
        <li> GraphQL -> AST -> Crawler Schema -> HTML -> DOM -> 静态资源 -> 列表页和详情页的展示  </li>
      <h3>视频播放</h3>
        <li>视频嗅探：通过 WebView 捕获视频资源地址(x.m3u8/x.mp4) </li>
        <li>HLS 协议：M3U8 + TS + HTTP</li>
      <h3>投屏</h3>
        <li>DLNA 协议：通过这种跨平台的标准化协议，将手机上获取到的视频地址传输到电视上播放 </li>
        <li>DLNA 原理：通过控制器，服务器，渲染器和播放器的协作，实现设备之间的互联互通</li>
        <li>SSDP 简单服务发现协议：可以让设备在同一网络上发现彼此的存在</li>
        <li>踩过的坑：引入缓存池，将获取到的 m3u8/mp4 文件保存下来，然后将手机作为服务器，向电视提供播放地址 </li>
</v-clicks>


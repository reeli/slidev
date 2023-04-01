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

---
transition: slide-left
layout: image-right
image: https://images.unsplash.com/photo-1538131052268-1af52c1db73d?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1770&q=80&w=1920
---
# 视频网站现状

- 超前点播/点映礼
- 各种独播资源，需要买购买多个平台视频会员
- 会员专属广告
- 限制多设备登录
- 普通会员涨价
- 手机端会员和电视端会员不能通用
- 普通 VIP 用户无法投屏/投屏清晰度太低

---
transition: slide-left
---
# App 展示

<div class="flex">
  <div class="flex-1">
    <img src="/app_home.jpeg"  width="200">
  </div>
  <div class="flex-1">
    <img src="/app_favorite.jpeg" width="200">
  </div>
  <div class="flex-1">
    <img src="/app_detail.jpeg" width="200">
  </div>
</div>
---
transition: slide-left
layout: image-left
image: https://images.unsplash.com/photo-1538131052268-1af52c1db73d?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1770&q=80&w=1920
---
# 计算机软件保护条例

> 第十七条　为了学习和研究软件内含的设计思想和原理，通过安装、显示、传输或者存储软件等方式使用软件的，可以不经软件著作权人许可，不向其支付报酬。

<v-clicks>
  <ul class="mt20 text-grey-500">
    <li>不再内置数据源，未来考虑只提供工具，由用户侧进行数据源配置</li>
    <li>工具是合法的，是否合法取决于你使用什么数据源（韩剧 TV/人人视频）</li>
  </ul>
</v-clicks>
---
transition: slide-left
layout: image-left
image: https://images.unsplash.com/photo-1538131052268-1af52c1db73d?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1770&q=80&w=1920
---
# 技术栈

- Flutter & Dart
- GraphQL

---
transition: slide-left
---
# Overview

| 章节      | 功能        | 技术实现    |
|---------|-----------|---------|
| 1       | 列表页/详情页展示 | 静态资源抓取  |
| 2 | 视频播放      | 视频嗅探    |
| 3 | 投屏        | DLNA 投屏 |

---
transition: slide-left
layout: cover
background: https://images.unsplash.com/photo-1538131052268-1af52c1db73d?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1770&q=80&w=1920
---
# 静态资源抓取

---
transition: slide-left
layout: image-right
image: https://images.unsplash.com/photo-1538131052268-1af52c1db73d?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1770&q=80&w=1920
---
# 寻找资源
[示例网站](https://www.dm530p.net/list/?region=%E4%B8%AD%E5%9B%BD)
```shell
curl https://www.dm530p.net/list/\?region\=%E4%B8%AD%E5%9B%BD --output demo.html
```

---
transition: slide-left
---
# 服务端渲染

<img src="/ssr.svg">

---
transition: slide-left
---
# GraphQL
> - GraphQL 是一种用于构建 API 的查询语言和运行时。「请求你所要的数据，不多不少」


<div class="flex mt20" style="height: 150px">
<v-clicks>
  <img src="/graph_ql_1.png" class="mr4">
  <img src="/graph_ql_2.png" class="mr4">
  <img src="/graph_ql_3.png">
</v-clicks>
</div>



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
layout: two-cols
---
# 指令集
- _dom_query
- _dom_query_all
- _dom_siblings
- _dom_attr
- _string_replace
- _string_extract
- _string_switch
- _def

::right::
# Directives

- 标记如何获取该数据
- 通过组合 directives，应对复杂业务场景
- 通过扩展 Directives，应对需求变化

---
transition: slide-left
---
# 配置解析
GraphQL AST -> Crawler Config 

<img src="/ast.png">

---
transition: slide-left
---
# 配置解析

Crawler Config

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

---
transition: slide-left
---
# 静态资源抓取流程
<img src="/data_crawl.png">

---
transition: slide-left
---
# Why GraphQL
- 相较 JSON 而言，表达更简洁，方便后期维护配置
- 拥有类型系统，避免配置出错
- 可扩展性，可以使用自定义指令扩展查询语言
- 被多种语言支持，如 Dart/JavaScript/Kotlin，能够快速迁移到其他地方

---
transition: slide-left
layout: cover
background: https://images.unsplash.com/photo-1637580980556-085dee659c7e?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=1080&ixid=MnwxfDB8MXxyYW5kb218MHw5NDczNDU2Nnx8fHx8fHwxNjc5NTg3NTI4&ixlib=rb-4.0.3&q=80&utm_campaign=api-credit&utm_medium=referral&utm_source=unsplash_source&w=1920
---
# 视频播放

---
transition: slide-left
---
# HLS 流媒体协议 

HLS（HTTP Live Streaming）协议是由苹果公司提出的基于 HTTP 的流媒体传输协议，用于音频和视频的实时传输。

<div class="flex items-center gap-16">
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
      <div class="mt-4">
        应用场景：
        <div>- 直播/在线教育</div>
        <div>- 各大视频平台</div>
      </div>
    </v-clicks>
  </div>
  <v-clicks :every='1'>
  <div class="flex-1">
      <img src="/hls.png" width="460">
    </div>
  </v-clicks>
</div>

---
transition: slide-left
layout: image-right
image: https://images.unsplash.com/photo-1538131052268-1af52c1db73d?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1770&q=80&w=1920
---
# 为什么选择 HLS？

1. 适应不同网络状况：可以根据当前网络情况自动调整码率和分辨率
2. 支持多平台：包括手机/电脑/电视等，可以在不同的平台上提供一致的视频体验。
3. 可以实现直播和点播：为视频网站提供了更多应用场景。

---
transition: slide-left
---
# 视频嗅探
播放地址不是静态的，并不存在于 HTML 中。如何抓取播放链接？

<v-clicks :every='1'>
  <div class="center middle">
    <img src="/web_view.png" width="822">
  </div>
  <div class="mt8 text-gray-500">
    将 WebView 的透明度设为 0 或者使用 headless 模式
  </div>
</v-clicks>

---
transition: slide-left
---
# 投屏
> - 投屏技术是一种将移动设备或电脑屏幕内容「无线传输」到大屏幕设备上显示的技术。
> - 通过Wi-Fi或蓝牙连接将源设备和大屏幕设备连接在一起，并使用特定的投屏协议将屏幕内容从源设备传输到大屏幕设备。

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
layout: image-right
image: https://images.unsplash.com/photo-1538131052268-1af52c1db73d?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1770&q=80&w=1920
---
# DLNA
> - DLNA是数字生活联盟（Digital Living Network Alliance）的缩写，是一个非营利性组织，致力于推广数字娱乐设备之间的互联互通。

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
# 设备发现
<div class="flex justify-center">
  <img src="/ssdp_devices.png" width="200">
</div>

---
transition: slide-left
---
# SSDP
> 简单服务发现（Simple Service Discovery Protocol，SSDP）是一种基于 UDP 的协议，它允许设备在同一网络上发现彼此的存在，从而实现设备间的通信和协作。SSDP 是 UPnP（Universal Plug and Play）协议的子集。

<img src="/ssdp.svg" width="480">

---
transition: slide-left
---
# 各协议之间的关系
<img src="/dlna_base.svg" width="300">

---
transition: slide-left
---
# DLNA 原理

<img src="/dlna.svg" width="650">

---
transition: slide-left
---
# 单次消费的播放链接
<div class="flex center">
  <img src="/cache_pool.svg" width="700">
</div>


---
transition: slide-left
---
# 总结

<v-clicks>
 <ul>
  <li>静态资源的抓取：GraphQL -> AST -> Crawler Config -> Resource </li>
  <li>视频播放：HLS 协议 = HTTP + M3U8 + TS </li>
  <li>视频嗅探：通过 WebView 捕获视频资源地址(x.m3u8/x.mp4) </li>
  <li>DLNA 投屏协议：通过这种跨平台的标准化协议，将手机上获取到的视频地址传输到电视上播放 </li>
  <li>SSDP 简单服务发现协议：可以让设备在同一网络上发现彼此的存在</li>
  <li>DLNA 原理：通过控制器，服务器，渲染器和播放器的协作，实现设备之间的互联互通</li>
  <li>链接只能单次消费的解决方案：引入缓存池，将获取到的 m3u8/mp4 文件保存下来，然后将手机作为服务器，向电视提供播放地址 </li>
 </ul>
</v-clicks>


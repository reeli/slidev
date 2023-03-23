---
theme: seriph
background: https://images.unsplash.com/photo-1612334001559-947862cc2202?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=1080&ixid=MnwxfDB8MXxyYW5kb218MHw5NDczNDU2Nnx8fHx8fHwxNjc5NDkyNTU2&ixlib=rb-4.0.3&q=80&utm_campaign=api-credit&utm_medium=referral&utm_source=unsplash_source&w=1920
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
layout: image-left
image: https://source.unsplash.com/collection/94734566/1920x1080
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
# 计算机软件保护条例

> 第十七条　为了学习和研究软件内含的设计思想和原理，通过安装、显示、传输或者存储软件等方式使用软件的，可以不经软件著作权人许可，不向其支付报酬。

---
transition: slide-left
layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080
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
background: https://source.unsplash.com/collection/94734566/1920x1080
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
- 被多种语言支持，如 Dart/JavaScript/Kotlin，能够快速迁移到其他地方

---
transition: slide-left
layout: cover
background: https://source.unsplash.com/collection/94734566/1920x1080
---
# 视频播放

---
transition: slide-up
---
# HLS 流媒体协议 

HLS（HTTP Live Streaming）协议是由苹果公司提出的基于 HTTP 的流媒体传输协议，用于音频和视频的实时传输。

<div class="flex items-center gap-16">
    <div class="flex-1">
      <img src="/hls.png" width="460">
    </div>


  <div class="flex-1">
  原理：将媒体文件拆分成一系列小的片段，并使用 HTTP 协议来传输这些片段。这些媒体段可以被独立地请求和下载。

  组成：
  - HTTP: 传输协议
  - M3U8: 索引文件
  - TS: 音视频的媒体信息

  应用场景：
  - 视频直播/在线教育/视频平台
  </div>
</div>

---
transition: slide-up
---
# 展望

- 目前内置数据源，未来考虑只提供工具。工具是合法的，是否合法取决于你使用什么数据源（韩剧 TV/人人视频）
- 搜索

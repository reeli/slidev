> HLS 协议通过将媒体流分成一系列小的可下载的文件（通常是 10 秒左右的小片段）并使用 HTTP 协议来传输这些文件。每个文件都包含媒体的一个小段，这些小片段可以随时在客户端上播放。HLS 还使用了一个索引文件（.m3u8 文件）来告知客户端媒体文件的位置。
> HLS 还支持自适应比特率技术，它可以根据客户端的带宽和处理能力来自动选择最合适的媒体质量。这意味着客户端可以在网络速度较慢或带宽较小的情况下自动降低媒体质量，以确保流畅的播放。同时，HLS 还支持多语言、字幕、广告等高级功能。

HLS 协议被广泛用于视频直播、点播、电视应用等领域，并且已经成为了流媒体领域的一个重要标准。除了苹果公司，许多其他流媒体服务提供商和互联网电视广播公司也已经采用了 HLS 协议来实现他们的服务。

HLS协议通过将整个媒体文件分成一系列小的媒体段来实现流媒体传输，这些媒体段可以被独立地请求和下载。当客户端请求一个流媒体时，服务器会返回一个包含多个媒体段的播放列表（M3U8文件），客户端通过下载并播放这些媒体段来实现流媒体播放。

HLS协议具有以下特点：

支持多种分辨率、码率和编码格式：通过在播放列表中包含多个不同的媒体流（例如不同的分辨率、码率和编码格式），客户端可以根据当前的带宽和设备能力自动选择最适合的媒体流进行播放。
支持点播和直播：HLS协议可以用于点播和直播，其中直播需要实时切片，每隔一段时间将直播流切成一个个媒体段并生成新的播放列表。
兼容性好：HLS协议基于HTTP协议，可以在大多数网络环境下使用，且可以在iOS、Android、Windows、Mac等各种平台和设备上播放。
总的来说，HLS协议是一种可靠、高效、灵活和兼容性好的流媒体传输协议，被广泛应用于视频直播、点播、在线教育等领域。

---
视频封装格式和视频编码格式是两个不同的概念，它们分别用于描述视频文件的不同方面。

视频封装格式通常指的是视频文件的容器格式，用于将视频数据、音频数据、字幕等不同类型的数据打包到同一个文件中。常见的视频封装格式包括AVI、MP4、MKV、MOV等，它们有不同的特点和支持的功能，例如支持不同的音频和视频编码格式、字幕和章节等。

视频编码格式则是用于描述视频数据的压缩格式，用于将原始视频数据压缩为更小的文件大小，以便于存储和传输。常见的视频编码格式包括H.264、H.265、VP9等，它们有不同的压缩算法和特点，例如压缩率、图像质量、实时性等。

简单来说，视频封装格式是用于将不同类型的数据打包到一个文件中，而视频编码格式是用于压缩视频数据的格式。在实际应用中，不同的视频封装格式和视频编码格式的选择取决于具体的需求和应用场景。

视频容器格式（Video Container Format），也称为封装格式（Wrapper Format），是用于将视频和音频等多种数据流打包成一个文件的格式。它类似于一个“盒子”，可以将多种不同类型的数据（例如视频、音频、字幕、章节等）打包到同一个文件中，方便管理、存储和传输。

视频容器格式通常由一个头部和一系列数据块组成。头部包含了文件的基本信息，例如视频编码格式、分辨率、帧率、音频编码格式、声道数等，以及一些元数据信息，例如作者、拍摄日期、描述等。数据块则包含了实际的视频和音频数据，以及其他附加信息，例如字幕、章节等。

常见的视频容器格式有 AVI、MP4、MKV、MOV 等，它们有不同的特点和支持的功能。例如，MP4 是一种流行的容器格式，支持 H.264 和 H.265 等常见的视频编码格式，同时也支持 AAC 等常见的音频编码格式，还支持字幕

是的，TS是一种视频容器格式。TS代表Transport Stream（传输流），是一种用于数字视频广播和存储的标准格式。它通常用于数字电视广播和蓝光光盘中的视频，以及用于IPTV和视频流媒体服务的视频传输。TS格式使用MPEG-2视频压缩和AC3或MP2音频压缩，同时支持多个音频和字幕流。该格式还可以存储其他元数据，如时间戳、频道信息和节目信息。

----

视频压缩格式是指用于压缩数字视频文件的格式。数字视频文件的大小通常很大，压缩可以减小文件大小，使其更容易在互联网上共享和传输。

常见的视频压缩格式包括：

MPEG-2：一种广泛用于数字电视广播和DVD视频的压缩格式。

MPEG-4：一种比MPEG-2更先进的压缩格式，广泛用于网络视频和流媒体服务。

H.264：一种高效的视频压缩格式，也称为AVC（Advanced Video Coding），广泛用于网络视频和蓝光光盘等高清视频存储。

HEVC：一种比H.264更先进的压缩格式，也称为H.265，可以提供更高的压缩比，适用于4K和8K分辨率视频。

VP9：一种由谷歌开发的开放源代码视频压缩格式，广泛用于YouTube等视频分享网站。

这些压缩格式都有自己的优点和适用范围，选择哪种格式取决于使用场景、设备支持和文件大小等因素。

M3U8的完整名称是"UTF-8 M3U Playlist File"，其中M3U是一种媒体播放列表文件的格式，而"8"代表使用了UTF-8字符编码。因此，M3U8文件实际上是M3U文件的一种扩展，用于描述HLS（HTTP Live Streaming）协议中的播放列表。

以下是DLNA协议和AirPlay的主要区别的表格形式展示：

| 特征 | DLNA协议                           | AirPlay |
| --- |----------------------------------| --- |
| 设备兼容性 | 跨平台，支持 Android、IOS、Windows 等各种设备 | 仅限于苹果设备之间的连接和交互 |
| 支持的媒体格式和协议 | 支持多种不同的媒体格式和流媒体协议                | 仅支持特定的媒体格式和协议，如H.264和AAC等 |
| 控制选项 | 提供更多的控制选项，如播放控制、音量控制、暂停和跳过等功能    | 提供更简单、更直接的传输体验，但控制选项更少 |
| 连接方式 | 可以通过有线或无线网络连接设备                  | 仅能通过无线网络连接设备 |

总的来说，DLNA和AirPlay在兼容性、支持的媒体格式和协议、控制选项以及连接方式等方面存在一些区别。DLNA是一种跨平台的标准化协议，可以与多种不同品牌和操作系统的设备进行连接和交互，同时支持多种不同的媒体格式和流媒体协议，并提供更多的控制选项。AirPlay是苹果公司开发的专有协议，仅限于苹果设备之间的连接和交互，但提供更简单、更直接的传输体验，同时控制选项较少。
请使用 markdown 格式输出，我需要能够复制粘贴

以下是DLNA协议和AirPlay的主要区别的markdown格式输出：

总的来说，DLNA和AirPlay在兼容性、支持的媒体格式和协议、控制选项以及连接方式等方面存在一些区别。DLNA是一种跨平台的标准化协议，可以与多种不同品牌和操作系统的设备进行连接和交互，同时支持多种不同的媒体格式和流媒体协议，并提供更多的控制选项。AirPlay是苹果公司开发的专有协议，仅限于苹果设备之间的连接和交互，但提供更简单、更直接的传输体验，同时控制选项较少。
参考：


A: DLNA服务器(手机)
B: 控制点(手机/电视遥控器)
C: DLNA渲染器(电视)
D: DLNA客户端(电视)
A -> B: 1.发送设备信息
B -> A: 2.请求媒体库信息
A -> B: 3.响应媒体库信息
B -> D: 4.请求播放媒体文件
D -> B: 5. 返回媒体文件信息
B -> C: 6. 播放媒体文件
C -> B: 7. 返回播放状态


DLNA渲染器可以理解为一个可接收DLNA客户端的指令并将媒体文件播放输出的设备，类似于普通的播放器，但并不是所有的DLNA渲染器都能支持本地播放媒体文件。DLNA渲染器一般都需要配合DLNA客户端才能实现完整的功能，通过DLNA客户端将媒体文件推送到DLNA渲染器上进行播放。同时，DLNA渲染器通常还可以通过自身的UI控制界面或者通过DLNA客户端来控制音量、播放、暂停等媒体播放相关的操作


在DLNA网络中，控制点是指能够向DLNA设备发送指令的设备或应用程序，它负责向DLNA设备发送控制指令，以实现对媒体文件的播放、暂停、快进等操作。DLNA控制点可以是一个软件程序，也可以是一种物理设备，例如智能手机、平板电脑、电脑等。

电视遥控器本身并不是DLNA控制点，但可以通过配合支持DLNA协议的设备或应用程序，实现控制DLNA设备的功能。例如，一些支持DLNA的电视或电视盒子，可以通过手机或电脑上安装的DLNA控制点应用程序，实现通过手机或电脑控制电视的功能。因此，虽然电视遥控器本身不是DLNA控制点，但它可以作为控制点的一种输入方式，通过与其他支持DLNA协议的设备或应用程序配合使用，实现对DLNA设备的控制。

shape: sequence_diagram

Client: {
广播 Client 设备信息、IP地址、端口号\n通知其他设备自己的存在
}

Router: {
}

Router -> Device1: 发送 SSDP 搜索请求
Router -> Device2: 发送 SSDP 搜索请求

Device1: {
向客户端返回设备信息、IP地址、端口号
}
Device2 -> Client: 返回搜索响应
Device1 -> Client: 返回搜索响应



UDP（User Datagram Protocol）是一种无连接的网络传输协议，它是面向无连接的传输层协议，与TCP（传输控制协议）相对。UDP协议不像TCP协议那样需要在发送数据前建立连接和维护状态，因此UDP协议传输速度快、资源消耗少。但是UDP协议也有一些缺点，比如不保证数据传输的可靠性，没有重传机制，数据包也不保证按发送顺序到达目的地。UDP协议通常用于需要快速传输数据的应用场景，比如DNS查询、实时视频和音频传输等。

DLNA、UPnP和SSDP是三个不同但相关的协议。

UPnP（通用即插即用）是一个开放的网络协议，旨在使网络设备和计算机之间的通信更加简单。UPnP允许设备发现和控制其他设备，以便它们可以共享信息和服务。

SSDP（简单服务发现协议）是UPnP协议的子集，它是用于发现UPnP设备的协议。当一个设备加入网络时，它会广播一个SSDP请求，让其他设备知道它的存在。当其他设备回复时，新设备将被添加到UPnP设备列表中。

DLNA（数字生活网络联盟）是一组制定数字媒体设备间互操作性标准的公司组成的联盟。DLNA基于UPnP协议，增加了媒体格式和播放控制的规范。DLNA设备是UPnP设备的子集，可以通过UPnP协议来发现和控制。

因此，可以将它们看作是相互关联的协议，DLNA是建立在UPnP和SSDP之上的媒体协议，它使用UPnP协议和SSDP协议来发现和控制DLNA设备。



> - DLNA 是基于 UPnP 协议的，UPnP 协议使用 SSDP 协议进行服务发现，而 SSDP 协议则使用 UDP 协议进行通信。
> - SSDP（Simple Service Discovery Protocol）是 UPnP（Universal Plug and Play）协议的子集。UPnP 是一个面向设备的网络架构，它使用一组协议和技术来简化设备之间的连接和通信。


媒体播放和媒体渲染是两个不同的概念。

媒体播放是指播放媒体文件（例如音频或视频），通常由播放器完成。播放器通常提供一系列控制媒体播放的功能，例如播放、暂停、快进、快退、音量控制等。在 DLNA 中，DLNA播放器就是负责播放媒体文件的设备。

媒体渲染是指将媒体文件的内容呈现到屏幕或扬声器上，通常由渲染器完成。渲染器负责将音视频数据解码并渲染到屏幕上，同时也可以控制输出设备的音量、屏幕亮度等。在 DLNA 中，DLNA渲染器就是负责将媒体文件的内容呈现到屏幕或扬声器上的设备。

需要注意的是，同一个设备可能同时充当播放器和渲染器的角色，例如手机可以既播放音乐，又将音乐渲染到扬声器上。但在 DLNA 中，通常将这两个角色分开，以便更好地实现功能的拓展和组合。

- https://zhuanlan.zhihu.com/p/355136397
- https://zh.wikipedia.org/zh-cn/%E5%AA%92%E4%BD%93%E6%BA%90%E6%89%A9%E5%B1%95


B: 控制点(手机APP/电视遥控器)
C: DLNA渲染器(电视)

B -> C: 1. 发送播放请求并传输媒体文件
C -> B: 2. 返回播放状态



---
Video Provider: {
A
B
}

Cache Pool: {
FileA: m3u8 content A
FileB: m3u8 content B
}

Cache Pool -> DLNA Player
Cache Pool -> Player

Client -> Video Provider: request url
Video Provider -> Client: m3u8 content
Client -> Cache Pool: store data

https://kroki.io/d2/svg/eNoLy0xJzVcIKMovAzKKrBSquRQUHIHYiauWi8s5MTkjVSEgPz8HIuGWmZPqaKWQa1xqoZCcn1eSmlcCVgwSd0ITRzNAQddOwcXHz1EhICexMrUITQYqyOWckwnSCxQJQ3NXUWphaWpxiUJpUQ4XqhxINUQfqguQDEP2R3FJflGqQkpiSSIAlOxPTA==


sequenceDiagram
participant C as Control Device (Mobile)

    participant S as Server (DLNA)
    participant R as Rendering Device (TV)
    participant P as Player

participant MP as Media Provider

    C->>S: 发现设备
    S-->>C: 发送设备信息
  
    
    C->>P: 发送播放媒体资源
    activate P

   
    C->>R: 发送播放指令
    
    R->>P: 开始播放
    P->>MP: 请求媒体资源
    MP-->>P: 发送媒体资源
    P-->>R: 解码并传视频帧 
    
    R-->>C: 发送播放状态
     

    C->>R: 发送控制指令(暂停)
    R->>P: 暂停解码
    P-->>R: 通知暂停成功
    R-->>C: 发送控制响应

    deactivate P

https://mermaid.live/view#pako:eNptU11LG0EU_SvDPCWQlBZBMA-CJL65ZclaH8q-THbHdGAzk04moSJCNpRGbLVqfBKp2iqBQmv70LS1afpnMpvNv-gkk49dzD7t7jn3nHPvzN2FDnMxzECbVvDLKqYOzhFU5Khk0zLigjikjKgAWYAqIMuo4MwDOVwjDgYJgxWIh5M2LbBXgBcLKLG0lFpeTq2spB4_epIEm1s2BeqJClkjodzG0zVgYV7DHCTkbVN2G8GHC7BWLicfVuRHFXlMXcwJLc7MN7cWcM2ZuumhnUXqSifemTGuMbBLEDA5qxHlY1MtnU2vrloZIN-fDI6-hV978qapASutkOwYGdZ9jfT_XQf-3QjXnLmEOSUGp1-Cs578fNr_2wp_vA7uj3VR4ll-Y9INcgSpIYGBOQkxl8nHZYJ3zf6fm6hXfuLVrcv2W03SgKkAQyHh3c_geyPqr3HDTEdjPiSMceUftj8Nrnz5u9PvXoW9Vth-M_x4In-1QTxGdDg6x-CgE9R9jYPoeOdNHbXlfkc3lQjOG9K_SMba0v90gniqYf18cHmr8WD_WB5cLgwyNpCtQ3l_Nk3g4vi8YQqWMC8h4qqV2B2fJRQvcAnbMKNeXbyNqp6w1bbsKWq17KrKdZcIxmFmG3kVnIKoKpi1Qx2YEbyKp6TJUs1Y6uo9Z2z6vfcf7sZ1Sw


DLNA的工作原理是通过建立DLNA服务器和DLNA客户端之间的通信，实现不同设备之间的数据传输和共享。


UPnP(Universal Plug and Play): {
shape: text
简化设备之间的连接和通信
}
DLNA(Digital Living Network Alliance): {
shape: text
实现不同设备之间的数据传输和共享
}
SSDP(Simple Service Discovery Protocol): {
shape: text
用于服务发现
}
UDP(User Datagram Protocol): {
shape: text
传输数据
}

DLNA(Digital Living Network Alliance) -> UPnP(Universal Plug and Play)
UPnP(Universal Plug and Play) -> SSDP(Simple Service Discovery Protocol)
SSDP(Simple Service Discovery Protocol) -> UDP(User Datagram Protocol)


GraphQL 并没有和任何特定数据库或者存储引擎绑定，而是依靠你现有的代码和数据支撑


Serverside Render:

direction: right

C: Client {
HMTL 页面
}
S: Server {
组装 HTML
}
B: BFF {Data}
C -> S: 发起请求
S -> B: 获取数据
B -> S: 返回数据
S -> C: 返回 HTML


pipeline 流水线，通过组合方法来实现复杂功能

在计算机科学中，抽象语法树（Abstract Syntax Tree，AST），或简称语法树（Syntax tree），是源代码语法结构的一种抽象表示。 它以树状的形式表现编程语言的语法结构，树上的每个节点都表示源代码中的一种结构。 之所以说语法是“抽象”的，是因为这里的语法并不会表示出真实语法中出现的每个细节。

语法分析器通常是作为编译器或解释器的组件出现的，它的作用是进行语法检查、并构建由输入的单词组成的数据结构。


Video Provider: {
A
B
}

Cache Pool: {
FileA: m3u8 content A
FileB: m3u8 content B
}

Cache Pool <- Mobile Server
Cache Pool <- Mobile Player

Mobile Server -> DLNA Player

Client -> Video Provider: request url
Video Provider -> Client: m3u8 content
Client -> Cache Pool: store data


- web 安全问题，透明的，只要你经过浏览器，数据都能被截获
- 授权机制：m3u8 授权相当于授权了一组 ts, ts 可以放到 CDN，没有 m3u8 播放列表，不知道播放顺序，ts 拿去也没什么用
- 爬虫引擎 -> 列表/详情页的抓取
- 资源嗅探 -> 如何获取到动态的播放地址
- 投屏协议 -> 将手机的内容投到电视屏幕上
- 本地缓存 -> 用户数据 Cache -> 文件目录(document 不会被手机管家删除，temp 临时文件清除缓存是会被删除)


User Generated Content(用户原创内容）

directive 可以用来做复杂的输入限制，比如查询所有年龄大于 18 岁的数据

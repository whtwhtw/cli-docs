# OpenCLI 功能大全

> OpenCLI — Make any website your CLI. Zero setup. AI-powered.
> 
> 总计：**573 个内置命令**，覆盖 **93 个网站/服务**，另有 **7 个外部 CLI 集成**

---

## 目录

- [核心命令](#核心命令)
- [电商平台](#电商平台)
- [新闻资讯](#新闻资讯)
- [社交媒体](#社交媒体)
- [视频/播客](#视频播客)
- [金融/股票](#金融股票)
- [开发者社区](#开发者社区)
- [AI 工具](#ai-工具)
- [办公/效率](#办公效率)
- [生活/娱乐](#生活娱乐)
- [搜索/知识](#搜索知识)
- [外部 CLI 集成](#外部-cli-集成)
- [认证类型说明](#认证类型说明)
- [通用使用方法](#通用使用方法)

---

## 核心命令

### opencli 自身命令

| 命令 | 说明 |
|------|------|
| `opencli list` | 列出所有可用的 CLI 命令 |
| `opencli validate [target]` | 验证 CLI 定义 |
| `opencli verify [target]` | 验证 + 冒烟测试 |
| `opencli explore <url>` | 探索网站：发现 API、store 和推荐策略 |
| `opencli synthesize <target>` | 从 explore 结果合成 CLI |
| `opencli generate <url>` | 一键流程：explore → synthesize → verify → register |
| `opencli record <url>` | 从实时浏览器会话录制 API 调用 → 生成 YAML 候选 |
| `opencli cascade <url>` | 策略级联：寻找最简单的可用策略 |
| `opencli browser` | 浏览器控制 — 导航、点击、输入、提取、等待（无需 LLM） |
| `opencli doctor` | 诊断 opencli 浏览器桥接连接状态 |
| `opencli plugin` | 管理 opencli 插件 |
| `opencli adapter` | 管理 CLI 适配器 |
| `opencli daemon` | 管理 opencli 守护进程 |
| `opencli install <name>` | 安装外部 CLI |
| `opencli register <name>` | 注册外部 CLI |

### opencli browser — 浏览器自动化控制

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `open <url>` | 打开 URL | `opencli browser open "https://example.com"` |
| `back` | 返回上一页 | |
| `scroll <direction>` | 滚动页面 | `opencli browser scroll down` |
| `state` | 查看页面状态：URL、标题、可交互元素及 [N] 索引 | |
| `screenshot [path]` | 截图 | `opencli browser screenshot /tmp/screen.png` |
| `get` | 获取页面属性 | |
| `click <index>` | 按索引点击元素 | `opencli browser click 3` |
| `type <index> <text>` | 点击元素后输入文本 | `opencli browser type 1 "hello"` |
| `select <index> <option>` | 选择下拉菜单选项 | |
| `keys <key>` | 按下键盘按键 | |
| `wait <type> [value]` | 等待选择器/文本/时间 | `opencli browser wait selector ".loaded"` |
| `eval <js>` | 在页面上下文中执行 JS | |
| `network` | 显示捕获的网络请求 | |
| `close` | 关闭自动化窗口 | |

---

## 电商平台

### 1688（阿里巴巴批发）

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索商品（结果候选、卖家链接、价格/MOQ/销量文本） | `opencli 1688 search "蓝牙耳机"` |
| `item <input>` | 商品详情（公开商品字段、价格阶梯、卖家基础信息） | `opencli 1688 item "https://detail.1688.com/xxx.html"` |
| `store <input>` | 店铺/供应商公开信息（联系方式、主营、入驻年限、服务信号） | `opencli 1688 store "店铺URL"` |
| `assets <input>` | 列出商品页可提取的图片/视频素材 | `opencli 1688 assets "商品URL"` |
| `download <input>` | 批量下载商品页图片和视频素材 | `opencli 1688 download "商品URL"` |

### 淘宝 (Taobao)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索商品 | `opencli taobao search "机械键盘"` |
| `detail <input>` | 商品详情 | `opencli taobao detail "商品URL"` |
| `reviews <input>` | 商品评价 | `opencli taobao reviews "商品URL"` |
| `cart` | 查看购物车 | `opencli taobao cart` |
| `add-cart <input>` | 加入购物车 | `opencli taobao add-cart "商品URL"` |

### 京东 (JD)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索商品 | `opencli jd search "笔记本"` |
| `detail <input>` | 商品详情 | `opencli jd detail "商品URL"` |
| `item <input>` | 商品详情（价格、店铺、规格参数、AVIF 图片） | `opencli jd item "商品URL"` |
| `reviews <input>` | 商品评价 | `opencli jd reviews "商品URL"` |
| `cart` | 查看购物车 | `opencli jd cart` |
| `add-cart <input>` | 加入购物车 | `opencli jd add-cart "商品URL"` |

### 闲鱼 (Xianyu)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索商品 | `opencli xianyu search "二手手机"` |
| `item <input>` | 商品详情 | `opencli xianyu item "商品URL"` |
| `chat` | 打开闲鱼聊天会话，可发送消息 | `opencli xianyu chat` |

### Amazon（亚马逊）

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索结果（产品发现与粗筛） | `opencli amazon search "wireless mouse"` |
| `product <input>` | 商品详情页信息 | `opencli amazon product "商品URL"` |
| `offer <input>` | 卖家、Buy Box、配送信息 | `opencli amazon offer "商品URL"` |
| `discussion <input>` | 评论摘要和顾客讨论样本 | `opencli amazon discussion "商品URL"` |
| `bestsellers [input]` | 畅销榜 | `opencli amazon bestsellers` |
| `movers-shakers [input]` | 短期增长信号榜 | `opencli amazon movers-shakers` |
| `new-releases [input]` | 新品榜 | `opencli amazon new-releases` |

### Coupang（韩国电商）

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索商品 | `opencli coupang search "无线耳机"` |
| `product <input>` | 商品详情 | `opencli coupang product "商品URL"` |
| `review <input>` | 商品评价 | |

### eBay

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索商品 | `opencli ebay search "vintage camera"` |
| `item <input>` | 商品详情 | |

### CJ Dropshipping

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索商品 | `opencli cjdropshipping search "phone case"` |
| `product <input>` | 商品详情 | |

### 什么值得买 (SMZDM)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索好价 | `opencli smzdm search "AirPods"` |

---

## 新闻资讯

### 36氪 (36Kr)

**认证方式**: public / intercept

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `news` | 最新科技/创业新闻 | `opencli 36kr news` |
| `hot` | 热榜（人气/综合/收藏/目录） | `opencli 36kr hot --type renqi` |
| `search <query>` | 搜索文章 | `opencli 36kr search "AI"` |
| `article <id>` | 获取文章正文 | `opencli 36kr article "文章ID"` |

### BBC 新闻

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `news` | 新闻头条（RSS） | `opencli bbc news` |

### Bloomberg（彭博社）

**认证方式**: public / cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `main` | 首页头条（RSS） | `opencli bloomberg main` |
| `markets` | 市场新闻 | `opencli bloomberg markets` |
| `tech` | 科技新闻 | `opencli bloomberg tech` |
| `politics` | 政治新闻 | |
| `economics` | 经济新闻 | |
| `businessweek` | Businessweek 精选 | |
| `industries` | 行业新闻 | |
| `opinions` | 观点评论 | |
| `feeds` | 列出 RSS 源 | |
| `news <link>` | 读取文章全文 | `opencli bloomberg news "文章URL"` |

### Reuters（路透社）

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 新闻搜索 | `opencli reuters search "AI regulation"` |

###新浪财经 (SinaFinance)

**认证方式**: public / cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `news` | 7x24 小时实时快讯 | `opencli sinafinance news` |
| `rolling-news` | 滚动新闻 | `opencli sinafinance rolling-news` |
| `stock` | 行情（A股/港股/美股） | `opencli sinafinance stock "600519"` |
| `stock-rank` | 股票热搜榜 | `opencli sinafinance stock-rank` |

### 中国新闻聚合 (China-News)

**认证方式**: public

聚合多个中文新闻源。

---

## 社交媒体

### 微博 (Weibo)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `feed` | 首页动态流 | `opencli weibo feed` |
| `hot` | 热搜 | `opencli weibo hot` |
| `search <query>` | 搜索微博 | `opencli weibo search "AI"` |
| `user <uid>` | 用户资料 | `opencli weibo user "UID"` |
| `post <id>` | 单条博文详情 | `opencli weibo post "微博ID"` |
| `comments <id>` | 博文评论 | `opencli weibo comments "微博ID"` |
| `me` | 个人资料 | `opencli weibo me` |

### 小红书 (Xiaohongshu)

**认证方式**: cookie / intercept

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索笔记 | `opencli xiaohongshu search "穿搭"` |
| `note <input>` | 笔记正文和互动数据 | `opencli xiaohongshu note "笔记URL"` |
| `comments <input>` | 笔记评论（含楼中楼） | `opencli xiaohongshu comments "笔记URL"` |
| `feed` | 首页推荐 Feed | `opencli xiaohongshu feed` |
| `user <input>` | 用户公开笔记 | `opencli xiaohongshu user "用户URL"` |
| `download <input>` | 下载笔记图片和视频 | `opencli xiaohongshu download "笔记URL"` |
| `publish` | 发布图文笔记 | `opencli xiaohongshu publish` |
| `notifications` | 通知（@/赞/关注） | `opencli xiaohongshu notifications` |
| `creator-profile` | 创作者账号信息 | `opencli xiaohongshu creator-profile` |
| `creator-stats` | 创作者数据总览 | `opencli xiaohongshu creator-stats` |
| `creator-notes` | 创作者笔记列表+数据 | `opencli xiaohongshu creator-notes` |
| `creator-note-detail <input>` | 单篇笔记详细数据 | |

### 抖音 (Douyin)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索视频 | `opencli douyin search "美食"` |
| `feed` | 首页推荐 | `opencli douyin feed` |
| `video <input>` | 视频详情 | `opencli douyin video "视频URL"` |
| `comments <input>` | 视频评论 | |
| `download <input>` | 下载视频 | |

### Twitter/X

**认证方式**: cookie / ui / intercept

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `timeline` | 首页时间线 | `opencli twitter timeline` |
| `trending` | 热门话题 | `opencli twitter trending` |
| `search <query>` | 搜索推文 | `opencli twitter search "AI news"` |
| `thread <url>` | 推文串（原推+所有回复） | `opencli twitter thread "推文URL"` |
| `profile <handle>` | 用户资料 | `opencli twitter profile "elonmusk"` |
| `bookmarks` | 书签 | `opencli twitter bookmarks` |
| `likes <handle>` | 喜欢的推文 | |
| `lists` | 列表 | |
| `post` | 发推/线程 | `opencli twitter post` |
| `reply <url>` | 回复推文 | `opencli twitter reply "推文URL"` |
| `like <url>` | 点赞 | `opencli twitter like "推文URL"` |
| `bookmark <url>` | 书签 | `opencli twitter bookmark "推文URL"` |
| `follow <handle>` | 关注 | `opencli twitter follow "handle"` |
| `unfollow <handle>` | 取消关注 | |
| `block <handle>` | 屏蔽 | |
| `unblock <handle>` | 取消屏蔽 | |
| `delete <url>` | 删除推文 | |
| `notifications` | 通知 | `opencli twitter notifications` |
| `following <handle>` | 正在关注的用户 | |
| `followers <handle>` | 粉丝 | |
| `article <url>` | 长文文章（导出 Markdown） | |
| `download <input>` | 下载媒体（图片/视频） | |
| `reply-dm` | 发送私信 | |
| `hide-reply <url>` | 隐藏回复 | |
| `accept` | 自动接受含关键词的 DM 请求 | |

### Instagram

**认证方式**: cookie / ui

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索用户 | `opencli instagram search "photographer"` |
| `profile <username>` | 用户资料 | `opencli instagram profile "cristiano"` |
| `user <username>` | 最新帖子 | `opencli instagram user "username"` |
| `post` | 发布图文/轮播 | `opencli instagram post` |
| `reel` | 发布 Reel 视频 | |
| `story` | 发布 Story | |
| `note` | 发布文字 Note | |
| `like <input>` | 点赞 | |
| `unlike <input>` | 取消点赞 | |
| `follow <username>` | 关注 | |
| `unfollow <username>` | 取消关注 | |
| `save <input>` | 收藏 | |
| `unsave <input>` | 取消收藏 | |
| `saved` | 已收藏列表 | |
| `following <username>` | 正在关注 | |
| `comment <input>` | 评论 | |
| `reels <username>` | Reels 列表 | |
| `highlights <username>` | Highlights | |

### TikTok

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索视频 | `opencli tiktok search "dance"` |
| `explore` | 热门视频 | `opencli tiktok explore` |
| `profile <username>` | 用户资料 | |
| `user <username>` | 最新视频 | |
| `like <input>` | 点赞 | |
| `unlike <input>` | 取消点赞 | |
| `follow <username>` | 关注 | |
| `unfollow <username>` | 取消关注 | |
| `following` | 正在关注列表 | |
| `friends` | 好友推荐 | |
| `save <input>` | 收藏 | |
| `unsave <input>` | 取消收藏 | |
| `comment <input>` | 评论 | |
| `notifications` | 通知 | |
| `live` | 直播 | |

### Facebook

**认证方式**: cookie / ui

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `feed` | 首页动态 | `opencli facebook feed` |
| `notifications` | 通知 | `opencli facebook notifications` |
| `post` | 发状态 | `opencli facebook post` |
| `profile` | 个人资料 | |

### Reddit

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `frontpage` | 首页 / r/all | `opencli reddit frontpage` |
| `hot` | 热门帖子 | `opencli reddit hot` |
| `popular` | 热门 (/r/popular) | |
| `search <query>` | 搜索帖子 | `opencli reddit search "machine learning"` |
| `subreddit <name>` | 特定版块帖子 | `opencli reddit subreddit "python"` |
| `read <url>` | 阅读帖子和评论 | `opencli reddit read "帖子URL"` |
| `comment <url>` | 发表评论 | |
| `upvote <url>` | 投票 | |
| `save <url>` | 收藏 | |
| `saved` | 已收藏列表 | |
| `upvoted` | 已投票列表 | |
| `user <username>` | 用户资料 | |
| `user-posts <username>` | 用户发帖 | |
| `user-comments <username>` | 用户评论 | |
| `subscribe <subreddit>` | 订阅/退出版块 | |

### Discord

**认证方式**: cookie / ui

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `channels` | 频道列表 | `opencli discord channels` |
| `messages <channel>` | 消息 | |
| `send <channel>` | 发送消息 | |
| `mentions` | @提及 | |
| `servers` | 服务器列表 | |

### LinkedIn

**认证方式**: cookie / header

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `timeline` | 首页动态 | `opencli linkedin timeline` |
| `search <query>` | 搜索职位 | `opencli linkedin search "software engineer"` |

### BlueSky

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `trending` | 热门话题 | `opencli bluesky trending` |
| `search <query>` | 搜索用户 | `opencli bluesky search "username"` |
| `profile <handle>` | 用户资料 | |
| `user <handle>` | 最新动态 | |
| `thread <uri>` | 帖子串 | |
| `feeds` | 热门 Feed | |
| `followers <handle>` | 粉丝 | |
| `following <handle>` | 关注列表 | |
| `starter-packs <handle>` | 入门包 | |

### 豆瓣 (Douban)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索书影音 | `opencli douban search "流浪地球"` |
| `movie <id>` | 电影详情 | |
| `book <id>` | 书籍详情 | |
| `music <id>` | 音乐详情 | |
| `group <id>` | 小组话题 | |
| `groups` | 加入的小组 | |

### 即刻 (Jike)

**认证方式**: cookie / ui

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `feed` | 首页动态流 | `opencli jike feed` |
| `search <query>` | 搜索帖子 | `opencli jike search "AI"` |
| `post <id>` | 帖子详情和评论 | |
| `create` | 发布动态 | `opencli jike create` |
| `repost <id>` | 转发 | |
| `like <id>` | 点赞 | |
| `comment <id>` | 评论 | |
| `topic <id>` | 话题/圈子帖子 | |
| `user <id>` | 用户动态 | |
| `notifications` | 通知 | |

### V2EX

**认证方式**: public / cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `hot` | 热门话题 | `opencli v2ex hot` |
| `latest` | 最新话题 | `opencli v2ex latest` |
| `daily` | 每日签到领铜币 | `opencli v2ex daily` |
| `topic <id>` | 主题详情和回复 | `opencli v2ex topic "主题ID"` |
| `replies <id>` | 主题回复 | |
| `nodes` | 所有节点 | |
| `node <name>` | 节点话题 | |
| `member <username>` | 用户资料 | |
| `user <username>` | 用户发帖 | |
| `me` | 个人资料（余额/未读提醒） | `opencli v2ex me` |
| `notifications` | 提醒 | `opencli v2ex notifications` |

### 贴吧 (Tieba)

**认证方式**: public / cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `hot` | 热门话题 | `opencli tieba hot` |
| `search <query>` | 跨吧搜索 | `opencli tieba search "手机"` |
| `posts <name>` | 版块帖子 | `opencli tieba posts "弱智吧"` |
| `read <url>` | 阅读帖子 | |

### 虎扑 (Hupu)

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `hot` | 热帖 | `opencli hupu hot` |

### Threads

**认证方式**: cookie / ui

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `feed` | 首页动态 | `opencli threads feed` |
| `search <query>` | 搜索 | |
| `post` | 发帖 | |
| `profile <username>` | 用户资料 | |

### Band

**认证方式**: cookie / intercept

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `bands` | 加入的 Band 列表 | `opencli band bands` |
| `posts <band_no>` | Band 帖子列表 | `opencli band posts 1` |
| `post <band_no> <post_no>` | 帖子全文和评论 | `opencli band post 1 1` |
| `mentions` | @提及通知 | `opencli band mentions` |

### 脉脉 (Maimai)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search-talents <query>` | 多维度筛选搜索候选人 | `opencli maimai search-talents "Java 北京"` |

---

## 视频/播客

### B站 (Bilibili)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索视频/用户 | `opencli bilibili search "罗翔"` |
| `hot` | 热门视频 | `opencli bilibili hot` |
| `ranking` | 排行榜 | `opencli bilibili ranking` |
| `comments <bvid>` | 视频评论 | `opencli bilibili comments "BV1xx"` |
| `subtitle <bvid>` | 视频字幕 | `opencli bilibili subtitle "BV1xx"` |
| `download <bvid>` | 下载视频（需 yt-dlp） | `opencli bilibili download "BV1xx"` |
| `feed [uid]` | 动态时间线 | `opencli bilibili feed` |
| `feed-detail <id>` | 动态详情 | |
| `dynamic` | 用户动态 | |
| `favorite` | 收藏夹 | `opencli bilibili favorite` |
| `history` | 观看历史 | `opencli bilibili history` |
| `following [uid]` | 关注列表 | |
| `user-videos <uid>` | 用户投稿视频 | `opencli bilibili user-videos "UID"` |
| `me` | 个人资料 | `opencli bilibili me` |

### YouTube

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索视频 | `opencli youtube search "tutorial"` |
| `feed` | 首页推荐 | `opencli youtube feed` |
| `video <id>` | 视频元数据 | `opencli youtube video "视频ID"` |
| `comments <id>` | 评论 | |
| `transcript <id>` | 字幕/字幕文本 | |
| `channel <handle>` | 频道信息和最新视频 | |
| `playlist <id>` | 播放列表 | |
| `history` | 观看历史 | |
| `watch-later` | 稍后观看列表 | |
| `like <id>` | 点赞 | |
| `unlike <id>` | 取消点赞 | |
| `subscribe <handle>` | 订阅频道 | |
| `unsubscribe <handle>` | 取消订阅 | |
| `subscriptions` | 订阅列表 | |

### 小宇宙 (Xiaoyuzhou)

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `podcast <id>` | 播客主页 | `opencli xiaoyuzhou podcast "123"` |
| `podcast-episodes <id>` | 最新单集列表 | `opencli xiaoyuzhou podcast-episodes "123"` |
| `episode <url>` | 单集详情 | |
| `download <url>` | 下载音频 | |
| `transcript <url>` | 下载字幕文本 | |

### Apple Podcasts

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索播客 | `opencli apple-podcasts search "tech"` |
| `top` | 排行榜 | `opencli apple-podcasts top` |
| `episodes <id>` | 最新单集 | `opencli apple-podcasts episodes "播客ID"` |

---

## 金融/股票

### Binance（币安）

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `price <symbol>` | 实时价格 | `opencli binance price BTCUSDT` |
| `prices` | 所有交易对价格 | `opencli binance prices` |
| `pairs` | 交易对列表 | `opencli binance pairs` |
| `top` | 24h 成交量排行 | `opencli binance top` |
| `gainers` | 涨幅榜 | `opencli binance gainers` |
| `losers` | 跌幅榜 | `opencli binance losers` |
| `ticker` | 24h 统计 | `opencli binance ticker` |
| `klines <symbol>` | K线数据 | `opencli binance klines BTCUSDT` |
| `depth <symbol>` | 深度买卖盘 | `opencli binance depth BTCUSDT` |
| `asks <symbol>` | 卖盘 | |
| `trades <symbol>` | 最近成交 | |

### 雪球 (Xueqiu)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索股票 | `opencli xueqiu search "茅台"` |
| `stock <symbol>` | 实时行情 | `opencli xueqiu stock "SH600519"` |
| `kline <symbol>` | K线数据 | `opencli xueqiu kline "SH600519"` |
| `hot-stock` | 热门股票榜 | `opencli xueqiu hot-stock` |
| `hot` | 热门动态 | `opencli xueqiu hot` |
| `feed` | 首页时间线 | `opencli xueqiu feed` |
| `comments <symbol>` | 股票讨论 | |
| `earnings-date <symbol>` | 财报发布日期 | |
| `watchlist` | 自选股列表 | `opencli xueqiu watchlist` |
| `groups` | 自选股分组 | |
| `fund-snapshot` | 蛋卷基金快照 | `opencli xueqiu fund-snapshot -f json` |
| `fund-holdings` | 基金持仓明细 | |

### 同花顺 (THS)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `hot-rank` | 热股榜 | `opencli ths hot-rank` |

### 通达信 (TDX)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `hot-rank` | 热搜榜 | `opencli tdx hot-rank` |

### Barchart

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `quote <symbol>` | 股票报价 | `opencli barchart quote AAPL` |
| `options <symbol>` | 期权链（Greeks/IV/量/持仓） | `opencli barchart options AAPL` |
| `greeks <symbol>` | 期权 Greeks 概览 | |
| `flow` | 异常期权活动/期权流 | |

### Yahoo Finance

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `quote <symbol>` | 股票行情 | `opencli yahoo-finance quote AAPL` |

### 东方财富 (Eastmoney)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `stock <symbol>` | 股票行情 | |
| `hot-rank` | 热股榜 | |

---

## 开发者社区

### GitHub (gh)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索仓库 | `opencli github search "machine learning"` |
| `repo <owner/repo>` | 仓库信息 | `opencli github repo "torvalds/linux"` |
| `trending` | Trending 仓库 | `opencli github trending` |
| `issues <owner/repo>` | Issues 列表 | |
| `pulls <owner/repo>` | Pull Requests | |
| `releases <owner/repo>` | Releases | |
| `profile <username>` | 用户资料 | |
| `readme <owner/repo>` | README 内容 | |
| `stars <username>` | Star 列表 | |
| `feeds` | 动态 Feed | |

### Gitee

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索仓库 | `opencli gitee search "springboot"` |
| `repo <owner/repo>` | 仓库信息 | |

### Stack Overflow

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索问题 | `opencli stackoverflow search "python async"` |
| `hot` | 热门问题 | `opencli stackoverflow hot` |
| `unanswered` | 高票未回答问题 | |
| `bounties` | 悬赏问题 | |

### Hacker News

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `top` | 热门文章 | `opencli hackernews top` |
| `newest` | 最新文章 | |
| `best` | 最佳文章 | |
| `ask` | Ask HN | |
| `show` | Show HN | |
| `job` | 招聘 | |
| `item <id>` | 文章详情和评论 | `opencli hackernews item "ID"` |

### Lobste.rs

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `hot` | 热门 | `opencli lobsters hot` |
| `newest` | 最新 | |
| `active` | 最活跃讨论 | |
| `tag <tag>` | 按标签浏览 | `opencli lobsters tag "rust"` |

### Dev.to

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `feed` | 文章 Feed | `opencli devto feed` |
| `search <query>` | 搜索文章 | |
| `user <username>` | 用户文章 | |

### Linux.Do

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `hot` | 热门话题 | `opencli linux-do hot` |
| `latest` | 最新话题 | `opencli linux-do latest` |
| `feed` | 话题列表 | |
| `categories` | 分类列表 | |
| `category <id>` | 分类内话题 | |
| `tags` | 标签列表 | |
| `search <query>` | 搜索 | `opencli linux-do search "docker"` |
| `topic <id>` | 帖子摘要和回复 | `opencli linux-do topic "ID"` |
| `topic-content <id>` | 帖子正文（Markdown） | |
| `user-posts <username>` | 用户帖子 | |
| `user-topics <username>` | 用户创建的话题 | |

### Product Hunt

**认证方式**: public / intercept

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `today` | 今日上线产品 | `opencli producthunt today` |
| `hot` | 今日热门（含票数） | `opencli producthunt hot` |
| `posts [category]` | 最新发布 | |
| `browse [category]` | 分类浏览 | |

### LessWrong

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `frontpage` | 算法推荐首页 | `opencli lesswrong frontpage` |
| `top` | 历史最佳 | `opencli lesswrong top` |
| `top-week` | 本周最佳 | |
| `top-month` | 本月最佳 | |
| `top-year` | 年度最佳 | |
| `new` | 最新文章 | |
| `curated` | 编辑推荐 | |
| `shortform` | 短评 | |
| `read <url/id>` | 阅读全文 | `opencli lesswrong read "ID"` |
| `comments <url/id>` | 热门评论 | |
| `sequences <url/id>` | 文集收藏 | |
| `tag <tag>` | 按标签浏览 | |
| `tags` | 热门标签 | |
| `user <username>` | 用户资料 | |
| `user-posts <username>` | 用户文章 | |

### CSDN

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索文章 | `opencli csdn search "python"` |
| `article <url>` | 文章详情 | |

---

## AI 工具

### ChatGPT

**认证方式**: cookie / ui

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `chat <message>` | 发送消息并获取回复 | `opencli chatgpt chat "你好"` |
| `new` | 新对话 | `opencli chatgpt new` |
| `history` | 历史对话 | `opencli chatgpt history` |
| `models` | 可用模型列表 | `opencli chatgpt models` |
| `model <name>` | 切换模型 | |

### Claude (Codex / Cursor / Antigravity)

**认证方式**: cookie / ui

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `chat <message>` | 发送消息 | `opencli claude chat "解释这段代码"` |
| `new` | 新对话 | |
| `status` | 连接状态检查 | |

### Antigravity（Claude Desktop）

**认证方式**: ui

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `status` | 检查 CDP 连接和页面状态 | `opencli antigravity status` |
| `send <message>` | 发送消息 | `opencli antigravity send "hello"` |
| `read` | 读取最新消息 | `opencli antigravity read` |
| `watch` | 实时流式监听消息 | `opencli antigravity watch` |
| `new` | 新对话/清除上下文 | `opencli antigravity new` |
| `model <name>` | 切换 LLM 模型 | `opencli antigravity model "claude-sonnet-4-20250514"` |
| `dump` | 导出 DOM 帮助 AI 理解 UI | |
| `extract-code` | 提取对话中的代码块 | |
| `serve` | 启动 Anthropic 兼容 API 代理 | |

### Cursor

**认证方式**: ui

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `chat <message>` | 发送消息 | |
| `new` | 新对话 | |
| `read` | 读取回复 | |

### Gemini

**认证方式**: cookie / ui

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `chat <message>` | 发送消息 | `opencli gemini chat "你好"` |
| `new` | 新对话 | |

### Grok

**认证方式**: cookie / ui

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `chat <message>` | 发送消息 | |
| `new` | 新对话 | |

### 通义千问 / 通义万相 (Jimeng)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `generate <prompt>` | 文生图 | `opencli jimeng generate "一只可爱的猫"` |
| `history` | 最近生成的作品 | `opencli jimeng history` |
| `new` | 新建会话 | |
| `workspaces` | 工作区列表 | |

### 豆包 (Doubao)

**认证方式**: cookie / ui

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `chat <message>` | 发送消息 | |
| `new` | 新对话 | |

### 元宝 (Yuanbao)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `ask <prompt>` | 发送提示等待回复 | `opencli yuanbao ask "总结一下今天的新闻"` |
| `new` | 新对话 | `opencli yuanbao new` |

### Coze（扣子）

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `chat <message>` | 发送消息给 Bot | |
| `bots` | Bot 列表 | |

### ChatWise

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `chat <message>` | 发送消息 | |

### NotebookLM

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `list` | 列出笔记本列表 | `opencli notebooklm list` |
| `open <id/url>` | 打开指定笔记本 | `opencli notebooklm open "笔记本URL"` |
| `status` | 检查页面可用性和登录状态 | |
| `get` | 获取当前笔记本元数据 | `opencli notebooklm get` |
| `current` | 当前打开的笔记本元数据 | |
| `summary` | 获取摘要 | `opencli notebooklm summary` |
| `history` | 对话历史 | `opencli notebooklm history` |
| `source-list` | 来源列表 | `opencli notebooklm source-list` |
| `source-get <id/title>` | 获取指定来源 | |
| `source-fulltext <id>` | 获取来源全文 | |
| `source-guide <id>` | 获取来源指南 | |
| `note-list` | 保存的笔记列表 | `opencli notebooklm note-list` |
| `notes-get <title>` | 获取单条笔记 | |

### Yollomi（AI 图像/视频工具）

**认证方式**: cookie / public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `generate <prompt>` | AI 文生图/图生图 | `opencli yollomi generate "sunset beach"` |
| `video <prompt>` | AI 文生视频/图生视频 | |
| `edit <prompt>` | AI 文本提示编辑 | |
| `upscale` | 图像超分辨率 | |
| `remove-bg` | 去除背景（免费） | |
| `object-remover` | 去除不需要的对象 | |
| `restore` | 老照片修复 | |
| `face-swap` | 换脸 | |
| `try-on` | 虚拟试衣 | |
| `background` | AI 背景生成 | |
| `upload <file>` | 上传图片/视频 | |
| `models` | 可用模型列表 | `opencli yollomi models` |

### PaperReview.ai

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `submit <pdf>` | 提交 PDF 进行评审 | `opencli paperreview submit "paper.pdf"` |
| `review <token>` | 获取评审结果 | `opencli paperreview review "token"` |
| `feedback <token>` | 提交反馈 | |

---

## 办公/效率

### 飞书 (Lark)

**认证方式**: cookie / ui

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `messages` | 消息列表 | `opencli lark-cli messages` |
| `docs` | 文档管理 | |
| `sheets` | 电子表格 | |
| `calendar` | 日历 | |
| `tasks` | 任务 | |

### 钉钉 (DingTalk)

**认证方式**: cookie / ui

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `messages` | 消息列表 | `opencli dws messages` |
| `docs` | 文档 | |
| `calendar` | 日历 | |
| `contacts` | 通讯录 | |

### 企业微信 (WeCom)

**认证方式**: cookie / ui

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `messages` | 消息 | `opencli wecom-cli messages` |
| `contacts` | 通讯录 | |
| `todos` | 待办事项 | |
| `meetings` | 会议 | |
| `calendar` | 日历 | |
| `docs` | 文档 | |
| `smart-sheets` | 智能表格 | |

### Notion

**认证方式**: ui

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索页面和数据库 | `opencli notion search "project"` |
| `new` | 创建新页面 | `opencli notion new` |
| `read` | 读取当前打开的页面 | `opencli notion read` |
| `write` | 追加文本到当前页面 | `opencli notion write "内容"` |
| `export` | 导出为 Markdown | `opencli notion export` |
| `sidebar` | 侧边栏页面/数据库列表 | |
| `favorites` | 收藏列表 | |
| `status` | 检查 CDP 连接 | |

### ONES（项目管理）

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `me` | 当前用户信息 | `opencli ones me` |
| `login` | 通过 Chrome Bridge 登录 | |
| `logout` | 注销（使 token 失效） | |
| `token-info` | 会话详情（用户、团队、组织） | `opencli ones token-info` |
| `tasks <team>` | 工作项列表 | `opencli ones tasks "team-uuid"` |
| `task <id>` | 工作项详情 | `opencli ones task "123"` |
| `my-tasks` | 我的任务 | `opencli ones my-tasks` |
| `worklog` | 记录工时 | `opencli ones worklog "task-id"` |

### 幕布 (Mubu)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `docs` | 文档列表（默认根目录） | `opencli mubu docs` |
| `recent` | 最近编辑的文档 | `opencli mubu recent` |
| `doc <id>` | 读取文档内容 | `opencli mubu doc "ID"` |
| `search <query>` | 全局搜索文档 | `opencli mubu search "关键词"` |
| `notes` | 速记（默认今天） | `opencli mubu notes` |

### 小鹅通 (Xiaoe)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `courses` | 已购课程列表 | `opencli xiaoe courses` |
| `catalog <id>` | 课程目录 | `opencli xiaoe catalog "ID"` |
| `detail <id>` | 课程详情 | |
| `content <id>` | 图文内容 | |
| `play-url <id>` | 音视频回放 M3U8 地址 | |

### Obsidian

**认证方式**: ui

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索笔记 | `opencli obsidian search "关键词"` |
| `read` | 读取笔记 | |
| `write` | 写入笔记 | |
| `tags` | 标签列表 | |
| `tasks` | 任务列表 | |
| `sync` | 同步 | |

### 超星学习通 (Chaoxing)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `assignments` | 作业列表 | `opencli chaoxing assignments` |
| `exams` | 考试列表 | `opencli chaoxing exams` |

### 知识星球 (Zsxq)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `groups` | 加入的星球列表 | `opencli zsxq groups` |
| `dynamics` | 所有星球的最新动态 | `opencli zsxq dynamics` |
| `topics <id>` | 星球话题列表 | `opencli zsxq topics "星球ID"` |
| `topic <id>` | 单个话题详情 | `opencli zsxq topic "话题ID"` |
| `search <query>` | 搜索星球内容 | `opencli zsxq search "关键词"` |

---

## 生活/娱乐

### Spotify

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `auth` | OAuth 认证（首次运行） | `opencli spotify auth` |
| `play` | 播放或搜索播放 | `opencli spotify play "Bohemian Rhapsody"` |
| `pause` | 暂停 | `opencli spotify pause` |
| `next` | 下一首 | `opencli spotify next` |
| `prev` | 上一首 | `opencli spotify prev` |
| `status` | 当前播放状态 | `opencli spotify status` |
| `search <query>` | 搜索歌曲 | `opencli spotify search "song name"` |
| `volume <0-100>` | 设置音量 | `opencli spotify volume 50` |
| `shuffle` | 切换随机模式 | `opencli spotify shuffle` |
| `repeat` | 设置循环模式 | `opencli spotify repeat track` |
| `queue` | 添加到播放队列 | |

### Steam

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `top-sellers` | 畅销游戏 | `opencli steam top-sellers` |

### Pixiv

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索插画 | `opencli pixiv search "初音ミク"` |
| `ranking` | 排行榜（日/周/月） | `opencli pixiv ranking` |
| `detail <id>` | 插画详情 | `opencli pixiv detail "ID"` |
| `illusts <user_id>` | 画师插画列表 | |
| `user <user_id>` | 画师资料 | |
| `download <id>` | 下载插画图片 | |

### Dribbble

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `trending` | 热门设计 | `opencli dribbble trending` |
| `search <query>` | 搜索设计作品 | |

### IMDb

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索影视 | `opencli imdb search "Inception"` |
| `title <id>` | 详情 | |

### 携程 (Ctrip)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search` | 机票/酒店搜索 | |
| `orders` | 订单列表 | |

---

## 搜索/知识

### Google

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索 | `opencli google search "machine learning tutorial"` |

### Wikipedia（维基百科）

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索条目 | `opencli wikipedia search "Python"` |
| `summary <title>` | 条目摘要 | `opencli wikipedia summary "Python"` |
| `random` | 随机条目 | `opencli wikipedia random` |
| `trending` | 昨日最热 | `opencli wikipedia trending` |

### 微信 (Weixin)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `download <url>` | 导出公众号文章为 Markdown | `opencli weixin download "文章URL"` |

### 微信读书 (Weread)

**认证方式**: cookie / public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索书籍 | `opencli weread search "三体"` |
| `ranking` | 分类排行 | `opencli weread ranking` |
| `book <bookId>` | 书籍详情 | `opencli weread book "bookId"` |
| `highlights <bookId>` | 划线笔记 | `opencli weread highlights "bookId"` |
| `notes <bookId>` | 想法/笔记 | `opencli weread notes "bookId"` |
| `notebooks` | 有笔记的书籍列表 | `opencli weread notebooks` |
| `shelf` | 书架 | `opencli weread shelf` |

### arXiv

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索论文 | `opencli arxiv search "transformer"` |
| `paper <id>` | 论文详情 | `opencli arxiv paper "2401.12345"` |

### CNKI（中国知网）

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索论文 | `opencli cnki search "人工智能"` |

### 知乎 (Zhihu)

**认证方式**: cookie / ui

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `hot` | 热榜 | `opencli zhihu hot` |
| `search <query>` | 搜索 | `opencli zhihu search "如何学习AI"` |
| `question <id>` | 问题详情和回答 | `opencli zhihu question "问题ID"` |
| `download <url>` | 导出文章为 Markdown | `opencli zhihu download "文章URL"` |
| `answer <id>` | 回答问题 | `opencli zhihu answer "问题ID"` |
| `comment <id>` | 发表评论 | |
| `like <id>` | 赞同 | |
| `follow <id>` | 关注用户/问题 | |
| `favorite <id>` | 收藏到指定合集 | |

### 剑鱼标讯 (Jianyu)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索招标公告 | `opencli jianyu search "服务器采购"` |
| `detail <id>` | 详情页（抽取证据字段） | `opencli jianyu detail "ID"` |

### 贝壳找房 (Ke)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `ershoufang <city>` | 二手房列表 | `opencli ke ershoufang "北京"` |
| `zufang <city>` | 租房列表 | `opencli ke zufang "北京"` |
| `xiaoqu <city>` | 小区列表 | |
| `chengjiao <city>` | 成交记录 | |

### Boss直聘 (Boss)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索职位 | `opencli boss search "Python 北京"` |
| `detail <id>` | 职位详情 | |

### Substack

**认证方式**: cookie / public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索文章和 Newsletter | `opencli substack search "AI"` |
| `feed` | 热门文章 Feed | `opencli substack feed` |
| `publication <name>` | 特定 Newsletter 最新文章 | `opencli substack publication "newsletter-name"` |

### Medium

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `feed` | 热门文章 Feed | `opencli medium feed` |
| `search <query>` | 搜索文章 | `opencli medium search "machine learning"` |
| `user <username>` | 用户文章列表 | |

### 新浪博客 (SinaBlog)

**认证方式**: cookie / public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `hot` | 热门文章/推荐 | `opencli sinablog hot` |
| `search <query>` | 搜索文章 | `opencli sinablog search "关键词"` |
| `article <url>` | 单篇文章详情 | |
| `user <uid>` | 用户文章列表 | |

### 当当 (Dangdang)

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <query>` | 搜索图书 | `opencli dangdang search "Python编程"` |

### Uiverse

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `code <component>` | 导出组件代码（HTML/CSS/React/Vue） | `opencli uiverse code "button"` |
| `preview <component>` | 截取组件预览截图 | |

### 词典 (Dictionary)

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `search <word>` | 查询单词释义 | `opencli dictionary search "hello"` |

### Quark（夸克网盘）

**认证方式**: cookie

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `ls [path]` | 列出文件 | `opencli quark ls` |
| `mkdir <name>` | 创建文件夹 | `opencli quark mkdir "newfolder"` |
| `mv <files> <folder>` | 移动文件 | |
| `rm <files>` | 删除文件 | |
| `rename <file> <name>` | 重命名 | |
| `save <link>` | 保存分享文件 | |
| `share-tree <link>` | 获取分享目录树 | `opencli quark share-tree "分享链接"` |

### HuggingFace (hf)

**认证方式**: public

| 子命令 | 说明 | 示例 |
|--------|------|------|
| `models` | 模型列表 | `opencli hf models` |
| `datasets` | 数据集列表 | |
| `spaces` | Spaces 列表 | |
| `model <id>` | 模型详情 | |
| `search <query>` | 搜索 | |

---

## 外部 CLI 集成

opencli 还支持通过 `install` 命令安装的外部 CLI 工具：

| 外部 CLI | 说明 | 安装方式 |
|----------|------|----------|
| **docker** | Docker 命令行接口 | 已安装 (installed) |
| **gh** | GitHub CLI — 仓库、PR、Issues、Release、Gist | 已安装 (installed) |
| **dws** | 钉钉工作空间 CLI — 消息、文档、日历、联系人等 | 自动安装 (auto-install) |
| **lark-cli** | 飞书/Feishu CLI — 消息、文档、表格、日历、任务等 200+ 命令 | 自动安装 |
| **wecom-cli** | 企业微信 CLI — 通讯录、待办、会议、消息、日历、文档、智能表格 | 自动安装 |
| **vercel** | Vercel CLI — 部署、域名、环境变量、日志、Serverless 函数 | 自动安装 |
| **obsidian** | Obsidian 笔记管理 — 笔记、搜索、标签、任务、同步 | 自动安装 |

安装示例：
```bash
opencli install gh
```

---

## 认证类型说明

opencli 插件的命令标注了认证类型，含义如下：

| 类型 | 说明 |
|------|------|
| **public** | 公开接口，无需登录即可使用 |
| **cookie** | 需要浏览器登录态（Cookie），请确保浏览器已登录对应网站 |
| **ui** | 需要通过 UI 自动化操作（浏览器中打开的页面对应），确保页面已登录 |
| **intercept** | 通过拦截页面网络请求获取数据，需要页面加载时触发对应 API 调用 |
| **header** | 通过自定义请求头（如 Authorization）进行认证 |

---

## 通用使用方法

### 基本语法

```bash
opencli <插件名> <子命令> [参数] [选项]
```

### 常用选项

| 选项 | 说明 |
|------|------|
| `-h, --help` | 显示帮助信息 |
| `-f, --format <format>` | 输出格式（json/csv/markdown/text），默认 json |
| `-o, --output <file>` | 输出到文件 |
| `-l, --limit <n>` | 限制返回数量 |
| `-q, --quiet` | 静默模式，仅输出关键信息 |

### 实用示例

```bash
# 查看某个插件的所有可用命令
opencli help zhihu

# 查看知乎热榜（JSON 格式）
opencli zhihu hot

# 查看知乎热榜（Markdown 表格格式）
opencli zhihu hot -f markdown

# 搜索微博
opencli weibo search "AI"

# 获取 B站热门视频
opencli bilibili hot

# 获取 Binance BTC 价格
opencli binance price BTCUSDT

# Spotify 播放控制
opencli spotify play "Bohemian Rhapsody"

# 下载微信公众号文章
opencli weixin download "文章URL"

# 导出知乎文章为 Markdown
opencli zhihu download "https://zhuanlan.zhihu.com/p/xxx"

# 浏览器自动化 - 截图
opencli browser open "https://example.com" && opencli browser screenshot

# 网页转 Markdown
opencli web read "https://example.com"

# 获取 YouTube 视频字幕
opencli youtube transcript "视频ID"

# 小红书搜索
opencli xiaohongshu search "穿搭"
```

### Cookie 认证说明

对于标注为 `cookie` 的命令，需要确保在浏览器中已登录对应网站。opencli 通过浏览器桥接（Chrome DevTools Protocol）复用浏览器的登录状态。

```bash
# 1. 先在浏览器中登录对应网站
# 2. 然后运行命令
opencli taobao cart
```

### 输出格式

```bash
# JSON 格式（默认）
opencli zhihu hot

# Markdown 格式
opencli zhihu hot -f markdown

# 纯文本
opencli zhihu hot -f text

# CSV
opencli zhihu hot -f csv

# 保存到文件
opencli zhihu hot -f markdown -o hot.md
```

### 插件开发

如果你想自己开发 opencli 插件，可以使用以下命令：

```bash
# 探索一个网站，发现可用的 API 和策略
opencli explore "https://example.com"

# 合成 CLI 定义
opencli synthesize "explore结果"

# 一键生成并注册
opencli generate "https://example.com"

# 录制浏览器操作生成 YAML
opencli record "https://example.com"
```

---

*本文档基于 `opencli list` 输出和各插件 `opencli help` 内容生成，覆盖 93 个站点插件、573 个内置命令和 7 个外部 CLI 集成。*

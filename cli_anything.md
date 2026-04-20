# CLI-ANYTHING 功能大全

> **CLI-ANYTHING** — Making ALL Software Agent-Native（让所有软件具备 AI Agent 原生兼容性）
> 
> 通过全自动的 **7 阶段流水线**（分析→设计→实现→测试规划→编写测试→文档→发布），为任何具备源码的软件生成结构化、生产级的 CLI。
> 
> 总计：**22+ 核心 Harness**，覆盖 **2,152+ 项测试**，支持 **10+ AI Agent 平台**

---

## 目录

- [项目简介](#项目简介)
- [核心功能](#核心功能)
- [支持的 AI Agent 平台](#支持的-ai-agent-平台)
- [安装与集成](#安装与集成)
- [核心命令](#核心命令)
- [CLI-Hub 包管理器](#cli-hub-包管理器)
- [已支持的 Harness 列表](#已支持的-harness-列表)
- [各 Harness 详细说明](#各-harness-详细说明)
- [使用示例](#使用示例)
- [架构设计原则](#架构设计原则)
- [测试体系](#测试体系)
- [限制与注意事项](#限制与注意事项)

---

## 项目简介

**CLI-ANYTHING** 由 HKUDS 团队开源，旨在将传统面向人类的软件转化为"Agent-Native（智能体原生）"工具。它通过直接调用真实软件后端（拒绝脆弱的 UI 自动化或功能阉割），为 AI Agent 提供结构化 CLI 接口，支持 `--json` 结构化输出和统一 REPL 交互界面。

**GitHub 仓库**: https://github.com/HKUDS/CLI-ANYTHING  
**官方网站**: https://clianything.cc/  
**许可证**: MIT

---

## 核心功能

- 🎯 **直接后端调用** — 不依赖 UI 自动化，直接调用真实软件 API/CLI
- 📦 **结构化输出** — 内置 `--json` 标志，输出机器可读的 JSON 数据
- 💬 **REPL 交互** — 统一交互式命令行界面，支持 Agent 会话
- 🧪 **严苛测试** — 2,152+ 项单元测试与端到端测试，100% 通过率
- 🔄 **7 阶段流水线** — 分析→设计→实现→测试规划→编写测试→文档→发布
- 🌐 **CLI-Hub** — 社区包管理器，发现、安装、更新 Harness
- 🚀 **零配置部署** — `pip install` 即可使用

---

## 支持的 AI Agent 平台

| Agent 平台 | 集成方式 |
|------------|----------|
| **Claude Code** | `/plugin marketplace add HKUDS/CLI-Anything` → `/plugin install cli-anything` |
| **Pi Coding Agent** | 克隆仓库后运行 `bash .pi-extension/cli-anything/install.sh` |
| **OpenCode** | 复制 `opencode-commands/*.md` 与 `HARNESS.md` 至配置目录 |
| **Goose** | 扩展注册 |
| **Qodercli** | `bash CLI-Anything/qoder-plugin/setup-qodercli.sh` |
| **OpenClaw** | 复制对应 `SKILL.md` |
| **Codex** | 运行内置安装脚本 |
| **GitHub Copilot CLI** | `copilot plugin install` |
| **Cursor** | 即将支持 |
| **Windsurf** | 即将支持 |

---

## 安装与集成

CLI-Anything 提供 **两种完全不同的安装方式**，分别对应"使用社区已构建的 CLI"和"从源码自动生成 CLI"。

---

### 方式一：CLI-Hub 安装（推荐，直接使用）

**适用场景**：你想快速使用 GIMP、Blender、LibreOffice 等已被社区构建好的 CLI，无需自己生成。

```bash
# 1. 安装 CLI-Hub 包管理器
pip install cli-anything-hub

# 2. 从社区仓库安装指定 CLI
cli-hub install gimp
cli-hub install blender
cli-hub install libreoffice

# 3. 直接使用
cli-anything-gimp --help
cli-anything-gimp image new --width 1920 --height 1080
```

**特点**：
- 下载的是社区已构建、已测试的 CLI Harness
- 一条命令即可安装，无需 AI Agent 参与
- 支持 `cli-hub search`、`cli-hub list`、`cli-hub update` 等管理命令
- 安装后即可使用 `cli-anything-<软件名>` 命令

---

### 方式二：插件生成式安装（从零构建）

**适用场景**：你想为 Hub 里没有的软件生成 CLI，或想自己定制/重新生成某个 CLI。

#### Claude Code

```bash
# 1. 添加插件市场
/plugin marketplace add HKUDS/CLI-Anything
# 2. 安装插件
/plugin install cli-anything
# 3. 从源码生成 CLI
/cli-anything ./gimp                    # 本地源码
/cli-anything https://github.com/blender/blender  # GitHub 仓库
```

> Windows 提示：需安装 Git for Windows (含 bash/cygpath) 或使用 WSL。

#### Pi Coding Agent

```bash
git clone https://github.com/HKUDS/CLI-Anything.git
bash .pi-extension/cli-anything/install.sh
/cli-anything ./gimp
```

#### OpenCode（实验性）

```bash
cp CLI-Anything/opencode-commands/*.md ~/.config/opencode/commands/
cp CLI-Anything/cli-anything-plugin/HARNESS.md ~/.config/opencode/commands/
/cli-anything ./gimp
```

#### Qodercli

```bash
bash CLI-Anything/qoder-plugin/setup-qodercli.sh
/cli-anything ./gimp
```

#### Goose / OpenClaw / Codex / GitHub Copilot CLI

各平台提供对应扩展注册脚本或 `SKILL.md` 安装路径，安装后直接使用 `/cli-anything ./<软件名>` 或自然语言提示。

**特点**：
- 执行 7 阶段全自动流水线（分析→设计→实现→测试规划→编写测试→文档→发布）
- 为任意有源码的软件生成 CLI，不局限于社区已有 Harness
- 支持后续 `/cli-anything:refine` 迭代优化、`/cli-anything:test` 运行测试
- 生成结果同样通过 `pip install -e .` 安装，使用方式与方式一完全一致

---

### 两种方式对比

| | CLI-Hub 安装 | 插件生成式安装 |
|---|---|---|
| **本质** | 下载社区已构建好的 CLI | 从源码自动生成 CLI |
| **速度** | 秒级安装 | 较长（7 阶段流水线，依赖大模型） |
| **覆盖范围** | 社区已贡献的软件（22+） | 任何有源码的软件 |
| **是否需要 AI Agent** | 否 | 是（需 Claude Code / OpenCode 等） |
| **定制能力** | 使用社区版本 | 可自行 refine / 定制 |
| **最终产物** | `cli-anything-<软件名>` | `cli-anything-<软件名>`（完全一样） |
| **日常使用** | 两种方式使用方式完全相同 | 同左 |

**总结**：Hub 里有的，直接 `cli-hub install` 最快；Hub 里没有的，用 `/cli-anything` 从零生成。两者最终产出的 CLI 使用方式完全一致。

---

## 核心命令

CLI-Anything 以插件/扩展形式集成到主流 AI 编码平台中。以下是所有平台通用的核心命令及参数：

| 命令 | 描述 | 参数说明 |
|:---|:---|:---|
| `/cli-anything <path-or-repo>` | 生成完整的 CLI Harness（执行全部 7 个阶段） | `<path-or-repo>`：本地源码目录路径 或 GitHub 仓库 URL |
| `/cli-anything:refine <path> [focus]` | 精炼现有 Harness，通过差距分析扩展覆盖范围 | `<path>`：现有 Harness 路径<br>`[focus]`（可选）：指定聚焦的功能区域，如 `"batch processing and filters"` |
| `/cli-anything:test <path-or-repo>` | 运行测试并自动更新 `TEST.md` 结果文档 | `<path-or-repo>`：目标软件路径或仓库 |
| `/cli-anything:validate <path-or-repo>` | 对照 `HARNESS.md` 标准规范进行合规性验证 | `<path-or-repo>`：同上 |
| `/cli-anything:list [options]` | 列出所有可用的 CLI-Anything 工具 | `[options]`：过滤或格式化选项 |

### 使用示例

```bash
# 从本地源码生成 GIMP 的 CLI
/cli-anything /home/user/gimp

# 从 GitHub 仓库生成 Blender CLI
/cli-anything https://github.com/blender/blender

# 宽泛精炼：自动分析全部能力缺口
/cli-anything:refine ./gimp

# 定向精炼：针对特定功能
/cli-anything:refine ./shotcut "vid-in-vid and picture-in-picture compositing"

# 运行测试
/cli-anything:test ./inkscape

# 验证合规性
/cli-anything:validate ./audacity
```

---

## CLI-Hub 包管理器

CLI-Hub 是 CLI-ANYTHING 的社区包管理器，用于自主发现、安装、更新社区构建的 CLI Harness。

> 这是 **方式一：CLI-Hub 安装** 的配套工具。想了解两种方式的区别，见 [安装与集成](#安装与集成)。

### 安装 CLI-Hub

```bash
pip install cli-anything-hub
```

### CLI-Hub 命令

| 命令 | 说明 | 示例 |
|------|------|------|
| `cli-hub install <name>` | 安装指定 CLI Harness | `cli-hub install gimp` |
| `cli-hub search <keyword>` | 搜索 CLI Harness | `cli-hub search "image"` |
| `cli-hub update` | 更新所有已安装 CLI | `cli-hub update` |
| `cli-hub uninstall <name>` | 卸载指定 CLI | `cli-hub uninstall gimp` |
| `cli-hub list` | 列出已安装的 CLI | `cli-hub list` |

---

## 已支持的 Harness 列表

| 软件/领域 | Harness 名称 | 调用后端 | 测试覆盖 |
|:---|:---|:---|:---|
| 🎨 GIMP (图像编辑) | `cli-anything-gimp` | Pillow + GEGL/Script-Fu | ✅ 107 |
| 🧊 Blender (3D建模) | `cli-anything-blender` | bpy (Python) | ✅ 208 |
| ✏️ Inkscape (矢量) | `cli-anything-inkscape` | SVG/XML 直操作 | ✅ 202 |
| 🎵 Audacity (音频) | `cli-anything-audacity` | Python wave + sox | ✅ 161 |
| 🌐 Browser (自动化) | `cli-anything-browser` | DOMShell MCP | ✅ New |
| 📄 LibreOffice (办公) | `cli-anything-libreoffice` | ODF + headless LO | ✅ 158 |
| 📚 Zotero (文献) | `cli-anything-zotero` | SQLite + Local API | ✅ New |
| 📹 OBS Studio (直播) | `cli-anything-obs-studio` | obs-websocket | ✅ 153 |
| 🎞️ Kdenlive (视频剪辑) | `cli-anything-kdenlive` | MLT XML + melt | ✅ 155 |
| ✂️ Shotcut (视频剪辑) | `cli-anything-shotcut` | MLT XML + melt | ✅ 154 |
| 📞 Zoom (会议) | `cli-anything-zoom` | Zoom REST API | ✅ 22 |
| 🎵 MuseScore (乐谱) | `cli-anything-musescore` | mscore CLI | ✅ 56 |
| 📐 Draw.io (绘图) | `cli-anything-drawio` | mxGraph | ✅ 138 |
| 📊 Mermaid (图表) | `cli-anything-mermaid` | mermaid.ink | ✅ 10 |
| 🛡️ AdGuard Home (网络) | `cli-anything-adguardhome` | REST API | ✅ 36 |
| 🔌 WireMock (测试) | `cli-anything-wiremock` | HTTP Mock 服务 | ✅ New |
| 🦙 Ollama (AI) | `cli-anything-ollama` | REST API/SDK | ✅ 98 |
| 🎨 ComfyUI (AI绘画) | `cli-anything-comfyui` | REST API/SDK | ✅ 70 |
| 🔍 Exa (搜索) | `cli-anything-exa` | REST API | ✅ 40 |
| 🗺️ QGIS (地理信息) | `cli-anything-qgis` | PyQGIS / qgis_process | ✅ 22 |
| 🔧 FreeCAD (CAD) | `cli-anything-freecad` | FreeCAD API | ✅ 258 cmds |
| 🎮 Godot (游戏引擎) | `cli-anything-godot` | Godot 4 无头子进程 | ✅ |
| 📝 n8n (自动化) | `cli-anything-n8n` | 工作流 DSL | ✅ |
| 🔄 Dify Workflow | `cli-anything-dify-workflow` | 自动化封装 | ✅ |
| 📋 VideoCaptioner | `cli-anything-videocaptioner` | PyPI CLI 封装 | ✅ |
| **总计** | **22+ 核心 Harness** | **真实后端调用** | **✅ 2,152+ 项测试** |

---

## 各 Harness 详细说明

### 🎨 GIMP — 图像编辑

**调用后端**: Pillow + GEGL/Script-Fu  
**测试覆盖**: 107 项

| 功能类别 | 说明 |
|----------|------|
| 图像创建 | 新建图像、设置尺寸、颜色模式（RGB/RGBA/灰度等） |
| 图层操作 | 添加/删除图层、图层混合模式、不透明度、可见性 |
| 滤镜 | 模糊、锐化、颜色调整、几何变换、艺术效果等 GEGL 操作 |
| 选区 | 矩形/椭圆/自由选区、选区布尔运算 |
| 导出 | 导出为 PNG/JPEG/WebP/GIF 等格式 |

**使用示例**:
```bash
cli-anything-gimp image new --width 1920 --height 1080 -o project.xcf
cli-anything-gimp filter blur --radius 5 --input project.xcf
cli-anything-gimp export --format png --output output.png
```

---

### 🧊 Blender — 3D 建模与渲染

**调用后端**: bpy (Python 脚本)  
**测试覆盖**: 208 项

| 功能类别 | 说明 |
|----------|------|
| 场景管理 | 创建/删除/切换场景 |
| 对象操作 | 添加网格（立方体、球体、圆柱等）、变换（移动/旋转/缩放） |
| 材质 | 创建材质、设置颜色、粗糙度、金属度 |
| 灯光 | 添加光源（点光、日光、区域光）、调整强度和颜色 |
| 相机 | 添加/设置相机位置和角度 |
| 渲染 | 执行渲染（Cycles/EEVEE 引擎）、输出图像 |
| 动画 | 关键帧设置、播放动画 |

**使用示例**:
```bash
cli-anything-blender scene new --name ProductShot
cli-anything-blender object add-mesh --type cube --location 0 0 1
cli-anything-blender render execute --output render.png --engine CYCLES
```

**REPL 模式**:
```bash
$ cli-anything-blender
blender> scene new --name ProductShot
✓ Created scene: ProductShot

blender[ProductShot]> object add-mesh --type cube --location 0 0 1
✓ Added mesh: Cube at (0, 0, 1)

blender[ProductShot]*> render execute --output render.png --engine CYCLES
✓ Rendered: render.png (1920×1080, 2.3 MB) via blender --background

blender[ProductShot]> exit
Goodbye! 👋
```

---

### ✏️ Inkscape — 矢量图形编辑

**调用后端**: SVG/XML 直操作  
**测试覆盖**: 202 项

| 功能类别 | 说明 |
|----------|------|
| 文档创建 | 新建 SVG 文档、设置尺寸 |
| 形状绘制 | 矩形、椭圆、星形、多边形、路径 |
| 文本 | 添加文本、设置字体、大小、颜色 |
| 变换 | 移动、旋转、缩放、倾斜 |
| 填充与描边 | 设置填充颜色、描边宽度、线型 |
| 图层 | 创建/删除图层、图层排序 |
| 导出 | 导出为 PNG/PDF/SVG 等格式 |

**使用示例**:
```bash
cli-anything-inkscape document new --width 800 --height 600 -o design.svg
cli-anything-inkscape shape rect --x 10 --y 10 --width 100 --height 50
cli-anything-inkscape export --format png --output output.png
```

---

### 🎵 Audacity — 音频编辑

**调用后端**: Python wave + sox  
**测试覆盖**: 161 项

| 功能类别 | 说明 |
|----------|------|
| 音频导入 | 导入 WAV/MP3/OGG 等格式 |
| 音频操作 | 剪切、复制、粘贴、删除选区 |
| 效果 | 淡入/淡出、反转、标准化、压缩、均衡器 |
| 生成 | 生成音调、白噪音、静音 |
| 导出 | 导出为 WAV/MP3/OGG 等格式 |

**使用示例**:
```bash
cli-anything-audacity open input.wav
cli-anything-audacity effect normalize
cli-anything-audacity export output.mp3
```

---

### 🌐 Browser — 浏览器自动化

**调用后端**: DOMShell MCP  
**测试覆盖**: 新增

| 功能类别 | 说明 |
|----------|------|
| 导航 | 打开 URL、前进、后退、刷新 |
| 页面操作 | 点击、输入文本、选择下拉选项 |
| 内容提取 | 获取页面文本、DOM 结构、无障碍树 |
| 截图 | 截取页面截图 |
| 脚本执行 | 在页面上下文中执行 JavaScript |

---

### 📄 LibreOffice — 办公套件

**调用后端**: ODF 生成 + Headless 模式  
**测试覆盖**: 158 项

| 功能类别 | 说明 |
|----------|------|
| 文档类型 | Writer (文字)、Calc (表格)、Impress (演示) |
| 文档创建 | 新建文档、打开已有文档 |
| 内容编辑 | 添加标题、段落、表格、列表、图片 |
| 格式设置 | 字体样式、段落格式、页面布局 |
| 导出渲染 | 导出为 PDF/DOCX/XLSX/PPTX 等真实格式 |

**使用示例**:
```bash
# 创建 Writer 文档
cli-anything-libreoffice document new -o report.json --type writer

# 添加标题与表格
cli-anything-libreoffice --project report.json writer add-heading -t "Q1 Report" --level 1
cli-anything-libreoffice --project report.json writer add-table --rows 4 --cols 3

# 导出为真实 PDF
cli-anything-libreoffice --project report.json export render output.pdf -p pdf --overwrite

# Agent 友好的 JSON 模式输出
cli-anything-libreoffice --json document info --project report.json
```

**常用参数**:
| 参数 | 说明 |
|------|------|
| `-o <file>` | 指定输出文件名 |
| `--type writer/calc/impress` | 指定文档类型 |
| `--project <file>` | 绑定已有项目文件 |
| `-t <text>` | 传入文本内容 |
| `--rows / --cols` | 表格行列数 |
| `-p pdf/docx/xlsx` | 导出格式 |
| `--overwrite` | 覆盖已有文件 |
| `--json` | 强制输出机器可读 JSON |

---

### 📚 Zotero — 文献管理

**调用后端**: SQLite + Local REST API  
**测试覆盖**: 新增

| 功能类别 | 说明 |
|----------|------|
| 文献管理 | 添加、删除、查询文献条目 |
| 分类 | 创建集合、添加标签 |
| 附件 | 添加 PDF 附件、笔记 |
| 搜索 | 按标题、作者、标签搜索 |
| 导出 | 导出参考文献格式（BibTeX/RIS 等） |

---

### 📹 OBS Studio — 直播录制

**调用后端**: obs-websocket  
**测试覆盖**: 153 项

| 功能类别 | 说明 |
|----------|------|
| 场景管理 | 创建/切换/删除场景 |
| 来源管理 | 添加视频捕获、窗口捕获、图像、文本源 |
| 录制 | 开始/停止录制、保存路径设置 |
| 直播 | 开始/停止推流、设置流密钥 |
| 音频 | 调整音频源音量、静音 |

---

### 🎞️ Kdenlive — 视频剪辑

**调用后端**: MLT XML + melt 渲染器  
**测试覆盖**: 155 项

| 功能类别 | 说明 |
|----------|------|
| 项目管理 | 新建项目、打开项目 |
| 素材导入 | 导入视频、音频、图片 |
| 时间线 | 添加剪辑到时间线、设置入点/出点 |
| 转场 | 添加过渡效果（淡入淡出、擦除等） |
| 特效 | 应用视频效果（模糊、色彩调整等） |
| 字幕 | 添加标题和字幕 |
| 渲染 | 导出视频（设置编码器、分辨率、帧率） |

---

### ✂️ Shotcut — 视频剪辑

**调用后端**: MLT XML + melt 渲染器  
**测试覆盖**: 154 项

| 功能类别 | 说明 |
|----------|------|
| 项目管理 | 新建项目、打开项目 |
| 素材导入 | 导入视频、音频、图片 |
| 时间线 | 添加剪辑、画中画、视频叠加 |
| 滤镜 | 应用视频滤镜、音频滤镜 |
| 渲染 | 导出视频（多种预设格式） |

---

### 📞 Zoom — 视频会议

**调用后端**: Zoom REST API (OAuth2)  
**测试覆盖**: 22 项

| 功能类别 | 说明 |
|----------|------|
| 会议管理 | 创建、查询、删除会议 |
| 会议设置 | 设置会议时间、密码、等候室 |
| 用户管理 | 查询用户信息 |
| 录制管理 | 获取录制文件、下载链接 |

---

### 🎵 MuseScore — 乐谱编辑

**调用后端**: mscore CLI  
**测试覆盖**: 56 项

| 功能类别 | 说明 |
|----------|------|
| 乐谱创建 | 新建乐谱、设置调号/拍号/速度 |
| 音符编辑 | 添加音符、休止符、和弦 |
| 排版 | 设置页面布局、字体 |
| 导出 | 导出为 PDF/PNG/MIDI/MusicXML |

---

### 📐 Draw.io — 图表绘制

**调用后端**: mxGraph  
**测试覆盖**: 138 项

| 功能类别 | 说明 |
|----------|------|
| 图表创建 | 新建图表、设置画布尺寸 |
| 图形 | 添加矩形、圆形、菱形、箭头等基础图形 |
| 连接 | 创建图形间的连接线、设置线型 |
| 文本 | 添加文本标签、设置样式 |
| 导出 | 导出为 PNG/SVG/PDF/XML |

**使用示例**:
```bash
cli-anything-drawio diagram new
cli-anything-drawio shape add --type rectangle --x 100 --y 100 --width 120 --height 60
cli-anything-drawio connector add --from shape1 --to shape2
cli-anything-drawio export --format png --output diagram.png
```

---

### 📊 Mermaid — 图表生成

**调用后端**: mermaid.ink  
**测试覆盖**: 10 项

| 功能类别 | 说明 |
|----------|------|
| 流程图 | 生成流程图图 |
| 时序图 | 生成时序图 |
| 类图 | 生成类图 |
| 状态图 | 生成状态图 |
| 甘特图 | 生成甘特图 |
| 饼图 | 生成饼图 |
| 导出 | 导出为 PNG/SVG |

**使用示例**:
```bash
cli-anything-mermaid flowchart "A[开始] --> B[处理] --> C[结束]" -o flowchart.png
```

---

### 🛡️ AdGuard Home — 网络广告过滤

**调用后端**: REST API  
**测试覆盖**: 36 项

| 功能类别 | 说明 |
|----------|------|
| 状态查询 | 获取服务状态、统计信息 |
| 过滤规则 | 添加/删除过滤规则、白名单 |
| 客户端管理 | 管理客户端配置 |
| DNS 设置 | 配置上游 DNS 服务器 |

---

### 🔌 WireMock — HTTP Mock 服务

**调用后端**: HTTP Mock 服务  
**测试覆盖**: 新增

| 功能类别 | 说明 |
|----------|------|
| Stub 管理 | 创建、查询、删除 mock stub |
| 请求匹配 | 设置请求匹配规则（URL、方法、Header） |
| 响应配置 | 配置响应状态码、Body、Header |
| 录制 | 录制真实请求并生成 stub |

---

### 🦙 Ollama — 本地 AI 模型

**调用后端**: REST API/SDK  
**测试覆盖**: 98 项

| 功能类别 | 说明 |
|----------|------|
| 模型管理 | 拉取、删除、列出模型 |
| 推理 | 发送提示获取响应、流式输出 |
| 聊天 | 多轮对话、设置系统提示 |
| 嵌入 | 生成文本嵌入向量 |

---

### 🎨 ComfyUI — AI 绘画工作流

**调用后端**: REST API/SDK  
**测试覆盖**: 70 项

| 功能类别 | 说明 |
|----------|------|
| 工作流 | 加载、保存、执行工作流 |
| 图像生成 | 文生图、图生图 |
| 模型 | 查看已加载的模型、切换模型 |
| 队列 | 管理生成队列、获取任务状态 |

---

### 🔍 Exa — AI 搜索引擎

**调用后端**: REST API  
**测试覆盖**: 40 项

| 功能类别 | 说明 |
|----------|------|
| 搜索 | 关键词搜索、语义搜索 |
| 内容提取 | 获取页面全文内容 |
| 过滤 | 按域名、日期、语言过滤 |
| 相似内容 | 查找相似页面 |

---

### 🗺️ QGIS — 地理信息系统

**调用后端**: PyQGIS / qgis_process  
**测试覆盖**: 22 项

| 功能类别 | 说明 |
|----------|------|
| 项目管理 | 新建项目、加载图层 |
| 数据处理 | 矢量/栅格数据处理 |
| 分析 | 缓冲区分析、叠加分析 |
| 导出 | 导出地图为图片/PDF |

---

### 🔧 FreeCAD — CAD 设计

**调用后端**: FreeCAD API  
**测试覆盖**: 258 个命令

| 功能类别 | 说明 |
|----------|------|
| 文档管理 | 新建文档、保存 |
| 零件设计 | 创建草图、拉伸、旋转、布尔运算 |
| 装配 | 装配约束、配合 |
| 导出 | 导出为 STEP/STL/OBJ 等格式 |

---

### 🎮 Godot — 游戏引擎

**调用后端**: Godot 4 无头子进程  
**测试覆盖**: 有

| 功能类别 | 说明 |
|----------|------|
| 项目管理 | 创建/打开项目 |
| 场景 | 创建/编辑场景 |
| 脚本 | 编写/运行 GDScript |
| 导出 | 导出游戏可执行文件 |
| 调试 | 运行调试、分析性能 |

---

### 📝 n8n — 工作流自动化

**调用后端**: 工作流 DSL  
**测试覆盖**: 有

| 功能类别 | 说明 |
|----------|------|
| 工作流管理 | 创建、导入、导出工作流 |
| 节点 | 添加/配置节点（HTTP、定时、条件等） |
| 执行 | 触发工作流执行、查看结果 |
| 凭证 | 管理 API 凭证 |

---

### 🔄 Dify Workflow — AI 工作流

**调用后端**: 自动化封装  
**测试覆盖**: 有

| 功能类别 | 说明 |
|----------|------|
| 工作流管理 | 创建、发布、运行工作流 |
| 应用 | 创建 AI 应用（聊天、补全等） |
| 知识库 | 管理知识库文档 |

---

### 📋 VideoCaptioner — 视频字幕

**调用后端**: PyPI CLI 封装  
**测试覆盖**: 有

| 功能类别 | 说明 |
|----------|------|
| 字幕生成 | 从视频自动生成字幕 |
| 字幕编辑 | 编辑、调整字幕时间轴 |
| 导出 | 导出为 SRT/VTT/ASS 格式 |

---

## 使用示例

### 生成与精炼 Harness

```bash
# 从本地源码生成 GIMP 的 CLI
/cli-anything /home/user/gimp

# 从 GitHub 仓库生成 Blender CLI
/cli-anything https://github.com/blender/blender

# 宽泛精炼：自动分析全部能力缺口
/cli-anything:refine ./gimp

# 定向精炼：针对特定功能
/cli-anything:refine ./shotcut "vid-in-vid and picture-in-picture compositing"
```

### 使用生成的独立 CLI

#### 命令行模式

```bash
# GIMP 图像处理
cli-anything-gimp image new --width 1920 --height 1080 -o project.xcf
cli-anything-gimp filter blur --radius 5 --input project.xcf
cli-anything-gimp export --format png --output output.png

# Blender 3D 渲染
cli-anything-blender scene new --name ProductShot
cli-anything-blender object add-mesh --type cube --location 0 0 1
cli-anything-blender render execute --output render.png --engine CYCLES

# LibreOffice 文档处理
cli-anything-libreoffice document new -o report.json --type writer
cli-anything-libreoffice --project report.json writer add-heading -t "Q1 Report" --level 1
cli-anything-libreoffice --project report.json export render output.pdf -p pdf --overwrite
```

#### Agent JSON 模式

```bash
# 以 JSON 格式获取 LibreOffice 文档信息
cli-anything-libreoffice --json document info --project report.json

# 以 JSON 格式获取 GIMP 图像信息
cli-anything-gimp --json image info --input project.xcf
```

#### REPL 交互模式

```bash
$ cli-anything-blender
╔══════════════════════════════════════════╗
║       cli-anything-blender v1.0.0       ║
╚══════════════════════════════════════════╝

blender> scene new --name ProductShot
✓ Created scene: ProductShot

blender[ProductShot]> object add-mesh --type cube --location 0 0 1
✓ Added mesh: Cube at (0, 0, 1)

blender[ProductSpot]*> render execute --output render.png --engine CYCLES
✓ Rendered: render.png (1920×1080, 2.3 MB) via blender --background

blender[ProductShot]> exit
Goodbye! 👋
```

---

## 架构设计原则

### 1. 真实软件集成

- **绝不使用替代库** — CLI 仅生成项目文件（ODF, MLT, SVG），最终渲染/计算强制调用真实软件后端
- **后端缺失时测试直接失败** — 确保功能完整性，零降级依赖

### 2. 双模式交互

- **无状态子命令** — 适合流水线/脚本自动化
- **有状态 REPL** — 适合交互式 Agent 会话

### 3. Agent-Native 输出

- **`--json` 标志** — 全局支持，消除非结构化文本解析难题
- **`--help` 标准** — 供 Agent 自主发现能力

### 4. 零配置部署

- `pip install` 即可使用，无需额外配置

---

## 测试体系

CLI-ANYTHING 采用多层测试验证体系：

| 测试层级 | 验证目标 | 示例 |
|:---|:---|:---|
| **Unit Tests** | 核心函数隔离验证（合成数据） | 项目创建、图层操作、滤镜参数 |
| **E2E (Native)** | 项目文件生成管道 | ODF ZIP 结构、MLT XML、SVG 规范性 |
| **E2E (Backend)** | 真实软件调用与输出校验 | PDF 魔术字节校验、Blender 渲染 PNG 验证 |
| **CLI Subprocess** | 安装后命令的 `subprocess.run` 验证 | `cli-anything-gimp --json project new` 返回合法 JSON |

### 运行测试

```bash
cd <software>/agent-harness
python3 -m pytest cli_anything/<software>/tests/ -v

# 强制已安装模式验证
CLI_ANYTHING_FORCE_INSTALLED=1 python3 -m pytest cli_anything/<software>/tests/ -v -s
```

---

## 限制与注意事项

### ⚠️ 已知限制

1. **依赖前沿模型** — 需 Claude Opus/Sonnet 4.6、GPT-5.4 等强推理模型保证生成质量；弱模型可能需人工修正
2. **依赖源码可用性** — 若目标软件仅有编译后二进制文件，反向工程将显著降低 Harness 覆盖率
3. **迭代必要性** — 单次 `/cli-anything` 可能无法 100% 覆盖，建议多次运行 `/refine` 逐步逼近生产级质量

### 📚 官方文档路径

| 文件 | 说明 |
|------|------|
| `cli-anything-plugin/HARNESS.md` | 方法论 SOP（单一事实来源） |
| `cli-anything-plugin/QUICKSTART.md` | 5 分钟上手指南 |
| `cli-anything-plugin/PUBLISHING.md` | Harness 分发与发布指南 |

### 🤝 贡献指南

- **新增软件** — 使用插件生成 CLI 后，通过 `PUBLISHING.md` 提交 PR
- **方法迭代** — 欢迎提交 `HARNESS.md` 的经验补丁
- **测试扩展** — 补充边缘场景、E2E 工作流

### SKILL.md 统一分发

所有 Harness 的 AI 技能定义已统一至顶层 `skills/` 目录，可通过以下命令全局安装：

```bash
npx skills add HKUDS/CLI-Anything --skill <skill-name> -g -y
```

---

*本文档基于 CLI-ANYTHING 官方仓库 (HKUDS/CLI-ANYTHING) 整理，覆盖 22+ 核心 Harness、2,152+ 项测试，支持 10+ AI Agent 平台。*

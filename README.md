# 🎄 圣诞树粒子系统

<div align="center">

Claude Code 辅助创建的：一个基于 Three.js 和 MediaPipe 的交互式3D圣诞树照片展示系统，支持新手引导、手势控制、鼠标键盘控制、图片自动加载和手动上传、音频播放、截屏和录屏。

![Version](https://img.shields.io/badge/version-3.1-brightgreen)
![Three.js](https://img.shields.io/badge/Three.js-v0.160.0-blue)
![MediaPipe](https://img.shields.io/badge/MediaPipe-v0.10.3-orange)
![License](https://img.shields.io/badge/license-MIT-blue)

[功能特性](#-功能特性) • [快速开始](#-快速开始) • [使用说明](#-使用说明) • [配置说明](#%EF%B8%8F-配置说明)

</div>

---

## ✨ 功能特性

### 🎨 视觉效果
- **3D 粒子圣诞树** - 1500 个金色装饰品粒子组成动态圣诞树
- **雪花与尘埃系统** - 3000 个 GPU 加速粒子营造梦幻氛围
- **HDR 辉光效果** - 专业后处理效果，金色粒子发光
- **极简 UI 设计** - 玻璃拟态控制面板，圆形悬浮帮助按钮

### 🚀 交互增强
- **交互式新手引导** - 首次访问自动开启，三步掌握核心操作
- **手势控制系统**：
  - **握拳** → 粒子聚合成圣诞树形态
  - **张开手** → 照片散开成球形分布
  - **捏合** → 聚焦放大单张照片
- 5 帧移动平均滤波，识别更平滑

### 📸 智能图片系统
- 自动检测 6 种图片格式（jpg/jpeg/png/webp/gif/bmp）
- 智能批量加载（每批 10 张并发）
- **自动错误静默处理**：智能跳过不存在的序号，保持控制台整洁
- 超过 2048px 自动压缩
- 支持拖拽上传文件夹/文件

### 🎵 音频与录制
- 背景音乐播放控制（支持音格调节与静音）
- PNG 截图和 MP4 视频录制
- **性能休眠**：页面失焦时自动暂停渲染与多媒体，节省系统资源

### ⚡ 性能优化
- **99.8% DrawCall 降低**（3500+ → 6，使用 InstancedMesh）
- **10 倍加载速度提升**（60s → 6s，批量并发加载）
- **GPU 加速**雪花粒子（GLSL 着色器）
- 标签页隐藏时自动休眠

---

## 🚀 快速开始

### 配置要求
- 现代浏览器（Chrome 90+、Firefox 88+、Edge 90+）
- 本地 HTTP 服务器（必需，不能直接打开 HTML 文件）
- Python 3.6+（可选，用于图片预处理工具）

### 三步启动

#### 步骤 1：启动本地服务器

```bash
# 方式 1：Python（推荐）
python -m http.server 8000

# 方式 2：Node.js
npx serve

# 方式 3：VS Code Live Server
# 安装 Live Server 扩展，右键 christmas.html → Open with Live Server
```

#### 步骤 2：访问应用

打开浏览器访问：
```
http://localhost:8000/christmas.html
```

#### 步骤 3：添加照片

**方式 A：预加载图片（推荐）**
1. 将照片重命名为 `(1).jpg`、`(2).jpg`、`(3).jpg`...
2. 放入 `images/` 文件夹
3. 刷新页面，自动加载

**方式 B：手动上传**
1. 点击右上角 "Select Folder" 或 "Select Files" 按钮
2. 选择照片
3. 自动压缩并加载

**方式 C：使用 Python 工具（最佳性能）**
```bash
# 1. 批量重命名
python rename_images.py -y

# 2. 批量压缩（提前压缩，加载更快）
python compress_images.py --no-backup

# 3. 刷新页面
```

---

## 📖 使用说明

### 手势控制

首次访问时允许摄像头权限以启用手势识别：

| 手势 | 操作 | 效果 |
|------|------|------|
| **握拳** | 五指收拢成拳头 | 照片聚合成圣诞树形态 |
| **张开手** | 五指完全张开 | 照片散开成球形分布 |
| **捏合** | 拇指 + 食指捏合 | 聚焦放大单张照片 |

**提示**：
- 确保光线充足
- 手掌完全进入摄像头画面
- 如果识别不准确，可在 `config.json` 中调整阈值

### 鼠标/触摸控制

#### 鼠标操作

| 操作 | 功能 |
|------|------|
| **左键拖拽** | 旋转场景 |
| **右键拖拽** | 平移场景 |
| **滚轮** | 缩放场景 |
| **双击** | 聚焦单张照片 |

#### 触摸操作（移动设备）

| 操作 | 功能 |
|------|------|
| **单指拖拽** | 旋转场景 |
| **双指捏合** | 缩放场景 |
| **双指拖拽** | 平移场景 |

### 截图与录制

#### 截图
```
方式 1：按 P 键
方式 2：点击右上角 "Screenshot" 按钮

→ 自动保存为 christmas_screenshot_YYYYMMDD_HHMMSS.png
```

#### 视频录制
```
方式 1：按 V 键开始/停止
方式 2：点击右上角 "Record" 按钮

录制中：显示红点 🔴 和计时器
停止后：自动下载 MP4 视频

限制：最长 2 分钟（可在代码中调整）
```

---

## ⌨️ 键盘快捷键

| 键 | 功能 | 说明 |
|---|------|------|
| `H` | 隐藏/显示 UI | 切换所有 UI 元素（包括音乐控制） |
| `C` | 切换摄像头 | 显示/隐藏摄像头预览窗口 |
| `M` | 播放/暂停音乐 | 切换背景音乐播放 |
| `N` | 静音/取消静音 | 切换音频静音 |
| `P` | 截图 | 保存 PNG 截图（自动隐藏 UI） |
| `V` | 录制视频 | 开始/停止 MP4 视频录制（最长 2 分钟） |
| `1` | 树形模式 | 强制粒子进入圣诞树形态 |
| `2` | 球形模式 | 强制照片进入球形分布 |
| `3` | 聚焦模式 | 强制进入聚焦模式（放大单张照片） |
| `Esc` | 退出聚焦 | 从聚焦模式返回上一个模式 |

---

## ⚙️ 配置说明

编辑 `config.json` 可调整所有参数，无需修改代码。

### 主要配置选项

<details>
<summary>📸 图片加载设置</summary>

```json
{
  "loader": {
    "filePattern": "(${i})",
    "folder": "./images/",
    "maxImages": 500,
    "maxConsecutiveFails": 10,
    "supportedExtensions": [".jpg", ".jpeg", ".png", ".webp", ".gif", ".bmp"]
  }
}
```
- `maxImages`：最多扫描的序号
- `maxConsecutiveFails`：连续失败 N 次后停止
- `supportedExtensions`：按优先级尝试的扩展名

</details>

<details>
<summary>⚡ 性能设置</summary>

```json
{
  "performance": {
    "autoScale": true,
    "maxPhotos": 50,
    "quality": "auto",
    "targetFPS": 60,
    "minFPS": 30
  }
}
```
- `autoScale`：低端设备自动降级
- `maxPhotos`：最大加载照片数量
- `quality`：渲染质量（auto/high/low）

</details>

<details>
<summary>✨ 粒子系统设置</summary>

```json
{
  "particles": {
    "tree": {
      "count": 1500,
      "treeHeight": 24,
      "treeRadius": 8
    },
    "dust": { "count": 2000, "enabled": true },
    "snow": { "count": 1000, "enabled": true }
  }
}
```
- 减少粒子数量可提升低端设备性能
- 设置 `enabled: false` 可禁用粒子系统

</details>

<details>
<summary>🖐️ 手势识别设置</summary>

```json
{
  "gestures": {
    "fist": { "threshold": 1.5 },
    "pinch": { "threshold": 0.35 },
    "open": { "threshold": 1.7 },
    "smoothing": 0.3,
    "cooldownMs": 500
  }
}
```
- 降低阈值 = 更容易触发
- 提高平滑度 = 更平滑但响应更慢
- 增加冷却时间可防止快速切换

</details>

<details>
<summary>🎵 音频设置</summary>

```json
{
  "audio": {
    "enabled": true,
    "autoplay": true,
    "defaultVolume": 0.5,
    "fadeIn": true,
    "fadeInDuration": 2000,
    "sources": [
      "./music/christmas.mp3",
      "./music/christmas.ogg"
    ]
  }
}
```
- 设置 `enabled: false` 可禁用音乐
- `defaultVolume`：0.0-1.0
- 替换 `music/` 文件夹中的音乐文件即可更换音乐

</details>

### 常见配置场景

**低端设备优化**
```json
{
  "particles": {
    "tree": { "count": 800 },
    "dust": { "count": 500 },
    "snow": { "count": 300 }
  },
  "performance": { "targetFPS": 30 },
  "postprocessing": { "bloom": { "enabled": false } }
}
```

**加载更多照片**
```json
{
  "loader": { "maxImages": 1000 },
  "performance": { "maxPhotos": 100 }
}
```

**处理图片序号缺口**
```json
{
  "loader": { "maxConsecutiveFails": 20 }
}
```

---

## 🐍 Python 工具

### 1. rename_images.py - 批量重命名

将任意命名的图片批量重命名为 `(1).jpg`、`(2).jpg` 等。

```bash
# 交互模式
python rename_images.py

# 自动确认模式
python rename_images.py -y
```

**支持格式**：JPG、JPEG、PNG、WebP、GIF、BMP

### 2. compress_images.py - 批量压缩

将图片预压缩到 2048×2048，加快网页加载速度。

```bash
# 压缩并备份（推荐）
python compress_images.py

# 压缩不备份
python compress_images.py --no-backup

# 输出到指定文件夹
python compress_images.py --output ./compressed
```

**压缩参数**：
- 最大尺寸：2048×2048px
- JPEG 质量：90%
- 算法：LANCZOS 高质量缩放
- 典型压缩率：80-95%

**依赖安装**：`pip install Pillow`

### 推荐工作流程

```bash
# 1. 将照片复制到 images 文件夹
cp ~/Photos/*.jpg images/

# 2. 批量重命名
python rename_images.py -y

# 3. 批量压缩（提升加载速度）
python compress_images.py

# 4. 检查压缩结果
ls -lh images/

# 5. 确认无误后删除备份
rm images/*_original.jpg

# 6. 刷新网页
```

---

## 🌐 浏览器支持

| 浏览器 | 最低版本 | WebGL 2.0 | 手势识别 | 文件夹选择 | 推荐程度 |
|--------|---------|-----------|----------|-----------|---------|
| **Chrome** | 90+ | ✅ | ✅ | ✅ | ⭐⭐⭐⭐⭐ |
| **Edge** | 90+ | ✅ | ✅ | ✅ | ⭐⭐⭐⭐⭐ |
| **Firefox** | 88+ | ✅ | ✅ | ⚠️ 部分支持 | ⭐⭐⭐⭐ |
| **Safari** | 15.4+ | ✅ | ✅ | ❌ | ⭐⭐⭐ |
| **Opera** | 76+ | ✅ | ✅ | ✅ | ⭐⭐⭐⭐ |

**注意**：
- 摄像头访问需要 HTTPS 或 localhost
- IE 11 及以下版本不支持（不支持 WebGL 2.0）
- 不支持直接打开 file:// 访问（CORS 策略限制）

---

## 📁 项目结构

```
my-christmas/
├── christmas.html              # 主应用（单文件，108KB，2500+ 行代码）
├── config.json                 # 全局配置文件（1.5KB）
├── hand_landmarker.task        # MediaPipe 手势识别模型（7.5MB）
├── README.md                   # 项目文档（本文件）
├── LICENSE                     # MIT 许可证
├── CHANGELOG.md                # 详细版本历史
├── CONTRIBUTING.md             # 贡献指南
│
├── .github/                    # GitHub 模板
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   └── feature_request.md
│   └── PULL_REQUEST_TEMPLATE.md
│
├── images/                     # 照片存储目录
│   ├── (1).jpg                 # 按序号命名的照片
│   ├── (2).png                 # 支持混合格式
│   ├── (3).webp
│   ├── ...
│   └── README.md               # 使用说明
│
├── music/                      # 音乐文件目录
│   ├── christmas.mp3           # 圣诞音乐（主格式）
│   ├── christmas.ogg           # 圣诞音乐（备选格式）
│   └── README.md               # 音乐设置说明
│
├── compress_images.py          # Python 工具：批量压缩图片
└── rename_images.py            # Python 工具：批量重命名图片
```

### 文件说明

| 文件 | 大小 | 说明 |
|-----|------|------|
| `christmas.html` | 108KB | 主程序，包含所有前端代码（HTML+CSS+JS） |
| `config.json` | 1.5KB | 配置文件，控制所有可调参数 |
| `hand_landmarker.task` | 7.5MB | MediaPipe 预训练模型，用于手势识别 |
| `LICENSE` | 2KB | MIT 许可证及第三方依赖声明 |
| `CHANGELOG.md` | 15KB | 详细版本历史和升级指南 |
| `CONTRIBUTING.md` | 8KB | 项目贡献指南 |
| `compress_images.py` | 8KB | 图片压缩工具，支持批量处理 |
| `rename_images.py` | 2.5KB | 图片重命名工具，生成序号格式 |

---

## 🚢 部署说明

### 本地部署

**Python HTTP 服务器（推荐）**
```bash
python -m http.server 8000
# 访问：http://localhost:8000/christmas.html
```

**Node.js serve**
```bash
npm install -g serve
serve -p 8000
```

**VS Code Live Server**
1. 安装 Live Server 扩展
2. 右键 christmas.html → Open with Live Server

### 远程部署

#### GitHub Pages（免费）
```bash
# 1. 创建 GitHub 仓库
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/用户名/my-christmas.git
git push -u origin main

# 2. 启用 GitHub Pages
# 进入 Settings → Pages → Source: main 分支 → 保存

# 3. 访问地址：
# https://用户名.github.io/christmas-tree/christmas.html
```

**注意**：所有文件公开可见。如有私人照片，请使用私有托管。

#### Netlify / Vercel（免费）
```bash
# 安装 CLI
npm install -g netlify-cli
# 或
npm install -g vercel

# 部署
netlify deploy --prod
# 或
vercel
```

### 部署检查清单

部署前检查：
```
☐ 图片已压缩（使用 compress_images.py）
☐ 备份文件已删除（*_original.jpg）
☐ config.json 路径正确
☐ 已启用 HTTPS（手势识别必需）
☐ 浏览器控制台无错误
☐ 已在目标浏览器测试
```

---

## ❓ 常见问题

<details>
<summary><b>Q1：图片无法加载？</b></summary>

检查：
1. 图片是否放在 `images/` 文件夹
2. 图片命名是否为 `(1).jpg`、`(2).jpg` 等
3. 是否启动了本地服务器（不能直接打开 HTML）
4. 查看浏览器控制台错误信息
</details>

<details>
<summary><b>Q2：摄像头无法启用？</b></summary>

解决方案：
1. 确保浏览器允许摄像头权限
2. 使用 HTTPS 或 localhost 访问
3. 检查是否有其他应用占用摄像头
4. 手势识别失败会自动降级到鼠标控制
</details>

<details>
<summary><b>Q3：FPS 过低 / 画面卡顿？</b></summary>

优化方法：
1. 在 `config.json` 中减少粒子数量
2. 禁用辉光：`"bloom": { "enabled": false }`
3. 限制照片数量：`"maxPhotos": 20`
4. 使用 `compress_images.py` 预压缩图片
</details>

<details>
<summary><b>Q4：手势识别不准确？</b></summary>

调整方法：
1. 调整 `config.json` 中 `gestures` 的阈值
2. 确保光线充足
3. 手掌完全进入摄像头画面
4. 增大 `smoothing` 值使识别更平滑
</details>

<details>
<summary><b>Q5：如何更换背景音乐？</b></summary>

步骤：
1. 准备音乐文件（MP3 或 OGG 格式）
2. 重命名为 `christmas.mp3`
3. 放入 `music/` 文件夹
4. 刷新页面

禁用音乐：在 `config.json` 中设置 `"audio.enabled": false`

详见 `music/README.md`。
</details>

<details>
<summary><b>Q6：图片序号不连续怎么办？</b></summary>

调整容忍度：
```json
{
  "loader": {
    "maxConsecutiveFails": 20  // 允许连续失败 20 次
  }
}
```
示例：有 (1).jpg、(5).jpg、(10).jpg
- 默认配置（10 次）：只加载 (1).jpg
- 调整后（20 次）：全部加载
</details>

<details>
<summary><b>Q7：页面白屏 / 初始化失败？</b></summary>

排查步骤：
1. 刷新页面并查看错误提示
2. 按 F12 查看控制台错误
3. 验证 `config.json` 格式是否为有效 JSON
4. 检查 `hand_landmarker.task` 文件是否存在（7.5MB）
5. 如果显示错误页面，点击"刷新页面"按钮
</details>

---

## 🛠️ 技术栈

| 技术 | 版本 | 用途 |
|-----|------|------|
| **Three.js** | v0.160.0 | 3D 渲染引擎 |
| **MediaPipe Tasks Vision** | v0.10.3 | 手势识别 |
| **WebGL** | 2.0 | GPU 加速渲染 |
| **GLSL** | - | 着色器编程（雪花系统） |
| **html2canvas** | v1.4.1 | 截图功能 |
| **MediaRecorder API** | - | 视频录制 |
| **Pillow** | 10.0+ | 图片压缩（Python 工具） |

---

## 📊 性能亮点

### v3.0 优化成果

| 指标 | 优化前 | 优化后 | 提升 |
|-----|-------|-------|-----|
| **FPS（低端设备）** | 30-45 | 55-60 | **+83%** |
| **DrawCall** | ~3500 | ~6 | **-99.8%** |
| **内存占用** | ~250MB | ~150MB | **-40%** |
| **图片加载速度** | 60s | 6s | **-90%** |
| **文件大小（168 张）** | 542MB | 85MB | **-84%** |

**关键优化技术**：
- 粒子系统使用 InstancedMesh
- GPU 加速雪花粒子（GLSL 着色器）
- 批量并发加载（每批 10 张）
- 超过 2048px 的图片自动压缩
- Page Visibility API 实现自动休眠
- Blob URL 正确清理，防止内存泄漏

详见 [CHANGELOG.md](CHANGELOG.md) 查看完整版本历史。

---

## 📄 许可证

本项目采用 MIT 许可证 - 详见 [LICENSE](LICENSE) 文件。

**第三方依赖**：
- Three.js - MIT 许可证
- MediaPipe - Apache 许可证 2.0
- html2canvas - MIT 许可证
- Pillow - HPND 许可证

---

## 🎁 致谢

### 技术支持
- **[Three.js](https://threejs.org/)** - 优秀的 3D 渲染库
- **[MediaPipe](https://mediapipe.dev/)** - Google 强大的手势识别框架
- **[Pillow](https://python-pillow.org/)** - Python 图像处理库
- **[html2canvas](https://html2canvas.hertzen.com/)** - 网页截图解决方案

### 灵感来源
- Github 开源项目基础
- Three.js 官方示例
- WebGL 粒子系统演示
- 节日主题网页设计

### 特别感谢
- **开源社区** - 全球开发者的无数贡献
- **Claude Code** - 高效的AI代码辅助
- **你** - 感谢使用本项目！

---

## 📮 联系与反馈

### 需要帮助？
1. 查看 [常见问题](#-常见问题) 章节
2. 查阅 [CHANGELOG.md](CHANGELOG.md) 了解已知问题
3. 检查浏览器控制台错误信息
4. 查看 [CONTRIBUTING.md](CONTRIBUTING.md) 了解问题报告流程

### 想要贡献？
查看 [CONTRIBUTING.md](CONTRIBUTING.md) 了解：
- 错误报告指南
- 功能请求流程
- 开发环境搭建
- 代码风格指南
- Pull Request 要求

---

<div align="center">

### ⭐ 如果这个项目对你有帮助，请给个 Star 吧！⭐

**Made with ❤️ and Claude Code**

🎄 **圣诞快乐！新年快乐！** 🎄

---

**版本**：v3.0
**更新日期**：2025-12-07
**状态**：✅ 稳定版本

</div>

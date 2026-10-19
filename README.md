<div align="center">

# LuLu Paper Reader

**把英文 PDF 论文，变成能读的中文 Word + 一个能悬停看图的阅读器**

[![Version](https://img.shields.io/badge/version-1.0-blue)](https://github.com/liuzizi2961/LuLuPaperReader)
[![Platform](https://img.shields.io/badge/platform-Windows%2010%2F11-lightgrey)]()
[![License](https://img.shields.io/badge/license-免费非商业-orange)]()

</div>

---

## 这是什么


**LuLu Paper Reader 先把 PDF 按真实阅读顺序拆成段落**，再逐段翻译，最后重新排版成 Word，同时生成一个可以**鼠标停在图注上就弹出原图**的阅读器。

它不追求「一键全自动」，只做一件事：**让你少花时间在排版和找图上**。

同时配备**完全免费离线且轻量化**的本地翻译选项（300MB），下载解压之后点开即用。

针对以下出版社的常见排版做过适配：

**ACS** · **AIP** · **Elsevier** · **Frontiers** · **IOP** · **MDPI** ·· **Springer** · **Wiley**

**只支持 Windows**

---

## 主要功能

### 提取阶段
- **按栏序还原阅读顺序** —— 双栏论文先读左栏读完再读右栏，不会左右交错
- **图表原地保留** —— 图、表、公式区域自动截图，插在译文对应位置
- **图注 / 表题 / 表注完整保留** —— 图注不做截断，全文翻译
- **丢弃无关内容** —— 页眉页脚、下载水印、版权行、坐标轴标签不进正文
- **只丢参考文献** —— 致谢、作者贡献、资助声明、Extended Data 都保留

### 翻译阶段
- **段落级翻译** —— 按段落喂给模型，保证上下文连续
- **术语与公式保护** —— 行内公式、化学式、单位不参与翻译
- **多引擎可选** —— 硅基流动（DeepSeek 等）/ OpenAI 兼容接口 / 本地 Argos

### 输出阶段
- **三种 Word** —— 纯中文（`-zh.docx`）、中英对照（`-dual.docx`）、英文原文（`-EN.md`）
- **阅读器**
  - 左侧目录树，按章节跳转
  - **鼠标停 1 秒**在图注上
  - 点击图注直接显示，不用等
  - 图片可缩放、拖动、置顶

---

## 快速开始

### 1. 安装

下载 `LuLuPaperReader_v1.0_win64.zip`，解压到任意目录，双击 **`LuLuPaperReader.exe`**。

绿色版，不用安装，解压即用（约 290 MB，含全部依赖）。

**系统要求**：Windows 10 / 11（64 位）

### 2. 配置翻译接口（只需一次）

菜单 **设置 → 翻译服务设置**：

| 项 | 说明 |
|---|---|
| 接口地址 | 如 `https://api.siliconflow.cn/v1` |
| API Key | 在服务商后台申请 |
| 模型 | 如 `deepseek-ai/DeepSeek-V3` |

点「测试连接」确认可用。

### 3. 翻译

1. 拖入 PDF（或 `Ctrl+O`）
2. 选输出目录
3. 点「开始翻译」（`Ctrl+R`）

一篇 10 页论文大约 1~5 分钟（取决于接口速度）。

### 4. 阅读

翻译完成后自动打开阅读器，或点 `Ctrl+1`。

输出目录结构：

```
输出目录/
└── 论文标题-时间/
    ├── 论文标题-zh.docx      纯中文
    ├── 论文标题-dual.docx    中英对照
    ├── 论文标题-EN.md        英文原文（提取结果）
    ├── 论文标题.json         阅读器数据
    └── images/               图/表/公式截图
```

---

---

## 技术实现

| 环节 | 方案 |
|---|---|
| PDF 解析 | [PyMuPDF](https://pymupdf.readthedocs.io/) |
| 版面分析 | 自研：栏检测、阅读顺序、图表聚类、噪声过滤 |
| 翻译 | 硅基流动 / OpenAI 兼容 API / [Argos Translate](https://github.com/argosopentech/argos-translate) |
| GUI | PySide6 (Qt 6) |
| Word 输出 | python-docx |

翻译引擎接口设计参考了 [PDFMathTranslate](https://github.com/Byaidu/PDFMathTranslate) (EMNLP 2025)。

---



---

## 免责声明

> **本软件免费传播和使用，请勿用于任何商业用途。**

- **仅供个人学习、研究与教学使用**。未经作者许可，禁止出售、捆绑分发、机构内部批量生产使用或提供付费翻译服务。
- **不提供、不分发、不存储任何论文内容**。您处理的 PDF 及其中的文字、图表著作权归原作者与出版方所有。请**仅处理您通过合法渠道有权访问的文献**，并遵守所在地区著作权法及各数据库使用条款。
- **译文由机器翻译生成，仅供参考**。可能存在错译、漏译、术语不准。**请勿直接用于论文投稿、专利申请、法律或医疗用途**。涉及学术结论时务必核对原文。
- 使用在线接口时，待翻译文本会发送至您配置的第三方服务商，请自行确认其隐私政策。**涉密或未公开内容请勿使用在线接口**。
- 本软件按「现状」提供，不附带任何担保。在法律允许的最大范围内，作者不对使用本软件造成的任何直接或间接损失承担责任。

完整条款见软件内 **关于 → 关于本软件**。

---

## 致谢

- 感谢 **中国矿业大学图书馆** 提供的文献资源支持
- 感谢 [PyMuPDF](https://github.com/pymupdf/PyMuPDF)、[PySide6](https://www.qt.io/)、[Argos Translate](https://github.com/argosopentech/argos-translate)、[PDFMathTranslate](https://github.com/Byaidu/PDFMathTranslate) 等开源项目

---

## 联系

- 项目主页：https://github.com/liuzizi2961/LuLuPaperReader
- 邮箱：2512457694@qq.com


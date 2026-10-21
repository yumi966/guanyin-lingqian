[English](README.en.md) | 简体中文

# 观音灵签 · 静心一问

一个基于观音灵签一百首的离线可用、问答式抽签网页。

原生 HTML、CSS、JavaScript 编写，零依赖、单文件，可双击打开，也可直接部署到 GitHub Pages。

> 本项目是传统文化与自我反思工具，不是算命或预测工具。抽签结果不构成医疗、法律、投资、心理等专业建议。请先阅读文末的[免责声明](#免责声明)。

![License](https://img.shields.io/badge/license-MIT-green)
![Single File](https://img.shields.io/badge/build-single--file-b35a3f)
![No Dependencies](https://img.shields.io/badge/dependencies-none-2f6f57)

## 功能

- **问答式抽签**：先选择所问之事，再抽取签文，只展示与当前类别对应的分项断语。
- **单文件离线运行**：`index.html` 内嵌全部 100 首签文，不依赖外部脚本、接口或网络。
- **移动端适配**：支持窄屏布局、长签诗换行、触摸操作和系统减少动态效果设置。
- **等概率抽取**：使用 `crypto.getRandomValues` 与拒绝采样，避免简单的模偏差。
- **本机历史记录**：使用 `localStorage` 保存最近抽签结果，不上传任何用户数据。
- **输入安全处理**：用户输入在渲染前经过 HTML 转义，降低 XSS 风险。
- **缺失数据显式标注**：原文未标等级或未列分项时，界面明确显示，不补造内容。
- **无追踪、无广告**：项目不包含统计脚本、广告代码或第三方数据采集逻辑。

## 页面预览

| 桌面端 | 手机端 |
| --- | --- |
| <img src="docs/desktop-preview.png" alt="观音灵签桌面端预览" width="720"> | <img src="docs/mobile-preview.png" alt="观音灵签手机端预览" width="260"> |

## 在线演示

站点已通过 GitHub Pages 发布：

```text
https://yumi966.github.io/guanyin-lingqian/
```

也可以直接下载 `index.html`，用现代浏览器打开，完全离线使用。

## 快速开始

### 方式一：直接打开

1. 下载或克隆本仓库。
2. 双击 `index.html`。
3. 选择所问之事并抽签。

该方式不需要安装 Node.js、Python 或任何构建工具。

### 方式二：本地静态服务器

如果需要通过 HTTP 地址预览，可在仓库根目录运行：

```bash
python -m http.server 8000
```

然后访问 `http://localhost:8000/`。

### 方式三：部署到 GitHub Pages

1. 将仓库推送到 GitHub。
2. 打开仓库的 **Settings → Pages**。
3. 在 **Build and deployment** 中选择 **Deploy from a branch**。
4. Branch 选择 `main`，目录选择 `/ (root)`。
5. 保存并等待部署完成。

页面的入口文件必须命名为 `index.html`，并放在仓库根目录。

### 方式四：其他静态托管

本项目可以上传到 Cloudflare Pages、Netlify、Vercel、腾讯云 COS、EdgeOne Pages 等任意静态托管平台。上传 `index.html` 即可，无需服务端逻辑。

## 项目结构

```text
guanyin-lingqian/
├── index.html                         # 单文件应用：HTML + CSS + JS + 100 首签文
├── README.md                          # 中文说明
├── README.en.md                       # English README
├── LICENSE                            # MIT 许可证
├── DATA_NOTICE.md                     # 数据来源、缺失字段与许可说明
├── CONTRIBUTING.md                    # 贡献指南
├── CODE_OF_CONDUCT.md                 # 社区行为准则
├── SECURITY.md                        # 安全说明
├── .editorconfig                      # 编辑器格式约定
├── .gitignore
├── docs/
│   ├── desktop-preview.png
│   └── mobile-preview.png
└── .github/
    ├── ISSUE_TEMPLATE/
    │   ├── bug_report.yml
    │   ├── data_correction.yml
    │   └── config.yml
    └── PULL_REQUEST_TEMPLATE.md
```

## 数据说明

- 项目包含 **100 首签文**，整理自民间流传的观音灵签电子文本。
- 数据**未经严格学术校勘**。不同庙宇、网站或印刷版本之间可能存在文字、等级、签题和分项差异。
- 本项目不代表任何庙宇、宗教组织或出版机构的官方版本。
- 原文缺失的等级和分项会明确显示为未标或未列，不根据其他版本擅自补写。
- 如需提交数据修订，请注明签号、字段、当前内容、建议内容和可核验的出处。
- 数据授权、使用边界与修订规则详见 [DATA_NOTICE.md](DATA_NOTICE.md)。

## 技术实现

- 使用原生 HTML、CSS 和 JavaScript，无框架、无包管理器、无构建步骤。
- 数据以 `window.SIGNS = [...]` 的形式内嵌，避免 `file://` 环境中的 `fetch` 跨域限制。
- 抽签使用 `crypto.getRandomValues` 与拒绝采样。
- 签文、等级、分项和用户输入在拼接进 DOM 前统一做 HTML 转义。
- `localStorage` 读写均包含异常处理，存储不可用时仍可正常抽签。
- 响应式断点针对桌面、平板、手机和极窄屏分别处理。
- 支持键盘操作，并尊重 `prefers-reduced-motion`。

## 隐私

- 项目没有服务器端组件。
- 项目不上传、同步或分析用户输入。
- 抽签记录只保存在当前浏览器的 `localStorage` 中。
- 清除浏览器站点数据或点击页面中的“清空”按钮即可删除历史记录。

## 已知限制

- 签文版本的准确性受原始电子文本限制。
- 不同浏览器对 `file://` 下 `localStorage` 的策略可能不同。
- 项目仅提供辅助性解读文案，不提供专业咨询。
- 暂未提供多语言界面，当前界面为简体中文。

## 贡献

欢迎通过 Issue 或 Pull Request 修正错字、补充可核验的数据出处、改进移动端体验或提升可访问性。

提交前请阅读 [CONTRIBUTING.md](CONTRIBUTING.md) 和 [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)。

## 免责声明

本项目是传统文化展示与自我反思工具，不是算命、预测或决策工具。

- 签文整理自民间流传的电子文本，未经严格校勘，可能存在错漏、异体字或版本差异。
- 抽签结果不构成医疗、法律、投资、心理或任何其他专业建议，也不能预测未来。
- 如遇健康、法律、财务或情绪危机，请咨询具备资质的专业人士。
- 请勿反复抽签追问同一问题，抽签结果不应替代个人判断与专业意见。

使用本项目即表示你已理解并接受上述说明。

## 许可证

代码与项目文档采用 [MIT License](LICENSE)。

签文数据的来源与授权边界请另行阅读 [DATA_NOTICE.md](DATA_NOTICE.md)。MIT License 不应被理解为对第三方签文内容主张独占版权。

## 致谢

感谢所有参与签文整理、错字反馈、版本核验和前端改进的贡献者。


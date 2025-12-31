# Repository Guidelines

## 项目结构与模块组织

- `index.html`：单页应用入口，负责页面结构与 CDN 依赖引入（marked / KaTeX / Mermaid / ECharts / html2canvas / jsPDF）。
- `script.js`：核心业务逻辑（Markdown 渲染、公式与图表渲染、导出 PNG/PDF/HTML、交互与状态管理）。
- `style.css`：整体样式与主题变量（Grid/Flex、响应式、导出样式）。
- `manifest.json`、`favicon.svg`、`madopic.png`：PWA/图标与示例资源。

## 构建、测试与本地开发命令

本仓库为纯静态前端，无需构建步骤；建议使用本地 HTTP 服务器运行（避免 `file://` 下的资源/CORS 限制影响导出）。

- `python3 -m http.server 8000`：在仓库根目录启动静态服务。
- `open http://localhost:8000`：打开页面进行开发调试。

## 编码风格与命名约定

- 缩进：HTML/JS/CSS 统一使用 4 空格；保持现有文件的排版风格与分段结构。
- JavaScript：优先 `const`/`let`，保留分号；新增逻辑优先封装为小函数/类方法并复用现有渲染管线。
- 资源缓存：如修改 `style.css`/图标等静态资源，记得同步更新 `index.html` 中的 `?v=YYYYMMDD` 版本参数以便缓存失效。

## 测试指南

当前无自动化测试。提交前至少手动验证：

- Markdown 基础渲染、代码块换行、预览缩放。
- KaTeX（含 mhchem）、Mermaid、ECharts 渲染与导出一致性。
- 导出 PNG/PDF/HTML：检查清晰度、分页/尺寸、以及含图片场景。

## Commit 与 Pull Request 指南

- 提交信息：沿用现有历史的英文祈使句风格（例如 `Fix ...`），一句话说明改动目的。
- PR 要求：描述问题与方案、列出手动验证步骤；涉及 UI/样式变更请附截图；如关联问题请链接 Issue。

## 安全与配置提示

- 导出依赖 canvas：远程图片可能触发 “tainted canvas”，优先使用本地/粘贴图片或确保图片资源具备正确的 CORS 头。
- 处理用户输入（Markdown/HTML）时避免引入新的不受控 `innerHTML` 写入路径；如必须新增，说明风险与防护策略。

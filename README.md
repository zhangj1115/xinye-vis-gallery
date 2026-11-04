<!-- Origin: CODEX_NEW — public introduction, installation and usage; generated counts. -->
# 新叶绘图 · xinye-vis MCP

**AI 生信绘图，生信技能树出品。** 看文献原图，选喜欢的样式，把已有分析结果交给 Agent，生成来源清楚、可以复现的科研图。

[在线图册](https://zhangj1115.github.io/xinye-vis-gallery/) · [安装与使用指南](https://zhangj1115.github.io/xinye-vis-gallery/guide.html) · [下载安装包](https://github.com/zhangj1115/xinye-vis-gallery/releases/latest) · [更新记录](CHANGELOG.md)

当前版本 **v0.8.0**：**93 个独立案例**，**93 个可直接绘图入口**，关联 **64 篇参考文献**。图册负责选图、核对出处和复制提示词；MCP 在你的电脑上检查输入、执行绘图并导出结果。

## 可以做什么

- 按组学、图形标签、关键词与来源找图；放大文献原图，查看期刊、日期、论文及教程作者。
- 使用自然语言描述目标，或提供已有结果的字段，让 Agent 推荐方法并指出缺少的数据。
- 优先复用作者或教程代码、保留参考样式；改编和独立实现分别标明，原件单独归档。
- 导出 PDF、SVG、PNG，保留输入、参数、依赖版本、代码来源及重运行脚本。

| 分类 | 展示案例数 |
|---|---:|
| bulk转录组 | 37 |
| 单细胞转录组 | 37 |
| 空间转录组 | 5 |
| 蛋白组 | 3 |
| 代谢组 | 0 |
| 基因组与突变 | 5 |
| 微生物组 | 4 |
| 通用绘图 | 3 |

跨分类案例只计一次总数；代谢组为预留栏目。组合图可出现在多个图形标签下。正式编号为 BK / SC / SP / P / M / MR / G / X；已撤下编号不恢复。

## 安装

1. 从 [Releases](https://github.com/zhangj1115/xinye-vis-gallery/releases/latest) 下载 **`xinye-vis-mcp-0.8.0.zip`**，解压到长期保留的目录。GitHub 自动提供的 “Source code” 是图册仓库，**安装 MCP 请用上述专用 ZIP**。
2. 安装 [uv](https://docs.astral.sh/uv/getting-started/installation/) 和 [R 4.6.x](https://cran.r-project.org/)，确保终端能找到 `uv` 与 `Rscript`。Python 3.11 由 uv 准备。
3. 在解压后的 `xinye-vis-mcp` 目录运行安装脚本。首次安装会按 uv / renv 锁文件联网恢复依赖。

macOS / Linux：

```sh
bash install.sh --example BK13
```

Windows PowerShell：

```powershell
powershell -ExecutionPolicy Bypass -File .\install.ps1 --example BK13
```

成功后会生成一张 GSVA 示例图，以及 `config/mcp-client.json` 和 `config/workbuddy.mcp.json`。两个配置文件均包含接收者本机的绝对路径，不要直接复制他人电脑的配置。

## 接入 Agent

- **WorkBuddy AI**：打开 MCP 服务器配置，将 `config/workbuddy.mcp.json` 中的 `xinye-vis-mcp` 服务合并进去，保留已有其他服务。
- **Codex**：将生成配置中的 `command`、`args` 写入 `~/.codex/config.toml` 的 `[mcp_servers.xinye-vis-mcp]`；`env` 对应 `[mcp_servers.xinye-vis-mcp.env]`。下面是字段结构，实际值取自生成配置。

```toml
[mcp_servers.xinye-vis-mcp]
command = "/你的安装目录/xinye-vis-mcp/.venv/bin/python"
args = ["/你的安装目录/xinye-vis-mcp/scripts/launch_mcp.py"]

[mcp_servers.xinye-vis-mcp.env]
XINYE_VIS_ROOT = "/你的安装目录/xinye-vis-mcp"
XINYE_RSCRIPT = "/你的R安装路径/Rscript"
```

- **ZCode / 其他 stdio 客户端**：将生成配置中的服务字段合并到客户端 MCP 设置；ZCode 使用 `mcp.servers.xinye-vis-mcp`。Windows 的 Python 路径为 `.venv\Scripts\python.exe`，以安装程序生成的值为准。

保存后重连 MCP，再对 Agent 说：

> 用 xinye-vis-mcp 检查环境，列出可用方法，并用 BK13 生成一张示例图。

## 使用案例

**1. GSVA t 值双向条形图（BK13）**

> 用 xinye-vis-mcp 读取 BK13 的输入要求。数据在 `/你的数据/gsva_limma_diff.csv`；先检查列名并校验输入，以原始 pvalue < 0.1 着色，保留参考图样式，输出 PDF、SVG 和 PNG。

**2. 单细胞 UMAP 大群轮廓与亚群标签（SC01）**

> 我已有 UMAP 坐标和细胞注释。读取 SC01 的字段要求，核对我的 CSV，按大群画轮廓、按亚群着色并加标签。使用已有坐标。

**3. 临床亚组 HR 森林图（BK36）**

> 使用 BK36 展示我的亚组结果。先检查 label、count、percent、hr、lower、upper，使用已有 HR 和置信区间，导出矢量图。

**4. 根据文件推荐图形**

> 我有三份基因列表，想展示交集。请用 xinye-vis-mcp 找合适的方法，读取输入模板，说明如何整理文件，再校验和绘图。

也可在图册点击 **“Agent复制提示词调用”**，展开核对提示词，将其中的数据路径换成自己的路径后粘贴给 Agent。示例请求在安装包 `examples/<方法ID>/request.json`，字段说明在 `docs/METHODS.md`。

## 数据与运行范围

支持 CSV、TSV、XLSX 和显式声明类型的 RDS。常用字段可映射；以每款 `get_method` 返回的数据契约为准。原始 P 值和校正 P 值分别标注，参数按方法确定。工具读取已有分析结果，不执行差异分析、富集检验、GSVA 打分或降维推断；BK08 可重建运行 ES，不推算 NES/P 值。

8 个工具：`list_methods`、`search_methods`、`recommend_methods`、`get_method`、`validate_inputs`、`render_plot`、`render_example`、`check_environment`。推荐使用“搜索 → 读取说明 → 校验文件 → 绘图”的流程。

安装包中的示例使用合成数据；网页中的论文原图、真实公开数据复现和 MCP 示例按各自来源说明区分。第三方代码、文献图片与教程保留作者署名和许可记录，详见包内 `THIRD_PARTY_NOTICES.md` 与 `CODE_ORIGINS.tsv`。

## 常见问题

- **连接失败**：确认安装脚本已成功，配置路径存在；保存配置后重连。移动安装目录后重新运行安装脚本并更新客户端配置。
- **找不到 Rscript**：将 R 加入 PATH，或设置 `XINYE_RSCRIPT` 后重新安装。
- **缺少 R 依赖或中文字体**：查看安装日志及 `check_environment`；按日志补齐编译工具或本机字体。
- **只打开网站能否绘图**：网站提供图册和提示词，实际绘图需要本机安装 MCP。

macOS 接收者目录安装与绘图的实际验收范围见 Release 附件。Windows / Linux 提供安装脚本，尚未做独立系统验收。

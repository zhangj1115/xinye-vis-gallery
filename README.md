<!-- Origin: CODEX_NEW — generated publication README; version and counts come from the catalog. -->
# 新叶绘图(xinye-vis MCP) · 文献原图索引

[打开在线图册](https://zhangj1115.github.io/xinye-vis-gallery/) · [版本变更记录](CHANGELOG.md)

当前图册版本为 **v0.7.0**，收录 **91 个独立案例**，其中 **91 个提供可直接调用的本地 MCP 绘图入口**。网站用于选图、查看出处和复制调用提示词；实际绘图在使用者的本地 MCP 环境运行。

| 分类 | 展示案例数 |
|---|---:|
| bulk转录组 | 35 |
| 单细胞转录组 | 37 |
| 空间转录组 | 5 |
| 蛋白组 | 3 |
| 代谢组 | 0 |
| 基因组与突变 | 5 |
| 微生物组 | 4 |
| 通用绘图 | 3 |

跨分类案例只计一次总数。正式编号采用 BK、SC、SP、P、M、G、MR、X；已移除或合并的编号不再提供独立入口。

本版新增 **BK36 临床亚组 HR 森林图**，位于 **bulk转录组 → 森林图**。参考图是 MONARCH 3 Fig 3，代码来源为“小丫画图”教程；教程随附的 2,166 人示例数据与论文的 493 人数据分别说明。作者原代码按原始字节归档，MCP 适配另存。

图册支持组学分类、图形标签、关键词搜索、原图放大、MCP 示例预览、来源资料阅读，以及展开和复制 Agent 提示词。论文原图、教程配图和 MCP 示例分别标注，第三方资料保留署名及许可状态，版权归原权利人。

通过 GitHub Pages 发布 `main` 分支根目录。部署时保留 `index.html`、`assets/`、`recipes/`、`sources/` 和来源清单；旧预览入口统一转向主页面。`references.json`、`references.tsv` 保存案例来源，`build-report.json` 记录构建版本，`.xinye-public-files.json` 记录公开文件的 SHA-256。

每次正式发布使用独立提交和带说明的版本标签；回退通过新提交恢复旧版本内容，保留已有历史，不强制覆盖分支或标签。MCP 服务、环境配置和用户分析数据保留在本地。

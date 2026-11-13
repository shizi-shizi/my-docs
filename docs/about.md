# 项目说明

## 项目目标

把 `docs` 目录里的四页文档构建成静态网站并公开访问，做到推送之后不用人工构建和上传。

## 工具分工

| 工具 | 负责的环节 | 出现在哪里 |
| --- | --- | --- |
| Markdown | 写文档内容 | `docs/*.md` |
| MkDocs | 把 Markdown 构建成 HTML | `mkdocs.yml`、`requirements.txt` |
| Material 主题 | 页面样式、左侧导航、搜索框 | `mkdocs.yml` 的 `theme` 段 |
| Git | 记录文档与配置的改动 | 仓库的提交记录 |
| GitHub Actions | 安装环境、构建、上传产物、发布 | `.github/workflows/deploy.yml` |
| GitHub Pages | 提供公开访问地址 | 仓库 Settings → Pages |

## 发布流程

1. 修改 `docs` 下的 Markdown，提交并推送到 `main`。
2. 工作流启动，安装 Python 3.12 和 `requirements.txt` 里的依赖。
3. 执行 `mkdocs build --strict`，生成 `site` 目录。
4. `site` 作为构建产物上传，`deploy` 任务把它发布到 Pages。
5. 打开 `https://shizi-shizi.github.io/my-docs/` 看到更新后的内容。

## 仓库结构

| 路径 | 作用 |
| --- | --- |
| `docs/` | 文档源文件，内容都在这里 |
| `site/` | 构建产物，每次构建重新生成，不提交 |
| `mkdocs.yml` | 站点名称、主题、导航 |
| `.github/workflows/deploy.yml` | 构建与部署的工作流 |
| `report/` | 实践报告与截图 |

`docs` 是源，`site` 是产物。产物由构建生成，手工改动会在下次构建时被覆盖，所以写进 `.gitignore`，不纳入版本管理。

## 配置检查清单

| 检查项 | 正确写法 | 容易出错的地方 |
| --- | --- | --- |
| `nav` 路径 | `index.md` | 写成 `docs/index.md`，构建会报找不到文件 |
| `site_url` | `https://shizi-shizi.github.io/my-docs/` | 漏掉仓库名，线上和本地预览都会 404 |
| Pages 发布来源 | GitHub Actions | 留在分支发布，网站打不开 |
| 部署权限 | `pages: write`、`id-token: write` | 缺失时 `deploy` 步骤报权限错误 |
| 触发范围 | `docs/**`、`mkdocs.yml`、`requirements.txt`、工作流文件 | 改报告不会触发部署，属预期行为 |
| `.gitignore` | `site/`、`.venv/`、`__pycache__/` | 把产物或虚拟环境提交进仓库 |

## 小结

静态文档的构建和发布可以交给流水线，但配置项比较集中，一处写错就会卡在上一步。本地的 `build --strict` 和 Actions 的日志，是排查这类问题的两个入口。

[返回首页](index.md) · [操作步骤](guide.md) · [接口示例](api.md)

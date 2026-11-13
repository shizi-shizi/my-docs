# my-docs

《软件工程概论》实践项目 2 的个人作业仓库：用 MkDocs Material 搭建四页文档站，通过 GitHub Actions 自动构建并部署到 GitHub Pages。

- 网站地址：https://shizi-shizi.github.io/my-docs/
- 个人实验报告：[report/README.md](report/README.md)
- 四页文档：首页 `docs/index.md`、项目说明 `docs/about.md`、操作步骤 `docs/guide.md`、接口示例 `docs/api.md`
- 工作流：[.github/workflows/deploy.yml](.github/workflows/deploy.yml)

## 本地预览

```bash
python -m venv .venv
# Windows Git Bash: source .venv/Scripts/activate
# Windows PowerShell: .\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m mkdocs serve
```

打开 `http://127.0.0.1:8000/`。只想检查有没有写错，用严格模式构建：

```bash
python -m mkdocs build --strict
```

## 部署方式

推送到 `main` 且改动命中 `docs/**`、`mkdocs.yml`、`requirements.txt` 或工作流本身时，Actions 自动构建并发布；也可以在 Actions 页面手动触发。`site/` 是构建产物，不提交到仓库。

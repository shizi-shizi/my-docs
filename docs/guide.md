# 操作步骤

## 前置条件

- Python 3.12（本机用 3.14 也能构建成功）
- Git
- 文本编辑器，如 VS Code

## 一、准备环境

```bash
python -m venv .venv
python -m pip install -r requirements.txt
```

PowerShell 下激活虚拟环境：

```powershell
.\.venv\Scripts\Activate.ps1
```

## 二、本地预览

```bash
python -m mkdocs serve
```

浏览器打开 `http://127.0.0.1:8000/my-docs/`。地址里的 `my-docs` 不能省：`site_url` 带了仓库路径，预览时按同一路径挂载，直接访问 `/about/` 会返回 404。

## 三、构建检查

```bash
python -m mkdocs build --strict
```

生成的静态文件在 `site` 目录。加 `--strict` 后警告会当成错误处理，链接写错、文件找不到时构建当场失败，比推送之后再去翻日志省事。

## 四、配置发布来源

仓库 Settings → Pages → Build and deployment，把 Source 设为 **GitHub Actions**。这一套不需要 `gh-pages` 分支，也不用申请访问令牌。

## 五、提交并推送

```bash
git add docs mkdocs.yml requirements.txt .github/workflows/deploy.yml
git commit -m "更新文档"
git push origin main
```

推送后到 Actions 页面确认 `build` 和 `deploy` 都通过，再刷新网站核对内容。

## 常见问题

| 现象 | 原因 | 处理 |
| --- | --- | --- |
| 网站打开 404 | Pages 的发布来源仍是分支发布 | 改成 GitHub Actions 后重新运行工作流 |
| `deploy` 步骤报权限错误 | 少了 `pages: write` 或 `id-token: write` | 在 `deploy` 任务的 `permissions` 中补上 |
| 推送后网站没变化 | 改动的文件不在 `paths` 里 | 改 `docs` 下的文件，或手动触发 `workflow_dispatch` |
| 本地构建失败，提示链接不存在 | `--strict` 把警告当错误 | 页面之间改用相对链接，如 `about.md` |
| 子页面打不开，首页正常 | 网址缺仓库名 | 用 `用户名.github.io/仓库名/` |

[返回首页](index.md) · [项目说明](about.md) · [接口示例](api.md)

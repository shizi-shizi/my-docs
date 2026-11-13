# 接口示例

这里放一份示例接口文档，用来练习接口描述的结构。接口是虚构的，站点上没有对应的服务。

## 查询文章列表

### 基本信息

| 项目 | 值 |
| --- | --- |
| 方法 | `GET` |
| 路径 | `/api/v1/articles` |
| 返回类型 | `application/json` |
| 用途 | 按分页返回文章列表 |

### 查询参数

| 名称 | 位置 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- | --- |
| `pageNo` | query | Integer | 否 | 页码，从 1 开始，默认 1 |
| `pageSize` | query | Integer | 否 | 每页条数，默认 20，上限 100 |
| `q` | query | String | 否 | 标题关键字，模糊匹配 |

### 响应示例

```json
{
  "pageNo": 1,
  "pageSize": 20,
  "total": 2,
  "list": [
    { "articleId": 101, "name": "操作步骤", "updatedAt": "2026-11-12" },
    { "articleId": 102, "name": "项目说明", "updatedAt": "2026-11-12" }
  ]
}
```

### 字段说明

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `pageNo` | Integer | 当前页码 |
| `pageSize` | Integer | 每页条数 |
| `total` | Integer | 记录总数 |
| `list` | Array | 文章数组 |
| `list[].articleId` | Integer | 文章编号 |
| `list[].name` | String | 文章名称 |
| `list[].updatedAt` | String | 最近更新日期 |

### 状态码

| 状态码 | 说明 |
| --- | --- |
| `200` | 查询成功 |
| `400` | 参数不合法，如 `pageSize` 超过 100 |
| `404` | 路径不存在，检查是否漏了版本号 `/v1` |

写这类文档时，参数表和响应示例里的字段名要保持一致，改了一边记得同步另一边。

[返回首页](index.md) · [项目说明](about.md) · [操作步骤](guide.md)

# 数据模型

## Diary
```ts
type Diary = {
  id: string
  title: string
  content: string
  createdAt: string
  updatedAt: string
}
```

## 本地存储键
- `little-diary:entries`

## 数据规则
- `id` 由前端生成，保证唯一即可。
- `title` 可选，但建议保留以便列表展示。
- `content` 是日记正文的主要内容。
- `createdAt` 和 `updatedAt` 用于排序和展示。

## 排序规则
- 默认按 `updatedAt` 倒序展示。
- 新建日记首次保存时同时写入 `createdAt` 和 `updatedAt`。

## 说明
这个数据模型只面向单设备、本地保存的 demo 场景，不包含同步和多人协作字段。

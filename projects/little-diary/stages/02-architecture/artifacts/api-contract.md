# API 合同

## 结论
无远程 API，仅前端内部数据接口约定。

## 内部接口
- `loadDiaries(): Diary[]`
- `saveDiary(diary: Diary): void`
- `deleteDiary(id: string): void`
- `getDiary(id: string): Diary | null`

## 存储约定
- 浏览器本地仅保存一个日记数组。
- 读写都通过存储适配模块完成。
- 页面层不直接操作底层键值。

## 不存在的内容
- 不存在 HTTP 接口。
- 不存在鉴权接口。
- 不存在同步接口。
- 不存在服务端错误码。

# 模块边界

## 边界划分
- `pages/`：页面容器和路由入口。
- `features/diary-list/`：列表展示、空状态和进入编辑。
- `features/diary-editor/`：新增、编辑、删除和保存动作。
- `domain/diary/`：日记实体、排序规则和字段校验。
- `services/storage/`：本地持久化读写。
- `utils/`：时间格式化、ID 生成等通用工具。

## 职责约束
- 页面层不直接操作 `localStorage`。
- 存储层不关心 UI 呈现。
- 领域层不依赖浏览器 API。
- 编辑模块只关心当前一条日记，不承担列表逻辑。

## 结果
这个项目的模块边界足够支撑一个轻量 H5 demo，同时不会引入服务端边界。

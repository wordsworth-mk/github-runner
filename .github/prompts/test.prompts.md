---
mode: "agent"
tools: ["githubRepo", "codebase"]
description: "生成新的React表单组件"
---

你的目标是基于 `#githubRepo contoso/react-templates` 中的模板生成一个新的 React 表单组件。

如果未提供表单名称和字段，请询问。

表单要求：

- 使用 `react-hook-form` 进行表单状态管理：
- 始终为表单数据定义 TypeScript 类型
- 优先使用 register 来处理不受控制的组件
- 使用 `defaultValues` 来避免不必要的重新渲染
- 使用 `yup` 进行验证：
- 在单独的文件中创建可复用的验证模式
- 使用 TypeScript 类型来确保类型安全
- 自定义用户体验友好的验证规则

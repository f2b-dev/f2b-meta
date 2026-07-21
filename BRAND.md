# 品牌与文案

## 命名

| 场景 | 使用 |
|------|------|
| 对外产品名 | **灵境云** |
| 英文 / 组织 | **F2B-Navo** / [f2b-dev](https://github.com/f2b-dev) |
| npm / 包（目标） | `@f2b/*` |
| 过渡 monorepo | 历史 `@nova/*` 仅迁移源；新代码与新仓用 `@f2b/*` |
| 控制台标题 | 灵境云 · 控制台 |
| 首发能力 | **AI 沙箱服务**（自研产品叙事） |

## 视觉

- 主色：**`#FF5C33`**
- 控制台顶栏：**`#001529`**
- 风格：云厂商控制台 — 细边框、克制渐变、清晰状态色；避免默认「模板紫」同质化

## 对外宣传（用户可见）

- 定位：灵境云提供 **AI Agent 的安全执行云** / **自研 AI 沙箱服务**  
- 强调：独立内核隔离、秒级弹性、用完即焚、控制台 + SDK、网络策略  
- **禁止**在官网、控制台、metadata、页脚等用户可见处写：  
  - 「基于腾讯 / CubeSandbox / 开源内核」等数据面实现品牌  
- 可对标常见沙箱 SDK 习惯；不贬低友商；不必每次点名  

## 工程文档（内部 / 开发者）

- README 架构段、adapter、env（如数据面 URL / token **仅服务端**）可写实现细节  
- 用户看到的是「灵境云沙箱」；仓库里才是 adapter 与 Fake/生产切换  

## UI 栈（f2b-web）

- **Tailwind CSS v4 + shadcn 风格（Radix + CVA）+ lucide-react**  
- **禁止** Ant Design / `@ant-design/*`  
- CI 硬约束：`f2b-web/scripts/ci-guards.sh`

## 包名迁移摘要

详见文档站 [版本与发版](https://github.com/f2b-dev/f2b-docs)（`architecture/versioning`）与设计 §4.3：至 **1.0** 前新功能只进 `f2b-*`；1.0 起 registry 仅 `@f2b/*`。

# 贡献指南

感谢关注灵境云 / F2B。本页约定如何向 [f2b-dev](https://github.com/f2b-dev) 下的开源仓贡献。

## 开始之前

1. 阅读 [REPOS.md](./REPOS.md) 确认改动应落在哪个仓。  
2. 跨产品字段 / 错误码 → 先改 **[f2b-spec](https://github.com/f2b-dev/f2b-spec)**，再改实现与 SDK。  
3. 安全问题 → 走 [SECURITY.md](./SECURITY.md)，**不要**开公开 Issue 贴利用细节。

## 开发环境

- Node.js **≥ 22**，包管理 **pnpm 9**（`packageManager` 字段为准）  
- 本地多仓建议同级克隆：

```text
workspace/
  f2b-spec/
  f2b-sandbox/
  f2b-web/
  f2b-sdk-js/
  …
  f2b-infra/     # compose 联调
```

- 依赖契约：`"@f2b/spec": "file:../f2b-spec"`（**1.0 前不做 npm 正式发布**）  
- 一键联调：见 [f2b-infra](https://github.com/f2b-dev/f2b-infra)（`docker compose up` 或 `scripts/dev-host.sh`）

## 提交 PR

1. Fork 目标仓，从最新 `main` 开分支。  
2. 保持改动聚焦；跨仓破坏性变更在 PR 描述列出影响仓与迁移方式。  
3. 本地至少：  
   - `pnpm typecheck`（或仓内等价命令）  
   - 有契约 / smoke 的仓跑 `pnpm smoke` / `pnpm ci:contract`  
   - **f2b-web**：`bash scripts/ci-guards.sh`（无 antd、无管理密钥进 client、无禁用宣传文案）  
4. Commit message **中文**为宜，说明**为什么**。  
5. PR 描述：动机、行为变化、测试证据（命令输出摘要即可）。

### 破坏性契约

见 [f2b-spec README](https://github.com/f2b-dev/f2b-spec#版本约定semver)：先加后删、发布列车 `spec → 服务 → SDK → web → docs`。

### 版本与 1.0

- 组织级清单与 CHANGELOG 约定：[RELEASE.md](./RELEASE.md)  
- 文档站：[版本与发版](https://github.com/f2b-dev/f2b-docs/blob/main/docs/architecture/versioning.md)  
- **1.0 前禁止** npm / PyPI 正式发布

## 代码与文案

| 项 | 约定 |
|----|------|
| 用户可见文案 | 中文产品名 **灵境云**；工程名 F2B-Navo / `f2b-*` |
| 标识符 | 英文 |
| 注释 / 文档 Markdown | 中文 |
| UI | Tailwind v4 + shadcn 风格 + lucide；**禁止 antd** |
| 密钥 | 浏览器与客户端示例**永不**含数据面管理 token（如 `CUBE_API_TOKEN` / admin） |

详见 [BRAND.md](./BRAND.md)。

## Issue

- Bug：复现步骤、期望/实际、版本或 commit、是否 Fake 后端。  
- 功能：问题场景优先于实现方案；大功能先讨论再开大 PR。  
- 安全：私密渠道，见 SECURITY。

## 许可

贡献默认以各仓 **Apache-2.0** 授权。提交即表示你有权按该许可贡献。

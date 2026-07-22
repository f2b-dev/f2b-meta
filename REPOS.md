# 仓库地图

组织：[github.com/f2b-dev](https://github.com/f2b-dev)

## 首批仓库

| 仓库 | 职责 |
|------|------|
| [f2b-spec](https://github.com/f2b-dev/f2b-spec) | 跨产品契约：OpenAPI、错误码、TS 类型 |
| [f2b-sandbox](https://github.com/f2b-dev/f2b-sandbox) | 沙箱微服务：生命周期 / 命令 / 文件 / API Key / Fake·生产 adapter |
| [f2b-web](https://github.com/f2b-dev/f2b-web) | 官网 + 控制台壳 + BFF + 产品插件 |
| [f2b-sdk-js](https://github.com/f2b-dev/f2b-sdk-js) | 官方 TypeScript / JavaScript SDK |
| [f2b-sdk-python](https://github.com/f2b-dev/f2b-sdk-python) | 官方 Python SDK |
| [f2b-mcp-gateway](https://github.com/f2b-dev/f2b-mcp-gateway) | MCP 网关（工具映射沙箱） |
| [f2b-tunnel](https://github.com/f2b-dev/f2b-tunnel) | 隧道 / 预览 URL 反代 |
| [f2b-infra](https://github.com/f2b-dev/f2b-infra) | 本地 compose / 部署编排（无业务逻辑） |
| [f2b-docs](https://github.com/f2b-dev/f2b-docs) | 开发者文档站（VitePress） |
| **f2b-meta**（本仓） | 贡献、安全、品牌、地图、[1.0 发版清单](./RELEASE.md) |

## 运行时关系

```text
浏览器 → f2b-web（BFF）→ f2b-sandbox → Fake | microVM 集群
SDK / MCP → f2b-sandbox 公网 API（或经网关）
契约 ← f2b-spec
编排 ← f2b-infra
```

## 边界原则（摘要）

1. 一产品一服务仓；跨切面进 **spec**。  
2. 网页单仓多**插件**，不每个产品单独前端仓。  
3. BFF 在 web；数据面管理密钥仅服务端。  
4. SDK 只依赖公开 HTTP + spec。  
5. infra 不写业务逻辑。  
6. 开源默认；密钥与客户数据永不入库。

## 后置（未建或占位）

| 名 | 说明 |
|----|------|
| f2b-platform | 租户 / 账单独立服务 |
| 更多语言 SDK | 按需 |
| Phase C 真集群 | 生产 microVM 字段校准（在 sandbox adapter） |

完整设计（迁移源）：各贡献者本地 Nova 仓 `docs/superpowers/specs/2026-07-20-f2b-org-multi-repo-design.md`（§1–§4 已定稿）；公开摘要见 [f2b-docs 架构](https://github.com/f2b-dev/f2b-docs)。

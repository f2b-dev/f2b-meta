# 1.0 发版清单与版本约定

> 组织级约定。契约细节以 [f2b-spec README](https://github.com/f2b-dev/f2b-spec) 与文档站 [版本与发版](https://github.com/f2b-dev/f2b-docs/blob/main/docs/architecture/versioning.md) 为准。  
> **当前：预 1.0** — **禁止** npm / PyPI 正式 registry 发布。

## 1. Semver（全仓）

| 产物 | 版本源 | 说明 |
|------|--------|------|
| `@f2b/spec` | `f2b-spec/package.json` | 契约真相；破坏性见 PR `breaking` |
| `@f2b/sdk` | `f2b-sdk-js/package.json` | 对齐 OpenAPI 子集 |
| `f2b`（PyPI 名预留） | `f2b-sdk-python` 包元数据 | 1.0 后才发 |
| `f2b-sandbox` / `f2b-tunnel` / `f2b-mcp-gateway` | 各仓 `package.json` | 服务版本；镜像另见 tag |
| `f2b-web` | 根/workspace 版本或 git | 控制台随 git 部署即可 |
| OpenAPI 文件 | `*-v1.yaml` | major 暗示；与包 semver 同步说明 |

变更类型（patch / minor / major）与 **先加后删**、**发布列车** 见 f2b-spec README「版本约定」。

## 2. CHANGELOG

- 产品仓维护根目录 **`CHANGELOG.md`**（Keep a Changelog 风格，中文条目可接受）。
- 至少维护：`f2b-spec`、`f2b-sandbox`、`f2b-sdk-js`、`f2b-sdk-python`、`f2b-web`（web 可记用户可见能力）。
- 预 1.0 可用单节 `## [Unreleased]`；发 1.0 时切出版本头 `## [1.0.0] - YYYY-MM-DD`。
- 破坏性变更必须在条目中写 **迁移方式**。

## 3. 1.0 门槛（全部勾选后再 registry 发布）

> **预 1.0 Fake 闸门（2026-07-22）**：上表中 Fake 产品路径、契约 CI、文档端口、控制台诚实、安全演练、镜像**策略文档**已勾选。  
> **仍阻塞 1.0 registry**：真 microVM 单节点验收、各仓 `CHANGELOG` 的 `1.0.0` 节、npm/PyPI **实装 publish**、镜像 semver tag +（按需）SBOM/cosign 实装。


### 产品与契约

- [x] Fake 路径：create → 命令/SSE → 文件 → 模板 → 用量 → 密钥 → 隧道 可验收（`f2b-web` `e2e:bff` + GHA job `e2e-bff` 绿；香港 2026-07-22 `E2E_BFF_OK`）
- [ ] 真 microVM 单节点至少一台验收通过（healthz `backend` ≠ 未配置时的误报；见 f2b-infra `cube-single-node`）
- [x] 能力矩阵与 quickstart / cookbook 与端口/行为对齐（文档站；真 Cube 行待装栈后刷新）
- [x] OpenAPI Spectral + `check:errors` + sandbox `ci:contract`（含 mock `smoke:cube` / `smoke:cube-http`）
- [x] SDK JS / Python smoke 绿；MCP smoke 绿（各仓 GHA）
- [x] 控制台 backend 徽章诚实（healthz → badge）

### 发布与供应链

- [ ] 各仓 `CHANGELOG` 有 `1.0.0` 节
- [x] npm：`@f2b/spec`、`@f2b/sdk` 发布策略文档（见 §7；**正式 publish 仍 1.0 后**；scope 2FA/provenance 按 org 能力启用）
- [x] PyPI：`f2b` 发布策略与包名预留说明（见 §7；**正式 upload 仍 1.0 后**）
- [x] 镜像策略文档：`ghcr.io/f2b-dev/sandbox` 的 `latest`+`:<sha>`、main 推送、SBOM/签名后置（见 f2b-docs `architecture/versioning`）
- [ ] 镜像：1.0 时打 semver tag + cosign（按需）；**SBOM**：main 已挂 Syft 工件（非 semver tag）
- [x] 依赖审计：无已知 Critical 未处理（2026-07-22 `pnpm audit --prod --registry https://registry.npmjs.org`；web/mcp 用 overrides 清 high/moderate；镜像源 npmmirror 无 audit 端点）

### 安全与品牌

- [x] [SECURITY.md](./SECURITY.md) 渠道可达（2026-07-22 产品仓 Private vulnerability reporting `enabled`；邮件 `security@f2b.dev` 为备选）
- [x] 完成一次 **安全披露桌面演练**（`docs/security-drill-2026-07-22.md`）
- [x] 用户可见文案终检：无「腾讯 / CubeSandbox / 基于腾讯」；`f2b-web` `ci-guards` 绿
- [x] 浏览器路径无管理密钥 / `CUBE_API_TOKEN`（`ci-guards`）

### 文档与运维

- [x] f2b-docs 导航与端口（13200 / 13287 / 8790）正确（预 1.0）
- [x] all-in-one + 香港/试验床 runbook 可复现 `INSTALL_OK`（2026-07-22）
- [x] 贡献指南指向本文件与 versioning

## 4. 1.0 当日顺序（建议）

```text
1. 冻结 breaking PR；main 全绿
2. 打 git tag（各仓 v1.0.0 或 mono 说明）
3. 写 CHANGELOG 1.0.0
4. 发布 @f2b/spec → 等消费方可解析
5. 发布服务镜像 / 部署说明
6. 发布 @f2b/sdk 与 Python f2b
7. 更新 f2b-docs 与 f2b-meta REPOS
8. 发组织公告（能力边界 + Fake vs 真数据面）
```

**1.0 前**默认依赖：

```json
"@f2b/spec": "file:../f2b-spec",
"@f2b/sdk": "file:../f2b-sdk-js"
```

## 5. 安全披露桌面演练（不发真实漏洞）

目标：确认流程可走通，**不**利用生产、**不**公开细节。

| 步骤 | 动作 | 通过标准 |
|------|------|----------|
| 1 | 指定一名「报告人」与一名「接收人」（可同一人分角色） | 角色明确 |
| 2 | 报告人按 SECURITY 模板起草**虚构**场景（如「API Key 出现在错误 JSON」） | 含仓名、commit、复现、影响 |
| 3 | 走 Private vulnerability reporting **或** 邮件标题 `[SECURITY]`（勿发真实客户数据） | 渠道有回执或本地存档 |
| 4 | 接收人在 3 个工作日目标内写「已收到 + 初判」回复草稿 | 有时间戳记录 |
| 5 | 对照安全设计要点（控制面≠数据面、hash、日志）列检查项 | 勾选表归档到内部笔记（勿提交密钥） |
| 6 | 若需修复：走正常 PR；演练可在无代码改动时结束 | 记录「演练完成日期」 |

演练记录建议只写：日期、参与人、渠道、结论（流程 OK / 需改 SECURITY 文案）。**不要**把虚构 PoC 写进公开 Issue。

## 6. 相关

- [CONTRIBUTING.md](./CONTRIBUTING.md)
- [SECURITY.md](./SECURITY.md)
- [REPOS.md](./REPOS.md)
- [BRAND.md](./BRAND.md)

## 7. Registry 发布策略（预写，1.0 后执行）

> **硬闸门**：未勾完 §3 且未开 1.0 发版日序前，**禁止** `npm publish` / `twine upload` 到正式 registry。

### npm（`@f2b/*`）

| 项 | 约定 |
|----|------|
| 包 | 先 `@f2b/spec`，消费方解析后再 `@f2b/sdk` |
| 权限 | org `f2b-dev` scope；发布账号开 2FA；优先 Trusted Publishing / provenance（按 npm org 能力） |
| 版本 | 与各仓 `package.json` + `CHANGELOG` `1.0.0` 节一致 |
| 校验 | 各仓 `pnpm pack:check` / `scripts/pack-check.sh`（**禁止** publish）；审 `files`、无密钥、无 `data/` |
| 1.0 前 | 仅 `file:../f2b-spec` / `file:../f2b-sdk-js` 或 git 依赖 |

### PyPI（`f2b`）

| 项 | 约定 |
|----|------|
| 项目名 | 预留 **`f2b`**（与 SDK 目录 `f2b-sdk-python` 对应） |
| 构建 | `python -m build`；`scripts/pack-check.sh` 审 sdist；元数据与 README 品牌「灵境云」 |
| 上传 | 1.0 后 Trusted Publisher（GitHub → PyPI）或 API token；禁止把 token 写入仓 |
| 1.0 前 | `pip install -e ../f2b-sdk-python` |

### 镜像 semver（与策略文档对齐）

| 项 | 约定 |
|----|------|
| 现网 | `ghcr.io/f2b-dev/sandbox:latest` + `:<sha>`（`main` 推送；GHA `image` job） |
| 1.0 日 | 追加 tag `1.0.0` / `1`；可选 SBOM attestation、cosign keyless |
| 禁止 | 在未装真 Cube 时用镜像文案暗示「已含 microVM 内核」 |


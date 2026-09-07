---
tags: [SOP]
sop_id: SOP-09
up: "[[现行开发流程SOP-2026-09-07]]"
---

# SOP-09：分层合并

> ← 返回总览：[[现行开发流程SOP-2026-09-07]]

## 分支模板

```
prototype/p0/s{stage}/{scope}    （第一期阶段交互原型分支模板）
task/s{stage}/{group}/{module}/{role}    （任务分支模板）
feat/s{stage}/{group}/{module}    （功能分支模板）
group/s{stage}/{group}    （分组分支模板）
stage/s{stage}    （阶段分支模板）
integration/p0    （第一期集成分支）
release/p0    （第一期发布分支）
main    （主分支）
```

辅助分支：

```
fix/p0/{module}/{issue}    （一期模块问题修复分支模板）
int/{stage}/{scope}    （阶段跨组联调分支模板）
```

Worktree（工作树） 模板：

```
D:\工作\项目-worktrees\{stage}-{group}-{module}-{role}    （模块工作树路径模板）
```

## 合并规则

唯一业务合并流向：

```
task → feat → group → stage    （任务分支依次合入功能分支、分组分支和阶段分支）
```

要求：

- 业务功能任务在用户真实功能验收通过后才进入分层合并；[[SOP-10 阶段完成统一验证]] 的测试夹具专项按其明确授权与直接验证结果累计。
- prototype（交互原型） ancestry（祖先链） 永不进入 formal（正式开发） ancestry（祖先链）。
- formal（正式开发） task（任务分支） 只正向累计，不把 Stage（阶段） 反向注入旧 task（任务分支）。
- Group（分组）、Stage（阶段） 等共享分支禁止 rebase/force-push（变基/强制推送）。
- 禁止自审 Stage（阶段）、直接向 `main`（主分支） 开发或 push（推送）。
- `stage → integration/p0 → release/p0 → main`（阶段分支依次进入第一期集成分支、第一期发布分支和主分支） 每一步都要用户明确批准。
- 自 S5（第五阶段）起，模块真实验收通过且分层合入阶段后，才释放公共验收窗口；不因合并单个模块停止共享环境。

## 技术续作

跨阶段 technical-task（技术续作任务） 只沿其 exact（精确登记） registration（注册记录） 指定的 task（任务分支）→feat（功能分支）→group（分组）→stage（阶段） 正向链合并。registration（注册记录） 只是执行身份，不自动关闭依赖、不授权共享资源、不替代 UI（用户界面）/真实功能验收，也不得新增 BM/TI（业务模块/技术项） 或业务功能。

用户已明确批准的零生产改动、单测试文件夹具专项，可以按 [[SOP-10 阶段完成统一验证]] 免除不相关的界面原型及重复真实业务验收；这种例外不扩展到生产实现、接口、迁移或新交互修改。

## 相关步骤

- [[SOP-02 任务调度与唯一Owner]]（工作树/分支模板落地）
- [[SOP-08 真实功能人工验收]]（验收通过才合并）
- [[SOP-10 阶段完成统一验证]]（夹具专项累计）

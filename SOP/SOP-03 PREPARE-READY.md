---
tags: [SOP]
sop_id: SOP-03
up: "[[现行开发流程SOP-2026-09-07]]"
---

# SOP-03：PREPARE（只读预读准备） / READY（准备就绪）

> ← 返回总览：[[现行开发流程SOP-2026-09-07]]

PREPARE（只读预读准备） 只能进行只读核对。

## 工作现场

核对：

- 当前 Stage（阶段）、Group（分组）、BM/TI（业务模块/技术项） 和角色；
- 工作树、分支、HEAD（当前提交头）、tree（版本控制目录树）、clean（干净无未提交变更） 状态；
- formal（正式开发） 基线是否为调度时最新 clean（干净无未提交变更） `stage/sN`（阶段编号占位符对应的阶段分支模板） fixed point（固定基点）；
- 是否存在同模块第二 owner（负责人）；
- business-link plan（业务联动规划） 的波次、依赖、唯一 writer（写入者） 和共享资源窗口；
- manifest（清单）、控制文件和当前任务的允许范围。

正式 task（任务分支） 必须从调度时最新 clean（干净无未提交变更） Stage（阶段） fixed point（固定基点） 创建。禁止把 Stage（阶段） 反向 merge（合并）/rebase/cherry-pick（合并/变基/摘取提交） 到旧 task（任务分支）；旧 task（任务分支） 也不能作为新 formal（正式开发） 基线。

## 文档预读

普通 BM（业务模块） task（任务分支） 按 manifest（清单） 路由至少读取：

- 快照 manifest（清单）；
- source（来源） retrieval（检索路由） manifest（清单）；
- control（控制配置） 中的公共文档；
- 快照计划；
- 当前业务域业务索引和技术索引；
- 当前 BM（业务模块） 业务文档；
- 当前 TI（技术项） 技术切片；
- business-link plan（业务联动规划） 已声明的直接上下游和边界文件。

当前普通任务幂等键：

```
stage/group/module/role/manifestHash    （阶段、分组、模块、角色和清单哈希组成的幂等键）
```

跨阶段技术续作必须存在 `p0-control.yml`（项目唯一控制文件） 中 exact（精确登记） technical-task（技术续作任务） registration（注册记录），并严格匹配 taskId（任务标识）、registration（注册记录） id（标识）、执行 Stage（阶段）、Group（分组）、角色和分支；不得借注册身份扩大业务范围。

## PREPARE（只读预读准备） 结果

- `READY`（准备就绪）：事实、范围、依赖、分支、owner（负责人） 和共享资源均满足，可进入下一步。
- `BLOCKED`（已阻塞状态）：精确写明最小阻塞、受影响模块/能力、责任方和解阻条件。

`BLOCKED`（已阻塞状态） 只暂停受影响模块或能力，不默认停止无依赖模块。BLOCKED（已阻塞） 状态下禁止写业务代码、创建迁移、占用 formal（正式开发） 共享资源或伪造测试/验收结论。

## 相关步骤

- [[SOP-01 阶段业务联动规划]]（依赖与共享资源预读来源）
- [[SOP-02 任务调度与唯一Owner]]（owner 与槽位核对）
- [[SOP-05 正式开发]]（PREPARE 的下一跳）

---
name: unity-ecs-specialist
description: Use when working on Unity data-oriented architecture — ECS/DOTS, job system, Burst, memory layout, batching, or when migrating OOP-heavy systems to data-driven design. Triggered by Unity, ECS, DOTS, Burst, JobSystem, 数据导向, 性能架构. For OffByOne Studio when Unity projects require large-scale entity simulation.
---

# Unity ECS 专精（数据导向架构）

## 适用
Unity 项目需要处理大量实体（弹幕、RTS 单位、大世界物件）或追求极致性能时；常规小项目不建议 DOTS。

## 核心概念
1. **ECS 三段**：Entity（ID 句柄）+ Component（纯数据，无方法）+ System（逻辑）。数据与行为分离，天然缓存友好。
2. **内存布局**：Component 按 type 连续存储（Archetype chunk），避免 OOP 对象散落堆内存；遍历时命中缓存。
3. **Job System + Burst**：System 逻辑放 IJob 并行化（多线程），Burst 编译器生成 SIMD 优化原生代码。
4. **批处理**：同材质同网格实例化（GPU Instancing/SRP Batcher）；ECS 与渲染数据解耦后批量更新。

## 迁移策略
- 局部试点：把"大量单位 AI / 弹幕更新"这类瓶颈系统迁到 ECS，其余保持 MonoBehaviour；禁止一次性全量重构。
- OOP 对照：先写 MonoBehaviour 版本过逻辑，再按 Entity prefab（Baker + Authoring）落地。

## 常见坑
- Entity 引用不可跨 frame 缓存（结构变更后句柄失效），用 EntityQuery 重新获取。
- Component 只放数据，别放引用（用 Entity ref 或 SystemHandle）。
- Burst 对字符串/委托限制多，热路径避免托管对象。

## 检查清单
- [ ] 迁移前有性能基线（Profiler 帧耗时/GC 分配）
- [ ] 每个 System 有明确 Update 顺序与依赖（SystemGroup）
- [ ] 无跨 frame 缓存 Entity 句柄
- [ ] Burst 编译日志无 AOT 告警
- [ ] 迁移后 GC.Alloc 归零（热路径）

## 交接
- 产出：迁移前后基线对比 + 迁移系统清单 + 未迁移项的后续建议。

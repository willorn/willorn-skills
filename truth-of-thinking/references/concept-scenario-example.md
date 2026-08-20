# Example:「什么是 HashMap？」

This is a worked example of the compact full loop. Adapt the depth to the user's level; do not paste it mechanically.

## 1. Definition + boundary + scope

```text
Concept: HashMap
Scope: Java / common hash-table map, unless the user specifies another language
Definition: 用 key 的哈希值定位桶，在平均近 O(1) 时间做 KV 存取的数据结构；正确性依赖 hashCode 与 equals 的一致性
Boundary / not:
- 不是保证排序的 Map（那更接近 TreeMap / 有序结构）
- 不是线程安全的并发 Map（那更接近 ConcurrentHashMap）
- 不是 List；也不是只关心“有没有”的纯 Set 语义
```

## 2. Classification

Useful cut for understanding — **by job**:

```text
标准：这个 Map 主要承接什么任务？
- 计数 / 聚合
- 去重 / 索引
- 缓存 / 查找表
```

Another valid cut — **by constraint**:

```text
标准：调用方还要求什么？
- 要不要保插入序
- 要不要按 key 排序
- 要不要并发安全
```

State the standard. Do not mix “用途” and “并发” in one flat list without saying so.

## 3. Comparison

Same category: Map / 键值查找结构.

| Criterion | HashMap | TreeMap | LinkedHashMap | ConcurrentHashMap |
|---|---|---|---|---|
| 平均查找 | 很快 | 较慢（树） | 很快 | 很快 |
| 顺序 | 不保证 | 按 key 排序 | 可保插入/访问序 | 不保证 |
| 并发写 | 不安全 | 不安全 | 不安全 | 面向并发 |
| null | 允许（Java HashMap） | key 通常不行 | 允许 | key/value 通常受限 |

Comparison result depends on the criterion that matters in the scene, not on a vague “哪个更好”.

## 4. Causality

Why is it fast?

```text
分散良好的哈希 → 桶内元素少 → 平均接近 O(1)
```

When does it degrade?

```text
候选原因：
- hashCode / equals 写错 → 大量碰撞或查不到
- 数据倾斜 / 坏哈希 → 链或树退化
- 频繁扩容 / rehash → 偶发卡顿
- 多线程误用普通 HashMap → 数据损坏或死循环类问题
```

Run the four-question test on the claimed cause. “HashMap 慢” is a phenomenon, not a root cause.

## 5. Scenarios

该用：

```text
单线程词频统计、ID → 对象索引、请求内临时查找表
理由：核心需求是按 key 快查；不要求排序或跨线程共享写
```

不该用：

```text
多个线程同时读写同一共享 Map 做缓存
理由：边界已经排除线程安全；应比较并切换到 ConcurrentHashMap 或外层同步策略
```

Another avoid scene:

```text
需要按 key 范围查询 / 有序遍历
理由：比较标准变成“顺序”；TreeMap 或显式排序更合适
```

## 6. Three-table update

```text
概念表 Create/Update:
- HashMap = 平均近 O(1) 的哈希 KV 表；非有序、非并发安全

关系表 Create/Update:
- HashMap vs TreeMap：速度 vs 排序
- HashMap vs ConcurrentHashMap：单线程简洁 vs 并发安全

流程表 Create:
- 选型：先问是否并发、是否要序、是否只要快查
- 排查变慢：先查 equals/hashCode、碰撞、扩容、误用并发
```

If an answer only says “HashMap 是一种哈希表”, none of these rows are really written — that is the failure mode this skill should avoid.

# 匹配算法设计（matching-algorithm）

> 把"答题 → 推荐狗狗"串起来的逻辑。核心原则：**可解释**，每个结果都能用人话说清为什么。
> 状态：v1，随真机体验校准权重。

## 三步

### Step 1 · 门槛过滤（硬约束做减法）
读 type=hard 的题答案，排除明显不合适的狗：
- `max_size`（住房）：排除体型超过上限的狗（small < medium < large）
- `require_good_with_kids`：只留 `good_with_kids: true`
- `require_hypoallergenic`：只留 `hypoallergenic: true`

> ⚠️ v1.1 调整：**吵闹（noise）原为硬过滤，已改为软性重扣分**（见 Step 2）。
> 原因：原型实测发现「合租必须安静」一刀切后，小型犬池子常被砍到只剩 2 只，被迫推出自相矛盾的狗。改成重扣分后，安静的狗仍优先，但不会空池。

> 过滤后若候选池为空，放宽最不致命的一条（体型可放宽一级），保证有结果。

### Step 2 · 负担打分（核心，不对称惩罚）
关键洞察：**痛苦几乎都来自「狗要求的 > 你能给的」**；反过来你富余、狗佛系，基本不痛苦。所以两个方向罚得不一样重。

每个维度算 `gap = 需求 - 供给`：

| 维度 | 需求(demand) | 供给(supply) | 权重 |
|---|---|---|---|
| exercise 运动 | 狗.exercise | 用户活力(q_morning) | 1.5 |
| noise 吵闹 | 狗.noise | 用户容忍(q_neighbor) | 1.4 |
| alone 独处 | 用户需独处时长(q_away) | 狗.alone_tolerance | 1.3 |
| grooming 打理 | 狗.grooming | 用户忍受度(q_mess) | 1.0 |
| train 训练 | 狗.train_difficulty | 用户经验(q_experience) | 1.0 |
| budget 预算 | 狗.budget | 用户预算(q_budget) | 1.0 |

```
gap = demand - supply
if gap > 0:  penalty += gap * 权重          // 狗超出用户，重罚
else:        penalty += |gap| * 权重 * 0.2  // 用户富余，轻罚
matchScore = round(100 * (1 - penalty / maxPenalty))   // maxPenalty = Σ 4*权重 = 28.8
```

注意：alone 维度方向是反的——用户那边是"需要狗独处多久"(需求)，狗那边是"能独处的能力"(供给)。其余维度都是狗=需求、用户=供给。

### Step 3 · 喜好排序（微调，打破平手）
读 type=pref（q_vibe）：狗的 `size`/`personality` 命中用户偏好，每命中一项 +3 分（封顶 +6）。只影响排序，不改变合不合适。

## 输出
- 按最终分排序，取 Top 3，置顶第一名为"最佳匹配"
- 每只生成「为什么是它」：
  - ✓ 命中点：gap ≤ 0 的维度里挑 2 条（"你想躺平，它也不爱动"）
  - ⚠️ 注意点：gap 最大的那条（"但它掉毛偏多，得接受"）+ 狗的 real_talk

## 养宠人格标签（传播钩子）
从用户 5 维画像生成一个 4 字称号 + 一句话。v1 用简单决策：
- 活力高(exercise≥4) + 户外 → "出门撒野型"
- 活力低(exercise≤2) + 高陪伴(availability高) → "居家暖被窝型"
- 怕脏(grooming≤2) → "精致洁癖型"
- 不差钱(budget≥4) → "富养宠妈/宠爸型"
- 没经验求省心(train≤2) → "新手保命型"
- 默认 → "随性养狗型"
（标签体系待扩展成更好玩的矩阵）

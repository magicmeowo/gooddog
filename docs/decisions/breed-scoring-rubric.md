# 品种打分标尺（breed-scoring-rubric）

> 所有品种必须用这同一把尺子打分，否则匹配算法会失真。
> 用户侧的题目答案也映射到这同一套 1–5 分刻度。
> 数据来源优先级：AKC (akc.org breed traits) > Dogtime > 中文养犬资料。AKC 本身就是 1–5 分制，可直接转。
> 状态：标尺 v1，分值待真实数据填充后再校准。

---

## 负担维度（traits，1–5）

### exercise · 运动量需求
狗每天需要多少运动，否则会憋坏/拆家。（≈ AKC Energy Level + Exercise Needs）
- 1 = 每天散步 20 分钟就满足（巴哥、马尔济斯）
- 2 = 30–45 分钟散步
- 3 = 每天约 1 小时活动（柯基、金毛偏中）
- 4 = 1.5–2 小时，需要跑/玩
- 5 = 工作犬级，2 小时+剧烈运动，否则拆家（边牧、哈士奇、阿拉斯加）

### grooming · 打理投入
综合「掉毛量 + 美容频率/花费 + 口水」。（≈ AKC Shedding + Coat Grooming Frequency + Drooling）
- 1 = 极省心，几乎不掉毛、不用打理
- 2 = 偶尔梳理
- 3 = 定期梳/洗，中等掉毛
- 4 = 掉毛多 或 需定期美容花钱（金毛、贵宾/比熊美容）
- 5 = 掉毛灾难 或 美容成本很高（萨摩耶、阿拉斯加、金毛换毛季）

### alone_tolerance · 独处耐受（越高越能独处）
独自在家时是否容易分离焦虑、拆家、吠叫。无 AKC 直接对应，用品种习性判断。
- 1 = 极黏人，独处易崩溃（很多小型伴侣犬、哈士奇）
- 3 = 一般，能忍几小时
- 5 = 独立，可较好独处（柴犬、部分梗类）

### train_difficulty · 训练/管理难度
新手能不能驾驭。综合「服从性 + 固执程度 + 是否需要经验」。
注意方向：**1 = 超好训新手友好，5 = 固执/难驾驭需经验**（与 AKC Trainability 方向相反，AKC 高=好训，转换时取反）。
- 1 = 超好训，新手无压力（金毛、拉布拉多、贵宾）
- 3 = 中等，需要一点耐心
- 5 = 固执/高能难管，需有经验的主人（哈士奇、阿拉斯加、柴犬、德牧偏专业）

### budget · 月开销
狗粮 + 日常 + 潜在医疗，主要随体型和易病程度放大。
- 1 = 小型省吃（月 ~300 内）
- 3 = 中型 或 需美容（月 ~500–800）
- 5 = 大型 + 易病 + 高美容（月 1500+）

---

## 门槛/标签（filters）

### size · 体型
`small`（< 10kg，柯基/泰迪/法斗）/ `medium`（10–25kg，边牧/柴犬）/ `large`（> 25kg，金毛/德牧/阿拉斯加）

### noise · 吠叫程度（1–5）（≈ AKC Barking Level）
- 1 = 很安静 ｜ 3 = 一般 ｜ 5 = 爱叫（雪纳瑞、博美、小型犬常见）

### hypoallergenic · 是否低敏/少毛
true = 适合过敏人群（贵宾、比熊、马尔济斯、雪纳瑞、约克夏、蝴蝶犬等少毛品种）

### good_with_kids · 对小孩友好
true / false（≈ AKC Good With Young Children）

### novice_friendly · 新手友好
true / false（综合 train_difficulty、运动量、固执度判断；难驾驭的为 false）

---

## 文案字段
- `personality`：2–4 个性格关键词（用于喜好题匹配 + 文案）
- `one_liner`：一句话有趣画像（卖点）
- `real_talk`：一句话现实提醒（缺点 / 要接受什么）

---

## MVP 品种清单（25，偏中国常见）

1. 泰迪 / 贵宾 Poodle (Toy/Miniature)
2. 比熊 Bichon Frise
3. 博美 Pomeranian
4. 柯基 Pembroke Welsh Corgi
5. 金毛 Golden Retriever
6. 拉布拉多 Labrador Retriever
7. 哈士奇 Siberian Husky
8. 萨摩耶 Samoyed
9. 阿拉斯加 Alaskan Malamute
10. 柴犬 Shiba Inu
11. 法斗 French Bulldog
12. 巴哥 Pug
13. 雪纳瑞 Miniature Schnauzer
14. 边牧 Border Collie
15. 德牧 German Shepherd
16. 中华田园犬 Chinese Rural Dog（无 AKC，用中文资料 + 常识）
17. 腊肠 Dachshund
18. 吉娃娃 Chihuahua
19. 约克夏 Yorkshire Terrier
20. 马尔济斯 Maltese
21. 比格 Beagle
22. 可卡 Cocker Spaniel
23. 蝴蝶犬 Papillon
24. 杜宾 Doberman Pinscher
25. 大白熊 Great Pyrenees

## 常识推理

### 综述

1. Commonsense Reasoning for Natural Language Understanding: A Survey of Benchmarks, Resources, and Approaches



### 任务与数据集

#### Coreference Resolution

共指消解，即确定文中一个特定的代词（pronoun）指代的是哪个实体/事件。

##### Winograd Schema Challenge (WSC)

给一句话与一个问句What was xxx (adj.)? 判断两个答案中哪个是对的。 http://commonsensereasoning.org/winograd.html.  

#### QA

1. MCScript
   强调需要常识，包含了14000条基于短文的 2-way 的多选题，其中一些甚至可以只使用常识来回答
2. CoQA
3. OpenBookQA
4. AI2 Reasoning Challenge (ARC)
   一个14m句子的科学相关语料作为常识集合，还有8000个四选一选择题，用常识集合来解题。
5. SQuAD
6. CommonsenseQA
   9500个三选一，每个问题都需要从ConceptNet的三个concept中选一个出来

#### Textual Entailment

文本蕴含，考察两句话或若干句话之间的互相蕴含关系

1. RTE Challenges (1\~5)
   给定一句话作为文本，一句话作为命题，判断从文本中是否能推导命题成立
2. SICK
   有约10000对句子，包含两个任务，一个是句间关系，一个是文本蕴含（三选一，蕴含/中立/反对，类似RTE4、5）
3. SNLI
   有约60w对句子，不仅有文本蕴含三选一，还有众包衡量的分数五选一
4. MultiNLI
   SNLI的加强版，包含了更多类型/流派的句子对，比如电话通话记录
5. SciTail
   27000对句子，蕴含二选一（类似RTE1），主要基于科学知识，所以比普遍意义的尝试更高难一点

#### Plausible Inference

不确定推理，与文本蕴含要求得出具体结论不同，这个任务要求得出中间结论/假定推理/不确定的推论，比如推测一个人**可能**接下来做什么事情

1. COPA
   包含约1000个实例，同时包含了前向和后项推理，这说明题面既可能是原因也可能是结果
2. CBT
   包含约687000个完形填空题，需要从10个候选词中选择一个来填空
3. ROCStories
   大约50000个故事，需要从故事的若干个假结局中选择更有可能的结局
4. JOCI
   给定一段上下文和一个猜想，判断上下文产生猜想的可能性（打分1-5）
5. CLOTH
   10w道高考完型四选一，每个题目会高数你是语法题/短程推理/变形/长程推理中的哪一个
6. SWAG
   和ROCStories类似，有11.3w个故事短开头，四个可能的结尾选一个
7. ReCoRD

#### Psychological Reasoning

对情绪与人为意愿进行推理

1. Triangle-COPA
   基于社会心理学实验，包含100个样例，形式类似COPA但是集中在心理领域
2. Story Commonsense
3. Event2Mind
   包含25000个事件中的57000个情绪/反应标记，任务要求预测事件主要参与者的情绪和反应，以及其他人的反应

#### Multiple Tasks

1. bAbI
2. Inference is Everything (IIE)
3. GLUE
4. DNC



### 常识来源

1. Cyc
   其中包含了实体、集合、函数、真值函数，使用CycL语言写成
2. ConceptNet
   以字符串名字作为实体，构建实体间的关系，包含了8m个节点之间的21m个关系
3. AnalogySpace
   基于OMCS的产物，将concepts映射到goodness、difficulty等特征维度上
4. SenticNet
   专门用来情感分析
5. IsaCore
   结合了ProBase和ConceptNet3，里面由is a关系组成
6. COGBASE
   包含了关于2.7m个实体内含的10m条常识事实
7. WebChild
   包含了78000个名词含义，5600个不同的形容词含义，以及它们之间的修饰关系
8. LocateNear
   包含了各种物品之间是否应该倾向于位置接近的关系（约5000条）
9. ATOMIC
   大约30w个节点，每个节点是一个关于某个日常事件的desc，包含了他们之间的if-then关系


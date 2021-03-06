## 常识推理

### 综述

1. Commonsense Reasoning for Natural Language Understanding: A Survey of Benchmarks, Resources, and Approaches



### 任务与数据集

#### Coreference Resolution

共指消解，即确定文中一个特定的代词（pronoun）指代的是哪个实体/事件。

1. Winograd Schema Challenge (WSC)
   给一句话与一个问句What was xxx (adj.)? 判断两个答案中哪个是对的。 http://commonsensereasoning.org/winograd.html.  
2. PDP-60
   小版的WSC。

#### QA

1. MCScript
   强调需要常识，包含了14000条基于短文的 2-way 的多选题，其中一些甚至可以只使用常识来回答
2. CoQA
3. OpenBookQA
4. AI2 Reasoning Challenge (ARC)
   一个14m句子的科学相关语料作为常识集合，还有8000个四选一选择题，用常识集合来解题。
5. SQuAD
6. CommonsenseQA
   1.2W个五选一，每个问题都需要从ConceptNet的5个concept中选一个出来。构造方法：给一个问题concept，选和它有相同关系的三个邻居，构造三个问题分别以三个邻居为答案，每个问题再选择一个相同关系的distractor，人工写一个distractor，总共是5个。每个问题+答案通过搜索引擎搜100个snippet作为textual context，每个问题总共500个（最后发现没啥用）。

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
   和ROCStories类似，有11.3w个故事短开头，四个可能的结尾选一个。使用对抗式训练模型生成，即指定一系列已有的模型，选定一部分negative后循环，每次从选定集里排除几个最容易被分辨的，从未选定集里选出几个最有迷惑性的交换（使用多折训练集分割来训练多个模型），这样可以减少数据中的human annotation bias。
7. Hellaswag
   和SWAG类似，也使用对抗式训练模型，但是用更强的BERT作为discriminator，用GPT作为generator
8. ReCoRD
9. LSDSem 2017 Task
   和ROCStories类似，从两个结局里选一个

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
5. SemEval-2020 Task 4 （ComVE）
   分为三个任务：给定两句话，判断哪句是不合理的；从3个理由中选择前面那个不合理的理由；生成前面那个不合理的理由。

#### Commonsense Generation

1. CommonGen
   包含有3.5w的concept-sets，和相应的7.7w句子，是从图片标题和视频标题中抽取出来的，每个concept-set包含3-5个concept。

#### Abductive Natural Language Inference

$\alpha NLI$，考虑一个因果关系A+B->C，给出两个B1 B2，选择合理的一个

#### Couterfactual Invariance Prediction (CIP)

考虑一个因果关系A+B1->C，把B1换成B2看是否仍然成立



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
   大约30w个节点，每个节点是一个关于某个日常event的desc，包含了他们之间的if-then关系（如理由、结果、执行者性格之类的），event是指代词（PersonX）+动词谓词短语，出现足够频繁的参数（如personX eat spaghetti的spaghetti）也会出现
10. OMCS
      包含了许多描述常识的语句
11. Event2Mind
    类似ATOMIC，但是只有表示情感的dimension



### 方法

1. **KagNet**: Knowledge-Aware Graph Networks for Commonsense Reasoning 

   用图结构来解决CommonsenseQA问题。首先将问题和答案中的所有词（除stop word外）识别为ConceptNet中的concept（用soft matching with lemmatization），将question concept和answer concept之间所有少于k个节点的path找出来，使用KG嵌入方法（如TransE）为每个path的每个triple计算分数，一条path的分数为所有triple的积，丢弃分数小于一个threshold的path。在剩余的path组成的subgraph上先用GCN，然后对q concept和a concept之间两两path使用LSTM来编码path，其序列为triples，node用GCN输出，edge是trainable的，有多条路径则将结果attention。将path结果与semantic结果结合起来做$|C_q|*|C_a|$上的attention过MLP，得到最终分数。

2. Explain Yourself! Leveraging Language Models for Commonsense Reasoning
   为常识问答增加解释，有两种：先根据问题生成解释再得到答案（推理），根据问题得到答案再生成解释（合理化）。**CoS-E**是人工制造的解释数据集，而**CAGE**是提出的用LM生成解释的方法。在CQA、SWAG、ROCStories上进行了实验。

3. Contrastive Self-Supervised Learning for Commonsense Reasoning
   使用对抗式的成对样本来弱监督地学习常识。WSC的任务中会有一些trigger word（改变了就会影响答案），于是使用trigger word来构造成对的答案相反的问题，用概率逻辑代数将两者答案相同的逻辑表达式（用XOR和AND）转化成包含4个概率的loss函数。在指代消解任务上进行了实验。

4. Attention Is (not) All You Need for Commonsense Reasoning
   考虑共指消解问题中BERT的attention，有$H\times L\times |C|$个，分别是head、layer、cand。在每个位置只保留一个cand，最终得到$H\times L$的attention，当前cand在这些attn总和中占的比例即为其得分。

5. An Enhanced Knowledge Injection Model for Commonsense Generation
   **EKI-BART**，基于BART来进行常识文本的生成。每个问题给出原型$o_1...,o_{n_o}$，需要替换进去的concept $c_1...c_{n_c}$，生成目标$t_1...t_{n_t}$。模型将$c_i$与$o_i$串起来，分别加两个不同的group embedding。使用MLP为每个$o_i$ token计算一个$\lambda$来改变其对BART输出的影响（0-2，平均为1），并假定那些在target中出现的$o_i$ token更重要。为$o_i$中每个token根据其与最近concept的距离进行编码来加入BART计算。

6. Improving Commonsense Causal Reasoning by Adversarial Training and Data Augmentation
   通过生成某个词语的替换来进行对抗性增强训练。在大语料中抽取because，或是包含有*implicitly causal verbs*的句子来生成因果文本，不会包含两层或以上的因果。

7. I Know What You Asked: Graph Path Learning using AMR for Commonsense Reasoning  
   **ACP**，为QA的**题面**构建AMR Graph，每个节点既是词语也是concept，然后将ConceptNet中与其有相交的所有关系并入，（此处考虑只保留ARG0/ARG1的端点有关联的边），对扩展图上的任意两个点之间，只计算最短路上的GRU，经过一通计算后得到任意两点的score（可以用来观察重要推理路径），用来更新图的embedding（初始为glove和position），最后所有点的总和为graph embedding。再结合容纳了**cand**的LM-based language embedding。

8. Social Commonsense Reasoning with Multi-Head Knowledge Attention
   考虑$\alpha NLI$和CIP（新）任务，分别将$[CLS] O_1 H_i[SEP]O_2[SEP]$和$[CLS]s_1s_2s_3[SEP]s_1s_2's_3[SEP]$作为输入。**MHKA**首先将输入文本送过LM，用SRL和COMET2.0抽取外部知识（也是一句话），送到另外一个Encoding layers中，输出的作为K和V，将前面LM的输出作为Q，再放进另一个Transformer中，输出的结果来做线性判断。
   
9. **KG-BART**: Knowledge Graph-Augmented BART for Generative Commonsense Reasoning
   将KG注入BART来提高**常识语句生成**的性能。encoder：先将concept字面放入BART打散编码后，将编码结果用SCI模块池化重组成concept，和TransE拼接成node init，子图过一个multi-head的GAT，再用CSD模块打散成BART可以处理的结构。decoder：扩展一层子图，先在星状上gat，再在整个子图gat，encoder输出的结果分别与gat输出/encoder hidden state做attention，两个attn连一起，decoder输出文本。

10. Language Generation with Multi-Hop Reasoning on Commonsense Knowledge Graph
    **Generation** with Multi-Hop Reasoning Flow (**GRF**) ，通过graph上的多跳推理计算生成一个concept填补token的分布，并通过门控来选择是用text-gen还是concept。每次将context+已经和生成的token输入模型，由source concepts出发走H-hop的inter-connected path构建一个subgraph，过一个GNN，从source concept出发向周围如RL般计算score，增量R为graph嵌入与LM嵌入算分，所有score过softmax得到concept分布再过门控。
    
11. **ATOMIC**: An Atlas of Machine Commonsense for If-Then Reasoning
    提出了一个存储了event-dimension(if-then)-event的常识数据集atomic，不同的inference dimension是event之间的关系（如xIntent，oReact之类的）。任务是给一个event，预测它在9个dimension之后可能会连接哪些event。用GloVe+ELMo+bi-GRU编码input event str，用GRU解码。实验发现按照不同的hierarchy将相似的dimension（如Xintent和Xneed都算是求input event的执行者起因）的encoder参数共享可以提高效果。
    
12. **ECNU-SenseMaker** at SemEval-2020 Task 4: Leveraging Heterogeneous Knowledge Resources for Commonsense Validation and Explanation
    使用引入知识的GAT来解决ComVE，选择不合理的选项并选择/生成不合理的理由。对于一句输入，找到其中所有ConceptNet中对应的concept，每个再根据在ConceptNet中的边权重选择几个重要的邻居，按模板生成描述插入原语句，如Sugar-IsA-sweetfood则对应原句Sugar (is a sweet food)，在新语句上使用soft-position和attention mask。给每个concept根据权重抽样构造子图（彼此可以通过公共邻居相连），中心concept取平均，与LM output相连后过个MLP计算本句的propability。使用双loss共享机制自动控制两个loss之间的平衡。


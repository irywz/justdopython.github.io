---
layout: post
category: python
title: 这个数据分析报告，居然没写一行代码
tagline: by 太阳雪
tags:
  - python100
---
数据分析和机器学习是目前的热门，相关书籍教程汗牛充栋，大多数都在讲环境创建、数据处理、工具应用，以及各种理论和算法，虽然实践起来难度不大，但学习之后还是云里雾里，不知道怎么应用。今天我们从另外的角度上了解下数据分析的基本步骤，并结合一个分析案里，体验一次数据分析的过程，不用写代码噢。
<!--more-->

## 数据分析过程

数据分析是对数据和业务信息反复处理的过程，具有螺旋上升的特点，每个阶段，可以分解为如下几个过程：

- **确定**：确定问题，得到分析目标，以免走错方向
- **分解**：对问题进行分解，对收集到的数据进行分解，以便转换为可分析和对比的程度
- **评估**：对问题和数据进行对比分析，发现关联、规律，各种假设的验证
- **决策**：结合目标和评估结果得到结论，可以是对目标的认可、原因的证明也可以是接下来行动的指导
- **验证**：分析的结果并非十全十美，需要经过实际的验证，如果没有达到效果，需要结合新的证据重复这个过程

数据分析就是不断的这这几个过程阶段反复，由于有的验证过程麻烦，分析过程可能持续很久

分解和评估阶段，可以借助数据分析工具、编程来提高处理效率

在评估阶段，可以用图形化工具对数据进行展示，以便方便的看出数据关联和规律

下面我们结合一个实例，对各个过程阶段进行进一步了解

## 任务来了

我们接到一个任务，任务来自一个化妆品公司，最近他们遇到一些麻烦，想提高保湿霜产品的销量，但所有尝试都没效果，最近他们调整了广告策略，还不确定这个调的效果如何，期望我们能帮他：

- 确定调整策略是否有效
- 提高产品销量

收到任务，开干

### 第一步 确定问题、收集数据

别急，虽然有了任务，且给了目标，但是开始前，需要进一步确定问题，并为解决这问题收集必要的数据，否则可能会经历一场没有目的地的旅行。

首先要确定调整策略是否有效，那么我们需要一些调整前和调整后的销量数据，下面是得到的数据：

|  |1月|2月|3月|4月|5月|6月|
|--|---:|---:|---:|---:|---:|---:|
|总销量|528000|550100|546900|548000|553300|555400|
|目标|528000|550000|572900|596800|621700|647600|
|广告费|10560|95040|73920|52800|31680|31680|
|网推|0|10560|31680|52800|73920|73920|
|&nbsp;|  &nbsp;| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp;|
|单价|2|2|2|1.9|1.9|1.9|

另外需要进一步了解业务，以及用户对这件事情的认识，以便收集更多的信息，并且明确可量化指标，**可量化** 是个重要的概念，客户会说要提高销量，但是应该提高多少呢？还会说看看什么方式行不行，那么什么才叫行或不行呢？这些都是需要在确定问题的部分弄清楚的。 实际中，不可能将所有问题都明确化，需要采取循序渐进的策略，逐步靠近目标

> 请注意：数据并不是信息，数据经过业务角度的解读和整理才能得到信息，例如明天要下雨，是个数据或者消息，明天上班要带伞，才是信息，但如果明天需要雨中漫步，得到的信息可能是明天尽早出门

通过对业务方的调研，得到了如下信息：

- 期望销量回到目标值，可以从数据中看到，从2月份开始，销量与目标分道扬镳了
- 客户认为，目标用户是少女消费者，想要提高销量就需要让更多目标用户购买，并且目标用户有足够的钱可以购买产品，可以进一步向她们推销产品
- 市场中存在一些竞争对手，他们会极力打压我们，而且他们的销售额是我们的 0.5 到 1 倍
- 之所以进行网络推广，是做一种新的尝试，因为过去一直用常规广告，现在销量下降，必须采取新的策略，否则后果严重

> 应该怎么做问题调研呢？有几点建议：
>
> - 确认目标，例如想要销售量提高多少
> - 不停的问 是多少，使目标逐步的可量化
> - 反向提问，比如问问竞争对手的情况，市场份额的情况
> - 对数据的疑惑，从原始数据中发现的一些不能理解或者感到器官的地方，做调查

### 第二步 整理和分解数据

收集了数据，并且明确了目标（主要是可量化）之后，就可以对数据进行分析整理了，如有必要还需要对问题进行拆分，比如要提高销售额这样**含糊不清**的问题，应该拆分成哪些小的步骤，让这些问题**可管理**、**可解决**，下面是分解后的：

- 客户希望我们给他们什么？
- 哪种促销方式最有可能有效？
- 客户的广告做的怎么样？

接下来，我们需要将数据和客户的目标相结合，从中得到一些推论和表述

因为客户所说的可能并非事实，另外单从数据可能无法还原业务过程

现在通过客户表述，以及从数据上得到的结果，可以得得到一些推论

>你得到的推论可能与我的不同，这很正常，因为不同的人看待世界的方式不同，即认知模型不同，后面文章中我们会进一步讨论认知模型的问题

**从客户的观点中可以得到**：

- 产品的目标消费者是 11 到 15 岁的少女，她们基本上是唯一的消费群体
- 客户试图重新分配广告费，但直到今天这个方法是否成功尚未可知
- 目标消费者，仍有相当强的购买潜力
- 客户的竞争对手很强悍

**从收集到的数据中可以得到**：

- 6 月份销售数据比 1 月份有所增加，但相对增速太慢
- 2 月份开始加入了网络推广的广告类型，但效果不明显
- 从 4 月份开始，单价从原来的 2 元，降低为 1.9 元，降价并未提高销量
- 增加网络推广，以及降价，从 4 月份开始双管齐下，但最终效果不佳
- 虽然增加了网络推广，但广告费总额度并没有发生变化

通过对数据的比较和分类，我们对手头上的数据有了更好的认识，并进一步了解了客户的业务时如何展开的

### 第三步 分析评估

分析评估和数据分解一样，关键就是比较，将客户观点和数据块放在一起比较。

分析过程是个发挥主管能动性的过程，需要将自己的假设融入到分析结果中，所以可以说分析结果是分析师的信用基础，即好的结果有助于提升分析师的信用，反之亦然。

无论在建构复杂的模型还是简单的模型，数据分析就是你的一切：**你的信念、你的判断、你的信用**

加入了你的思路和分析，将从你和客户那里得到好处：

**来自自己的好处**：

- 将知道数据中发生了什么
- 避免得到过头的结论
- 将对你的工作负责

说到底，就是不只是展示数据本身，而是了解了业务结合自己分析的思考结果，是自己对这个这件事情的一个认知

**来自客户的好处**：

- 客户将更尊敬你的判断
- 客户将理解到你的判断是具有局限性的

相反，如果只是展示了数据本身，**没有自己的思考和判断，相当于是在说**：

- 数据就是这样，我已经告诉你了，言下之意：我不该对错误的结论负责
- 数据后面的业务我怎么知道，言下之意：你没告诉我，我得到错误得结论是应该的

如果是这样，那你将失去客户的信任，甚至做出过头的结论，最后使用户蒙受损失

最后，**给客户提出建议的形式和方法至关重要**：

- 我们必须 **将自己的设想和判断以合适的格式整合起来**，让客户参考和选取
- 我们要 **确保自己的意见传达到位**，让人们根据你的意见做出正确的决策

### 第四步 得到决策

经过分析思考之后，就可以完成最终的分析报告了，注意报告的形式，和包含的内容，虽然是个简单的报告，但麻雀虽小五脏俱全：

- **背景**  
是对收集到的信息的一个总结，以及客户业务开展方式的描述，作为整个报告的参考系  
- **数据解说**  
是从数据中得到的推论的展示，必要时要配上图表，让客户更容易认识和理解
- **建议**  
是在分析评估阶段结合自己的思考得到的结论，简洁命令，且能在前面背景以及数据解说中找到支撑点，对我们自己的结论，即我们自己思考得到的需要标明来自于我们自己

**分析报告如下**：

- 背景:  
  1. 保湿霜的主要客户是少女消费者（具体是 11-15 岁），她们基本是唯一的消费群体；
  2. 公司正在尝试增加用户网络推广费，但迄今为止，这个做法的效果尚未可知；
  3. 能看到我们的产品在少女消费者中的销售潜力巨大。公司面临这巨大的竞争压力。

- 数据解说：
  - 6 月份销售数据比 1 月份有所增加，但相对增速太慢
  - 与销售目标相去甚远，削减广告费可能会影响销售达标能力，而降价无助于销量达标

![配上图表更具说服力](http://www.justdopython.com/assets/images/2020/07/data_analysis_without_code/01.png)

- 建议：
  - 销量相对于目标下降可能与广告费相对从前的广告费下降有关
  - 没有充分的证据让我们相信网络广告策略如我们所愿取得成功
  - **我** 将把广告费重新调整到1月份的水平，看看少女消费者的反应
  - **针对少女消费者做广告是让总销售额重新达到销售目标的手段**

### 验证决策

如果分析报告严谨可信，将会被采用，并付诸行动，但并不意味着分析工作结束了因为

1. **结论中有些部分是没有确定的证据支撑，需要进一步的验证**
2. **我们的认知有局限性**

而造成我们认知局限性的原因有多种：

- 收集的数据并非完整
- 调查得到的业务并非全面
- 我们自己的认知偏差
- 分析模型于实际的匹配程度
- 现实时在不断变化的，当下正确的结论，在未来可能会失效
- ...

如果不对结论进行验证的证明，就相当于给出了一个无法证明的结论，参考价值将大大缩减

我们知道，现代的科学理论都有建立在 **严格的科学逻辑证明** 基础上的，才使得我们能在科学理论上，创建出美好的现代化世界， 我们的数据分析是科学的，所以需要是可证明的。

## 总结

今天的文章虽然描述的是数据分析，但是却没有用到常用的数据分析工具，也没有使用高深的数据分析数据公式，不过这是数据分析的基础和开端，明白了数据分析的意义和过程，才能更好的使用各种工具，让我们在数据分析过程中事半功倍，否则将会迷失在众多工具和理论中，不知所终。

文章中的示例主要来自于我学习数据分析过程中的《Head First 深入浅出数据分析》一书，如有兴趣可以参考，值得阅读。

## 参考

- [Head First 数据分析：https://book.douban.com/subject/5257905/](https://book.douban.com/subject/5257905/)
- [https://jingyan.baidu.com/article/624e7459086a4a34e8ba5af4.html](https://jingyan.baidu.com/article/624e7459086a4a34e8ba5af4.html)
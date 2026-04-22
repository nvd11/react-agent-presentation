第2.5页  的细节

首先, 

用一个代码例子表面llm 需要常识类知识丰富, 但是无法解答特定方面的问题

这个例子是

用提示词: 请问Jacky 有多少个女儿 来调用llm

llm 返回表示自己无法解答这个问题, 因为没有足够的上下文信息


然后ppt 给一段解析



接下来第2个demo代码例子

我们先构建一个system prompt 内容是 jack 有4个孩子,其中2个是男孩

再把userquery 请问Jacky 有多少个女儿  结合system prompt 一起发给llm

这次llm 轻松地回答了这个问题

然后ppt 给一段解释, 所谓RAG 就是把 上下文结合问题一起让llm 基于上下文回答问题

至于如何或得这个相关的上下文, 后面的slide 会讲解

==================================

第3页

首先 我们分析上面第2个demo代码例子

其中可以将代码分割为两部分, 一个是retriever(虽然本例子是hardcode), 2是generator

说明一下这两个就是RAG agent的核心组件, 在企业级别的RAG agent里会抽象化, 并给出一段代码例子

这页要有动画效果
===============================

第4页 我们讲解知识库构建

说明知识库构建与etriever 的实现方式息息相关

例如如果我们简单地将知识库的文本构建成文本文件

那么retriver的实现就必须要能读取磁盘文件内容的能力, 并给出代码例子

另 一个例子
假如 我们把知识库作为文本存入数据库, 则retriever的实现就需要具备数据库查询的能力, 同样也要给出代码例子

这一页也要有 这页要有动画效果


======================================

第5页, 我们讲解向量化 和embedding

首先 我们要举个例子说明文本查询的一些限制, 主要是很难判断语义相近的两个文本

例如我们的问题是查询苹果的营养价值,   知识库里只有 雪梨 和 米饭的数据


正常的文本比较是很难去判断苹果和 雪梨米饭两个词哪个语义更相近的

所以要引入向量化 

这里要介绍什么是向量化,和高维向量, 要有图例


然后介绍什么是embedding,  常见的embedding model

给一段embedder 的代码例子(也要抽象化)


======================

第 6 页要讲解chunking 

首先, 我们要解释为何存储知识库时要chunkikng

要点(请补充)
1. 通常知识库的导入是以文档为单位
2. 但个文档的内容对于一个问题里通常过于复杂, 会给llm带来上下文噪音(这里举一个具体例子)
3. RAG 的输出通常不能只有问题回答, 还要带上问题回答参考了那些知识库内容和相关度分数, 给出一个具体回答的例子(这里引入为何要分段和top k)

然后介绍常见的chunkikng方法, 还有overlap 度数, 
要说明先chunking 然后说明要先chunking 再对每一个chunk 做embedding 要有代码例子

代码要有抽象化的体现
这一页也要有 这页要有动画效果

最后引出下一页会介绍vectordb 和 常见知识库表结构


第7页

首先我们介绍什么是么是vector db, 然后介绍常见的vectordb 例如prosgresql with pgvector, alloy db, BigQuery等

然后我们介绍常见的表结构
请参考
https://github.com/nvd11/automated-rag-evaluator/blob/main/docs/database_schema_design.md
里面的 document_chunks 介绍一个字段的意思, 和为何要存在
要介绍为何除了vector数据外, 还要存储chunk的文本(作用是喂给generator/llm)

然后是document_topics 表, 特别要重点介绍我们为何要为文档用topic 分类

要给出用带topic的sql 查询语句
这一页也要有 这页要有动画效果

第8页

这里我们介绍generator
重点是这里要有llm参与和 retirver的output

给出具体代码例子-带提示词

给出带top5 参考chunks 和相关度的 output例子
还要重点介绍top k参数的调优

这一页也要有 这页要有动画效果

第9页
这里我们介绍Rag agent 的代码实现和调用的代码例子

你可以用https://github.com/nvd11/automated-rag-evaluator/blob/main/src/agents/rag_agent.py
来动态讲解

这一页也要有 这页要有动画效果

=================================

第10页

介绍RAG agent 在我们SDLC中的潜力

如果我们能把jira stories 构建成知识库, 则, 大大方便我们BA sm 获取当前sprint report 和总体进度等信息

如果我们能把团队的confluence page 构建成知识库, 则..........
如果能把change requests 构建成知识库 则.....

还要介绍我们当前的痛点, 缺少开发者参与和一个好用的embedding model
=========================================================

第11页
总结

后面的之前的页就删掉
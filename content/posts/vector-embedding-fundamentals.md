---
title: "向量嵌入的数学本质: 从 Word2Vec 到 Transformer Embedding"
date: 2023-01-15T10:00:00+08:00
lastmod: 2023-01-15T10:00:00+08:00
draft: false
tags: ["AI", "RAG", "Vector", "Embedding", "NLP"]
categories: ["AI技术"]
author: "cathay"
---

## 前言

在 ChatGPT 引发的 AI 浪潮中,向量嵌入(Vector Embedding)成为了连接自然语言和机器理解的关键桥梁。本文将深入探讨为什么要把文本变成向量,以及向量嵌入技术的演进历程。

## 为什么要把文本变成向量?

### 语义相似性的几何表达

计算机只能处理数字,但人类用文字交流。如何让机器"理解"文本的含义?答案是将文本映射到高维向量空间。

核心思想很简单:**语义相似的文本,在向量空间中的距离应该更近**。

想象一个三维空间:
- "国王"这个词可能在坐标 `[0.8, 0.3, 0.1]`
- "女王"可能在 `[0.75, 0.35, 0.15]`
- "苹果"可能在 `[-0.2, 0.9, -0.5]`

"国王"和"女王"的距离很近(都是皇室概念),而"苹果"离它们很远。这就是向量嵌入的魔法:把语义关系转化为几何关系。

## Word2Vec: 词向量的开端

### CBOW vs Skip-gram

Word2Vec 提出了两种训练词向量的方法:

**CBOW (Continuous Bag of Words)**:
- 用上下文预测中心词
- 例如: "我喜欢___编程" → 预测"学习"
- 速度快,适合大规模语料

**Skip-gram**:
- 用中心词预测上下文
- 例如: "学习" → 预测 ["我", "喜欢", "编程"]
- 对低频词效果更好,语义表达更丰富

本质区别:CBOW 是"完形填空",Skip-gram 是"联想扩散"。实践中 Skip-gram 更常用,因为它能更好地捕捉词与词之间的细微关系。

### 词向量的代数性质

Word2Vec 最令人惊叹的发现是:**词向量具有代数性质**。

经典案例:
```
vector("国王") - vector("男人") + vector("女人") ≈ vector("女王")
```

这不是巧合,而是向量空间捕捉到了语义关系:
- "国王" - "男人" = "皇室身份"
- "皇室身份" + "女人" = "女王"

类似的例子:
```
vector("巴黎") - vector("法国") + vector("中国") ≈ vector("北京")
vector("走") - vector("走了") + vector("跑了") ≈ vector("跑")
```

这种代数性质证明了向量空间不仅仅是"相似度计算",而是真正捕捉到了语言的结构化知识。

## Sentence-BERT: 句子级语义表达

### 从词向量到句向量的挑战

Word2Vec 解决了词的表达,但句子怎么办?

**简单方案:词向量平均**
```python
sentence_vector = mean([word_vec1, word_vec2, word_vec3])
```

问题:丢失了词序和语法信息。"狗咬人"和"人咬狗"的向量会一样。

**BERT 的突破**:
- 用 Transformer 编码整个句子
- 每个词的向量都包含了上下文信息
- "bank"在"河岸"和"银行"两个句子中的向量完全不同

**Sentence-BERT 的优化**:
- BERT 太慢,不适合大规模检索
- 用 Siamese 网络训练句子级别的编码器
- 一次编码,永久使用,检索速度提升 1000 倍

### BERT 的池化策略

BERT 输出的是每个 token 的向量,如何得到整个句子的向量?

**常见池化方法**:

1. **[CLS] token**: 使用第一个特殊 token 的向量
   - BERT 预训练时 [CLS] 用于分类任务
   - 简单但效果一般

2. **Mean Pooling**: 对所有 token 向量求平均
   - 最常用的方法
   - Sentence-BERT 的默认选择

3. **Max Pooling**: 取每个维度的最大值
   - 保留最显著的特征
   - 对某些任务效果更好

4. **Weighted Pooling**: 根据 attention 权重加权平均
   - 更复杂但更精确
   - 计算成本更高

实践中 **Mean Pooling** 是性价比最高的选择。

## 现代 Embedding 模型对比

### OpenAI text-embedding-ada-002

OpenAI 的商业 Embedding 模型,2022 年底发布:

**特点**:
- 1536 维向量
- 支持 8191 tokens 输入
- 多语言支持优秀
- 价格: $0.0001 / 1K tokens

**优势**:
- 开箱即用,无需训练
- 质量稳定,持续优化
- API 调用简单

**劣势**:
- 成本累积(大规模应用)
- 数据隐私(需发送到 OpenAI)
- 无法针对特定领域微调

### 开源模型: all-MiniLM, BGE, E5

开源社区提供了强大的替代方案:

**all-MiniLM-L6-v2** (Sentence-Transformers):
- 384 维,模型小(80MB)
- 速度快,适合边缘部署
- 英文效果好,中文一般

**BGE (BAAI General Embedding)**:
- 智源研究院出品
- 中英文双语优秀
- bge-large-zh: 1024 维,中文最强之一

**E5** (Microsoft):
- text2vec-base-chinese: 768 维
- 对比学习训练,效果优秀
- 开源可商用

**选择建议**:
- 英文场景: all-MiniLM (速度) 或 E5 (质量)
- 中文场景: BGE 系列
- 预算充足: OpenAI ada-002
- 数据敏感: 必须用开源模型

## 距离度量: 如何衡量相似度?

### Cosine Similarity

**余弦相似度**:衡量两个向量的夹角。

```python
cosine_sim = dot(A, B) / (norm(A) * norm(B))
# 范围: [-1, 1]
# 1 表示完全相同方向
# 0 表示正交(无关)
# -1 表示完全相反方向
```

**为什么最常用?**
- 不受向量长度影响,只看方向
- 文本向量的长度往往无意义(长文本 vs 短文本)
- 计算高效,适合大规模检索

**应用场景**: 几乎所有文本相似度任务

### Euclidean Distance

**欧氏距离**:向量空间中的直线距离。

```python
euclidean_dist = sqrt(sum((A - B) ** 2))
# 范围: [0, ∞)
# 0 表示完全相同
# 值越大越不相似
```

**特点**:
- 受向量长度影响
- 对向量的绝对位置敏感
- 计算直观,几何意义明确

**何时使用**:
- 向量已归一化(长度为 1)
- 需要考虑向量的"强度"差异
- 低维空间(高维会有"维度灾难")

### Dot Product

**点积**:向量对应元素相乘后求和。

```python
dot_product = sum(A * B)
# 范围: (-∞, ∞)
# 值越大越相似
```

**与 Cosine 的关系**:
```python
cosine_sim = dot(A, B) / (norm(A) * norm(B))
# 如果向量已归一化,dot(A, B) == cosine_sim
```

**何时使用**:
- 向量已归一化(最常见)
- 需要最快的计算速度(省去除法)
- 某些向量数据库(如 Pinecone)默认使用点积

**实践建议**: 归一化向量 + 点积 = 最快的余弦相似度

## 实战: 向量计算示例

```python
import numpy as np
from sentence_transformers import SentenceTransformer

# 加载模型
model = SentenceTransformer('all-MiniLM-L6-v2')

# 文本示例
texts = [
    "我喜欢编程",
    "我热爱写代码",
    "今天天气真好",
    "苹果是一种水果"
]

# 生成向量
embeddings = model.encode(texts)
print(f"向量维度: {embeddings.shape}")  # (4, 384)

# 计算相似度矩阵
from sklearn.metrics.pairwise import cosine_similarity
sim_matrix = cosine_similarity(embeddings)

print("\n相似度矩阵:")
for i, text1 in enumerate(texts):
    for j, text2 in enumerate(texts):
        if i < j:  # 只打印上三角
            print(f"'{text1}' vs '{text2}': {sim_matrix[i][j]:.3f}")

# 输出示例:
# '我喜欢编程' vs '我热爱写代码': 0.847  # 高相似度
# '我喜欢编程' vs '今天天气真好': 0.123  # 低相似度
# '我喜欢编程' vs '苹果是一种水果': 0.089  # 低相似度
# '我热爱写代码' vs '今天天气真好': 0.134
# '我热爱写代码' vs '苹果是一种水果': 0.092
# '今天天气真好' vs '苹果是一种水果': 0.156

# 词向量代数示例(概念演示)
def vector_analogy(word1, word2, word3, word_vectors):
    """
    word1 - word2 + word3 ≈ ?
    例如: king - man + woman ≈ queen
    """
    result_vec = word_vectors[word1] - word_vectors[word2] + word_vectors[word3]
    # 找到最接近的词(实际需要完整词表)
    return result_vec
```

## 小结

向量嵌入是 AI 理解语言的基石:

1. **核心思想**: 将语义关系转化为几何关系,相似的文本在向量空间中距离更近
2. **技术演进**: Word2Vec(词) → BERT(上下文) → Sentence-BERT(句子) → 现代 Embedding 模型
3. **关键特性**: 词向量的代数性质揭示了语言的结构化知识
4. **实用工具**: OpenAI ada-002(商业) vs BGE/E5(开源),根据场景选择
5. **距离度量**: Cosine Similarity 是文本相似度的首选

有了向量表达,下一个问题是:**如何存储和检索这些向量?** 这就引出了向量数据库和知识图谱两种不同的知识表达范式。

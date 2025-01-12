---

title: 通过微调smolLM模型实现抄袭检测
Based Model: https://huggingface.co/HuggingFaceTB/SmolLM-135M
---

# 通过微调smolLM模型实现抄袭检测（NLP+LLM）

这个仓库存放了三个文件，其中py文件在colab上运行的，然后运行步骤就是将数据集和该文件同时导入colab，**数据集的相对地址老师要自己修改**，然后最后运行完之后会将模型和分词器保存下来，就不用再hugging face中下载，节省时间。**运用colab-T4GPU训练时长大概为9个小时**。



## 训练集划分情况

- 微调数据集，提供标记的句子对，其中每对被标记为抄袭或非抄袭。这个标签用于二值分类，使其非常适合检测句子级别的相似性。
- 训练集: 70%
- 验证集: 10% 
- 测试集: 20%



## 模型优化细节

-   **架构**：模型已修改为具有两个标签的序列分类。
-   **优化器**：AdamW，学习率为 2e-5。
-   **损失函数**：交叉熵损失。
-   **Batch Size**： 16
-   **Epochs**：3
-   **Padding**：自定义 padding token，以符合 SmolLM 要求。



## 测试集评估

**Accuracy**: 96.20%

| Class | Precision | Recall | F1-Score | Support |
|-------|-----------|--------|----------|---------|
| 0     | 0.96      | 0.97   | 0.96     | 36,586  |
| 1     | 0.97      | 0.96   | 0.96     | 36,888  |

**整体指标**:

- **Accuracy**: 0.96
- **Macro Average**:
  - Precision: 0.96
  - Recall: 0.96
  - F1-Score: 0.96
- **Weighted Average**:
  - Precision: 0.96
  - Recall: 0.96
  - F1-Score: 0.96
- **Total Support**: 73,474




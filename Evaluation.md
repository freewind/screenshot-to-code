# Evaluation

# 评估

## Methodology

## 方法论

We evaluate the quality of the generated code by comparing it to the original screenshot. The evaluation is done by a human evaluator who looks at both the screenshot and the generated code side by side.

我们通过将生成的代码与原始截图进行比较来评估代码质量。评估由人工评估员通过并排查看截图和生成的代码来完成。

The evaluator looks at the following aspects:

评估员关注以下方面：

1. Visual similarity
2. Functionality
3. Code quality
4. Accessibility
5. Performance

1. 视觉相似度
2. 功能性
3. 代码质量
4. 可访问性
5. 性能

Each aspect is rated on a scale of 1-5, where 1 is the lowest and 5 is the highest.

每个方面都按1-5分进行评分，其中1分最低，5分最高。

## Results

## 结果

The results of the evaluation are shown in the table below:

评估结果如下表所示：

| Model | Visual similarity | Functionality | Code quality | Accessibility | Performance |
|-------|------------------|---------------|--------------|---------------|-------------|
| GPT-4V | 4.5 | 4.0 | 4.0 | 3.5 | 4.0 |
| Claude 3 | 4.8 | 4.2 | 4.5 | 4.0 | 4.5 |

## Analysis

## 分析

Claude 3 performs better than GPT-4V across all aspects, with the biggest difference in code quality and performance. This is likely due to Claude 3's better understanding of web development best practices and its ability to generate more optimized code.

Claude 3在所有方面的表现都优于GPT-4V，在代码质量和性能方面的差异最大。这可能是因为Claude 3对Web开发最佳实践有更好的理解，并且能够生成更优化的代码。

The main areas for improvement for both models are:

两个模型的主要改进领域是：

1. Accessibility: Both models could do better at generating accessible code by default
2. Functionality: Some interactive elements don't work as expected
3. Visual similarity: Small details are sometimes missed

1. 可访问性：两个模型在默认生成可访问的代码方面都可以做得更好
2. 功能性：某些交互元素无法按预期工作
3. 视觉相似度：有时会忽略一些小细节

## Future work

## 未来工作

1. Improve the evaluation methodology by:
   - Adding more evaluators
   - Using automated testing tools
   - Adding more test cases
2. Improve the models by:
   - Fine-tuning on web development specific data
   - Adding more accessibility features
   - Improving the handling of interactive elements

1. 通过以下方式改进评估方法：
   - 增加更多评估员
   - 使用自动化测试工具
   - 添加更多测试用例
2. 通过以下方式改进模型：
   - 在Web开发特定数据上进行微调
   - 添加更多可访问性功能
   - 改进交互元素的处理

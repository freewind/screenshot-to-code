# Claude 3 for converting screenshots to code

# Claude 3用于将截图转换为代码

Claude 3 dropped yesterday, claiming to rival GPT-4 on a wide variety of tasks. I maintain a very popular open source project called "screenshot-to-code" (this one!) that uses GPT-4 vision to convert screenshots/designs into clean code. Naturally, I was excited to see how good Claude 3 was at this task.

Claude 3昨天发布，声称在广泛的任务上可以与GPT-4匹敌。我维护着一个非常受欢迎的开源项目"screenshot-to-code"(就是这个！)，它使用GPT-4 vision将截图/设计转换为整洁的代码。自然地，我很兴奋想看看Claude 3在这个任务上表现如何。

**TLDR:** Claude 3 is on par with GPT-4 vision for screenshot to code, better in some ways but worse in others.

**总结：** Claude 3在截图转代码方面与GPT-4 vision不相上下，在某些方面更好但在其他方面更差。

## Evaluation Setup

## 评估设置

I don't know of a public benchmark for "screenshot to code" so I created simple evaluation setup for the purposes of testing:

我不知道有"截图转代码"的公开基准测试，所以我创建了一个简单的评估设置用于测试：

- **Evaluation Dataset**: 16 screenshots with a mix of UI elements, landing pages, dashboards and popular websites.

- **评估数据集**：16张截图，包含UI元素、着陆页、仪表盘和流行网站的混合。

<img width="784" alt="Screenshot 2024-03-05 at 3 05 52 PM" src="https://github.com/abi/screenshot-to-code/assets/23818/c32af2db-eb5a-44c1-9a19-2f0c3dd11ab4">

- **Evaluation Metric**: Replication accuracy, as in "How close does the generated code look to the screenshot?" While there are other metrics that are important like code quality, speed and so on, this is by far the #1 thing most users of the repo care about.

- **评估指标**：复制准确度，即"生成的代码看起来与截图有多接近？"虽然还有其他重要的指标如代码质量、速度等，但这是目前仓库大多数用户最关心的事情。

- **Evaluation Mechanism**: Each output is subjectively rated by a human on a rating scale from 0 to 4. 4 = very close to an exact replica while 0 = nothing like the screenshot. With 16 screenshots, the maximum any model can score is 64.

- **评估机制**：每个输出由人工主观评分，评分范围从0到4。4分=非常接近完全复制，而0分=与截图完全不像。对于16张截图，任何模型的最高得分是64分。

To make the evaluation process easy, I created [a Python script](https://github.com/abi/screenshot-to-code/blob/main/backend/run_evals.py) that runs code for all the inputs in parallel. I also made a simple UI to do a side-by-side comparison of the input and output.

为了使评估过程更容易，我创建了[一个Python脚本](https://github.com/abi/screenshot-to-code/blob/main/backend/run_evals.py)，可以并行运行所有输入的代码。我还制作了一个简单的UI来进行输入和输出的并排比较。

![Google Chrome](https://github.com/abi/screenshot-to-code/assets/23818/38126f8f-205d-4ed1-b8cf-039e81dcc3d0)

## Results

## 结果

Quick note about what kind of code we'll be generating: currently, screenshot-to-code supports generating code in HTML + Tailwind, React, Vue, and several other frameworks. Stacks can impact the replication accuracy quite a bit. For example, because Bootstrap uses a relatively restrictive set of user elements, generations using Bootstrap tend to have a distinct "Bootstrap" style.

关于我们将生成什么样的代码的快速说明：目前，screenshot-to-code支持生成HTML + Tailwind、React、Vue和其他几个框架的代码。技术栈会对复制准确度产生很大影响。例如，因为Bootstrap使用相对受限的用户元素集，使用Bootstrap生成的代码往往具有明显的"Bootstrap"风格。

I only ran the evals on HTML/Tailwind here which is the stack where GPT-4 vision tends to perform the best.

我这里只在HTML/Tailwind上运行评估，这是GPT-4 vision表现最好的技术栈。

Here are the results (average of 3 runs for each model):

以下是结果(每个模型3次运行的平均值)：

- GPT-4 Vision obtains a score of **65.10%** - this is what we're trying to beat
- Claude 3 Sonnet receives a score of **70.31%**, which is a bit better.
- Surprisingly, Claude 3 Opus which is supposed to be the smarter and slower model scores worse than both GPT-4 vision and Claude 3 Sonnet, comes in at **61.46%**.

- GPT-4 Vision获得**65.10%**的分数 - 这是我们要试图超越的
- Claude 3 Sonnet获得**70.31%**的分数，稍好一些。
- 令人惊讶的是，本应更智能和更慢的Claude 3 Opus的得分比GPT-4 vision和Claude 3 Sonnet都低，只有**61.46%**。

Overall, a very strong showing for Claude 3. Obviously, there's a lot of subjectivity involved in this evaluation but Claude 3 is definitely on par with GPT-4 Vision, if not better.

总的来说，Claude 3表现非常强劲。显然，这个评估涉及很多主观因素，但Claude 3肯定与GPT-4 Vision不相上下，如果不是更好的话。

You can see the [side-by-side comparison for a run of Claude 3 Sonnet here](https://github.com/abi/screenshot-to-code-files/blob/main/sonnet%20results.png). And for [a run of GPT-4 Vision here](https://github.com/abi/screenshot-to-code-files/blob/main/gpt%204%20vision%20results.png).

你可以在这里看到[Claude 3 Sonnet的一次运行的并排比较](https://github.com/abi/screenshot-to-code-files/blob/main/sonnet%20results.png)。以及[GPT-4 Vision的一次运行](https://github.com/abi/screenshot-to-code-files/blob/main/gpt%204%20vision%20results.png)。

Other notes:

其他注意事项：

- The prompts used are optimized for GPT-4 vision. Adjusting the prompts a bit for Claude did yield a small improvement. But nothing game-changing and potentially not worth the trade-off of maintaining two sets of prompts.

- 使用的提示词是为GPT-4 vision优化的。为Claude稍微调整提示词确实带来了一些改进。但没有什么革命性的变化，可能不值得维护两套提示词的代价。

- All the models excel at code quality - the quality is usually comparable to a human or better.

- 所有模型在代码质量方面都很出色 - 质量通常可以与人类相媲美或更好。

- Claude 3 is much less lazy than GPT-4 Vision. When asked to recreate Hacker News, GPT-4 Vision will only create two items in the list and leave comments in this code like `<!-- Repeat for each news item -->` and `<!-- ... other news items ... -->`.

- Claude 3比GPT-4 Vision勤奋得多。当被要求重建Hacker News时，GPT-4 Vision只会在列表中创建两个项目，并在代码中留下注释，如`<!-- Repeat for each news item -->`和`<!-- ... other news items ... -->`。

<img width="699" alt="Screenshot 2024-03-05 at 9 25 04 PM" src="https://github.com/abi/screenshot-to-code/assets/23818/04b03155-45e0-40b0-8de0-b1f0b4382bee">

While Claude 3 Sonnet can sometimes be lazy too, most of the time, it does what you ask it to do.

虽然Claude 3 Sonnet有时也会偷懒，但大多数时候它会按要求完成任务。

<img width="904" alt="Screenshot 2024-03-05 at 9 30 23 PM" src="https://github.com/abi/screenshot-to-code/assets/23818/b7c7d1ba-47c1-414d-928f-6989e81cf41d">

- For some reason, all the models struggle with side-by-side "flex" layouts

- 由于某些原因，所有模型在处理并排的"flex"布局时都很困难

<img width="1090" alt="Screenshot 2024-03-05 at 9 20 58 PM" src="https://github.com/abi/screenshot-to-code/assets/23818/8957bb3a-da66-467d-997d-1c7cc24e6d9a">

- Claude 3 Sonnet is a lot faster
- Claude 3 gets background and text colors wrong quite often! (like in the Hacker News image above)
- My suspicion is that Claude 3 Opus results can be improved to be on par with the other models through better prompting

- Claude 3 Sonnet快得多
- Claude 3经常会把背景和文字颜色弄错！(就像上面的Hacker News图片那样)
- 我怀疑通过更好的提示词，Claude 3 Opus的结果可以提升到与其他模型相当的水平

Overall, I'm very impressed with Claude 3 Sonnet for this use case. I've added it as an alternative to GPT-4 Vision in the open source repo (hosted version update coming soon).

总的来说，我对Claude 3 Sonnet在这个用例中的表现印象深刻。我已经将它作为GPT-4 Vision的替代选项添加到开源仓库中(托管版本的更新即将推出)。

If you'd like to contribute to this effort, I have some documentation on [running these evals yourself here](https://github.com/abi/screenshot-to-code/blob/main/Evaluation.md). I'm also working on a better evaluation mechanism with Elo ratings and would love some help on that.

如果你想为这项工作做出贡献，我有一些关于[自己运行这些评估的文档](https://github.com/abi/screenshot-to-code/blob/main/Evaluation.md)。我也在开发一个使用Elo评分的更好的评估机制，希望能得到一些帮助。

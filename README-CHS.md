# 发布研究论文代码的小技巧

<img src="https://upload.wikimedia.org/wikipedia/en/thumb/0/08/Logo_for_Conference_on_Neural_Information_Processing_Systems.svg/1200px-Logo_for_Conference_on_Neural_Information_Processing_Systems.svg.png" width=200>

**💡 整理了最受欢迎的ML研究论文代码库中的最佳实践，现已成为 NeurIPS 2021 会议的官方指南！**

为了促进项目的可重复性，基于对 200 多个机器学习项目代码库的分析和 GitHub Stars 的数目 ，我们总结了如下建议。有关更多详细信息，请参见我们的我们的 [博客文章](https://medium.com/paperswithcode/ml-code-completeness-checklist-e9127b168501)。

对于 NeurIPS 2021 会议的代码提交，建议（但不是强制性的）使用 [用前须知.md 模板](templates/README.md)，并根据 ML代码完整性清单（如下所述）核对项目。

## 📋 用前须知.md 模板

我们提供了一个 [用前须知.md 模板](templates/README.md)，可用于发布 ML 研究项目代码库。 

模版中的各小节是通过查看在社区中最受欢迎的代码库并分析各代码库中与欢迎程度相关联的公共组件得到的。

## ✓ ML代码完整性检查清单

我们通过查看最受欢迎的 ML 研究项目代码库的共同点来编制此清单。 此外，我们优先考虑了可重复性高的项目，使得其他项目更容易基于此构建研究代码库。

ML代码完整性检查清单包含以下五个要素：

1. **依赖说明**

2. **训练代码**

3. **评估代码**

4. **预训练模型**

5. **自述文件，包括结果表格以及运行/产生这些结果的精确命令代码**

我们证实，拥有代码完整性检查清单中更多要素的代码库，也倾向于拥有更多的 GitHub Stars。 通过分析官方 NeurIPS 2019 代码库已验证了这一点——更多详细信息请访问我们的 [博客文章](https://medium.com/paperswithcode/ml-code-completeness-checklist-e9127b168501)。 我们还提供 [数据](notebooks/code_checklist-neurips2019.csv) 和 [笔记](notebooks/code_checklist-analysis.pdf)以重现本文的分析。

进一步的，满足所有完整性检查清单中这五个要素的 NeurIPS 2019 代码库，具有最高数量的 GitHub Stars（中位数196星，平均2664星）。

接下来，我们会针对检查清单上的每个要素进行详细说明。

#### 1. 依赖说明

如果您使用的是Python，则意味着需要提供 `requirements.txt`文件（如果使用 `pip` 和 `virtualenv` ），或者提供 `environment.yml` 文件（如果使用 anaconda ），或者提供 `setup.py`（如果您使用代码是一个库）。

优秀的做法是在 **`用前须知.md`** 中安排一个小节，说明如何安装这些依赖项。 假定用户需要掌握最少的背景知识，并且要清楚而全面了解项目——如果用户无法设置您的依赖项，那么他们很可能也会放弃其余的代码。

如果您希望提供整个可复现模型的环境，则可能要考虑使用 Docker 并将您环境的 Docker镜像上传到 Dockerhub 。

#### 2. 训练代码

您的代码应当包含一个训练脚本，该脚本可用于获取论文所述的主要结果。 这意味着脚本中应该包括模型超参数以及在获取结果的过程中使用的所有技巧。 为了最大程度地发挥作用，在编写此代码时，最好考虑到可扩展性：如果您的用户希望在自己的数据集上使用相同的训练脚本，该怎么办？

您可以提供打包好的文档化的命令行程序（例如 `train.py` ）作为用户的使用入口。

#### 3. **评估代码**

模型评估和实验通常取决于细微的细节，而这些细微的细节并不总是能在论文中得到解释。 这就是为什么包含用于评估或运行实验的精确代码，将有助于对实验过程进行完整描述的原因。 反过来，这可以帮助用户信任和理解您的研究工作，并以您的研究为基础。

您可以提供打包好的文档化的命令行程序（例如 `eval.py` ）作为用户的使用入口。

#### 4. 预训练模型

从头开始训练模型可能既耗时又昂贵。 一种增加对结果的可信度的方法是提供预训练模型，从而让社区可以使用该模型获得最终结果并进行评估。 这意味着用户无需重新模型训练，就可以看到可信的结果。

另一个常见使用场景是对下游任务进行微调，在此情况下，发布预训练模型非常有用，以便其他人可以在其基础上构建模型以应用于自己的数据集。

最后，一些用户可能想尝试一下您的模型，看看它是否适用于某些示例数据。 提供预训练模型可以使您的用户随心所欲地玩转您的工作，并有助于理解您论文中的成就。

#### 5. 自述文件，包括结果表格以及运行/产生这些结果的精确命令代码

在  **`用前须知.md`**  中添加结果表格，可让您的用户快速理解对代码库的期望（有关示例，请参见 [用前须知.md 模板](templates/README.md)）。 有关如何复现这些结果的说明（带有任何相关脚本，预训练模型等的链接）可以为用户提供另一个使用入口，并直接促进复现性。 在某些情况下，一篇论文的主要结果是一个图表，但对于用户而言，如果不阅读该论文，可能会难以理解该结果。

您可以进一步提供包含其他论文的最新结果的完整指标排行榜的链接，从而进一步帮助用户理解您的结果并将其关联起来。 有[多个排行榜服务](#指标排行榜)可以存储该信息。



## 🎉用于发布研究论文代码的其他优质资源

- [ ] 注：尚未根据国内情况推荐相关工具。

### 托管预训练模型文件

1. [Zenodo](https://zenodo.org) - 支持版本管理，50GB，带宽免费，DOI，可长期保存
2. [GitHub Releases](https://help.github.com/en/github/administering-a-repository/managing-releases-in-a-repository) - 支持版本管理，2GB 文件大小限制，带宽免费
3. [OneDrive](https://www.onedrive.com/) - 支持版本管理，2GB（免费 ）/ 1TB （需要Office 365套装），带宽免费
4. [Google Drive](https://drive.google.com) - 支持版本管理，15GB，带宽免费
5. [Dropbox](https://dropbox.com) - 支持版本管理，2GB（付费无限容量），带宽免费
6. [AWS S3](https://aws.amazon.com/s3/) - 支持版本管理，仅付费使用，带宽需付费
7. [huggingface_hub](https://github.com/huggingface/huggingface_hub) - 支持版本管理，无大小限制，带宽免费
8. [DAGsHub](https://dagshub.com/) - 支持版本管理，无大小限制，带宽免费
9. [CodaLab Worksheets](https://worksheets.codalab.org/) - 10GB，带宽免费

### 管理模型文档

1. [RClone](https://rclone.org/) - 针对众多不同的云存储提供商，提供统一访问方案

### 标准化模型接口

1. [PyTorch Hub](https://pytorch.org/hub/)
2. [Tensorflow Hub](https://www.tensorflow.org/hub)
3. [Hugging Face NLP models](https://huggingface.co/models)
4. [ONNX](https://onnx.ai/)

### 指标排行榜

1. [Papers with Code leaderboards](https://paperswithcode.com/sota) - 4000+ 个排行榜
2. [CodaLab Competitions](https://competitions.codalab.org/) - 450+ 个排行榜
3. [EvalAI](https://eval.ai/) - 100+ 个排行榜
4. [NLP Progress](https://nlpprogress.com/) - 90+ 个排行榜
5. [Collective Knowledge](https://cKnowledge.io/reproduced-results) - 40+ 个排行榜
6. [Weights & Biases - Benchmarks](https://www.wandb.com/benchmarks) - 9+ 个排行榜

### 制作项目页面

1. [GitHub pages](https://pages.github.com/)
2. [Fastpages](https://github.com/fastai/fastpages)

### 制作演示、教程和可执行论文

1. [Google Colab](https://colab.research.google.com/)

2. [Binder](https://mybinder.org/)

3. [Streamlit](https://github.com/streamlit/streamlit)

4. [CodaLab Worksheets](https://worksheets.codalab.org/)

   

## 贡献

如果您想做出贡献或对这些指南有任何建议，可以通过 im.young@foxmail.com 与本中文界面维护者取得联系（或者通过 hello@paperswithcode.com 与 Paper with Code 联系 ），亦可在此 GitHub 项目中提出问题（open an issue）。

任何贡献都是受到欢迎的！ 此项目中的所有内容均遵照 MIT许可协议进行许可授权。
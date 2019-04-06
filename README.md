[TOC]

# TensorFlow 2.0 高级教程

其实学习一个框架的时候，我们非常推荐先从整个框架上去了解这个框架，在这个基础上，我们再去学习其中的细节。这样自上而下学习方式的好处在于你把握了整个框架的脉络。如果你的水平足够，那么你应该站在一个框架的设计者的角度去思考。

## Requirements

 TODO

## 架构设计

![](https://flyman-cjb.oss-cn-hangzhou.aliyuncs.com/picgos/20190311145825.png)

我们来看整个Deep Learning的过程，其实就只有 **训练(包括自己离线做验证)** 、**部署** 两个阶段：

1. 在实际工作中，除了需要训练、验证模型外，当我们的模型经过验证发现效果还不错后，我们会将其 **部署** 到服务器、手机端、浏览器等等应用环境中。因此除了训练模型之外，还有一块很重要的框架要做的事情就是模型部署。
2. 还需要补充一点，大多数时候我们并不会从头训练一个网络，因为太耗时。因此通常我们会用预训练权重来加速网络收敛，那么框架中就需要一个专门管理预训练权重和模型的模块。

那么最终整个框架就非常明确了，正如上图所示，当然其中有很多细节被忽略掉了。

### 训练框架

我们需要着重看的是TensorFlow训练部分的框架设计，因为这事我们经常接触到的：

<img src="https://flyman-cjb.oss-cn-hangzhou.aliyuncs.com/picgos/20190406163445.png" width="500" height="高度" alt="图片名称" align=center>

训练可以分为 **用户层** 和 **硬件层**：

- **用户层**

  也是我们经常需要操作的，也就是如何构建、训练、验证模型。

- **硬件层**

  这部分也有需要我们操作的，主要是如何写分布式训练策略对网络分布式训练。剩下的致于如何GPU、主机、进程间通信等等都是谷歌工程师需要考虑的。

 

<img src="https://flyman-cjb.oss-cn-hangzhou.aliyuncs.com/picgos/20190406173739.png" width="700" height="高度" alt="图片名称" align=center>

1. `tf.data`加载数据集

   > 使用输入管道读取训练数据，用 `tf.data `创建的输入线程读取训练数据。使用` tf.feature_column `描述特征，例如嵌套和特征交叉。还支持从内存数据（例如 NumPy）中方便地输入。

2. 使用 `tf. Keras `或 `Premade Estimators` 构建、训练和验证模型

   > Keras 与 TensorFlow 的其余部分紧密集成，因此您可以随时访问 TensorFlow 的功能。一组标准的打包模型 ( 例如，线性或逻辑回归、梯度增强树、随机森林 ) 也可以直接使用 ( 利用 `tf.estimator` API 实现 )。如果你不想从头开始训练一个模型，你很快就能通过` TensorFlow Hub` 的模块利用迁移学习来训练 Keras 或 Estimator 模型

3. 使用 eager execution 运行和调试，然后在图形上使用` tf.function`

   > TensorFlow 2.0 在默认情况下以 eager execution 方式运行，以便于使用和顺利调试。此外，tf.function annotation 透明地将 Python 程序转换成 TensorFlow 图。这个过程保留了 1.x TensorFlow 基于图执行的所有优点：性能优化、远程执行以及轻松序列化、导出和部署的能力，同时增加了使用简单的 Python 表达程序的灵活性和易用性

4. 使用分布策略进行分布式训练

   > 对于大型机器学习训练任务来讲，Distribution Strategy API 使得在不更改模型定义的情况下，在不同硬件配置上分布和训练模型变得很容易。由于 TensorFlow 提供了对 CPU、GPU 和 TPU 等一系列硬件加速器的支持，因此可以将训练工作负载分布到单节点 / 多加速器以及多节点 / 多加速器配置，包括 TPU Pods。虽然此 API 支持各种集群配置，但还提供了在本地或云环境中部署 Kubernetes 集群训练的模板

5. 导出到 SavedModel

   > TensorFlow 将在 SavedModel 上标准化，作为 TensorFlowServing、TensorFlow Lite、TensorFlow.js、TensorFlow Hub 等的交换格式

### 部署框架

<img src="https://flyman-cjb.oss-cn-hangzhou.aliyuncs.com/picgos/20190406174841.png" width="宽度" height="高度" alt="图片名称" align=center>

我们需要将其部署到不同的环境下。主要是服务器、移动端、浏览器这些环境下。

## 教程目录

### TODO

- [ ] 01 数据读取及预处理
- [ ] 02 Keras 搭建/训练/验证 模型
- [ ] 03 Estimator 搭建/训练/验证 模型
- [ ] 04 分布式训练模型

### 训练

 

### 部署
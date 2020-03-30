---
title: Python 教程：定型模型
description: 本教程系列由四个部分组成。在第三部分中，你将在 Python 中定型线性回归模型，以在 SQL Server 机器学习服务中预测雪橇租赁次数。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/20/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c564ac26c5706e67d9a633a05f81cb48d00fb771
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75681758"
---
# <a name="python-tutorial-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Python 教程：在 SQL Server 机器学习服务中定型线性回归模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

此系列教程由四个部分组成。在第三部分中，引导你在 Python 中定型线性回归模型。 在本系列的下一部分中，使用机器学习服务在 SQL Server 数据库中部署此模型。

本文将指导如何进行以下操作：

> [!div class="checklist"]
> * 定型线性回归模型
> * 使用线性回归模型进行预测

在[第一部分](python-ski-rental-linear-regression.md)中，你了解了如何还原示例数据库。

在[第二部分](python-ski-rental-linear-regression-prepare-data.md)中，你了解了如何将数据从 SQL Server 加载到 Python 数据框架，并在 Python 中准备数据。

[第四部分](python-ski-rental-linear-regression-deploy-model.md)介绍如何将模型存储到 SQL Server，然后根据在第二和第三部分中开发的 Python 脚本来创建存储过程。 存储过程将在 SQL Server 中运行，以便基于新数据进行预测。

## <a name="prerequisites"></a>先决条件

* 本教程的第三部分假设你已完成[第一部分](python-ski-rental-linear-regression.md)及其先决条件。

## <a name="train-the-model"></a>定型模型

为进行预测，必须找到一个最能描述数据集中变量之间的依赖关系的函数（模型）。 这称为定型模型。 定型数据集是在此系列第二部分中创建的 pandas 数据帧“df”中的整个数据集的一个子集  。

使用线性回归算法定型模型 lin_model  。

```python
# Store the variable we'll be predicting on.
target = "Rentalcount"

# Generate the training set.  Set random_state to be able to replicate results.
train = df.sample(frac=0.8, random_state=1)

# Select anything not in the training set and put it in the testing set.
test = df.loc[~df.index.isin(train.index)]

# Print the shapes of both sets.
print("Training set shape:", train.shape)
print("Testing set shape:", test.shape)

# Initialize the model class.
lin_model = LinearRegression()

# Fit the model to the training data.
lin_model.fit(train[columns], train[target])
```

可得到类似于下面的结果。

```results
Training set shape: (362, 7)
Testing set shape: (91, 7)
```

## <a name="make-predictions"></a>作出预测

使用 PREDICT 函数预测使用模型 lin_model 的租赁计数  。

```python
# Generate our predictions for the test set.
lin_predictions = lin_model.predict(test[columns])
print("Predictions:", lin_predictions)
# Compute error between our test predictions and the actual values.
lin_mse = mean_squared_error(lin_predictions, test[target])
print("Computed error:", lin_mse)
```

可得到类似于下面的结果。

```results
Predictions: [ 40.  38. 240.  39. 514.  48. 297.  25. 507.  24.  30.  54.  40.  26.
  30.  34.  42. 390. 336.  37.  22.  35.  55. 350. 252. 370. 499.  48.
  37. 494.  46.  25. 312. 390.  35.  35. 421.  39. 176.  21.  33. 452.
  34.  28.  37. 260.  49. 577. 312.  24.  24. 390.  34.  64.  26.  32.
  33. 358. 348.  25.  35.  48.  39.  44.  58.  24. 350. 651.  38. 468.
  26.  42. 310. 709. 155.  26. 648. 617.  26. 846. 729.  44. 432.  25.
  39.  28. 325.  46.  36.  50.  63.]
Computed error: 2.9960763804270902e-27
```

## <a name="next-steps"></a>后续步骤

在本系列教程的第三部分中，你已完成以下步骤：

* 定型线性回归模型
* 使用线性回归模型进行预测

若要部署已创建的机器学习模型，请按照本系列教程的第四部分进行操作：

> [!div class="nextstepaction"]
> [Python 教程：部署机器学习模型](python-ski-rental-linear-regression-deploy-model.md)
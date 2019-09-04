---
title: Python 教程：训练模型（线性回归）
description: 在本教程中，您将在 SQL Server 机器学习服务中使用 Python 和线性回归来预测滑雪租赁的数量。 你将在 Python 中训练线性回归模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 30f390681dc63d6de9a95e805b6cc8f273b2b8d7
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242545"
---
# <a name="python-tutorial-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Python 教程：在 SQL Server 中训练线性回归模型机器学习服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在这四个部分的系列教程的第三部分中，你将在 Python 中训练线性回归模型。 在本系列的下一部分中，你将使用机器学习服务在 SQL Server 数据库中部署此模型。

本文将介绍如何执行以下操作：

> [!div class="checklist"]
> * 为线性回归模型定型
> * 使用线性回归模型进行预测

在[第一部分](python-ski-rental-linear-regression.md)中，您学习了如何还原示例数据库。

在[第二部分](python-ski-rental-linear-regression-prepare-data.md)中，您学习了如何将数据从 SQL Server 加载到 python 数据帧，并在 python 中准备数据。

在[第四部分](python-ski-rental-linear-regression-deploy-model.md)中，你将了解如何将模型存储到 SQL Server，然后从你在第二和第三部分中开发的 Python 脚本中创建存储过程。 存储过程将在 SQL Server 中运行，以便基于新数据进行预测。

## <a name="prerequisites"></a>先决条件

* 本教程的第三部分假设你已完成[第一个部分](python-ski-rental-linear-regression.md)及其必备组件。

## <a name="train-the-model"></a>训练模型

为了进行预测，您必须查找一个函数（模型），该函数最能描述数据集中的变量之间的依赖关系。 这称为 "定型模型"。 训练数据集将是在此系列的第二部分中创建的 pandas 数据帧**df**中整个数据集的子集。

您将使用线性回归算法训练模型**lin_model** 。

```python
# Store the variable we'll be predicting on.
target = "RentalCount"

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

应会看到如下所示的结果。

```results
Training set shape: (362, 7)
Testing set shape: (91, 7)
```

## <a name="make-predictions"></a>进行预测

使用 predict 函数预测使用模型**lin_model**的租赁计数。

```python
# Generate our predictions for the test set.
lin_predictions = lin_model.predict(test[columns])
print("Predictions:", lin_predictions)
# Compute error between our test predictions and the actual values.
lin_mse = mean_squared_error(lin_predictions, test[target])
print("Computed error:", lin_mse)
```

```results
Predictions: [  40.   38.  240.   39.  514.   48.  297.   25.  507.   24.   30.   54.
   40.   26.   30.   34.   42.  390.  336.   37.   22.   35.   55.  350.
  252.  370.  499.   48.   37.  494.   46.   25.  312.  390.   35.   35.
  421.   39.  176.   21.   33.  452.   34.   28.   37.  260.   49.  577.
  312.   24.   24.  390.   34.   64.   26.   32.   33.  358.  348.   25.
   35.   48.   39.   44.   58.   24.  350.  651.   38.  468.   26.   42.
  310.  709.  155.   26.  648.  617.   26.  846.  729.   44.  432.   25.
   39.   28.  325.   46.   36.   50.   63.]
Computed error: 3.59831533436e-26
```

## <a name="next-steps"></a>后续步骤

在本系列教程的第三部分中，你已完成以下步骤：

* 为线性回归模型定型
* 使用线性回归模型进行预测

若要部署已创建的机器学习模型，请遵循本系列教程中的第四部分：

> [!div class="nextstepaction"]
> [Python 教程：部署机器学习模型](python-ski-rental-linear-regression-deploy-model.md)
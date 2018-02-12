---
title: "创建 R 模型 （SQL 和 R 深入） |Microsoft 文档"
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.assetid: a195d5e2-72e2-4dd6-bf43-947312e4a52a
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: a076c6b1bdc06709d14cb8e98be1d01b59cb935e
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="create-r-models-sql-and-r-deep-dive"></a>创建 R 模型 （SQL 和 R 深入）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是有关如何使用数据科学深入了解教程的一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

现在已丰富了定型数据，就可以使用线性回归来分析数据了。 线性模型是预测分析领域中的重要工具， **中的** RevoScaleR [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 包中包含高性能的可缩放算法。

## <a name="create-a-linear-regression-model"></a>创建线性回归模型

在此步骤中，创建简单的线性模型，估算对于客户，使用作为自变量中的值的信用卡平衡*性别*和*creditLine*列。
  
若要执行此操作，使用[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)函数，支持远程计算上下文。
  
1. 创建 R 变量来存储已完成模型，并调用**rxLinMod**，传递相应的公式。
  
    ```R
    linModObj <- rxLinMod(balance ~ gender + creditLine,  data = sqlFraudDS)
    ```
  
2. 若要查看结果的摘要，请调用标准 R`summary`模型对象上的函数。
  
     ```R
     summary(linModObj)
     ```

您可能会认为特殊纯的 R 函数，如`summary`将适用于此处，因为在以前步骤中，你可以将计算上下文设置为服务器。 但是，即使 **rxLinMod** 函数使用远程计算上下文创建模型，它也会返回包含本地工作站模型的对象并将其存储在共享目录中。

因此，你可以假定该模型是使用“本地”上下文创建的，然后对其运行标准 R 命令。

**结果**

```
Linear Regression Results for: balance ~ gender + creditLineData: sqlFraudDS (RxSqlServerData Data Source)
Dependent variable(s): balance
Total independent variables: 4 (Including number dropped: 1)
Number of valid observations: 10000
Number of missing observations: 0
Coefficients: (1 not defined because of singularities)

Estimate Std. Error t value Pr(>|t|) (Intercept)
3253.575 71.194 45.700 2.22e-16
gender=Male -88.813 78.360 -1.133 0.257
gender=Female Dropped Dropped Dropped Dropped
creditLine 95.379 3.862 24.694 2.22e-16
Signif. codes: 0  0.001  0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 3812 on 9997 degrees of freedom
Multiple R-squared: 0.05765
Adjusted R-squared: 0.05746
F-statistic: 305.8 on 2 and 9997 DF, p-value: < 2.2e-16
Condition number: 1.0184
```

## <a name="create-a-logistic-regression-model"></a>创建逻辑回归模型

接下来，你将创建逻辑回归模型，该值指示特定客户是否欺诈风险。 你将使用**RevoScaleR** [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)函数，在远程逻辑回归模型的支持调整计算上下文。

1.  将计算上下文保持为原样。 你还将继续使用相同的数据源。

2.  调用 rxLogit 函数并传递需用于定义模型的公式。

    ```R
    logitObj <- rxLogit(fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS, dropFirst = TRUE)
    ```
  
    因为它是大型模型，其中包含 60 个独立变量（包括三个删除的虚拟变量），所以可能必须等待一段时间，让计算上下文返回对象。
    
    模型如此大的原因在于，在 R 中（以及在 **RevoScaleR** 包中），分类系数变量的每个级别都自动被视为单独的虚拟变量。
  
3.  若要查看返回模型的摘要，请调用 R`summary`函数。
  
    ```R
    summary(logitObj)
    ```
  
**部分结果**

```
Logistic Regression Results for: fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine
Data: sqlFraudDS (RxSqlServerData Data Source)
Dependent variable(s): fraudRisk
Total independent variables: 60 (Including number dropped: 3)
Number of valid observations: 10000 -2

LogLikelihood: 2032.8699 (Residual deviance on 9943 degrees of freedom)

Coefficients:
Estimate Std. Error z value Pr(>|z|)     (Intercept)
-8.627e+00  1.319e+00  -6.538 6.22e-11
state=AK                Dropped    Dropped Dropped  Dropped
state=AL             -1.043e+00  1.383e+00  -0.754   0.4511

(other states omitted)

gender=Male             Dropped    Dropped Dropped  Dropped
gender=Female         7.226e-01  1.217e-01   5.936 2.92e-09
cardholder=Principal    Dropped    Dropped Dropped  Dropped
cardholder=Secondary  5.635e-01  3.403e-01   1.656   0.0977
balance               3.962e-04  1.564e-05  25.335 2.22e-16
numTrans              4.950e-02  2.202e-03  22.477 2.22e-16
numIntlTrans          3.414e-02  5.318e-03   6.420 1.36e-10
creditLine            1.042e-01  4.705e-03  22.153 2.22e-16

Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1
Condition number of final variance-covariance matrix: 3997.308
Number of iterations: 15
```

## <a name="next-step"></a>下一步

[分数新数据](../../advanced-analytics/tutorials/deepdive-score-new-data.md)

## <a name="previous-step"></a>上一步

[使用 R 可视化 SQL Server 数据](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)

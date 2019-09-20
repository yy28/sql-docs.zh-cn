---
title: 什么是 SQL Server 2016 R Services？
titleSuffix: ''
description: R Services 是 SQL Server 2016 的一项功能，它使你能够使用关系数据运行 R 脚本。 可以使用开源包和框架，并使用 Microsoft R 包进行预测分析和机器学习。 脚本在数据库中执行，而不将数据移动到 SQL Server 外部或是在网络上移动。 本文介绍 SQL Server R Services 的基础知识。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/12/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 99aba9748e7ee6d53aabb18919324243740d996a
ms.sourcegitcommit: 1661c3e1bb38ed12f8485c3860fc2d2b97dd2c9d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2019
ms.locfileid: "71149932"
---
# <a name="what-is-sql-server-2016-r-services"></a>什么是 SQL Server 2016 R Services？
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

R Services 是 SQL Server 2016 的一项功能，它使你能够使用关系数据运行 R 脚本。 可以使用开源包和框架，并使用[Microsoft R 包](#packages)进行预测分析和机器学习。 脚本在数据库中执行，而不将数据移动到 SQL Server 外部或是在网络上移动。 本文介绍 SQL Server R Services 的基础知识。

> [!Note]
> R Services 在 SQL Server 2017 及更高版本中已重命名为[机器学习服务](../what-is-sql-server-machine-learning.md)，同时支持 Python 和 R。

## <a name="what-is-r-services"></a>什么是 R Services？

SQL Server R Services 使你能够在数据库中执行 R 脚本。 您可以使用它来准备和清理数据，执行特征工程，以及在数据库中训练、评估和部署机器学习模型。 此功能在数据所在的位置运行脚本，并消除跨网络到另一台服务器的数据传输。

R 服务中包含 R 的基本分发版。 除了 Microsoft 包[RevoScaleR](../r/ref-r-revoscaler.md)、 [MicrosoftML](../r/ref-r-microsoftml.md)、[olapR] 以外，还可以使用开源包和框架。/r/ref-r-olapr.md）和[sqlrutils](../r/ref-r-sqlrutils.md) （适用于 r）。

R Services 使用扩展性框架在 SQL Server 中运行 R 脚本。 详细了解此功能的工作原理：

+ [扩展性框架](../concepts/extensibility-framework.md)
+ [R 扩展](../concepts/extension-r.md)

## <a name="what-can-i-do-with-r-services"></a>如何处理 R Services？

您可以使用 R Services 在 SQL Server 中生成和培训机器学习和深度学习模型。 你还可以将现有模型部署到 R 服务，并将关系数据用于预测。

SQL Server R Services 的预测类型的示例包括：

|||
|-|-|
|分类/分类|自动将客户反馈划分为正值和负值类别|
|回归/预测连续值|根据大小和位置预测房屋价格|
|异常检测|检测欺诈银行交易 |
|建议|根据客户以前购买的内容建议在线购物者可能希望购买的产品|

### <a name="how-to-execute-r-scripts"></a>如何执行 R 脚本

在 R Services 中执行 R 脚本的方法有两种：

+ 最常见的方法是使用 T-sql 存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

+ 你还可以使用首选的 R 客户端并编写脚本将执行（称为*远程计算上下文*）推送到远程 SQL Server。 有关详细信息，请参阅如何[设置数据科学客户端开发](../r/set-up-a-data-science-client.md)。

<a name="packages"></a>

## <a name="r-packages"></a>R 包

除了 Microsoft 的企业包外，还可以使用开源包和框架。 大多数常见的开源 R 包都预安装在 R Services 中。 还包括 Microsoft 提供的以下 R 包：

| package | 描述 |
|-|-|
| [RevoScaleR](../r/ref-r-revoscaler.md) | 可缩放的 R 的主包。数据转换和操作、统计汇总、可视化和多种形式的建模。 此外，此包中的函数会自动在可用内核之间分发工作负载，以便进行并行处理。 |
| [MicrosoftML （R）](../r/ref-r-microsoftml.md) | 添加机器学习算法，以便为文本分析、图像分析和情绪分析创建自定义模型。 |
| [olapR](../r/ref-r-olapr.md) | R 函数，用于针对 SQL Server Analysis Services OLAP 多维数据集的 MDX 查询。 |
| [sqlrutils](../r/ref-r-sqlrutils.md) | 一种机制，用于在 T-sql 存储过程中使用 R 脚本，将该存储过程注册到数据库，并从[R 开发环境](../r/set-up-a-data-science-client.md)运行存储过程。 |
| [Microsoft R Open](https://mran.microsoft.com/rro) | Microsoft R Open （MRO）是 Microsoft 的增强版本。 它是一个用于统计分析和数据科学的完整开源平台。 它基于与 R 兼容的 100%，并且包括更多的性能和可再现性的功能。 |

## <a name="how-do-i-get-started-with-rservices"></a>如何实现 RServices 入门？

1. [安装 SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

1. 配置开发工具。 你可以使用：

    + [Azure Data Studio](../../azure-data-studio/what-is.md)或[SQL Server Management Studio （SSMS）](../../ssms/sql-server-management-studio-ssms.md)使用 t-sql 和存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)来执行 R 脚本。
    + 在自己的开发便携式计算机或工作站上运行脚本。 可以从本地向下拉取数据，也可以远程推送执行，以便 SQL Server [RevoScaleR](../r/ref-r-revoscaler.md)。 有关详细信息，请参阅如何[设置数据科学客户端开发](../r/set-up-a-data-science-client.md)。

1. 编写第一个 R 脚本

    + 快速入门：[在 SQL Server 中创建和运行简单的 R 脚本](../tutorials/quickstart-r-create-script.md)
    + 快速入门：[在 R 中创建和训练预测模型](../tutorials/quickstart-r-train-score-model.md)
    + 教程：[在 t-sql 中使用 R](../tutorials/sqldev-in-database-r-for-sql-developers.md)：探索数据，执行特征工程，定型和部署模型，并进行预测（五部分系列）
    + 教程：[使用 r Services 中的 r Services](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)：探索数据，创建图形和绘图，执行特征工程，定型和部署模型，并进行预测（六部分系列）

## <a name="next-steps"></a>后续步骤

+ [安装 SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [为 R 开发设置数据科学客户端](../r/set-up-a-data-science-client.md)
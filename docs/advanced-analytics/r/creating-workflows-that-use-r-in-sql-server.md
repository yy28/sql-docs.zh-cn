---
title: 使用 R 的 SQL Server 机器学习服务创建商业智能 (BI) 工作流
description: 集成方案结合使用商业智能 (BI) 和 R 语言支持 SQL Server 和 SQL Server Integration Services (SSIS) 中。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 32dfb3317cb790c19289ab02362bf8ee765e5259
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432730"
---
# <a name="creating-bi-workflows-with-r"></a>使用 R 创建 BI 的工作流
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

关系数据库是一种高度优化的技术，用于交付进行事务处理、存储和数据查询的可缩放解决方案。

与此相反，传统上 R 解决方案通常依赖于从各种源，通常采用 CSV 格式，来执行进一步的数据浏览和建模导入数据。 这种做法不仅低效，而且不安全。

本文介绍适用于避免常见缺陷和可能发生数据库外部的开发机器学习解决方案的安全风险的 SQL Server 与 R 集成方案。

它还介绍了如何商业智能应用程序，值得注意的是 Integration Services 和 Reporting Services，可以使用 R 代码进行交互和使用数据或生成图形的示例

适用范围：SQL Server 2016 R Services、 SQL Server 2017 机器学习服务

## <a name="bring-compute-power-to-the-data"></a>引入数据的计算能力

将机器学习与 SQL Server 集成的一个主要设计目标是将接近于数据分析。 这提供了多个优点：

+ 数据安全性。 与数据源将 R 更接近避免了浪费性的或不安全的数据移动。

+ 速度。 数据库针对基于集的操作进行了优化。 如内存中表的数据库的最新创新请摘要和聚合既，和是对数据科学的完美补充。

+ 易于部署和集成。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是用于许多其他数据管理任务和应用程序的操作的中心点。 通过使用驻留在数据库或报告仓库中的数据，可以确保使用机器学习解决方案的数据是一致且最新。 

+ 跨云和本地的效率。 你可以依靠包括 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 Azure 数据工厂的企业数据管道，而非在 R 中处理数据。 可以通过 Power BI 或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 轻松执行结果报告或分析。

通过恰当地组合 SQL 和 R 来执行不同的数据处理和分析任务，数据科学家和开发人员变得更加高效。

## <a name="use-integration-services-for-data-transformation-and-automation"></a>使用 Integration Services 的数据转换和自动化

数据科学工作流具有高迭代性，并涉及许多数据转换操作，包括缩放、聚合、概率的计算，以及属性的重命名和合并。 数据科学家习惯于使用 R、Python 或其他语言执行其中许多任务，但对企业数据执行此类工作流时需要与 ETL 工具和过程无缝集成。

由于 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 支持在 R 中通过 Transact-SQL 和存储过程运行复杂的操作，因此，你可以将特定于 R 的任务与现有的 ETL 过程集成，只需执行极少的重新开发工作。 而是在 R 中执行占用大量内存的任务链，数据准备可以优化使用最高效的工具，包括[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和[!INCLUDE[tsql](../../includes/tsql-md.md)]。 

以下是有关如何自动执行数据处理的一些观点和使用建模管道[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ 使用[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]任务在 SQL 数据库中创建必要的数据功能
+ 使用条件分支切换 R 作业的计算上下文
+ 运行 R 作业在数据库中，生成自己的数据和共享该数据与应用程序
+ 当使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，加载文本变量中保存的 R 脚本并在 SQL Server 中运行

### <a name="examples"></a>示例

[Operationalize your machine learning project using SQL Server 2016 SSIS and R Services](https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/)（使用 SQL Server 2016 SSIS 和 R Services 实施机器学习项目）  

这篇博客文章说明了操作 R 代码使用的基本方法[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]: 

+ 调用 R 使用执行 SQL 任务，生成数据并将其保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

+ 使用存储过程训练 R 模型并将其存储在数据库中

+ 使用“脚本任务”和“执行 SQL 任务”对模型执行评分

##  <a name="bkmk_ssrs"></a> 将 Reporting Services 用于可视化效果

虽然 R 可以创建图表和有趣的可视化效果，但如果没有与外部数据源良好地集成，就意味着必须单独生成每个图表或图形。 共享可能也比较困难。

借助 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，你可以在 R 中通过 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程运行复杂的操作，这些操作可通过各种企业报告工具（包括 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 Power BI）轻松处理。

+ 使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]直观显示从 R 脚本返回的图形对象
+ 在 Power BI 中使用表

### <a name="examples"></a>示例

[用于 Microsoft Reporting Services (SSRS) 的R Graphics Device](https://rgraphicsdevice.codeplex.com/)

此 CodePlex 项目提供了代码来帮助你创建自定义报表项，用以将 R 的图形输出呈现为可以在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表中使用的图像。  通过使用自定义报表，你可以：

+ 将使用 R Graphics Device 创建的图表和绘图发布到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 仪表板

+ 将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 参数传递到 R 绘图

> [!NOTE]
> 对于此示例，在 Reporting Services 服务器上，以及 Visual Studio 中，必须安装支持的 Reporting Services 的 R Graphics Device 的代码。 还需要进行手动编译和配置。

---
title: 数据科学方案和解决方案模板-SQL Server 机器学习
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c40d5d60d43739ccfa6fa326ba0ca1c2688543a6
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58509842"
---
# <a name="data-science-scenarios-and-solution-templates"></a>数据科学方案和解决方案模板
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

模板是演示最佳做法和提供构建基块，以帮助快速实现解决方案的示例解决方案。 每个模板旨在解决特定问题，为特定的纵向或行业。 每个模板中的任务从数据准备和特征工程扩展到模型定型和计分。 使用这些模板来了解如何[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]工作原理。 然后，随意自定义模板，使其适合自己的方案生成自定义解决方案。 

每个解决方案包括示例数据、 R 代码或 Python 代码，并有可能的话，SQL 存储过程。 完成 SQL Server 中的计算，可以在首选 R 或 Python 开发环境中，运行代码。 在某些情况下，可以运行代码直接使用 T-SQL 和任何 SQL 客户端工具，如 SQL Server Management Studio。

> [!TIP]
> 
> 大多数模板有多个版本支持在本地和云的机器学习平台。 例如，您可以生成使用只有 SQL Server 的解决方案也可以构建在 Microsoft R Server 或 Azure 机器学习中的解决方案。

+ 有关详细信息和更新，请参阅此公告：[在 Azure ML 中令人兴奋的新模板](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

+ 有关下载和安装说明，请参阅[如何使用模板](#bkmk_HowTo)。

## <a name="fraud-detection"></a>欺诈检测

[在线欺诈检测模板 (SQL Server R Services)](https://github.com/Microsoft/r-server-fraud-detection)

**什么：** 在线业务检测欺诈性交易的能力至关重要。 若要减少计费的损失，企业需要快速确定使用被盗的付款工具或凭据所执行的事务。 发现欺诈性交易后，企业通常会采取措施尽快地阻止某些帐户，以防止进一步损失。 在此方案中，您将了解如何使用在线购买交易中的数据来识别可能的欺诈行为。

**如何：** 将欺诈检测作为二分类问题解决。 此模板中使用的方法可以轻松地应用于其他域中的欺诈检测。


## <a name="campaign-optimization"></a>营销活动优化

[预测如何以及何时联系潜在客户](https://microsoft.github.io/r-server-campaign-optimization/)

**什么：** 此解决方案使用保险行业数据来预测潜在客户根据人口统计信息、 历史响应数据以及特定于产品的详细信息。  建议还会生成以指示最佳渠道和给方法的用户能够影响购买行为的时间。

**如何：** 该解决方案创建，并将多个模型进行比较。 自动化的数据集成和使用存储的过程的数据准备，还演示了该解决方案。 对于 SQL Server 中的数据库，在 Azure 中，和 HDInsight Spark 中提供的并行的示例。 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>美国卫生保健： 预测在医院住院天数 

[预测医院住院](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**什么：** 准确地预测哪些患者可能需要长期住院是护理和规划的一个重要部分。 管理员需要能够确定哪些设施需要更多资源，并且医护人员想要确保他们能够满足病人的需求。

**如何：** 此解决方案使用数据科学虚拟机，并使用已启用的机器学习中包含的 SQL Server 实例。 它还包括一组可用于与已部署的模型进行交互的 Power BI 报表。

## <a name="customer-churn"></a>客户流失

[客户流失预测模板 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/README.md)

**什么：** 分析和预测客户流失在必须管理和阻止的客户和竞争对手丢失任何行业中很重要： 银行业、 电信业和零售业，仅举几例。 流失分析的目的是确认哪些客户可能会流失，然后采取适当措施维系这些客户及其业务。

**如何：** 此模板表述为客户流失问题**二元分类**问题。 它使用来自于两个源，客户人口统计和客户交易记录的示例数据，将客户分为“可能”和“不太可能”流失两类。
  
## <a name="predictive-maintenance"></a>预测维护

[预测维护模板 (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/README.md)

**什么：** 预测性维护的目标是通过捕获以前的故障并将该信息来预测设备何时或在何处可能会失败来提高维护任务的效率。 尤其是有价值的应用程序依赖于分布式的数据或传感器预测设备过时的功能。 此方法还可以应用来监视或预测 IoT （物联网） 设备时出错。

此公告的详细信息，请参阅：[新的预测维护模板](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

**如何：** 该解决方案关注于回答这个问题，"当将目前提供计算机故障？" 输入数据表示飞机引擎的模拟传感器测量值。 获取从监视引擎的当前操作条件，如当前工作周期、 设置和传感器测量值的数据用于创建三种类型的预测模型：

-   **回归模型**，预测引擎在出现故障之前可持续的时间。 示例模型预测指标"剩余使用寿命"(RUL)，也称为"时间到失败"(TTF)。
  
-   **分类模型**，预测引擎是否可能出现故障。
  
    **二元分类模型**预测在某段时间内是否引擎将会失败。

    **多类分类模型**预测特定引擎是否可能会失败，并提供的可能时间窗口为失败。 例如，对于某个给定的日期，可以预测是否有任何设备可能会在那天出现故障，或者在其后某个时间段内出现故障。

## <a name="energy-demand-forecasting"></a>能源需求预测

[能源需求预测与 SQL Server R Services 模板](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**什么：**:需求预测是一个重要问题包括能源、 零售和服务的各个领域。 准确需求预测可帮助公司进行规划，资源分配的更好地生产并做出其他重要业务决策。 在能源行业，需求预测是减少能源存储成本和平衡供给和需求的关键。

**如何：** 此模板使用 SQL Server R Services 预测对电力的需求。 用于预测的模型是基于的随机林回归模型**rxDForest**、 高性能机器学习算法，包括 Microsoft R Server 中。 解决方案包括一个需求模拟器、用于定型模型的所有 R 和 T-SQL 代码以及可用于生成和报告预测的存储过程。 


## <a name="bkmk_HowTo"></a>如何使用模板

要下载每个模板中包含的文件，可以使用 GitHub 命令，或者可以打开链接，然后单击“下载 Zip 文件”将所有文件都保存到计算机。  下载后，解决方案通常会包含这些文件夹：
  
-   **数据**:包含每个应用程序的示例数据。
  
-   **R**:包含解决方案所需的所有 R 开发代码。 解决方案需要 Microsoft R Server 提供的库，但可以在任何 R IDE 中打开和编辑。 通过将计算上下文设置为 SQL Server 实例，R 代码已经过优化，以便在“数据库内”执行计算。
  
-   **SQLR**:包含多个.sql 文件，您可以如运行的 SQL 环境中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]若要创建的存储的过程执行相关的任务，例如数据处理，特征工程和模型部署。
  
    文件夹还包含 PowerShell 脚本，可以运行此脚本来调用所有脚本以及创建端到端环境。 请务必编辑脚本以适应环境。

## <a name="next-steps"></a>后续步骤

+ [SQL Server 机器学习教程](machine-learning-services-tutorials.md)





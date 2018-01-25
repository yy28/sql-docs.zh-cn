---
title: "数据科学方案和解决方案模板 |Microsoft 文档"
ms.custom: 
ms.date: 08/22/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
ms.assetid: 49e54fa9-9b28-44ba-b256-06dad4e8dece
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 3c180282735da59d8d3dfa039e70d0eea5ebd7e5
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="data-science-scenarios-and-solution-templates"></a>数据科学方案和解决方案模板

模板是演示最佳做法和提供构建基块，以帮助快速实现解决方案的示例解决方案。 每个模板用于解决特定问题，为特定的垂直或行业。 每个模板中的任务从数据准备和特征工程扩展到模型定型和计分。 使用这些模板来了解如何[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]工作原理。 然后，随意自定义模板以适合你自己的方案并生成自定义解决方案。 

每个解决方案包括示例数据、 R 代码或 Python 代码，并有可能的话，SQL 存储过程。 与 SQL Server 中完成的计算，可以在你首选 R 或 Python 开发环境中，运行代码。 在某些情况下，你可以运行代码直接使用 T-SQL 和任何 SQL 客户端工具，例如 SQL Server Management Studio。

> [!TIP]
> 
> 大多数模板有多个版本支持在本地和云平台机器学习。 例如，您可以生成使用仅 SQL Server 的解决方案，也可以生成解决方案在 Microsoft R Server 或 Azure 机器学习。

+ 有关详细信息和更新，请参阅此公告：[振奋人心 Azure ML 中的新模板](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

+ 有关下载和安装说明，请参阅[如何使用模板](#bkmk_HowTo)。

## <a name="fraud-detection"></a>欺诈检测

[联机欺诈行为检测模板 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)

**新增功能：**检测欺诈性交易的能力是针对在线业务重要。 若要减少计费的损失，企业需要快速确定使用被盗的付款方式或凭据所执行的事务。 发现欺诈性交易后，企业通常会采取措施尽快地阻止某些帐户，以防止进一步损失。 在此方案中，你将了解如何使用在线购买事务中的数据来标识可能的欺诈行为。

**如何：**欺诈行为检测是否为二元分类问题已解决。 此模板中使用的方法可以轻松地应用于其他域中的欺诈检测。


## <a name="campaign-optimization"></a>营销活动优化

[预测何时以及如何联系主管](https://microsoft.github.io/r-server-campaign-optimization/)

**新增功能：**此解决方案使用保险行业数据来预测基于人口统计信息、 历史响应数据和特定于产品的详细信息的主管。  建议还会生成以指示最佳的通道和向方法用户影响购买行为的时间。

**如何：**解决方案创建，并将多个模型进行比较。 自动化的数据集成和使用存储的过程的数据准备，还演示了解决方案。 为 SQL Server 数据库中，在 Azure 和 HDInsight Spark 提供了并行示例。 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>卫生保健： 预测医院保持状态的长度 

[预测医院保持状态的长度](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**新增功能：**准确预测哪些患者可能需要长期医疗是保健和规划的一个重要部分。 管理员需要能够确定哪些功能需要更多资源，并且医护人员想要确保它们可以满足患者的需求。

**如何：**此解决方案使用数据科学虚拟机，并且与启用的机器学习中包括的 SQL Server 实例。 它还包括一组可用于与已部署的模型进行交互的 Power BI 报表。

## <a name="customer-churn"></a>客户改动

[客户改动预测模板 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/Introduction.md)

**新增功能：**分析和预测客户改动率很重要中必须管理和阻止的客户将你的竞争对手丢失任何行业： 银行、 电信和零售，仅举几例。 流失分析的目的是确认哪些客户可能会流失，然后采取适当措施维系这些客户及其业务。

**如何：**此模板依照改动问题**二元分类**问题。 它使用来自于两个源，客户人口统计和客户交易记录的示例数据，将客户分为“可能”和“不太可能”流失两类。
  
## <a name="predictive-maintenance"></a>预测维护

[预测维护模板 (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/Introduction.md)

**新增功能：**预测维护旨在提高通过捕获过去的失败并使用该信息来预测何时或在何处设备可能会失败的维护任务的效率。 为了便于预测设备过时的能力是特别有价值的应用程序依赖于分布式的数据或传感器。 此外可以应用此方法来监视或预测 IoT （物联网） 设备中的错误。

请参阅此公告的详细信息：[新预测维护模板](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

**如何：**本解决方案重点介绍回答这个问题，"时将一个服务中的计算机失败？" 输入数据表示飞机引擎的模拟传感器测量值。 获取从监视引擎的当前操作条件，如当前工作周期、 设置和传感器度量数据用于创建三种类型的预测模型：

-   **回归模型**，预测引擎在出现故障之前可持续的时间。 示例模型预测的度量值"剩余使用年限"(RUL)，也称为"时间到失败"(TTF)。
  
-   **分类模型**，预测引擎是否可能出现故障。
  
    **二元分类模型**预测是否引擎将在某段时间内失败。

    **多类分类模型**预测特定引擎是否可能会失败，并提供可能的时间窗口为失败。 例如，对于某个给定的日期，可以预测是否有任何设备可能会在那天出现故障，或者在其后某个时间段内出现故障。

## <a name="energy-demand-forecasting"></a>能源需求预测

[能量需预测具有 SQL Server R Services 模板](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**新增功能：**： 需求预测是包括能量、 零售版和服务的各个域中的重要问题。 准确需求预测可帮助公司进行规划，资源分配的更好生产和其他重要的业务决定。 能量扇区，在需求预测至关重要减少存储的能源成本和平衡供应和需求。

**如何：**此模板使用 SQL Server R Services 来预测的电力需求。 用于预测的模型是基于的随机林回归模型**rxDForest**的高性能机器学习 Microsoft R Server 内包含的算法。 解决方案包括一个需求模拟器、用于定型模型的所有 R 和 T-SQL 代码以及可用于生成和报告预测的存储过程。 


## <a name="bkmk_HowTo"></a>如何使用模板

要下载每个模板中包含的文件，可以使用 GitHub 命令，或者可以打开链接，然后单击“下载 Zip 文件”将所有文件都保存到计算机。  下载后，解决方案通常会包含这些文件夹：
  
-   **Data**：包含用于每个应用程序的示例数据。
  
-   **R**：包含解决方案所需的所有 R 开发代码。 解决方案需要 Microsoft R Server 提供的库，但可以在任何 R IDE 中打开和编辑。 通过将计算上下文设置为 SQL Server 实例，R 代码已经过优化，以便在“数据库内”执行计算。
  
-   **SQLR**：包含多个.sql 文件，可以在如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 之类的 SQL 环境中运行这些文件，以创建执行相关任务（如数据处理、特征工程和模型部署）的存储过程。
  
    文件夹还包含 PowerShell 脚本，可以运行此脚本来调用所有脚本以及创建端到端环境。 请务必编辑脚本以适应环境。

## <a name="next-steps"></a>后续步骤

+ [SQL Server 机学习教程](machine-learning-services-tutorials.md)





---
title: 数据科学方案和解决方案模板
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: cb144eb5c766b417884f6f1adb67dc0ac48504a5
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469780"
---
# <a name="data-science-scenarios-and-solution-templates"></a>数据科学方案和解决方案模板
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

模板是演示最佳做法和提供构建基块，以帮助快速实现解决方案的示例解决方案。 每个模板设计用于解决特定的纵向或行业的特定问题。 每个模板中的任务从数据准备和特征工程扩展到模型定型和计分。 使用这些模板了解[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]工作原理。 然后, 可以根据自己的方案随意自定义模板, 并构建自定义解决方案。 

每个解决方案都包含示例数据、R 代码或 Python 代码以及 SQL 存储过程 (如果适用)。 可以在首选的 R 或 Python 开发环境中运行代码, 并在 SQL Server 进行计算。 在某些情况下, 可以使用 T-sql 和任何 SQL 客户端工具 (如 SQL Server Management Studio) 直接运行代码。

> [!TIP]
> 
> 大多数模板都有多个版本, 支持本地和云平台以进行机器学习。 例如, 您可以仅使用 SQL Server 生成解决方案, 也可以在 Microsoft R Server 或 Azure 机器学习中生成解决方案。

+ 有关下载和设置说明, 请参阅[如何使用模板](#bkmk_HowTo)。

## <a name="fraud-detection"></a>欺诈检测

[在线欺诈检测模板 (SQL Server R Services)](https://github.com/Microsoft/r-server-fraud-detection)

**究竟**检测欺诈性交易的能力对于在线企业非常重要。 为了降低损失损失, 企业需要快速识别使用盗用支付票据或凭据进行的交易。 发现欺诈性交易后，企业通常会采取措施尽快地阻止某些帐户，以防止进一步损失。 在此方案中, 您将学习如何使用在线购买交易中的数据来识别可能的欺诈行为。

**帮助**将欺诈检测作为二分类问题解决。 此模板中使用的方法可以轻松地应用于其他域中的欺诈检测。


## <a name="campaign-optimization"></a>市场活动优化

[预测与潜在客户联系的方式和时间](https://microsoft.github.io/r-server-campaign-optimization/)

**究竟**此解决方案使用保险行业数据根据人口统计信息、历史响应数据和产品特定的详细信息预测潜在顾客。  还会生成建议, 用于指示用户影响购买行为的最佳渠道和时间。

**帮助**解决方案创建并比较多个模型。 此解决方案还演示了如何使用存储过程实现自动化数据集成和数据准备。 为在数据库中、在 Azure 和 HDInsight Spark 中 SQL Server 提供并行示例。 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>卫生保健: 预测位于医院中的时长 

[预测位于医院中的时长](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**究竟**准确预测哪些患者可能需要长期住院是护理和规划的重要组成部分。 管理员需要能够确定哪些设施需要更多的资源, 而医护人员需要确保他们能够满足患者的需求。

**帮助**此解决方案使用 Data Science Virtual Machine, 并包括启用了机器学习的 SQL Server 的实例。 它还包括一组可用于与已部署的模型进行交互的 Power BI 报表。

## <a name="customer-churn"></a>客户流失

[客户流失预测模板 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/README.md)

**究竟**分析和预测客户流失在任何行业中都很重要, 即必须管理和阻止客户丢失的客户: 银行、电信和零售等。 流失分析的目的是确认哪些客户可能会流失，然后采取适当措施维系这些客户及其业务。

**帮助**此模板将改动问题形成为**二元分类**问题。 它使用来自于两个源，客户人口统计和客户交易记录的示例数据，将客户分为“可能”和“不太可能”流失两类。
  
## <a name="predictive-maintenance"></a>预测维护

[预测维护模板 (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/README.md)

**究竟**预测性维护旨在通过捕获过去的故障并使用该信息来预测设备可能出现故障的时间或位置, 提高维护任务的效率。 对于依赖于分布式数据或传感器的应用程序, 预测设备过时功能特别有用。 此方法还可用于监视或预测 IoT (物联网) 设备中的错误。

**帮助**此解决方案侧重于回答问题 "服务内计算机何时出现故障？" 输入数据表示飞机引擎的模拟传感器测量值。 从监视引擎的当前操作条件 (如当前工作周期、设置和传感器度量) 中获取的数据用于创建三种类型的预测模型:

-   **回归模型**，预测引擎在出现故障之前可持续的时间。 示例模型预测指标 "剩余的可用寿命" (RUL), 也称为 "失败时间" (.TTF)。
  
-   **分类模型**，预测引擎是否可能出现故障。
  
    **二元分类模型**预测引擎在某个时间范围内是否会失败。

    **多类分类模型**预测特定引擎是否可能会失败, 并提供可能的故障时间范围。 例如，对于某个给定的日期，可以预测是否有任何设备可能会在那天出现故障，或者在其后某个时间段内出现故障。

## <a name="energy-demand-forecasting"></a>能源需求预测

[具有 SQL Server R Services 的能源需求预测模板](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**内容:** 需求预测是各种领域 (包括能源、零售和服务) 中的一个重要问题。 准确的需求预测可帮助公司进行更好的生产规划、资源分配, 并做出其他重要的业务决策。 在能源领域, 需求预测对于降低能源存储成本和平衡供应和需求非常重要。

**帮助**此模板使用 SQL Server R Services 预测电力需求。 用于预测的模型是一个随机林回归模型, 该模型基于**rxDForest**, 这是 Microsoft R Server 中包含的高性能机器学习算法。 解决方案包括一个需求模拟器、用于定型模型的所有 R 和 T-SQL 代码以及可用于生成和报告预测的存储过程。 


## <a name="bkmk_HowTo"></a>如何使用模板

要下载每个模板中包含的文件，可以使用 GitHub 命令，或者可以打开链接，然后单击“下载 Zip 文件”将所有文件都保存到计算机。  下载后，解决方案通常会包含这些文件夹：
  
-   **数据**:包含每个应用程序的示例数据。
  
-   **R**:包含解决方案所需的所有 R 开发代码。 解决方案需要 Microsoft R Server 提供的库，但可以在任何 R IDE 中打开和编辑。 通过将计算上下文设置为 SQL Server 实例，R 代码已经过优化，以便在“数据库内”执行计算。
  
-   **SQLR**:包含多个 .sql 文件, 您可以在 sql 环境 (例如) [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中运行这些文件, 以创建执行相关任务 (如数据处理、功能设计和模型部署) 的存储过程。
  
    文件夹还包含 PowerShell 脚本，可以运行此脚本来调用所有脚本以及创建端到端环境。 请务必编辑脚本以适应环境。

## <a name="next-steps"></a>后续步骤

+ [SQL Server 机器学习教程](machine-learning-services-tutorials.md)





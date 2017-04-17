---
title: "数据科学方案和解决方案模板 | Microsoft Docs"
ms.custom: 
ms.date: 04/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 49e54fa9-9b28-44ba-b256-06dad4e8dece
caps.latest.revision: 17
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0d82381261dabe370c6b34663bdf1f21d89664bf
ms.lasthandoff: 04/11/2017

---
# <a name="data-science-scenarios-and-solution-templates"></a>数据科学方案和解决方案模板
模板是演示最佳做法和提供构建基块，以帮助快速实现解决方案的示例解决方案。 每个模板都旨在解决特定问题，包括示例数据、R 代码 (Microsoft R Server) 和 SQL 存储过程。 每个模板中的任务从数据准备和特征工程扩展到模型定型和计分。 通过 SQL Server 中完成的计算或使用 SQL 客户端工具（如 SQL Server Management Studio ），可以在 R IDE 中运行代码。  
  
可以使用这些模板了解 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的工作原理，并通过自定义适应自己的方案的模板来生成和部署自己的解决方案。  
  
有关下载和安装说明，请参阅本主题末尾的 [如何使用模板](#bkmk_HowTo) 。  
  
## <a name="fraud-detection"></a>欺诈检测  
[在线欺诈检测模板 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)  
  
在线业务的重要任务之一是检测欺诈性交易，以及识别由被盗的付款工具或凭据进行的交易，减少退单损失。 发现欺诈性交易后，企业通常会采取措施尽快地阻止某些帐户，以防止进一步损失。 在此方案中，将学习如何使用在线购买交易中的数据来识别可能的欺诈行为。 这种方法是可轻松应用于其他域中欺诈检测的方法之一。  
  
在此模板中，将学习如何使用在线购买交易中的数据来识别可能的欺诈行为。 将欺诈检测作为二分类问题解决。 此模板中使用的方法可以轻松地应用于其他域中的欺诈检测。    
  
## <a name="customer-churn"></a>客户流失  
[客户流失预测模板 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/Introduction.md)  
  
分析和预测客户流失对于任何必须管理和防止客户流失到竞争对手的行业都非常重要，如：银行业、电信业和零售业等等。 流失分析的目的是确认哪些客户可能会流失，然后采取适当措施维系这些客户及其业务。  
  
此模板通过系统地阐述客户流失问题（如 **二分类** 问题），初步了解客户流失的预防。 它使用来自于两个源，客户人口统计和客户交易记录的示例数据，将客户分为“可能”和“不太可能”流失两类。   
  
## <a name="predictive-maintenance"></a>预测维护  
[预测维护模板 (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/Introduction.md)  
  
“数据驱动”预测维护的目的是通过捕获以前的故障并将该信息用于预测设备可能会出现故障的时间和位置，以此来提高维护任务的效率。 对于依赖于分布式数据或传感器的应用程序（以物联网 (IoT) 为例），预测设备过时的能力尤为重要。  
  
此模板的重点在于回答“服务中的计算机会在何时出现故障？”这一问题 输入数据表示飞机引擎的模拟传感器测量值。 通过监视引擎的当前操作条件（例如当前工作周期、设置、传感器测量值等）所获得的数据用于创建三种类型的预测模型：  
  
-   **回归模型**，预测引擎在出现故障之前可持续的时间。 示例模型预测指标剩余使用寿命 (RUL)，也称为故障时间 (TTF)。  
  
-   **分类模型**，预测引擎是否可能出现故障。  
  
    **二类分类模型** 预测在特定时间段（天数）内引擎是否会出现故障。  
  
    **多类分类模型** ，预测特定引擎是否会出现故障，以及如果出现故障，提供可能的故障时间窗口。 例如，对于某个给定的日期，可以预测是否有任何设备可能会在那天出现故障，或者在其后某个时间段内出现故障。  
      
      
## <a name="energy-demand-forecasting"></a>能量需求预测  
[使用 SQL Server R Services 的能量需求预测模板](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast_Template_with_SQL-Server-R-Services-1)  
  
此模板演示如何使用 SQL Server R Services 预测对电力的需求。 解决方案包括一个需求模拟器、用于定型模型的所有 R 和 T-SQL 代码以及可用于生成和报告预测的存储过程。   
  
## <a name="bkmk_HowTo"></a>如何使用模板  
要下载每个模板中包含的文件，可以使用 GitHub 命令，或者可以打开链接，然后单击“下载 Zip 文件”将所有文件都保存到计算机。  下载后，解决方案通常会包含这些文件夹：  
  
-   **Data**：包含用于每个应用程序的示例数据。  
  
-   **R**：包含解决方案所需的所有 R 开发代码。 解决方案需要 Microsoft R Server 提供的库，但可以在任何 R IDE 中打开和编辑。 通过将计算上下文设置为 SQL Server 实例，R 代码已经过优化，以便在“数据库内”执行计算。  
  
-   **SQLR**：包含多个.sql 文件，可以在如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 之类的 SQL 环境中运行这些文件，以创建执行相关任务（如数据处理、特征工程和模型部署）的存储过程。  
  
    文件夹还包含 PowerShell 脚本，可以运行此脚本来调用所有脚本以及创建端到端环境。  
  
    请务必编辑脚本以适应环境。  
  
  
## <a name="see-also"></a>另请参阅  
[SQL Server R Services 教程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
[在 Azure ML 中公告模板](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)  
[新的预测维护模板](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)  
  
  
  



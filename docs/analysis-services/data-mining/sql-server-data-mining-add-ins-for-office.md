---
title: SQL Server Office 数据挖掘外接程序 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2220bb48704fb29aa00236ebf1ec4ad46ecb4007
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34014734"
---
# <a name="sql-server-data-mining-add-ins-for-office"></a>SQL Server Office 数据挖掘外接程序

  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Office 数据挖掘外接程序是用于预测分析的一组轻型工具，允许您使用 Excel 中的数据生成分析模型来用于预测、建议或浏览。  
  
> [!IMPORTANT]
> 数据挖掘外接程序 Office 不支持 Office 2016 或更高版本。
  
 该外接程序中的向导和数据管理工具为以下这些常用的数据挖掘任务提供了分步说明：  
  
-   **建模前组织和清理你的数据。** 使用在 Excel 或任何 Excel 数据源中存储的数据。 可创建并保存连接以重用数据源、重复进行试验或将模型重新定型。  
  
-   **探查、抽样和准备。** 许多经验丰富的数据挖掘人员都说，一个数据挖掘项目中有百分之 70-90 的时间用在数据准备上。 该外接程序通过在 Excel 中提供可视化效果和帮助您完成以下这些常用任务的向导，可使此任务更快完成：  
  
    -   探查数据并了解其分布和特征。  
  
    -   通过随机抽样或过度抽样创建定型集和测试集。  
  
    -   找到离散值并删除或替换它们。  
  
    -   重新标记数据以提高分析质量。  
  
-   **通过监督的学习或无人监督的学习分析模式。** 单击用户友好的向导以便执行某些最常见数据挖掘任务，包括聚类分析、市场篮分析和预测。  
  
     该外接程序中包括的众所周知的计算机学习算法为 Naïve Bayes、逻辑回归、聚类分析、时序和神经网络。  
  
     如果您不熟悉数据挖掘，则可以使用 **“查询”** 向导帮助生成预测查询。  
  
     高级用户可通过拖放“高级查询编辑器”生成自定义 DMX 查询，或使用 Excel VBA 自动进行预测。  
  
-   **记载和管理。** 在您创建了某一数据集并且生成了一些模型后，通过生成数据和模型参数的统计摘要记录所做工作以及洞察到的情况。  
  
-   **浏览和展现。** 数据挖掘不是可完全自动进行的活动 - 需要探索并理解结果才能采取有意义的措施。 该外接程序帮助您探索各种内容，其中在 Excel、Visio 模板中提供交互式查看器，使您可自定义模型关系图，还可将图表和表导出到 Excel 供进一步筛选或修改。  
  
-   **部署和集成。** 创建有用的模型后，通过使用管理工具将该模型从试验服务器导出到另一个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例，将该模型投入生产。  
  
     您还可以将模型保留在服务器上创建它时的位置，但使用 Integration Services 或 DMX 脚本刷新定型数据并运行预测。  
  
     高级用户一定会感激 **“跟踪”** 功能，通过该功能，可看到发送到服务器的 XMLA 和 DMX 语句。  
  
## <a name="getting-started"></a>入门  
 有关详细信息，请参阅 [Office 数据挖掘外接程序中包含的功能](http://go.microsoft.com/fwlink/p/?LinkId=616849)  
  
## <a name="support-and-requirements"></a>支持和要求  
 可免费下载 SQL Server Office 数据挖掘外接程序。 必须已安装以下某个 Office 版本才能使用这些工具：  
  
-   Office 2010（32 位或 64 位版）  
  
-   Office 2013（32 位或 64 位版）  
  
> [!WARNING]  
>  请确保下载与您的 Excel 版本匹配的外接程序版本。  
  
 数据挖掘外接程序要求与以下 SQL Server Analysis Services 版本之一的连接：  
  
-   Enterprise  
  
-   Business Intelligence  
  
-   Standard  
  
 根据所连接的 SQL Server Analysis Services 版本，某些高级算法可能不可用。 有关信息，请参阅 [SQL Server 2016 各个版本支持的功能](../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。  
  
 有关安装的其他帮助，请参阅下载中心上此页面： [http://www.microsoft.com/download/details.aspx?id=29061](http://www.microsoft.com/download/details.aspx?id=29061)  
  
  

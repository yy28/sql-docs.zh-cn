---
title: 记录挖掘模型（Excel 数据挖掘外接程序） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- documenting models
- mining structures, managing
- mining models, managing
- model properties
ms.assetid: 0a663e11-e40c-4708-ad18-fabb6c976fa4
author: minewiskan
ms.author: owend
ms.openlocfilehash: 92ed5c43fa2b7484485b915d42946121487386d9
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528483"
---
# <a name="documenting-mining-models-data-mining-add-ins-for-excel"></a>记录挖掘模型（Excel 数据挖掘外接程序）
  ![“数据挖掘”功能区中的“文档模型”按钮](media/dmc-docmodel.gif "“数据挖掘”功能区中的“文档模型”按钮")  
  
 **文档模型**向导将创建一个报表，该报表提供有关已创建的挖掘模型的有用信息。 通过记录创建的模型，不但可以跟踪用于生成模型的数据的源，获取有关模型处理时间的其他信息，还可以跟踪影响模型结果的参数更改。  
  
## <a name="using-the-document-model-wizard"></a>使用文档模型向导  
  
1.  单击 "**数据挖掘**" 选项卡。  
  
2.  在 "**模型用法**" 组中，单击 "**文档模型**"。  
  
3.  在 "**选择模型**" 对话框中，选择要报告的模型，然后单击 "**下一步**"。 您必须为要记录的每个模型单独运行**文档模型**向导。  
  
4.  在 "**选择文档详细信息**" 对话框中，选择以下两个选项之一：**完整信息**或**摘要信息**。  
  
5.  单击“完成”。  
  
6.  向导将自动创建一个新的工作表，其中包含名为**Model 文档**的指定报表  
  
## <a name="understanding-the-report"></a>了解报表  
 创建记录数据挖掘模型的报表时，可以创建包含基本信息（模型的名称和说明）的摘要，或者也可以创建包含基础结构详细信息和挖掘模型高级信息的完整报表。  
  
 会根据创建模型所使用的算法，提供有不同类型的信息。 例如，在关联模型中，您可能对了解生成的项集数和规则数更感兴趣。 在聚类分析模型中，可能会对分类数更感兴趣。  
  
 下表列出了各选项以及报表中提供的每个选项的信息。  
  
> [!NOTE]  
>  默认情况下，该报表中的列设置为特定大小。 因此，如果列名或值很长，则在 Excel 中有可能不可见或显示为 ###。 您可以调整行的大小使值可见。 如果选择了单元格，则可以单击并拖动编辑栏右端的双箭头，以显示完整的值或字符串。  
  
### <a name="summary-report"></a>摘要报表  
  
||||  
|-|-|-|  
|**元数据**|模型名称<br /><br /> 模型说明<br /><br /> 算法名称<br /><br /> 上次处理日期||  
|**模型结果**|关联|项集计数<br /><br /> 规则计数|  
||群集|分类计数<br /><br /> 对每个分类的支持|  
||决策树|树数<br /><br /> 每个树中的节点数|  
||线性回归|树数（始终为 1）<br /><br /> 节点数（始终为 1）|  
||Naïve Bayes|重要属性|  
||神经网络|输入节点数<br /><br /> 输出节点数<br /><br /> 隐藏节点数|  
||顺序分析和聚类分析|分类数|  
  
### <a name="complete-report"></a>完整报表  
 完整报表包含摘要报表中的所有内容，此外还有模型中使用的数据列的详细信息以及分析的结果：  
  
||||  
|-|-|-|  
|**元数据**|模型元数据|算法参数和值|  
||列元数据|列名称<br /><br /> 使用情况<br /><br /> 数据类型<br /><br /> 内容类型<br /><br /> 值（离散值的列表或值的范围）|  
|**模型统计信息**|连续列|平均值<br /><br /> 最小值<br /><br /> 最大值<br /><br /> 均方根误差<br /><br /> 平均绝对误差<br /><br /> 对数评分<br /><br /> 回归公式（仅用于线性回归模型）|  
||离散列|传递计数<br /><br /> 失败计数<br /><br /> 对数评分<br /><br /> 提升|  
  
> [!NOTE]  
>  您可以记录 SQL Server Analysis Services 支持的任何模型类型。 因此，该表列出了使用表分析工具或数据挖掘客户端中的向导无法创建的某些模型类型。 不过，您可以使用**高级数据挖掘查询编辑器**创建所有模型类型。 有关详细信息，请参阅[查询 &#40;SQL Server 数据挖掘外接程序&#41;](query-sql-server-data-mining-add-ins.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Excel 数据挖掘外接程序部署和缩放挖掘模型&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  

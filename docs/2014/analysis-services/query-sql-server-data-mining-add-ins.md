---
title: 查询 （SQL Server 数据挖掘外接程序） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- queries [data mining]
- Data Mining Query Advanced Editor
- query builder [data mining]
- DMX
ms.assetid: 16af4a6f-18d4-496a-a304-7a13aa32ee76
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d2314c847745ac51d1bc7fb99b7c6f55a3f061af
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124875"
---
# <a name="query-sql-server-data-mining-add-ins"></a>查询（SQL Server 数据挖掘外接程序）
  ![查询模型按钮，数据挖掘功能区](media/dmc-query.gif "查询模型按钮，数据挖掘功能区")  
  
 **查询**向导可帮助你与现有的挖掘模型进行预测基于的 Excel 表，Excel 区域或另一个数据源中的数据进行交互。 将新的数据应用于现有模型来预测趋势的过程称为*预测查询*。  
  
 **查询**向导还将提供的高级的编辑器来创建或修改数据挖掘模型、 生成自定义查询，或使用其他工具，如嵌套数据集不支持的结构。  
  
-   使用文本编辑器可以键入数据挖掘扩展插件 (DMX) 语句或粘贴在别处创建的数据挖掘扩展插件语句。  
  
-   使用交互式查询生成器可在模版和对话框的帮助下编写自定义 DMX 语句。  
  
-   创建 DMX 语句来管理或备份挖掘模型和结构。  
  
## <a name="using-the-query-wizard"></a>使用查询向导  
  
1.  首先，必须指定要用作输入的数据的源。 您可以使用现有 Excel 表或区域中的数据，也可以指定一个 SQL 语句来检索数据。  
  
2.  然后，该向导提供一组要连接到的服务器上的数据挖掘模型。 如果你知道你想并熟悉数据挖掘模型，您也可以单击**高级**以打开**数据挖掘高级查询编辑器**。  
  
3.  根据选择的模型类型，您必须指定包含要计算的数据的列，并且定义输入数据列与模型列之间的映射。 根据选择的算法，您可以设置模型的其他属性。  
  
4.  最后，还可以通过该向导选择一个或多个预测，并且指定存储结果的目标。  
  
 在任何时候，你可以单击**高级**切换到**数据挖掘高级查询编辑器**，它会为你提供更好地控制 DMX 语句的每个部分。 有关如何使用高级的查询编辑工具的详细信息，请参阅[高级数据挖掘查询编辑器](advanced-data-mining-query-editor.md)。  
  
### <a name="requirements"></a>要求  
 若要使用**查询**向导，您必须连接到的实例[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。 此外，服务器必须至少包含一个具有适当类型的数据挖掘模型。 如果没有可用的挖掘模型，您可以使用 Excel 数据挖掘客户端中提供的向导创建一个。 有关如何使用向导创建新的挖掘模式的信息，请参阅[创建数据挖掘模型](creating-a-data-mining-model.md)。  
  
## <a name="see-also"></a>请参阅  
 [部署和缩放挖掘模型&#40;数据挖掘的 Excel 外接程序&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)   
 [Excel 数据挖掘客户端&#40;SQL Server 数据挖掘外接程序&#41;](data-mining-client-for-excel-sql-server-data-mining-add-ins.md)  
  
  
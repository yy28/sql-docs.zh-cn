---
title: 保存数据挖掘查询结果对话框 （挖掘模型预测视图） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.dm.savedataminingqueryresult.f1
helpviewer_keywords:
- Save Data Mining Query Result dialog box
ms.assetid: 112fb527-7466-4fd4-9cf1-75596135648f
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 709c3364ac5b4d6bc159af4ec6db40663d21fcbf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016944"
---
# <a name="save-data-mining-query-result-dialog-box-mining-model-prediction-view"></a>“保存数据挖掘查询结果”对话框（“挖掘模型预测”视图）
  使用 **“保存数据挖掘查询结果”** 对话框，可将数据挖掘查询的结果保存到新表中。  
  
 该新表将在数据源定义的数据库中创建。  
  
## <a name="options"></a>“常规”  
 **数据源**  
 从当前项目中选择数据源。 如果不存在正确的数据源，请单击 **“新建”** 以创建一个新的数据源。  
  
 **新建**  
 打开“数据源向导”。  
  
 **表名**  
 键入新表的名称。  
  
 **如果覆盖存在**  
 若要覆盖具有相同名称的现有表，则选择此选项。  
  
 如果下列任一条件成立，则需要覆盖现有表：  
  
-   您已向预测查询添加了列。  
  
-   您更改了预测查询中任何列的名称或数据类型。  
  
-   您对目标表运行了 ALTER 语句。  
  
 如果多个列具有相同的名称（例如多个派生列可能具有默认的列名 **Expression**），你必须为具有重复名称的每个列创建一个别名。 如果这些列没有唯一名称，则当设计器尝试将结果保存到 SQL Server 时将出错，因为表中的列必须要有唯一名称。  
  
 **将添加到 DSV**  
 （可选）如果希望将表添加到现有数据源中，请选择项目中包含的数据源视图。  
  
 如果您想在同一数据源中保留模型的所有相关表（如定型数据、预测源数据和查询结果），此选项很有用。  
  
## <a name="see-also"></a>请参阅  
 [预测查询生成器&#40;数据挖掘&#41;](prediction-query-builder-data-mining.md)   
 [数据挖掘查询接口](data-mining/data-mining-query-tools.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](/sql/dmx/data-mining-extensions-dmx-statements)  
  
  

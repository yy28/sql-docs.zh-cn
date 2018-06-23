---
title: 数据集属性对话框中，字段 |Microsoft 文档
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rtp.rptdesigner.datasetproperties.fields.f1
- "10140"
ms.assetid: e1367556-736e-4a6b-b9e7-10432a3e50b5
caps.latest.revision: 36
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 0006ff1564f6adbcadd529cd82e726d847ed646f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016095"
---
# <a name="dataset-properties-dialog-box-fields"></a>“数据集属性”对话框 -&gt;“字段”
  在 **“数据集属性”** 对话框中选择 **“字段”** 可更改报表数据集的字段集合。 尽管字段列表是自动填充的，但是可以使用 **“字段”** 来添加、编辑和删除查询及计算字段。  
  
## <a name="options"></a>“常规”  
 **“添加”**  
 将新查询字段或计算的字段添加到数据集。  
  
 **删除**  
 从数据集中删除所选字段。  
  
 **字段名称**  
 为字段键入名称。 该字段在数据集中必须是唯一的。 对于数据集查询中的每个现有字段，名称是预先填充的。  
  
 **字段源**  
 为字段输入一个值。  
  
 对于计算字段，字段源必须是由数据集查询检索的现有字段的名称或您所创建的表达式。 例如，若要创建表示 10 倍于查询字段 Sales 中值的字段，请使用表达式 `=10 * Fields!Sales.Value`。  
  
 对于查询字段，字段源必须是由数据集查询检索的现有字段的名称。  
  
 **表达式 (fx)**  
 添加或更改计算字段的表达式。 仅当单击 **“添加”** 并选择 **“计算字段”** 时，才会显示此按钮。  
  
## <a name="see-also"></a>请参阅  
 [数据集字段集合（报表生成器和 SSRS）](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [向报表添加数据&#40;报表生成器和 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [表达式（报表生成器和 SSRS）](report-design/expressions-report-builder-and-ssrs.md)  
  
  
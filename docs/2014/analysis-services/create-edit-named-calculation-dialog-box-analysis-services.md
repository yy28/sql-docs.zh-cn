---
title: 创建编辑命名计算对话框 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsveditor.createnamedcalculation.f1
helpviewer_keywords:
- Named Calculation dialog box
ms.assetid: 66fb30ae-f5c5-4bfc-80ca-8c8a3a9bb30d
caps.latest.revision: 21
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 42223e0a45e3e26c79e0d4d1cbcbfc0e81e92c4f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37232407"
---
# <a name="create-edit-named-calculation-dialog-box-analysis-services"></a>创建编辑命名计算对话框 (Analysis Services)
  可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的“创建/编辑命名计算”对话框，为数据源视图中的表定义或修改命名计算。 通过执行以下操作之一，可以显示“创建/编辑命名计算”对话框：  
  
-   在“数据源视图设计器”的“工具栏”窗格中，单击“新建命名计算”。  
  
-   右键单击“数据源视图设计器”的“表”窗格或“关系图”窗格中的表，再选择“新建命名计算”。  
  
-   右键单击“数据源视图设计器”的“关系图”窗格中某命名计算的名称，再选择“编辑命名计算”。  
  
## <a name="options"></a>“常规”  
 **列名**  
 键入命名计算的名称。  
  
 **Description**  
 键入命名计算的说明（可选）。  
  
 **表达式**  
 键入将返回标量值的有效的 SQL 表达式。 The expression is sent to the provider, and validated in the following expression:  
  
```  
SELECT <Table Name in Data Source>.* , <Expression> AS <Column Name> FROM <Table Name in Data Source>AS <Table Name in Data Source View>  
```  
  
 The expression can contain references to other tables, by means of a sub-select statement. If the expression would require parentheses in a SELECT statement, the expression entered must be enclosed between parentheses.  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [数据源视图设计器&#40;Analysis Services-多维数据&#41;](data-source-view-designer-analysis-services-multidimensional-data.md)  
  
  

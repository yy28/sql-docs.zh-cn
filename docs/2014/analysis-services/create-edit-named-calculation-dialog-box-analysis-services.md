---
title: 创建编辑命名计算对话框 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsveditor.createnamedcalculation.f1
helpviewer_keywords:
- Named Calculation dialog box
ms.assetid: 66fb30ae-f5c5-4bfc-80ca-8c8a3a9bb30d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a53db9413ce7877182ca5f9c768bb1e1ef71e383
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66086846"
---
# <a name="create-edit-named-calculation-dialog-box-analysis-services"></a>创建编辑命名计算对话框 (Analysis Services)
  可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的“创建/编辑命名计算”对话框，为数据源视图中的表定义或修改命名计算。 You can display the **Create/Edit Named Calculation** dialog box by:  
  
-   在“数据源视图设计器”的“工具栏”窗格中，单击“新建命名计算”。  
  
-   右键单击“数据源视图设计器”的“表”窗格或“关系图”窗格中的表，再选择“新建命名计算”。  
  
-   右键单击“数据源视图设计器”的“关系图”窗格中某命名计算的名称，再选择“编辑命名计算”。  
  
## <a name="options"></a>选项  
 **列名**  
 键入命名计算的名称。  
  
 **说明**  
 键入命名计算的说明（可选）。  
  
 **表达式**  
 键入将返回标量值的有效的 SQL 表达式。 The expression is sent to the provider, and validated in the following expression:  
  
```  
SELECT <Table Name in Data Source>.* , <Expression> AS <Column Name> FROM <Table Name in Data Source>AS <Table Name in Data Source View>  
```  
  
 The expression can contain references to other tables, by means of a sub-select statement. If the expression would require parentheses in a SELECT statement, the expression entered must be enclosed between parentheses.  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [数据源视图设计器（Analysis Services - 多维数据）](data-source-view-designer-analysis-services-multidimensional-data.md)  
  
  

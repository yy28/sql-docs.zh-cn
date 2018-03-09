---
title: "“查询参数”对话框 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdtsql.chm:69645
- vdt.dlgbox.definequeryparameters
ms.assetid: 31cdaee2-d7cd-4d64-a45f-924b27e8b1f0
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d75ed3debc9bb598ceb0a90147fc02d280f63d95
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2018
---
# <a name="query-parameters-dialog-box-visual-database-tools"></a>“查询参数”对话框 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 使用此对话框可为查询中定义的参数输入值。 在执行包含需要最终用户在运行时输入的参数的查询时，将显示此对话框。  
  
## <a name="options"></a>“常规”  
**名称**  
列出为正在执行的查询定义的参数。 如果该查询包含命名参数，则这些名称将显示在该列表中。 如果该查询包含未命名参数，则会为该查询中的每个参数列出系统定义的参数名称。  
  
**ReplTest1**  
为“名称”下列出的每个参数输入值。 最近所用的值将显示为默认的参数值。  
  
## <a name="example"></a>示例  
SQL 窗格中的以下查询在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject_md.md)] 数据库中执行时将打开“查询参数”对话框。  
  
```  
SELECT   FirstName, LastName  
FROM    Person.Person AS Lastname  
WHERE   (LastName = @Param1);  
```  
  
## <a name="see-also"></a>另请参阅  
[使用参数进行查询 (Visual Database Tools)](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
  

---
title: "“创建新条件”或“打开条件”对话框，“常规”页 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.dmf.condition.f1
ms.assetid: 106954bf-e4ba-412b-9c1a-907d06153dcd
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b90436634729185cf2703cc012aae3a4f0338cdb
ms.lasthandoff: 04/11/2017

---
# <a name="create-new-condition-or-open-condition-dialog-box-general-page"></a>“创建新条件”或“打开条件”对话框，“常规”页
  此对话框用于创建或更改基于策略的管理条件。 条件是一个布尔表达式，用于针对方面指定基于策略的管理目标的一组允许状态。 可在“表达式”/“字段”框中选择的属性取决于所使用的方面。 有关条件与方面和策略如何关联的详细信息，请参阅[使用基于策略的管理来管理服务器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)。  
  
## <a name="options"></a>选项  
 **名称**  
 对于新条件，请键入新条件的名称。 对于现有条件，将显示其名称。  
  
 **方面**  
 此条件所使用的方面。  
  
 **AndOr**  
 在添加多个表达式时，指示是否应使用 **And** 或 **Or**联接这些表达式。 如果只有一个表达式，将保留空白。  
  
 **字段**  
 每个方面公开一个或多个可设置的属性。 在“字段”框中，从可用属性列表中选择一个属性，为此条件创建一个表达式。  
  
 **运算符**  
 为该表达式选择一个比较运算符。 比较运算符包括：=、!=、>、>=、<、<=、[NOT]LIKE、[NOT]IN。 并非所有运算符都适用于某些属性。  
  
 **值**  
 该表达式的值设置。 允许的值取决于方面。 值可以为 TRUE/FALSE、字符串或数值。 字符串值必须用单引号引起来，例如： **'AdventureWorks'**。 并非所有运算符都适用于某些属性。  
  
## <a name="group-clauses"></a>子句分组  
 可以对子句进行分组，以使其作为独立于查询其余部分的一个单元来运行，就像在数学等式或逻辑语句中的表达式两侧加上括号一样。 在生成复杂查询时，对子句进行分组是非常有用的。  
  
 **对子句进行分组**  
  
-   按 Shift 或 Ctrl 键，然后单击两个或多个子句以选择一个范围。 右键单击所选区域，然后单击“子句分组”。  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来管理服务器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  

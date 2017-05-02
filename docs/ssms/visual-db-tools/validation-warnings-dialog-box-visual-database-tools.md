---
title: "“验证警告”对话框 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdtsql.chm:65556
- vdt.dlgbox.validationwarnings
ms.assetid: fc76e234-ec9c-4a19-a65b-cb558ec8268e
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 78aac0124cb34ac7699907df89c3251559bb79f8
ms.lasthandoff: 04/11/2017

---
# <a name="validation-warnings-dialog-box-visual-database-tools"></a>“验证警告”对话框 (Visual Database Tools)
如果尝试保存的修改具有潜在的破坏性副作用，或者数据库提交操作很可能会失败，则会显示此对话框。 此对话框可指示这些副作用可能会是什么或提交操作可能失败的原因。 使用此对话框可以选择继续修改还是取消操作。  
  
> [!NOTE]  
> 在尝试将修改传输到数据库或保存更改脚本时，将显示此对话框。  
  
以下任一原因都可能导致显示该对话框：  
  
-   您可能没有提交所有修改的数据库权限。  
  
-   您的修改将导致生成格式不正确的派生列、默认约束或 CHECK 约束。  
  
-   对列数据类型的修改可能导致数据丢失。  
  
-   修改可能导致索引大于 900 字节。  
  
-   修改将更改分配给绑定到架构的视图或用户定义函数的表或列。  
  
-   修改将导致重新创建具有一个或多个加密触发器的表；这些触发器将被删除。  
  
-   所做的修改将导致对一个表中的列的 ANSI_NULLS 或 ANSI_PADDING 选项进行重要设置，或同时对这两个选项进行设置。  
  
## <a name="options"></a>选项  
**是**  
继续操作以生成更改脚本或将修改传输到数据库。 提交操作在以下情况仍然会失败：您没有修改数据库的权限；所做的修改会导致索引大于 900 字节；或者修改会导致生成格式不正确的计算列、默认约束或 CHECK 约束。  
  
**“否”**  
取消保存操作。  
  
**保存文本文件**  
显示“另存为”****对话框，可以在其中为包含警告列表的文本文件指定位置。  
  
## <a name="see-also"></a>另请参阅  
[设计表 (Visual Database Tools)](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
[设计查询和视图操作指南主题 (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  


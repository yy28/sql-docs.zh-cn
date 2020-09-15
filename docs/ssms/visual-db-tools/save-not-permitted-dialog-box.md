---
description: “保存”（不允许）对话框
title: “保存”（不允许）对话框
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.table.tablerecreatenosave.f1
ms.assetid: 7efda8e3-739f-4c97-a497-b8808a0acbea
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 868925a64b24ab7f55551a691b4677a658082725
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88369083"
---
# <a name="save-not-permitted-dialog-box"></a>“保存”（不允许）对话框
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
“保存”（不允许）对话框警告不允许保存更改，因为所做的更改要求删除并重新创建列出的表****。  
  
以下操作可能要求重新创建表：  
  
-   在表中间添加一个新列  
  
-   删除列  
  
-   更改列为 Null 性  
  
-   更改列的顺序  
  
-   更改列的数据类型  
  
若要更改此选项，请在“工具”**** 菜单中单击“选项”****，展开“设计器”****，然后单击“表设计器和数据库设计器”****。 选中或清除“阻止保存要求重新创建表的更改”**** 复选框。  
  

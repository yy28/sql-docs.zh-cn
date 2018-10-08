---
title: “保存(不允许)”对话框 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.table.tablerecreatenosave.f1
ms.assetid: 7efda8e3-739f-4c97-a497-b8808a0acbea
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b491d5d0bf14c90d813b0fc66c0112eac1ff0e16
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47635295"
---
# <a name="save-not-permitted-dialog-box"></a>“保存”（不允许）对话框
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
“保存”（不允许）对话框警告不允许保存更改，因为所做的更改要求删除并重新创建列出的表。  
  
以下操作可能要求重新创建表：  
  
-   在表中间添加一个新列  
  
-   删除列  
  
-   更改列为 Null 性  
  
-   更改列的顺序  
  
-   更改列的数据类型  
  
若要更改此选项，请在“工具”菜单中单击“选项”，展开“设计器”，然后单击“表设计器和数据库设计器”。 选中或清除“阻止保存要求重新创建表的更改”复选框。  
  

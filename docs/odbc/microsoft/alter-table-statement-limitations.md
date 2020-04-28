---
title: ALTER TABLE 语句限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19afa8b07b0051de9ce45ec652ea337c0f689f52
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304696"
---
# <a name="alter-table-statement-limitations"></a>ALTER TABLE 语句限制
使用 dBASE 或 Paradox 驱动程序时，一旦创建了一个索引并添加了新记录，ALTER TABLE 语句就不能更改该表的结构，除非删除该索引并删除该表的内容。  
  
 Microsoft Excel 或文本驱动程序不支持 ALTER TABLE 语句。  
  
> [!NOTE]  
>  如果在不实现 Borland 数据库引擎的情况下使用 Paradox 驱动程序，则不支持 ALTER TABLE 语句;只允许使用 read 和 append 语句。

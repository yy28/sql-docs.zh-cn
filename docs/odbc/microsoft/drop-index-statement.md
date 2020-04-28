---
title: DROP INDEX 语句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DROP INDEX [ODBC]
- SQL grammar [ODBC], DROP INDEX
ms.assetid: cd0ff767-9254-413b-bd1a-bed26c6774f5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 638bae6491c020519a0123ff56fe31e9a9ca1cf7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303428"
---
# <a name="drop-index-statement"></a>DROP INDEX 语句
当使用 Microsoft Access、dBASE 或 Paradox 驱动程序时，DROP INDEX 语句的语法为 "DROP INDEX b"，其中 "a" 是索引的名称，"b" 是表的名称（不是 DROP INDEX*索引名称*）。  
  
 使用 Paradox 驱动程序时，DROP INDEX 语句会删除 Paradox 的辅助索引文件。  
  
 Microsoft Excel 或文本驱动程序不支持 DROP INDEX 语句。

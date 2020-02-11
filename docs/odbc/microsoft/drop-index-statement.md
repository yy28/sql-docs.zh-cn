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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 23823e53e516324832c79706e6171b48a9c5297c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071863"
---
# <a name="drop-index-statement"></a>DROP INDEX 语句
当使用 Microsoft Access、dBASE 或 Paradox 驱动程序时，DROP INDEX 语句的语法为 "DROP INDEX b"，其中 "a" 是索引的名称，"b" 是表的名称（不是 DROP INDEX*索引名称*）。  
  
 使用 Paradox 驱动程序时，DROP INDEX 语句会删除 Paradox 的辅助索引文件。  
  
 Microsoft Excel 或文本驱动程序不支持 DROP INDEX 语句。

---
title: CREATE INDEX 语句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6aa512ff789fcbd00f45f84fb194d4ab3f5da07
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280967"
---
# <a name="create-index-statement"></a>CREATE INDEX 语句
CREATE INDEX 语句的语法为：  
  
 CREATE [UNIQUE] 索引*索引-* *表名*上的名称（*列标识符*[asc] [DESC] [，*列标识符*[asc] [desc] ...]）带有\<*索引选项列表*>  
  
 其中\<*索引选项列表*> 可以是：主 &#124; 不允许 null &#124; 忽略 null  
  
 只有 Microsoft Access 驱动程序使用 "不允许 NULL" 和 "忽略 NULL 索引" 选项。 DBASE 和 Paradox 驱动程序接受语法，但忽略其中一个选项。  
  
 使用 Paradox 驱动程序时，CREATE INDEX 语句会创建 Paradox 主键文件和辅助文件。  
  
 Microsoft Excel 或文本驱动程序不支持此语句。

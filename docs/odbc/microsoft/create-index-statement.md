---
description: CREATE INDEX 语句
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
ms.openlocfilehash: 7a3f5a13624cdb137e8c86cf2c27044c6705298f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483630"
---
# <a name="create-index-statement"></a>CREATE INDEX 语句
CREATE INDEX 语句的语法为：  
  
 CREATE [UNIQUE] 索引 *索引-* *表* 名 (*列标识符* [asc] [desc] [， *列标识符* [asc] [desc] ...]) \<*index option list*>  
  
 其中 \<*index option list*> 可以是：主 &#124; 不允许为 null &#124; 忽略 null  
  
 只有 Microsoft Access 驱动程序使用 "不允许 NULL" 和 "忽略 NULL 索引" 选项。 DBASE 和 Paradox 驱动程序接受语法，但忽略其中一个选项。  
  
 使用 Paradox 驱动程序时，CREATE INDEX 语句会创建 Paradox 主键文件和辅助文件。  
  
 Microsoft Excel 或文本驱动程序不支持此语句。

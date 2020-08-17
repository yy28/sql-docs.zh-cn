---
description: DELETE 语句限制
title: DELETE 语句限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5ffb3a6d0ab28fc2b8bc8785df586ac6bbc86aa0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340893"
---
# <a name="delete-statement-limitations"></a>DELETE 语句限制
Microsoft Excel 或文本驱动程序不支持 DELETE 语句。 请注意，文本驱动程序支持 INSERT 语句。  
  
 DBASE 驱动程序不支持对表进行封装以删除 "已删除" 值。  
  
 对于 Paradox 驱动程序，要从表中删除行，表必须具有唯一索引 (Paradox 主键) 。

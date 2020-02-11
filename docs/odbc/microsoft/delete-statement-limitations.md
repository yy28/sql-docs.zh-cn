---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: eb2587f733f5042436144f7865627fee576e3d9c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096314"
---
# <a name="delete-statement-limitations"></a>DELETE 语句限制
Microsoft Excel 或文本驱动程序不支持 DELETE 语句。 请注意，文本驱动程序支持 INSERT 语句。  
  
 DBASE 驱动程序不支持对表进行封装以删除 "已删除" 值。  
  
 要使 Paradox 驱动程序删除表中的行，表必须具有唯一索引（Paradox 主键）。

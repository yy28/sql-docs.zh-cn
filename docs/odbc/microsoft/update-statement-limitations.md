---
title: 更新语句限制 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ddf19c0b672901b2e778833f8bf624996d4ced3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307618"
---
# <a name="update-statement-limitations"></a>UPDATE 语句限制
要更新表，表必须具有唯一索引（悖论主键）。 当您在不实现 Borland 数据库引擎的情况下使用悖论驱动程序时，无法更新 Paradox 表。  
  
 文本驱动程序不支持。  
  
 使用 Microsoft Excel 驱动程序时，可以更新值，但不能从基于 Microsoft Excel 电子表格的表中删除行。 因此，Microsoft Excel 驱动程序不认为 UPDATE 语句不受官方支持。 只有 INSERT 语句被视为受支持。

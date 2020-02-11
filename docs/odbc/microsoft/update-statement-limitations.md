---
title: UPDATE 语句限制 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1cc8cf58d4e4d826dc4b152e395dedbea395a095
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088206"
---
# <a name="update-statement-limitations"></a>UPDATE 语句限制
为了使 Paradox 驱动程序更新表，表必须具有唯一索引（Paradox 主键）。 使用 Paradox 驱动程序时，如果不实现 Borland 数据库引擎，将无法更新 Paradox 表。  
  
 不受文本驱动程序支持。  
  
 当使用 Microsoft Excel 驱动程序时，可能会更新值，但无法基于 Microsoft Excel 电子表格从表中删除行。 因此，Microsoft Excel 驱动程序不会将 UPDATE 语句视为正式支持。 仅将 INSERT 语句视为受支持。

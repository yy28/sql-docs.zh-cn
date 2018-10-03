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
manager: craigg
ms.openlocfilehash: a6b854cc417898c5576c60ca129c597eae280df4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826335"
---
# <a name="update-statement-limitations"></a>UPDATE 语句限制
Paradox 驱动程序更新的表，该表必须具有唯一索引 （Paradox 主键）。 当您使用 Paradox 驱动程序而无需实现 borland 公司数据库引擎时，不能更新 Paradox 表。  
  
 不支持文本驱动程序。  
  
 使用 Microsoft Excel 驱动程序时，它可以更新值，但不能从基于 Microsoft Excel 电子表格的表中删除行。 因此，UPDATE 语句不被视为正式支持的 Microsoft Excel 驱动程序。 仅在 INSERT 语句被视为受支持。

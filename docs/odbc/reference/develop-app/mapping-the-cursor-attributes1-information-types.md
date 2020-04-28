---
title: 映射 Cursor Attributes1 信息类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], mapping cursor attributes1 information types
- application upgrades [ODBC], mapping cursor attributes1 information types
- mapping cursor attributes1 information types [ODBC]
- backward compatibility [ODBC], mapping cursor attributes1 information types
- upgrading applications [ODBC], mapping cursor attributes1 information types
ms.assetid: 9f112449-ca86-45ac-a865-e6174d67f91b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d70cf0a93a6c6160faeb0afe991b2adfff11b8f1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301040"
---
# <a name="mapping-the-cursor-attributes1-information-types"></a>映射游标 Attributes1 信息类型
ODBC 3 时*x*应用程序使用 SQL_XXXX_CURSOR_ATTRIBUTES1 信息类型（对于动态、只进、键集驱动程序或静态游标）在 ODBC*2.x 驱动程序*中调用**SQLGetInfo** ，驱动程序管理器返回的位数取决于 ODBC 2 的内容。*x*驱动程序为相应的 ODBC 2 返回。*x*信息类型。 按下表中所示设置位。  
  
|位在<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|游标类型|ODBC 2。*x*信息<br /><br /> type|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|全部|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE SQL_CA1_BOOKMARK|动态、键集驱动程序、静态|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|动态、键集驱动程序、静态|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE SQL_CA1_SELECT_FOR_UPDATE|全部|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|动态、键集驱动程序、静态|SQL_POS_OPERATIONS|

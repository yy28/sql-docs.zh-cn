---
title: 映射光标属性1信息类型 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301040"
---
# <a name="mapping-the-cursor-attributes1-information-types"></a>映射游标 Attributes1 信息类型
当一个ODBC 3。*x*应用程序在 ODBC 2 *.x*驱动程序中调用**SQLGetInfo，** 该驱动程序具有SQL_XXXX_CURSOR_ATTRIBUTES1信息类型（对于动态、仅转发、键集驱动程序或静态游标），驱动程序管理器返回的位设置取决于 ODBC 2 的内容。*x*驱动程序返回相应的 ODBC 2。*x*信息类型。 位设置为下表所示。  
  
|位<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|光标类型|ODBC 2.*x*信息<br /><br /> type|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|全部|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARK|动态键集驱动程序，静态|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_UNLOCKSQL_CA1_LOCK_UNLOCKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVE|动态键集驱动程序，静态|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATE|全部|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITIONSQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POS_BULK_ADD|动态键集驱动程序，静态|SQL_POS_OPERATIONS|

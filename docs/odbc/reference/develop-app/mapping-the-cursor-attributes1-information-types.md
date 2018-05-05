---
title: 将光标 Attributes1 信息类型映射 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], mapping cursor attributes1 information types
- application upgrades [ODBC], mapping cursor attributes1 information types
- mapping cursor attributes1 information types [ODBC]
- backward compatibility [ODBC], mapping cursor attributes1 information types
- upgrading applications [ODBC], mapping cursor attributes1 information types
ms.assetid: 9f112449-ca86-45ac-a865-e6174d67f91b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec986c2feea1b5c2ef64de87d64944ce0d184898
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="mapping-the-cursor-attributes1-information-types"></a>将光标 Attributes1 信息类型映射
当一个 ODBC 3。*x*应用程序调用**SQLGetInfo** ODBC 2 中 *.x* SQL_XXXX_CURSOR_ATTRIBUTES1 信息类型的驱动程序 (对于动态、 只进、 键集-驱动程序，或静态游标） 返回由驱动程序管理器中的位设置依赖于哪些 ODBC 2。*x*驱动程序将返回相应的 ODBC 2。*x*信息类型。 位将设置以下表中所示。  
  
|中的位<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|游标类型|ODBC 2。*x*信息<br /><br /> type|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|全部|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE SQL_CA1_BOOKMARK|动态的键集驱动程序静态|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|动态的键集驱动程序静态|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE SQL_CA1_SELECT_FOR_UPDATE|全部|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|动态的键集驱动程序静态|SQL_POS_OPERATIONS|

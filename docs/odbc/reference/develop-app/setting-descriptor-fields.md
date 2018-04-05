---
title: 设置描述符字段 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: d735dc64-370f-48ab-a59f-6cef9bc4e1e8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fc02690bd62802f9d356851cd85522328107a707
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="setting-descriptor-fields"></a>设置描述符字段
若要修改的描述符字段，应用程序可以调用**SQLSetDescField**。 某些字段是只读的且无法进行设置。 (请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)函数说明。)  
  
 将描述符记录字段时，都设置记录编号 (*RecNumber*) 描述符标头字段使用记录号 0 的 1 个或更高版本，时间的设置。 记录号 0 还用于设置书签字段，根据在第 0 列包含书签的约定。 这可能导致这样的印象书签字段都包含在描述符标头，但这不是这种情况。 书签字段有别于标头字段。  
  
 在单独设置字段，该应用程序应该遵循中定义的序列[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 设置某些字段会导致要设置其他字段的驱动程序。 这可确保描述符始终可供使用后一种数据类型指定应用程序。 当应用程序将设置 SQL_DESC_TYPE 字段时，驱动程序将检查指定的类型的其他字段都有效且一致。  
  
 如果将设置一个描述符字段的函数调用失败，是不确定失败的函数调用后的描述符字段的内容。

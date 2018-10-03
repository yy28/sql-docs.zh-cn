---
title: 设置描述符字段 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: d735dc64-370f-48ab-a59f-6cef9bc4e1e8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14724a5cc863074344cfbb02615f0ccff228f04c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628415"
---
# <a name="setting-descriptor-fields"></a>设置描述符字段
若要修改的描述符字段，应用程序可以调用**SQLSetDescField**。 某些字段是只读的不能设置。 (请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)函数说明。)  
  
 描述符记录字段进行设置的记录号 (*RecNumber*) 0 的记录号的 1 个或更高版本，while 描述符标头字段进行设置。 0 的记录号还用于设置书签字段，根据在第 0 列包含书签的约定。 这可能会使人的印象，书签字段包含在描述符标头，但这不是这种情况。 书签字段是截然不同的标头字段。  
  
 应用程序时设置单独的字段，应遵循在中定义的序列[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 设置某些字段会导致驱动程序来设置其他字段。 这可确保该描述符是始终可供使用后一种数据类型指定应用程序。 当应用程序设置的 SQL_DESC_TYPE 字段时，驱动程序将检查指定类型的其他字段有效且一致。  
  
 如果将设置描述符字段的函数调用失败，失败的函数调用后不确定的描述符字段的内容。

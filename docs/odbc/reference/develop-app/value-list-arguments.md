---
title: 值列表参数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fd655bd745c3bb06923e047d4134b286cf64703e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306738"
---
# <a name="value-list-arguments"></a>值列表自变量
值列表参数由用于匹配的逗号分隔值列表组成。 ODBC 目录函数中只有一个值列表参数 **：SQLTables**中的*表类型*参数。 将*表类型*设置为空指针与将其设置为SQL_ALL_TABLE_TYPES相同，后者枚举值列表的所有可能成员。 此参数不受SQL_ATTR_METADATA_ID语句属性的影响。 有关详细信息，请参阅[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)函数说明。

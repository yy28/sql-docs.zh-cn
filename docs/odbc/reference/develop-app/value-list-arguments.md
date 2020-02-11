---
title: 值列表参数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 646d2724489140080a673f31e22429cc7ca39d4e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68022115"
---
# <a name="value-list-arguments"></a>值列表自变量
值列表参数由逗号分隔值列表组成，这些值用于匹配。 ODBC 目录函数中只有一个值列表参数： **SQLTables**中的*TableType*参数。 如果将*TableType*设置为 null 指针，则将其设置为与 SQL_ALL_TABLE_TYPES （枚举值列表中所有可能的成员）的值相同。 此参数不受 SQL_ATTR_METADATA_ID 语句特性的影响。 有关详细信息，请参阅[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)函数说明。

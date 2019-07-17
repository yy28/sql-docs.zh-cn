---
title: 支持的游标模型 （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], cursors
- cursors [ODBC], Visual FoxPro ODBC driver
- FoxPro ODBC driver [ODBC], cursors
- static cursors [ODBC]
- block cursors [ODBC]
- rowset cursors [ODBC]
ms.assetid: be95bbb2-6886-491e-a5a7-f58028d19c1e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e623c0ce5135a4b2e558be9c405ec2757e605ceb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080702"
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>支持的游标模型（Visual FoxPro ODBC 驱动程序）
Visual FoxPro ODBC 驱动程序同时支持*块*(*行集*) 和*静态*游标。 级别 1 ODBC 法规遵从性符合任何驱动程序支持静态游标。 该驱动程序不支持动态，由键集驱动或混合 （键集和动态） 游标。  
  
 你的应用程序可以调用[SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) SQL_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY （块游标） 或 SQL_CURSOR_STATIC （静态游标） 的选项。  
  
> [!NOTE]  
>  如果您调用**SQLSetStmtOption** SQL_CURSOR_FORWARD_ONLY 或 SQL_CURSOR_STATIC 以外 SQL_CURSOR_TYPE 选项后，该函数将返回 SQL_SUCCESS_WITH_INFO 01S02 sqlstate （选项值已更改）。 该驱动程序将所有不支持的游标模式设置为 SQL_CURSOR_STATIC。  
  
 有关详细信息，有关游标类型和有关**SQLSetStmtOption**，请参阅[ODBC 程序员参考](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="block-cursor"></a>块状游标 (block cursor)  
 向前滚动、 只读结果集返回到客户端，负责维护的数据存储。  
  
## <a name="static-cursor"></a>静态游标 (static cursor)  
 定义查询的数据集创建快照。 静态游标不反映其他用户的基础数据的实时变化。 由 ODBC 游标库，它允许向前和向后滚动维护游标的内存缓冲区。  
  
## <a name="rowset"></a>行集 (rowset)  
 表示从数据源检索行的游标中存储的数据块。

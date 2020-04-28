---
title: 支持的游标模型（Visual FoxPro ODBC 驱动程序） |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cf3400f24e20a8fa864404612bf07ea44efce49e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301123"
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>支持的游标模型（Visual FoxPro ODBC 驱动程序）
Visual FoxPro ODBC 驱动程序支持*块*（*行集*）和*静态*游标。 符合级别 1 ODBC 符合性的任何驱动程序均支持静态游标。 该驱动程序不支持动态、键集驱动的游标或混合（键集和动态）游标。  
  
 应用程序可以使用 SQL_CURSOR_FORWARD_ONLY （块游标）或 SQL_CURSOR_STATIC （静态游标） SQL_CURSOR_TYPE 选项调用[SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) 。  
  
> [!NOTE]  
>  如果使用除 SQL_CURSOR_FORWARD_ONLY 或 SQL_CURSOR_STATIC 之外的 SQL_CURSOR_TYPE 选项调用**SQLSetStmtOption** ，则该函数将返回 SQL_SUCCESS_WITH_INFO，SQLSTATE 为01S02 （选项值已更改）。 驱动程序将所有不受支持的游标模式设置为 SQL_CURSOR_STATIC。  
  
 有关游标类型和关于**SQLSetStmtOption**的详细信息，请参阅[ODBC 程序员参考](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="block-cursor"></a>块状游标 (block cursor)  
 向客户端返回一个向前滚动的只读结果集，负责维护数据的存储。  
  
## <a name="static-cursor"></a>静态游标 (static cursor)  
 查询定义的数据集的快照。 静态游标不会反映其他用户对基础数据的实时更改。 游标的内存缓冲区由 ODBC 游标库维护，后者允许向前和向后滚动。  
  
## <a name="rowset"></a>行集 (rowset)  
 存储在游标中的数据块，表示从数据源检索的行。

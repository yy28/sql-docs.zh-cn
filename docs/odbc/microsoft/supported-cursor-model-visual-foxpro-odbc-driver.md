---
title: 支持的光标模型（视觉福克斯Pro ODBC驱动程序） |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301123"
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>支持的游标模型（Visual FoxPro ODBC 驱动程序）
Visual FoxPro ODBC 驱动程序支持*块*（*行集*） 和*静态*游标。 任何符合 1 级 ODBC 合规性的驱动程序都支持静态游标。 驱动程序不支持动态、键集驱动或混合（键集和动态）游标。  
  
 您的应用程序可以使用SQL_CURSOR_TYPE选项"SQL_CURSOR_FORWARD_ONLY（块游标）或SQL_CURSOR_STATIC（静态光标）来调用[SQLSetStmtOption。](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md)  
  
> [!NOTE]  
>  如果使用SQL_CURSOR_FORWARD_ONLY或SQL_CURSOR_STATIC以外的SQL_CURSOR_TYPE选项调用**SQLSetStmtOption，** 则函数返回SQL_SUCCESS_WITH_INFO SQLSTATE 为 01S02（选项值已更改）。 驱动程序将所有不支持的游标模式设置为SQL_CURSOR_STATIC。  
  
 有关游标类型和**SQLSetStmtOption**的详细信息，请参阅[ODBC 程序员的参考](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="block-cursor"></a>块状游标 (block cursor)  
 返回的向前滚动、只读结果集返回给客户端，客户端负责维护数据的存储。  
  
## <a name="static-cursor"></a>静态游标 (static cursor)  
 由查询定义的数据集的快照。 静态游标不反映其他用户对基础数据的实时更改。 光标的内存缓冲区由 ODBC 游标库维护，允许向前和向后滚动。  
  
## <a name="rowset"></a>行集 (rowset)  
 存储在游标中的数据块，表示从数据源检索的行。

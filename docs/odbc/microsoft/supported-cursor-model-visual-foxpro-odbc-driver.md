---
title: 支持 （Visual FoxPro ODBC 驱动程序） 的游标模型 |Microsoft 文档
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
- Visual FoxPro ODBC driver [ODBC], cursors
- cursors [ODBC], Visual FoxPro ODBC driver
- FoxPro ODBC driver [ODBC], cursors
- static cursors [ODBC]
- block cursors [ODBC]
- rowset cursors [ODBC]
ms.assetid: be95bbb2-6886-491e-a5a7-f58028d19c1e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f12ee1bae3ae4b10b546801bf35ebbf370e1eaba
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32903622"
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>支持的游标模型 （Visual FoxPro ODBC 驱动程序）
Visual FoxPro ODBC 驱动程序同时支持*块*(*行集*) 和*静态*游标。 以任何符合的符合性级别 1 ODBC 的驱动程序支持静态游标。 该驱动程序不支持动态，键集驱动的或混合 （键集和动态） 游标。  
  
 你的应用程序可以调用[SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) SQL_CURSOR_TYPE 选项 SQL_CURSOR_FORWARD_ONLY （块状游标） 或 SQL_CURSOR_STATIC （静态游标）。  
  
> [!NOTE]  
>  如果调用**SQLSetStmtOption** SQL_CURSOR_FORWARD_ONLY 或 SQL_CURSOR_STATIC 以外 SQL_CURSOR_TYPE 选项，该函数将返回与 01s02 的警告的 SQLSTATE SQL_SUCCESS_WITH_INFO （选项值已更改）。 该驱动程序将所有不受支持的游标模式设置为 SQL_CURSOR_STATIC。  
  
 有关详细信息，有关游标类型和有关**SQLSetStmtOption**，请参阅[ODBC 程序员参考](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="block-cursor"></a>块状游标 (block cursor)  
 向前滚动、 只读结果集返回到客户端，负责维护数据的存储区。  
  
## <a name="static-cursor"></a>静态游标 (static cursor)  
 定义查询的数据集的快照。 静态游标不反映其他用户对基础数据的实时变化。 由 ODBC 游标库，它允许向前和向后滚动维护光标的内存缓冲区。  
  
## <a name="rowset"></a>行集 (rowset)  
 游标，表示从数据源检索的行中存储的数据块。

---
title: SQLSetScrollOptions 函数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetScrollOptions
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetScrollOptions
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC]
ms.assetid: 2a825ba7-7942-4c23-bcdb-c80dc12f8c86
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 77a85caefadb54c3db2716c4db18b504e02da996
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342940"
---
# <a name="sqlsetscrolloptions-function"></a>SQLSetScrollOptions 函数
**度**  
 引入的版本:ODBC 1.0 标准符合性:不推荐使用  
  
 **摘要**  
 在 ODBC 3.x*中, odbc*2.0 函数**SQLSetScrollOptions**已被调用**SQLGetInfo**和**SQLSetStmtAttr**。  
  
> [!NOTE]
>  有关 ODBC *2.x 应用程序*使用 odbc *2.x 驱动程序*时, 驱动程序管理器将此函数映射到的内容的详细信息,[请参阅附录](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)G:向后兼容的驱动程序准则。  
> 
> [!NOTE]
>  当驱动程序管理器为使用不支持**SQLSetScrollOptions***的 ODBC 1.x*驱动程序的应用程序映射**SQLSetScrollOptions**时, 驱动程序管理器将设置 SQL_ROWSET_SIZE 语句选项, 而不是 SQL_ATTR_ROW_ARRAY_SIZE 语句特性, 到**SQLSetScrollOption**中的*RowsetSize*参数。 因此, 在通过调用**SQLFetch**或**SQLFetchScroll**提取多行时, 应用程序不能使用**SQLSetScrollOptions** 。 它只能在通过调用**SQLExtendedFetch**提取多行时使用。  
  
## <a name="remarks"></a>备注  
 如果你的应用程序将在64位操作系统上运行, 请参阅[ODBC 64 位信息](../../../odbc/reference/odbc-64-bit-information.md)。  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)

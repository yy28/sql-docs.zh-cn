---
title: SQLSetScrollOptions 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetScrollOptions
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetScrollOptions
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC]
ms.assetid: 2a825ba7-7942-4c23-bcdb-c80dc12f8c86
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dbdd2038bc217a7ca2a2efe08940c03c5da5d8f0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62985241"
---
# <a name="sqlsetscrolloptions-function"></a>SQLSetScrollOptions 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：不推荐使用  
  
 **摘要**  
 在 ODBC 3 *.x*，ODBC 2.0 函数**SQLSetScrollOptions**已由调用**SQLGetInfo**并**SQLSetStmtAttr**。  
  
> [!NOTE]
>  有关哪些驱动程序管理器时，将映射此函数可对 ODBC 2 详细信息 *.x*应用程序使用 ODBC 3 *.x*驱动程序，请参阅[映射已弃用函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)附录 g:为了向后兼容的驱动程序指南。  
> 
> [!NOTE]
>  当驱动程序管理器映射**SQLSetScrollOptions**应用程序使用 ODBC 3 *.x*不支持的驱动程序**SQLSetScrollOptions**，驱动程序管理器将设置 SQL_ROWSET_SIZE 语句选项，不将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性，为*RowsetSize*中的参数**SQLSetScrollOption**。 因此， **SQLSetScrollOptions**由在调用提取多行时，应用程序不能使用**SQLFetch**或**SQLFetchScroll**。 仅当通过调用提取多行时，可以使用它**SQLExtendedFetch**。  
  
## <a name="remarks"></a>备注  
 如果你的应用程序将在 64 位操作系统上运行，请参阅[ODBC 64-Bit 信息](../../../odbc/reference/odbc-64-bit-information.md)。  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)

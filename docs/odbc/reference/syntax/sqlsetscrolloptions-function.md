---
title: SQLSetScrollOptions 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 79ab0c408748fcbea30fdc2c792e433db8a4309d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetscrolloptions-function"></a>SQLSetScrollOptions 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： 不推荐使用  
  
 **摘要**  
 ODBC 3 中 *.x*，ODBC 2.0 函数**SQLSetScrollOptions**已通过调用替换为**SQLGetInfo**和**SQLSetStmtAttr**。  
  
> [!NOTE]  
>  有关什么驱动程序管理器时，将映射此函数可对 ODBC 2 *.x*应用程序使用 ODBC 3 *.x*驱动程序，请参阅[映射弃用函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)为了向后兼容的附录 g： 驱动程序准则中。  
  
> [!NOTE]  
>  当驱动程序管理器映射**SQLSetScrollOptions**为应用程序使用 ODBC 3 *.x*驱动程序不支持**SQLSetScrollOptions**，驱动程序管理器将设置 SQL_ROWSET_SIZE 语句选项，不 SQL_ATTR_ROW_ARRAY_SIZE 语句特性，为*RowsetSize*中的参数**SQLSetScrollOption**。 因此， **SQLSetScrollOptions**按调用提取多行时，应用程序不使用**SQLFetch**或**SQLFetchScroll**。 仅当通过调用提取多个行时，才可以使用它**SQLExtendedFetch**。  
  
## <a name="remarks"></a>注释  
 如果你的应用程序将在 64 位操作系统上运行，请参阅[ODBC 64 位信息](../../../odbc/reference/odbc-64-bit-information.md)。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)

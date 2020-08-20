---
description: SQLSetScrollOptions 函数
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0197c3756b76b480cd5370b5edff9d6fc88b201c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491204"
---
# <a name="sqlsetscrolloptions-function"></a>SQLSetScrollOptions 函数
**度**  
 引入的版本： ODBC 1.0 标准符合性：已弃用  
  
 **摘要**  
 在 ODBC 3.x *中，odbc*2.0 函数 **SQLSetScrollOptions** 已被调用 **SQLGetInfo** 和 **SQLSetStmtAttr**。  
  
> [!NOTE]
>  有关 ODBC *2.x 应用程序**使用 odbc 2.x*驱动程序时，驱动程序管理器将此函数映射到的内容的详细信息，请参阅附录 G：驱动程序准则中的[映射弃用的函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)以实现向后兼容性。  
> 
> [!NOTE]
>  当驱动程序管理器为使用不支持**SQLSetScrollOptions***的 ODBC 1.x 驱动程序的*应用程序映射**SQLSetScrollOptions**时，驱动程序管理器会将 SQL_ROWSET_SIZE 语句选项，而不是 SQL_ATTR_ROW_ARRAY_SIZE 语句特性）设置为**SQLSetScrollOption**中的*RowsetSize*参数。 因此，在通过调用**SQLFetch**或**SQLFetchScroll**提取多行时，应用程序不能使用**SQLSetScrollOptions** 。 它只能在通过调用 **SQLExtendedFetch**提取多行时使用。  
  
## <a name="remarks"></a>备注  
 如果你的应用程序将在64位操作系统上运行，请参阅 [ODBC 64 位信息](../../../odbc/reference/odbc-64-bit-information.md)。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)

---
title: SQLSetScroll选项函数 |微软文档
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
ms.openlocfilehash: 056fc203581e1d5d8323b09ac62d692093d8c0f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287260"
---
# <a name="sqlsetscrolloptions-function"></a>SQLSetScrollOptions 函数
**一致性**  
 版本介绍： ODBC 1.0 标准合规性： 已弃用  
  
 **摘要**  
 在 ODBC *3.x*中，ODBC 2.0 函数**SQLSetScrollOptions**已被对**SQLGetInfo**和**SQLSetStmtAttr**的调用所取代。  
  
> [!NOTE]
>  有关驱动程序管理器将此功能映射到 ODBC *2.x*应用程序使用 ODBC *3.x*驱动程序时的详细信息，请参阅附录 G：向后兼容性驱动程序指南中的[映射已弃用函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)。  
> 
> [!NOTE]
>  当驱动程序管理器映射**SQLSetScrollOption 的应用程序 SQLSetScrollOption**时，使用不支持**SQLSetScrollOption**的 ODBC *3.x*驱动程序时，驱动程序管理器将SQL_ROWSET_SIZE语句选项（而不是SQL_ATTR_ROW_ARRAY_SIZE语句属性）设置为**SQLSetScrollOption**中的*RowsetSize*参数。 因此，当调用**SQLFetch**或**SQLFetchScroll**获取多行时，应用程序无法使用**SQLSetScrollOptions。** 它只能在调用**SQLExtendedFetch**获取多行时使用。  
  
## <a name="remarks"></a>备注  
 如果应用程序将在 64 位操作系统上运行，请参阅[ODBC 64 位信息](../../../odbc/reference/odbc-64-bit-information.md)。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)

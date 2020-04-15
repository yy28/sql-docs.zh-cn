---
title: SQLParam 选项函数 |微软文档
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLParamOptions
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLParamOptions
helpviewer_keywords:
- SQLParamOptions function [ODBC]
ms.assetid: ee08e987-0243-4060-ab21-64da11fe444f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 209cfe6444918a40f5199af1f1a839050a3a6a57
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306908"
---
# <a name="sqlparamoptions-function"></a>SQLParamOptions 函数
**一致性**  
 版本介绍： ODBC 1.0 标准合规性： 已弃用  
  
 **摘要**  
 ODBC 2.0 函数**SQLParamOptions**已在 ODBC 3 中进行了更换。*x*通过调用[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
> [!NOTE]  
>  有关驱动程序管理器将此功能映射到 ODBC 2 时的详细信息。*x*应用程序使用 ODBC 3。*x*驱动程序，请参阅附录 G 中的[映射已弃用函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)：向后兼容性的驱动程序指南。  
  
## <a name="remarks"></a>备注  
 如果应用程序将在 64 位操作系统上运行，请参阅[ODBC 64 位信息](../../../odbc/reference/odbc-64-bit-information.md)。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)

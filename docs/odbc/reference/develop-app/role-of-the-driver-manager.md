---
title: 驱动程序管理器的角色 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- diagnostic information [ODBC], driver manager error checking
- SQLGetDiagField function [ODBC], driver manager
- SQLGetDiagRec function [ODBC], driver manager
- ODBC driver manager [ODBC]
- diagnostic information [ODBC], SqlGetDiagRec
- driver manager [ODBC], error checking
ms.assetid: 7b861c82-357e-4590-8074-45136e9ed15e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee3d704ea43125c3cd912a4e67d90bf5d50c733e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304298"
---
# <a name="role-of-the-driver-manager"></a>驱动程序管理器的角色
驱动程序管理器确定返回它生成的状态记录的最终顺序。 特别是，它确定哪个记录的排名最高，并且要首先返回。 驱动程序负责排序它生成的状态记录。 如果状态记录由驱动程序管理器和驱动程序发布，则驱动程序管理器负责排序它们。 有关详细信息，请参阅[状态记录序列](../../../odbc/reference/develop-app/sequence-of-status-records.md)。  
  
 驱动程序管理器可以执行尽可能多的错误检查。 这样，每个驱动程序都免于检查相同的错误。 例如，如果函数参数接受离散数的值（如**SQLSetPos**中的*操作*），驱动程序管理器将检查指定值是否合法。  
  
 以下各节介绍驱动程序管理器检查的条件类型。 它们并非详尽无遗;有关驱动程序管理器返回的 SQLSTATA 的完整列表，请参阅每个函数的"诊断"部分;驾驶员管理器所做的每个检查的描述以字母"（DM）"开头。 另请参阅附录 B 中的状态转换[表：ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md);驱动器管理器检测到括号中显示的错误。  
  
 本部分包含以下主题。  
  
-   [参数值检查](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [状态转换检查](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [常规错误检查](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [驱动程序管理器错误和警告检查](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)

---
title: 驱动程序管理器的角色 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304298"
---
# <a name="role-of-the-driver-manager"></a>驱动程序管理器的角色
驱动程序管理器决定返回其生成的状态记录的最终顺序。 具体而言，它将确定哪个记录具有最高的排名，并将首先返回该记录。 驱动程序负责对其生成的状态记录进行排序。 如果状态记录由驱动程序管理器和驱动程序发布，则驱动程序管理器负责对它们进行排序。 有关详细信息，请参阅[状态记录序列](../../../odbc/reference/develop-app/sequence-of-status-records.md)。  
  
 驱动程序管理器执行的错误检查会尽可能多。 这会保存每个驱动程序检查是否存在相同的错误。 例如，如果函数自变量接受离散数量的值（如**SQLSetPos**中的*操作*），则驱动程序管理器会检查指定的值是否合法。  
  
 以下部分描述了驱动程序管理器检查的条件类型。 它们不是详尽的;有关驱动程序管理器返回的 SQLSTATEs 的完整列表，请参阅每个函数的 "诊断" 部分;驱动程序管理器所做的每个检查的说明都以字母 "（DM）" 开头。 另请参阅[附录 B： ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)中的状态转换表;括号中显示的错误由驱动程序管理器检测到。  
  
 本部分包含以下主题。  
  
-   [参数值检查](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [状态转换检查](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [常规错误检查](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [驱动程序管理器错误和警告检查](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)

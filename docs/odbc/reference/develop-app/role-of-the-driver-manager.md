---
title: 角色的驱动程序管理器 |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- diagnostic information [ODBC], driver manager error checking
- SQLGetDiagField function [ODBC], driver manager
- SQLGetDiagRec function [ODBC], driver manager
- ODBC driver manager [ODBC]
- diagnostic information [ODBC], SqlGetDiagRec
- driver manager [ODBC], error checking
ms.assetid: 7b861c82-357e-4590-8074-45136e9ed15e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 89d4b99deb3599765dfec30c5d2ec28975c8f875
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="role-of-the-driver-manager"></a>角色的驱动程序管理器
驱动程序管理器确定最终顺序返回它所生成的状态记录。 具体而言，它确定哪一记录具有最高排名，并首先返回。 该驱动程序负责排序它生成的状态记录。 如果状态记录发布的驱动程序管理器和驱动程序，驱动程序管理器负责对数据进行排序。 有关详细信息，请参阅[状态记录序列](../../../odbc/reference/develop-app/sequence-of-status-records.md)。  
  
 驱动程序管理器执行尽可能多的错误检查，因为它可以。 这将从相同的错误检查保存每个驱动程序。 例如，如果函数参数接受离散数目的值，如*操作*中**SQLSetPos**，驱动程序管理器检查指定的值是否合法。  
  
 下列各节描述类型的检查由驱动程序管理器的条件。 这些指南不打算详尽;有关驱动程序管理器返回 SQLSTATEs 的完整列表，请参阅每个函数; 的"诊断"部分每个检查所做的驱动程序管理器中的说明开头字母"(DM)。" 另请参阅中的状态转换表[附录 b: ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md); 由驱动程序管理器检测到错误显示在括号中。  
  
 本部分包含以下主题。  
  
-   [参数值检查](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [状态转换检查](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [常规错误检查](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [驱动程序管理器错误和警告检查](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)

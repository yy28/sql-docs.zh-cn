---
title: 角色的驱动程序管理器 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 485cd951992ed427461e497c53d17a4f6db24a38
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626095"
---
# <a name="role-of-the-driver-manager"></a>驱动程序管理器的角色
驱动程序管理器确定要返回其生成的状态记录中的最终顺序。 具体而言，它会确定哪些记录具有最高排名，首先返回。 该驱动程序负责排序它生成的状态记录。 如果状态记录所发送的驱动程序管理器和驱动程序，驱动程序管理器负责对数据进行排序。 有关详细信息，请参阅[序列的状态记录](../../../odbc/reference/develop-app/sequence-of-status-records.md)。  
  
 驱动程序管理器执行太多错误检查，可使用。 这样，每个驱动程序从相同的错误检查。 例如，如果函数参数接受离散数目的值，如*操作*中**SQLSetPos**，驱动程序管理器检查指定的值是否合法。  
  
 以下部分介绍类型的检查由驱动程序管理器的条件。 它们并不详尽;有关驱动程序管理器返回的 SQLSTATEs 的完整列表，请参阅"诊断"部分中的每个函数;每个驱动程序管理器做出的检查的说明开头的字母"(DM)。" 另请参阅中的状态转换表[附录 b: ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md); 由驱动程序管理器检测到错误显示在括号中。  
  
 本部分包含以下主题。  
  
-   [参数值检查](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [状态转换检查](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [常规错误检查](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [驱动程序管理器错误和警告检查](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)

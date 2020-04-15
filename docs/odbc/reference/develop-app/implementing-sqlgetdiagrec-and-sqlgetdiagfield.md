---
title: 实现 SQLGetDiagRec 和 SQLGetDiagField |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 11ba1857-b533-4517-8131-a2a8a0154a0a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c090af19a9296e46e3036ca23f6c97298bcb1b8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300137"
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>实现 SQLGetDiagRec 和 SQLGetDiagField
**SQLGetDiagRec**和**SQLGetDiagField**由驱动程序管理器和每个驱动程序实现。 驱动程序管理器和每个驱动程序维护每个环境、连接、语句和描述符句柄的诊断记录，并且仅在使用该句柄调用另一个函数或释放该句柄时释放这些记录。  
  
 尽管驱动程序管理器和每个驱动程序都必须根据[状态记录序列](../../../odbc/reference/develop-app/sequence-of-status-records.md)中的排名确定第一个状态记录，但驱动程序管理器确定记录的最终顺序。  
  
 **SQLGetDiagRec**和**SQLGetDiagField**不会发布有关自己的诊断记录。  
  
 本部分包含以下主题。  
  
-   [诊断处理规则](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [驱动程序管理器的角色](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [驱动程序的角色](../../../odbc/reference/develop-app/role-of-the-driver.md)

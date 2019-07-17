---
title: 实现 SQLGetDiagRec 和 SQLGetDiagField |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a4b602d5ff4a94d2888395e6a62f03553fb50f98
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68216375"
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>实现 SQLGetDiagRec 和 SQLGetDiagField
**SQLGetDiagRec**并**SQLGetDiagField**由驱动程序管理器和每个驱动程序实现。 驱动程序管理器和每个驱动程序维护的每个环境、 连接、 语句和描述符句柄的诊断记录，仅当另一个函数调用与释放句柄或句柄的释放这些记录。  
  
 尽管驱动程序管理器和每个驱动程序必须确定第一个状态记录中的排名根据[序列的状态记录](../../../odbc/reference/develop-app/sequence-of-status-records.md)，驱动程序管理器确定的记录的最后一个序列。  
  
 **SQLGetDiagRec**并**SQLGetDiagField**不发布有关自身的诊断记录。  
  
 本部分包含以下主题。  
  
-   [诊断处理规则](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [驱动程序管理器的角色](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [驱动程序的角色](../../../odbc/reference/develop-app/role-of-the-driver.md)

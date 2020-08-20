---
description: 实现 SQLGetDiagRec 和 SQLGetDiagField
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 91e43252aea4ebf12dedcb14bb1b7fb34f75df6f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461429"
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>实现 SQLGetDiagRec 和 SQLGetDiagField
**SQLGetDiagRec** 和 **SQLGetDiagField** 由驱动程序管理器和每个驱动程序实现。 驱动程序管理器和每个驱动程序都维护每个环境、连接、语句和描述符句柄的诊断记录，并且仅当通过该句柄调用另一个函数或释放该句柄时，才释放这些记录。  
  
 尽管驱动程序管理器和每个驱动程序必须根据 [状态记录序列](../../../odbc/reference/develop-app/sequence-of-status-records.md)中的排名确定第一个状态记录，但驱动程序管理器会确定最后一条记录的顺序。  
  
 **SQLGetDiagRec** 和 **SQLGetDiagField** 不会发布自身的诊断记录。  
  
 本部分包含以下主题。  
  
-   [诊断处理规则](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [驱动程序管理器的角色](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [驱动程序的角色](../../../odbc/reference/develop-app/role-of-the-driver.md)

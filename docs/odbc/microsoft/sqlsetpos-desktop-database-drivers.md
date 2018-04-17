---
title: SQLSetPos （桌面数据库驱动程序） |Microsoft 文档
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
- SQLSetPos function [ODBC], Desktop Database Drivers
ms.assetid: 8ef027ec-8512-48fe-8fe2-2ff7cd81e331
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dfeea1fe0ef6cbffd2090142e19df9a0f40afbf4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsetpos-desktop-database-drivers"></a>SQLSetPos （桌面数据库驱动程序）
大容量模型语义**SQLSetPos**使用调用*irow*支持参数等于 0。  
  
 支持 SQL_LOCK_NO_CHANGE *fLock*。 不支持 SQL_LOCK_EXCLUSIVE 和 SQL_LOCK_UNLOCK。  
  
 **SQLSetPos**支持可更新的联接。 (有关详细信息，请参阅*Microsoft Jet 数据库引擎程序员指南*。)

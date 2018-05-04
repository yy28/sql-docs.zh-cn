---
title: SQLSetPos （桌面数据库驱动程序） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], Desktop Database Drivers
ms.assetid: 8ef027ec-8512-48fe-8fe2-2ff7cd81e331
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 38b1e2578e6cb4a3e337d43211dd9497cc302518
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetpos-desktop-database-drivers"></a>SQLSetPos （桌面数据库驱动程序）
大容量模型语义**SQLSetPos**使用调用*irow*支持参数等于 0。  
  
 支持 SQL_LOCK_NO_CHANGE *fLock*。 不支持 SQL_LOCK_EXCLUSIVE 和 SQL_LOCK_UNLOCK。  
  
 **SQLSetPos**支持可更新的联接。 (有关详细信息，请参阅*Microsoft Jet 数据库引擎程序员指南*。)

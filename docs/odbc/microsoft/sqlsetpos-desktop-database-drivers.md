---
title: SQLSetPos （桌面数据库驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], Desktop Database Drivers
ms.assetid: 8ef027ec-8512-48fe-8fe2-2ff7cd81e331
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95117c82c213851d2e0600e65d8061ce532d9933
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601605"
---
# <a name="sqlsetpos-desktop-database-drivers"></a>SQLSetPos（桌面数据库驱动程序）
大容量模型的语义**SQLSetPos**使用调用*irow*支持等于 0 的参数。  
  
 支持 SQL_LOCK_NO_CHANGE*纷纷采用*。 不支持 SQL_LOCK_EXCLUSIVE 和 SQL_LOCK_UNLOCK。  
  
 **SQLSetPos**支持可更新的联接。 (有关详细信息，请参阅*Microsoft Jet 数据库引擎程序员指南*。)

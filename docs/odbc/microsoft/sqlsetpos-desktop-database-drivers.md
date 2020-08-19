---
description: SQLSetPos（桌面数据库驱动程序）
title: SQLSetPos (桌面数据库驱动程序) |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4aa126514bc84f5546e1f4a022d8d3e6235b2e7c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421661"
---
# <a name="sqlsetpos-desktop-database-drivers"></a>SQLSetPos（桌面数据库驱动程序）
支持*irow*参数等于0的**SQLSetPos**调用的大容量模型语义。  
  
 *FLock*支持 SQL_LOCK_NO_CHANGE。 不支持 SQL_LOCK_EXCLUSIVE 和 SQL_LOCK_UNLOCK。  
  
 **SQLSetPos** 支持可更新的联接。  (有关详细信息，请参阅 *Microsoft Jet 数据库引擎程序员指南*。 ) 

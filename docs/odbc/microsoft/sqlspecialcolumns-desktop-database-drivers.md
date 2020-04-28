---
title: SQLSpecialColumns （桌面数据库驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Desktop Database Drivers
ms.assetid: 3de66fdf-053b-4354-979d-e76a5a5e975f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5f8cd4ed0912f9f1e71d64b32449b5d46f9ef1a3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299387"
---
# <a name="sqlspecialcolumns-desktop-database-drivers"></a>SQLSpecialColumns（桌面数据库驱动程序）
*FColType*中的 SQL_BEST_ROWID 标志将返回唯一索引（如果存在）。 SQL_ROWVER 标志将不返回结果集。  
  
 所有行 Id 都有一个 SQL_SCOPE_CURROW 范围。  
  
 *SzTableQualifier*或*szTableName*参数不支持模式匹配。

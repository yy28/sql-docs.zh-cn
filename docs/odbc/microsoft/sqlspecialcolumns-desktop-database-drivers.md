---
title: SQLSpecialColumns （桌面数据库驱动程序） |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Desktop Database Drivers
ms.assetid: 3de66fdf-053b-4354-979d-e76a5a5e975f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2d2bfda1bb8732e3036c3803628bbe8247f9e76
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlspecialcolumns-desktop-database-drivers"></a>SQLSpecialColumns （桌面数据库驱动程序）
唯一索引将返回 （如果存在） SQL_BEST_ROWID 标志*fColType*。 将 SQL_ROWVER 标志不返回任何结果集。  
  
 所有行 Id 都具有 SQL_SCOPE_CURROW 的作用域。  
  
 模式匹配为不支持*szTableQualifier*或*szTableName*自变量。

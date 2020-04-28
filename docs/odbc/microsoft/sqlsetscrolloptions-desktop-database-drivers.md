---
title: SQLSetScrollOptions （桌面数据库驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Desktop Database Drivers
ms.assetid: 51d643ed-015b-4639-969a-9491d9875aca
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c47255b455354c49133d61c3546be63ab2380a1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299428"
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions（桌面数据库驱动程序）
SQL_CONCUR_READ_ONLY 支持向前游标和静态游标。  
  
 SQL_CONCUR_LOCK 的*fConcurrency*参数仅支持键集驱动的游标。  
  
 不支持 SQL_CONCUR_ROWVER 的*fConcurrency*参数。  
  
 不支持动态游标和混合游标。

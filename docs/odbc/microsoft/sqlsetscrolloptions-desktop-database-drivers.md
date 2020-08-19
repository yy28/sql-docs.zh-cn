---
description: SQLSetScrollOptions（桌面数据库驱动程序）
title: SQLSetScrollOptions (桌面数据库驱动程序) |Microsoft Docs
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
ms.openlocfilehash: 57237aca0a68119f6ab8f967b9641f2a2a52fc8c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421641"
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions（桌面数据库驱动程序）
SQL_CONCUR_READ_ONLY 支持向前游标和静态游标。  
  
 SQL_CONCUR_LOCK 的 *fConcurrency* 参数仅支持键集驱动的游标。  
  
 不支持 SQL_CONCUR_ROWVER 的 *fConcurrency* 参数。  
  
 不支持动态游标和混合游标。

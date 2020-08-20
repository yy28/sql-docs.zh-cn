---
description: 定长书签
title: 固定长度书签 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d357ba96141c658889628941c7f9492db5fd6b66
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466173"
---
# <a name="fixed-length-bookmarks"></a>定长书签
如果 ODBC 2.x *驱动程序* 应与使用固定长度书签的 odbc *2.x 应用程序* 一起使用，则驱动程序必须支持以下各项：  
  
-   SQL_UB_ON 作为 SQL_USE_BOOKMARKS 语句选项的值。 *ODBC 2.x*中 (SQL_UB_ON 已弃用 )   
  
-   SQL_GET_BOOKMARK 语句选项。

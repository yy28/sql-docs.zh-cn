---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5877a6cb7a99803f854338321e333c87037c2e90
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67913586"
---
# <a name="fixed-length-bookmarks"></a>定长书签
如果 ODBC 2.x*驱动程序*应与使用固定长度书签的 odbc *2.x 应用程序*一起使用，则驱动程序必须支持以下各项：  
  
-   SQL_UB_ON 作为 SQL_USE_BOOKMARKS 语句选项的值。 （SQL_UB_ON 已*在 ODBC 2.x 中弃用。）*  
  
-   SQL_GET_BOOKMARK 语句选项。

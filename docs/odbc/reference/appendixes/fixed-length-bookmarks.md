---
title: 固定长度书签 |微软文档
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
ms.openlocfilehash: f90c5888a68506c056b2a56fce516080148528e7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306978"
---
# <a name="fixed-length-bookmarks"></a>定长书签
如果 ODBC *3.x*驱动程序应使用使用固定长度书签的 ODBC *2.x*应用程序，则驱动程序必须支持以下内容：  
  
-   SQL_UB_ON作为SQL_USE_BOOKMARKS语句选项的值。 （SQL_UB_ON在 ODBC *3.x*中弃用）  
  
-   SQL_GET_BOOKMARK语句选项。

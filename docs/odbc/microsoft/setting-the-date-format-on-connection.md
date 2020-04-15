---
title: 在连接上设置日期格式 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date formats [ODBC]
- ODBC driver for Oracle [ODBC], date formats
ms.assetid: ba0d5123-db52-448b-8e19-b7647ce4b361
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9da75702275959b48d4965189c9ef5cd856491ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300737"
---
# <a name="setting-the-date-format-on-connection"></a>连接时设置日期格式
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 新版本的 Oracle ODBC 驱动程序不会自动设置 Oracle 日期字段的日期格式。 以前，当驱动程序连接时，它`ALTER SESSION SET NLS_DATE_FORMAT ='YYYY-MM-DD HH:MI:SS'`使用 。  
  
 要设置日期格式，请调用 ALTER 会话设置，然后执行插入。 例如：  
  
```  
conn.Execute "ALTER SESSION SET NLS_DATE_FORMAT = 'YYYY-MM-DD HH:MI:SS' "  
sSql = "INSERT INTO DATETEST VALUES (24,'1988-12-01 10:23:03')"  
conn.Execute sSql  
```

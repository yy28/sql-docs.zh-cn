---
title: 在连接上设置的日期格式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e36192279bfc5730559c795ee076db11394ab94
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654275"
---
# <a name="setting-the-date-format-on-connection"></a>连接时设置日期格式
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 适用于 Oracle 的 Microsoft ODBC 驱动程序的新版本不自动设置 Oracle 日期字段的日期格式。 以前，驱动程序连接时，它使用`ALTER SESSION SET NLS_DATE_FORMAT ='YYYY-MM-DD HH:MI:SS'`。  
  
 若要设置日期格式，调用 ALTER 会话组，然后执行插入。 例如：  
  
```  
conn.Execute "ALTER SESSION SET NLS_DATE_FORMAT = 'YYYY-MM-DD HH:MI:SS' "  
sSql = "INSERT INTO DATETEST VALUES (24,'1988-12-01 10:23:03')"  
conn.Execute sSql  
```

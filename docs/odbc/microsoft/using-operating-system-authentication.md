---
title: "使用操作系统身份验证 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], authentication
- authentication [ODBC]
ms.assetid: 613daef7-3171-42d0-b7e3-3879280f864d
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d3fbe8f4ce9fe9edbb88c7c895311bd9560dc28f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-operating-system-authentication"></a>使用操作系统身份验证
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 Oracle 操作系统身份验证依赖于底层操作系统，控制对数据库帐户的访问。 使用此类型的登录名时，用户不需要输入密码。  
  
 若要充分利用此功能，指定"/"作为用户 ID，而且你使用任何以下连接 Api 进行连接时未指定密码： [SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md)， [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)，或[SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)。  
  
 Oracle 数据库使用 SQL * Net 身份验证服务登录的用户进行身份验证。 如果用户登录到 Oracle SQLPlus; 通过此服务的工作原理但是，Internet Information Services 之类的服务登录的用户时，身份验证将失败。 这是已知的 SQL 限制\*Net 身份验证，并生成以下错误:"[Microsoft] [适用于 Oracle 的 ODBC 驱动程序] [Oracle] ORA 12641: TNS:authentication 服务初始化失败。"  
  
 可以通过编辑 Sqlnet.ora 文件来更正此问题。 此配置文件通常存储在 Oracle 主目录的 Network\Admin 子目录中。 将以下行添加到 Sqlnet.ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```

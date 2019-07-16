---
title: 使用操作系统身份验证 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], authentication
- authentication [ODBC]
ms.assetid: 613daef7-3171-42d0-b7e3-3879280f864d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 56f09a82c2e67ee74ce140f4742bfaf0bcce247f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088117"
---
# <a name="using-operating-system-authentication"></a>使用操作系统身份验证
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 Oracle 操作系统身份验证依赖于底层操作系统，控制对数据库帐户的访问。 使用此类型的登录名时，用户需要输入密码。  
  
 若要充分利用此功能，请指定"/"作为用户 ID 和使用任何以下连接 Api 进行连接时未指定密码：[SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md)， [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)，或[SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)。  
  
 Oracle 数据库使用 SQL * Net 身份验证服务登录的用户进行身份验证。 如果用户同时登录到 Oracle SQLPlus; 通过此服务的工作原理但是，如 Internet 信息服务的服务登录的用户时，身份验证失败。 这是 SQL 的已知的限制\*Net 身份验证，并生成以下错误:"[Microsoft] [Oracle ODBC 驱动程序] [Oracle] ORA 12641:TNS:authentication 服务初始化失败。"  
  
 可以通过编辑 Sqlnet.ora 文件来更正此问题。 此配置文件通常存储在 Oracle 主目录的 Network\Admin 子目录。 将以下行添加到 Sqlnet.ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```

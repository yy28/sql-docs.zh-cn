---
title: 使用操作系统身份验证 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d6520202bdbc31baf1156531457cb70a98656e88
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292837"
---
# <a name="using-operating-system-authentication"></a>使用操作系统身份验证
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 Oracle 操作系统身份验证依赖于基础操作系统来控制对数据库帐户的访问。 使用此类登录时，用户无需输入密码。  
  
 要利用此功能，请将"/"指定为用户 ID，并且在使用以下任何连接 API 进行连接时不要指定密码[：SQLBrowseConnect、SQLConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md)或[SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)[SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)。  
  
 Oracle 数据库使用 SQL_Net 身份验证服务对登录的用户进行身份验证。 如果用户通过 SQLPlus 登录到 Oracle，则此服务效果良好;但是，当登录用户是 Internet 信息服务等服务时，身份验证将失败。 这是 SQL\*Net 身份验证的已知限制，并产生以下错误："[Oracle[Oracle]ORA_12641：TNS：身份验证服务无法初始化。  
  
 您可以通过编辑 Sqlnet.ora 文件来更正此问题。 此配置文件通常存储在 Oracle 主目录的 Network_Admin 子目录中。 将以下行添加到 Sqlnet.ora：  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```

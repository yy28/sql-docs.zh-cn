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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d6520202bdbc31baf1156531457cb70a98656e88
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292837"
---
# <a name="using-operating-system-authentication"></a>使用操作系统身份验证
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 Oracle 操作系统身份验证依赖于基础操作系统来控制对数据库帐户的访问。 使用此类型的登录名时，用户无需输入密码。  
  
 若要利用此功能，请将 "/" 指定为用户 ID，在使用以下任一连接 Api 进行连接时不要指定密码： [SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md)、 [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)或[SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)。  
  
 Oracle 数据库使用 SQL * Net 身份验证服务对登录的用户进行身份验证。 如果用户通过 SQLPlus 登录到 Oracle，则此服务可以正常工作;但是，当登录用户是 Internet Information Services 的服务时，身份验证将失败。 这是 SQL\*网络身份验证的已知限制，并产生以下错误： "[Microsoft] [用于 ORACLE 的 ODBC 驱动程序] [ORACLE] tnsnames.ora-12641： TNS：身份验证服务无法初始化"。  
  
 可以通过编辑 Sqlnet. tnsnames.ora 文件来更正此问题。 此配置文件通常存储在 Oracle 主目录的 Network\Admin 子目录中。 将以下行添加到 Sqlnet。 tnsnames.ora：  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```

---
title: 测试 ODBC 连接 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- testing connections [ODBC]
- ODBC driver for Oracle [ODBC], testing connections
ms.assetid: 5e671665-2aba-49a7-8871-70784d8b3cc9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02509ddb6a986ebb7796d80aca10c6f18cde6e69
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939708"
---
# <a name="testing-the-odbc-connection"></a>测试 ODBC 连接
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 对 Oracle 的 ODBC 访问进行故障排除时 7.x 和 Oracle8 RDBMS 服务器，可能需要验证的基础 SQL * Net 和 Oracle 协议适配器是否正确安装。 若要执行此操作，使用 Oracle 提供实用工具 Nettest.exe Orawin\Bin 目录中。  
  
 Nettest 是一个简单的实用程序，尝试登录到选定的服务器使用已安装的 SQL * Net 是 Oracle 客户端的一部分的软件。 该实用程序将要求提供登录名，密码和 TNS 连接字符串。 如果正确安装 Oracle 客户端，则该实用工具将只显示"Ping 成功。" 如果该登录名不成功，将需要与数据库管理员进行协商。

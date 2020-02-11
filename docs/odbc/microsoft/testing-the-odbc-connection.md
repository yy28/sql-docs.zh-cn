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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67939708"
---
# <a name="testing-the-odbc-connection"></a>测试 ODBC 连接
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 对 Oracle 7、windows 和 Oracle8 RDBMS 服务器的 ODBC 访问进行故障排除时，可能需要验证是否正确安装了基础 SQL * Net 和 Oracle 协议适配器。 为此，请在 Orawin\Bin 目录中使用 Oracle 提供的实用程序 Nettest。  
  
 Nettest 是一个简单的实用程序，它仅尝试使用属于 Oracle 客户端的已安装 SQL * Net 软件登录到所选服务器。 实用工具将要求提供登录名、密码和 TNS 连接字符串。 如果正确安装了 Oracle 客户端，则实用工具只显示 "Ping 成功"。 如果登录不成功，你将需要与数据库管理员联系。

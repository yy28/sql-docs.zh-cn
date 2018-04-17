---
title: 测试的 ODBC 连接 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- testing connections [ODBC]
- ODBC driver for Oracle [ODBC], testing connections
ms.assetid: 5e671665-2aba-49a7-8871-70784d8b3cc9
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dee186c832f79c59da23adc48295ef647446711e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="testing-the-odbc-connection"></a>测试的 ODBC 连接
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 对 Oracle 的 ODBC 访问进行故障排除时 7.x 和 Oracle8 RDBMS 服务器，可能需要验证基础 SQL * Net 和 Oracle 协议适配器是否正确安装。 若要执行此操作，请使用 Orawin\Bin 目录中的 Oracle 提供实用工具 Nettest.exe。  
  
 Nettest 是简单实用工具，可尝试登录到选定的服务器使用安装的 SQL * Net 属于 Oracle 客户端的软件。 该实用工具将要求提供登录名，密码和 TNS 连接字符串。 如果正确安装 Oracle 客户端，则该实用工具将只显示"Ping 成功。" 如果登录不成功，你将需要与数据库管理员，请查阅。

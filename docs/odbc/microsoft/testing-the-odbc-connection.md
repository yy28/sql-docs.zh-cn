---
title: 测试 ODBC 连接 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8de19af2b50a58eef22ec074a308f86717278a48
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303108"
---
# <a name="testing-the-odbc-connection"></a>测试 ODBC 连接
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 在排除对 Oracle 7.x 和 Oracle8 RDBMS 服务器的 ODBC 访问进行故障排除时，可能需要验证基础 SQL_Net 和 Oracle 协议适配器是否已正确安装。 为此，请使用 Orawin_Bin 目录中的 Oracle 提供的实用程序 Nettest.exe。  
  
 Nettest 是一个简单的实用程序，它尝试仅使用作为 Oracle 客户端一部分的已安装的 SQL_Net 软件登录到选定的服务器。 该实用程序将要求一个登录名、密码和 TNS 连接字符串。 如果 Oracle 客户端安装正确，实用程序将仅显示"Ping 成功"。 如果登录不成功，则需要咨询数据库管理员。

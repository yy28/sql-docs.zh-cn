---
title: 连接到 Oracle (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 23a48cb6-ff30-49bb-b4a7-603ebcab336f
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: da846d4afb4ce8fe745b98c8503901fe804520e0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287731"
---
# <a name="connect-to-oracle-oracletosql"></a>连接到 Oracle (OracleToSQL)
使用**连接到 Oracle**对话框以连接到你想要迁移的 Oracle 数据库。  
  
若要访问此对话框，请在**文件**菜单中，选择**连接到 Oracle**。 如果你之前已连接，则命令是**重新连接到 Oracle**。  
  
## <a name="options"></a>选项  
**提供程序**  
选择数据访问接口连接到 Oracle 数据库。 可用的提供程序是 Oracle 客户端提供程序和 OLE DB 访问接口。 默认值是 Oracle 客户端提供程序。  
  
**模式**  
选择标准版、 TNSNAME 或连接字符串模式。  
  
-   在标准模式下，输入或选择的提供程序、 服务器名称、 服务器端口、 Oracle SID、 用户名和密码值。  
  
-   在 TNSNAME 模式下，您输入 Oracle 数据库、 用户名和密码的连接的标识符 （TNS 别名）。  
  
-   在连接字符串模式下，提供了一个连接字符串。  
  
    > [!IMPORTANT]  
    > 我们不建议使用连接字符串模式，因为文本可能包含密码，并且它以明文形式发送。  
  
默认为标准模式。  
  
**服务器名称**  
输入 Oracle 服务器名称。 默认服务器名称是与计算机名称相同。 这是标准模式选项。  
  
**服务器端口**  
如果使用 1521 （默认值） 以外的端口号以便连接到 Oracle，输入端口号。 这是标准模式选项。  
  
**连接标识符**  
输入 Oracle 连接标识符。 这是数据库的因为本地 tnsnames.ora 文件中定义的别名。  
  
这是 TNSNAME 模式选项。  
  
**Oracle SID**  
输入数据库的 SID。 SID 是区分开来的计算机上的 Oracle 数据库的标识符。 数据库的默认值 SID 是数据库名称的前八个字符。  
  
这是标准模式选项。  
  
**用户名**  
输入 SSMA 将用于连接到 Oracle 数据库的用户名。  
  
**密码**  
输入用户名的密码。  
  
**连接字符串**  
> [!IMPORTANT]  
> 我们不建议使用连接字符串模式，因为文本可能包含密码，并且它以明文形式发送。  
  
如果你使用连接字符串模式，请输入完整的连接字符串连接到 Oracle。  
  
连接字符串包含参数名称和值对。  
  
-   OLE DB 连接字符串信息，请参阅[Microsoft OLE DB Provider for Oracle](https://go.microsoft.com/fwlink/?LinkId=85640) MSDN 库文章。  
  
SSMA 连接字符串始终包含提供程序参数。 此外，请确保连接到 Oracle 时包括端口参数。  
  

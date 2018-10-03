---
title: 连接到 DB2 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9d485fd0-ab5d-402a-a59a-e9982a61b7de
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 74ece76fcb02fe77825d0f08e76b262df195d7b4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47768905"
---
# <a name="connect-to-db2-db2tosql"></a>连接到 DB2 (DB2ToSQL)
使用**连接到 DB2**对话框以连接到你想要迁移的 DB2 数据库。  
  
若要访问此对话框，请在**文件**菜单中，选择**连接到 DB2**。 如果你之前已连接，则命令是**重新连接到 DB2**。  
  
## <a name="options"></a>选项  
**提供程序**  
选择数据访问接口连接到 DB2 数据库。 可用的提供程序是 DB2 客户端提供程序和 OLE DB 访问接口。 默认值为 DB2 客户端提供程序。  
  
**模式**  
选择标准版、 TNSNAME 或连接字符串模式。  
  
-   在标准模式下，输入或选择的提供程序、 服务器名称、 服务器端口、 DB2 SID、 用户名和密码值。  
  
-   在 TNSNAME 模式下，您输入 DB2 数据库、 用户名和密码的连接的标识符 （TNS 别名）。  
  
-   在连接字符串模式下，提供了一个连接字符串。  
  
    > [!IMPORTANT]  
    > 我们不建议使用连接字符串模式，因为文本可能包含密码，并且它以明文形式发送。  
  
默认为标准模式。  
  
**服务器名称**  
输入的 DB2 服务器名称。 默认服务器名称是与计算机名称相同。 这是标准模式选项。  
  
**服务器端口**  
如果使用 1521 （默认值） 以外的端口号以便连接到 DB2，输入端口号。 这是标准模式选项。  
  
**连接标识符**  
输入 DB2 连接标识符。 这是数据库的因为本地 tnsnames.ora 文件中定义的别名。  
  
这是 TNSNAME 模式选项。  
  
**DB2 SID**  
输入数据库的 SID。 SID 是区分开来的计算机上的 DB2 数据库的标识符。 数据库的默认值 SID 是数据库名称的前八个字符。  
  
这是标准模式选项。  
  
**用户名**  
输入 SSMA 将用于连接到 DB2 数据库的用户名。  
  
**密码**  
输入用户名的密码。  
  
**连接字符串**  
> [!IMPORTANT]  
> 我们不建议使用连接字符串模式，因为文本可能包含密码，并且它以明文形式发送。  
  
如果你使用连接字符串模式，请输入完整的连接字符串连接到 DB2。  
  
连接字符串包含参数名称和值对。  
  
-   OLE DB 连接字符串信息，请参阅[Microsoft OLE DB Provider for DB2](http://go.microsoft.com/fwlink/?LinkId=85640) MSDN 库文章。  
  
SSMA 连接字符串始终包含提供程序参数。 此外，请确保连接到 DB2 时，包括端口参数。  
  

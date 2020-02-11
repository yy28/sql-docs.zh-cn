---
title: 连接到 Oracle （OracleToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 23a48cb6-ff30-49bb-b4a7-603ebcab336f
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 42ab1e77dbdb7cee237a9ec22c49a725a64390c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68264483"
---
# <a name="connect-to-oracle-oracletosql"></a>连接到 Oracle (OracleToSQL)
使用 "**连接到 oracle** " 对话框连接到要迁移的 Oracle 数据库。  
  
若要访问此对话框，请在 "**文件**" 菜单上选择 "**连接到 Oracle**"。 如果你以前已连接，则该命令将**重新连接到 Oracle**。  
  
## <a name="options"></a>选项  
**提供程序**  
选择用于连接到 Oracle 数据库的数据访问接口。 可用的提供程序是 Oracle 客户端提供程序和 OLE DB 提供程序。 默认值为 Oracle 客户端提供程序。  
  
**模式**  
选择 "标准"、"TNSNAME" 或 "连接字符串" 模式。  
  
-   在 "标准" 模式下，为提供程序、服务器名称、服务器端口、Oracle SID、用户名和密码输入或选择值。  
  
-   在 TNSNAME 模式下，你可以输入 Oracle 数据库的连接标识符（TNS 别名）、用户名和密码。  
  
-   在连接字符串模式下，你将提供一个连接字符串。  
  
    > [!IMPORTANT]  
    > 建议您不要使用连接字符串模式，因为文本可能包含密码，并以明文形式发送。  
  
默认值为 "标准模式"。  
  
**服务器名称**  
输入 Oracle 服务器名称。 默认服务器名称与计算机名称相同。 这是一个标准模式选项。  
  
**服务器端口**  
如果你使用的端口号不是1521（默认值），请输入端口号。 这是一个标准模式选项。  
  
**连接标识符**  
输入 Oracle connect 标识符。 这是在本地 tnsnames.ora. tnsnames.ora 文件中定义的数据库的别名。  
  
这是一个 TNSNAME 模式选项。  
  
**Oracle SID**  
输入数据库的 SID。 SID 是用于区分计算机上的 Oracle 数据库的标识符。 数据库的默认 SID 是数据库名称的前八个字符。  
  
这是一个标准模式选项。  
  
**用户名**  
输入 SSMA 将用于连接到 Oracle 数据库的用户名。  
  
**权限**  
输入用户名的密码。  
  
**连接字符串**  
> [!IMPORTANT]  
> 建议您不要使用连接字符串模式，因为文本可能包含密码，并以明文形式发送。  
  
如果使用连接字符串模式，请输入与 Oracle 的连接的完整连接字符串。  
  
连接字符串包含参数名称和值对。  
  
-   有关 OLE DB 连接字符串的信息，请参阅 MSDN Library 上的[Oracle 的 Microsoft OLE DB 提供程序](https://go.microsoft.com/fwlink/?LinkId=85640)文章。  
  
对于 SSMA 连接字符串，请始终包含提供程序参数。 此外，请确保在连接到 Oracle 时包含 Port 参数。  
  

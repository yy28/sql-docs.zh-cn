---
title: SQL Server Express 安全性
description: 介绍 SQL Server Express 的安全注意事项。
ms.date: 09/26/2019
ms.assetid: cf9cf6d9-4b05-43e9-ac7b-6cefbfcd6d4e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 9d6b711109f7d94e3bca8d9cf2bda6d2c124c798
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452027"
---
# <a name="sql-server-express-security"></a>SQL Server Express 安全性

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Microsoft SQL Server Express Edition (SQL Server Express) 基于 Microsoft SQL Server，支持数据库引擎的大部分功能。 它设计为默认情况下不重要的功能和网络连接。 这会减少恶意用户可用的攻击面。  
  
SQL Server Express 通常作为命名实例安装。 实例的默认名称为 `SQLExpress`。 命名实例是由计算机的网络名称和在安装过程中指定的实例名称标识的。  
  
## <a name="network-access"></a>网络访问  
出于安全原因，SQL Server Express 中默认禁用网络协议。 这会阻止来自外部用户的攻击，这些攻击可能会损害承载 SQL Server Express 实例的计算机。 您必须显式启用网络连接并启动 SQL Server Browser 服务，以从另一台计算机连接到 SQL Server Express 实例。  
  
启用网络连接后，SQL Server Express 实例的安全要求与其他版本 SQL Server 相同。  
  
## <a name="user-instances"></a>用户实例  
用户实例是由 SQL Server Express 的父实例生成的 SQL Server Express 数据库引擎的单独实例。 用户实例的主要目的是允许在最低特权用户帐户下运行 Windows 的用户在其本地计算机上具有对 SQL Server Express 实例的系统管理员（`sysadmin`）权限。 用户实例不适用于用户自己的计算机上的系统管理员。  
  
用户实例是通过代表用户的 SQL Server 或 SQL Server Express 的主实例生成的。 它在用户的 Windows 安全上下文下作为用户进程运行，而不是作为一种服务运行。 不允许 SQL Server 登录名;仅支持 Windows 登录名。 这可以防止在用户实例上执行的软件进行系统范围的更改，而用户不会有权限进行更改。 用户实例也称为子实例或客户端实例，有时使用 RANU 首字母缩写词（"以普通用户身份运行"）来引用。  
  
每个用户实例均独立于其父实例和在同一计算机上运行的其他用户实例。 用户实例上安装的数据库仅以单用户模式打开;多个用户无法连接到它们。 为用户实例禁用复制、分布式查询和远程连接。 当连接到用户实例时，用户对父 SQL Server Express 实例没有任何特殊权限。  
  
## <a name="external-resources"></a>外部资源  
有关 SQL Server Express 的详细信息，请参阅以下资源。  
  
|||  
|-|-|  
|[Microsoft SQL Server 2005 Express Edition 联机丛书](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms165706(v=sql.90))|SQL Server 2005 Express Edition 的完整文档。|  
|SQL Server 联机丛书中的[非管理员的用户实例](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/ms143684(v=sql.100))|描述如何创建和部署用户实例。|  
|[SQL Server Express 用户实例](sql-server-express-user-instances.md)|介绍 ADO.NET 应用程序中的用户实例功能。 提供有关如何启用用户实例、使用 <xref:Microsoft.Data.SqlClient.SqlConnection>、用户实例生存期和用户实例方案连接到用户实例的信息。|  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 安全性](sql-server-security.md)
- [SQL Server Express 用户实例](sql-server-express-user-instances.md)

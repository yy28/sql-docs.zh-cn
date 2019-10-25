---
title: SQL Server 中的应用程序安全方案
description: 包含对 ADO.NET 和 SQL Server 应用程序的各种应用程序安全方案进行讨论的主题。
ms.date: 09/26/2019
ms.assetid: 0164f3a4-406e-4693-bec3-03c8e18b46d7
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 711086e881951d9e82fd34851c451e5472e49d7e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452348"
---
# <a name="application-security-scenarios-in-sql-server"></a>SQL Server 中的应用程序安全方案

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

创建安全的 SQL Server 客户端应用程序没有一种正确的方式。 每个应用程序都具有独特的要求、部署环境和用户群体。 最初部署时合理安全的应用程序在一段时间内可能会变得不太安全。 不可能以任何准确性预测未来可能会出现的威胁。  
  
作为一种产品，SQL Server 已在许多版本的基础上进行了改进，以合并使开发人员能够创建安全数据库应用程序的最新安全功能。 但是，安全性并不是它需要持续监视和更新。  
  
## <a name="common-threats"></a>常见威胁  
开发人员需要了解安全威胁、提供的用于应对这些威胁的工具，以及如何避免波及安全漏洞。 最好将安全性看作是一个链，其中任何一个链接的中断都削弱了整体的强度。 下面列出了一些常见的安全威胁，此部分中的主题将对此进行详细讨论。  
  
### <a name="sql-injection"></a>SQL 注入  
SQL 注入是恶意用户输入 Transact-sql 语句而不是有效输入的过程。 如果在未经过验证的情况下将输入直接传递到服务器，且应用程序无意中执行了注入的代码，则攻击可能会损坏或破坏数据。 使用存储过程和参数化命令，避免使用动态 SQL，并限制所有用户的权限，可以防止受到 SQL Server 注入攻击。  
  
### <a name="elevation-of-privilege"></a>特权提升  
如果用户能够采用可信帐户（如所有者或管理员）的权限，则会发生特权提升攻击。 始终在最低权限的用户帐户下运行并仅分配所需的权限。 避免使用管理帐户或所有者帐户来执行代码。 这会限制攻击成功时可能发生的损坏量。 执行需要附加权限的任务时，请仅在任务的持续时间内使用过程签名或模拟。 你可以使用证书为存储过程签名，或使用模拟来临时分配权限。  
  
### <a name="probing-and-intelligent-observation"></a>探测和智能观察  
探测攻击可以使用应用程序生成的错误消息来搜索安全漏洞。 在所有过程代码中实现错误处理，以防止向最终用户返回 SQL Server 错误信息。  
  
### <a name="authentication"></a>身份验证  
如果在运行时构造基于用户输入的连接字符串，则在使用 SQL Server 登录名时可能会发生连接字符串注入攻击。 如果没有为有效关键字对检查连接字符串，则攻击者可以插入额外字符，这可能会访问服务器上的敏感数据或其他资源。 尽可能使用 Windows 身份验证。 如果必须使用 SQL Server 登录名，请使用 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> 在运行时创建和验证连接字符串。  
  
### <a name="passwords"></a>密码  
许多攻击都成功，因为入侵者能够获取或猜测特权用户的密码。 密码是抵御入侵者的第一道防线，因此设置强密码对于系统安全是绝对必要的。 为混合模式身份验证创建和强制实施密码策略。  
  
即使使用 Windows 身份验证，也始终为 `sa` 帐户分配一个强密码。  
  
## <a name="in-this-section"></a>在本节中  
[在 SQL Server 中编写安全动态 SQL](writing-secure-dynamic-sql.md)  
介绍使用存储过程编写安全的动态 SQL 的技术。  

## <a name="next-steps"></a>后续步骤
- [SQL Server 安全性](sql-server-security.md)

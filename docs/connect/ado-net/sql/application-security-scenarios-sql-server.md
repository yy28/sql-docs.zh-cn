---
title: SQL Server 中的应用程序安全方案
description: 包含对 ADO.NET 和 SQL Server 应用程序的各种应用程序安全方案进行讨论的主题。
ms.date: 09/26/2019
ms.assetid: 0164f3a4-406e-4693-bec3-03c8e18b46d7
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 2173a6aaf0f07ffaa50d87ed7563dca8022ceebc
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75250974"
---
# <a name="application-security-scenarios-in-sql-server"></a>SQL Server 中的应用程序安全方案

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

创建安全的 SQL Server 客户端应用程序没有唯一正确的方法。 每个应用程序都具有独特的要求、部署环境和用户群体。 即便应用程序的最初部署具有合理的安全性，但在一段时间后，安全性可能会降低。 没有办法准确地预测未来可能出现的威胁。  
  
作为一种产品，SQL Server 已在许多版本的基础上进行了改进，以合并最新的安全功能，使开发人员能够创建安全的数据库应用程序。 但是，安全性并不是与生俱来的，需要不断进行监视和更新。  
  
## <a name="common-threats"></a>常见威胁  
开发人员需要了解安全威胁、为应对这些威胁而提供的工具以及如何避免自身造成的安全漏洞。 最好将安全性视为一条链，其中任何一个链接的中断都会削弱整体实力。 下面列出了一些常见的安全威胁，本节中的主题将对此进行详细讨论。  
  
### <a name="sql-injection"></a>SQL 注入  
SQL 注入是恶意用户输入 Transact-SQL 语句而不是有效输入的过程。 如果输入未经验证直接传递到服务器，并且应用程序无意中执行了注入的代码，攻击可能会损坏或破坏数据。 使用存储过程和参数化命令，避免使用动态 SQL，并限制所有用户的权限，可以防止受到 SQL Server 注入攻击。  
  
### <a name="elevation-of-privilege"></a>特权提升  
当用户能够获得可信帐户（所有者或管理员）的特权时，就会发生特权提升攻击。 始终在最低特权的用户帐户下运行，并仅分配所需的权限。 避免使用管理帐户或所有者帐户来执行代码。 这可以限制攻击成功后可能发生的破坏程度。 执行需要附加权限的任务时，请仅在任务期间使用过程签名或模拟。 你可以使用证书为存储过程签名，或使用模拟来临时分配权限。  
  
### <a name="probing-and-intelligent-observation"></a>探测和智能观察  
探测攻击可以使用应用程序生成的错误消息来搜索安全漏洞。 在所有过程代码中实现错误处理，以防止向最终用户返回 SQL Server 错误信息。  
  
### <a name="authentication"></a>身份验证  
如果在运行时构造了基于用户输入的连接字符串，则在使用 SQL Server 登录名时可能会发生连接字符串注入攻击。 如果未检查连接字符串中是否有有效的关键字对，则攻击者可以插入其他字符，从而有可能访问服务器上的敏感数据或其他资源。 尽可能使用 Windows 身份验证。 如果必须使用 SQL Server 登录名，请在运行时使用 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> 创建和验证连接字符串。  
  
### <a name="passwords"></a>密码  
许多攻击成功是因为入侵者能够获取或猜出特权用户的密码。 密码是抵御入侵者的第一道防线，因此设置强密码对于系统安全是绝对必要的。 创建并强制实施用于混合模式身份验证的密码策略。  
  
即使使用 Windows 身份验证，也请始终为 `sa` 帐户分配一个强密码。  
  
## <a name="in-this-section"></a>在本节中  
[在 SQL Server 中编写安全动态 SQL](writing-secure-dynamic-sql.md)  
介绍使用存储过程编写安全动态 SQL 的技术。  

## <a name="next-steps"></a>后续步骤
- [SQL Server 安全性](sql-server-security.md)

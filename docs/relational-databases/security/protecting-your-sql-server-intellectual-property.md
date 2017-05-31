---
title: "保护 SQL Server 知识产权 | Microsoft Docs"
ms.custom: 
ms.date: 01/31/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- protecting intellectual property
- intellectual property
ms.assetid: 174a646a-d65c-4074-8249-d783e91be2dd
caps.latest.revision: 3
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 64297656b09d9f0843127887b490cef98d07b835
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="protecting-your-sql-server-intellectual-property"></a>保护 SQL Server 知识产权
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

软件开发人员经常关注如何将 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 数据应用程序分发给客户，但却忽视了如何防止客户分析和解构其应用程序。 此处的重要原则在于，保护知识产权是一个法律问题，许可协议中就会规定保护措施。 在其他人管理的计算机上安装 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 时，你必然会失去某些方面的控制权。 

## <a name="nature-of-the-problem"></a>问题的性质
计算机的所有者/管理员始终可以访问该计算机上安装的 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例。 如果你将自己的应用程序部署在客户的计算机上，由于客户是管理员，因此他们能够以 **sysadmin** 固定服务器角色成员的身份连接到 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 他们可以执行的操作包括授予权限、管理备份（包括将备份还原到其他计算机）、解密和移动数据文件，等等。有关详细信息，请参阅 [在系统管理员被锁定时连接到 SQL Server](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)。 

可以加密存储过程和数据，但无法隐藏数据结构。可将调试器附加到服务器进程的用户可在运行时从内存中检索已解密的过程和数据。

如果客户端不是计算机上的管理员，则你可以阻止客户端的访问。 你可以使用[透明数据加密](../../relational-databases/security/encryption/transparent-data-encryption-tde.md)来加密数据文件、加密备份，以及审核所有用户的操作。 但是，[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 管理员以及 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计算机的管理员可以撤消这些操作。

## <a name="solution"></a>解决方案
在不将 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安装在客户端计算机上的情况下，可通过多种方式配置客户端数据访问。 最简单的方法可能是使用 [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]（也许可以结合 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)），使客户端不会成为管理员。 有关如何开始使用 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 的详细信息，请参阅[什么是 SQL 数据库？SQL 数据库简介](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)。  

还可以将 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 托管在自己的网络中，并允许客户端在你的网络中直接或通过 Web 应用程序访问数据。

## <a name="see-also"></a>另请参阅

[SQL Server 数据库引擎和 Azure SQL Database 的安全中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
[保护 SQL Server](../../relational-databases/security/securing-sql-server.md)  



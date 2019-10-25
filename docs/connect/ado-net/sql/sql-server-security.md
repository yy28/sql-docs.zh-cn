---
title: SQL Server 安全性
description: 简要介绍 SQL Server 安全功能，以及创建面向 SQL Server 的安全 ADO.NET 应用程序的应用程序方案。
ms.date: 09/26/2019
ms.assetid: 9053724d-a1fb-4f0f-b9dc-7f6dd893e8ff
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: bb9e02743122958cb567e01f5011fc9f8b3481e6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452004"
---
# <a name="sql-server-security"></a>SQL Server 安全性

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server 具有许多支持创建安全数据库应用程序的功能。  
  
无论要使用哪个版本的 SQL Server，通用安全注意事项（如数据盗窃和蓄意破坏）都适用。 还应将数据完整性视为一个安全问题。 如果数据不受保护，则可能会毫无意义，前提是允许即席数据操作，并且数据被意外或恶意修改为不正确的值或被完全删除。 此外，通常还必须遵守法律要求，例如正确存储机密信息。 存储某些类型的个人数据是完全规定的，具体取决于特定司法辖区中适用的法律。  
  
与每个版本的 Windows 一样，每个版本的 SQL Server 都具有不同的安全功能，版本越高，功能越强。 必须了解的是，安全功能本身无法保证安全的数据库应用程序。 每个数据库应用程序都具有独特的要求、执行环境、部署模型、物理位置和用户群体。 在范围内处于本地的某些应用程序可能只需要最小的安全性，而其他本地应用程序或通过 Internet 部署的应用程序可能需要严格的安全措施和持续的监视和评估。  
  
SQL Server 数据库应用程序的安全要求应该在设计时就加以考虑，而不应事后再考虑。 在开发周期的早期评估威胁使你能够在检测到漏洞的任何地方降低潜在损害。  
  
即使应用程序的初始设计非常合理，系统也会出现新的威胁。 通过在数据库中创建多个防线，可以最大程度地减少安全漏洞波及的损害。 第一道防线是通过从不授予比绝对必需的权限更多的权限来减少攻击面。  
  
本节中的主题简要说明了 SQL Server 中开发人员相关的安全功能，并提供了指向 SQL Server 联机丛书中相关主题以及提供更详细说明的其他资源的链接。  
  
## <a name="in-this-section"></a>在本节中  
[SQL Server 中的身份验证](authentication-sql-server.md)  
介绍 SQL Server 中的登录名和身份验证，并提供指向其他资源的链接。 
  
[SQL Server 中的应用程序安全方案](application-security-scenarios-sql-server.md)  
包含对 ADO.NET 和 SQL Server 应用程序的各种应用程序安全方案进行讨论的主题。  
  
[SQL Server Express 安全性](sql-server-express-security.md)  
介绍 SQL Server Express 的安全注意事项。  
  
## <a name="related-sections"></a>相关章节  
[SQL Server 数据库引擎和 Azure SQL Database 的安全中心](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
描述 SQL Server 和 Azure SQL 数据库的安全注意事项。

[安装 SQL Server 的安全注意事项](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
描述在安装 SQL Server 之前要考虑的安全问题。

## <a name="next-steps"></a>后续步骤
- [SQL Server 和 ADO.NET](index.md)

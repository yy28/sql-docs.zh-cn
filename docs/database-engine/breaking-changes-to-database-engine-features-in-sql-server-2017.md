---
title: 数据库引擎：中断性变更 | Microsoft Docs
titleSuffix: SQL Server 2017
description: SQL Server 2017 中数据库引擎功能的重大更改
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- breaking changes 2017 [SQL Server]
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: b41127570a91cd49137955530433c5e2f437aab3
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "75244710"
---
# <a name="breaking-changes-to-database-engine-features-in-includesssqlv14-mdincludessssqlv14-mdmd"></a>[!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] 中数据库引擎功能的重大更改
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]


  本主题介绍 [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] 中的中断性变更。 这些更改可能导致基于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的早期版本的应用程序、脚本或功能无法继续使用。 在进行升级时可能会遇到这些问题。  
  
## <a name="breaking-changes-in-includesssqlv14-mdincludessssqlv14-mdmd-includessdeincludesssde-mdmd"></a>[!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] 中的中断性变更  
  
-  CLR 在 .NET Framework 中使用代码访问安全性 (CAS)（不可再作为安全边界）。 引入叫做 `clr strict security` 的 `sp_configure` 选项（该选项以 [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)] 开头）以增强 CLR 程序集的安全性。 默认情况下启用 clr 严格安全性，并将 `SAFE` 和 `EXTERNAL_ACCESS` CLR 程序集视为标记为 `UNSAFE`。 可禁用 `clr strict security` 选项以实现后向兼容性，但不建议这样做。 禁用 `clr strict security` 后，使用 `PERMISSION_SET = SAFE` 创建的 CLR 程序集可以访问外部系统资源、调用非托管的代码以及获取“sysadmin”  特权。 启用严格安全性后，未签名的任何程序集都将加载失败。 此外，如果数据库具有 `SAFE` 或 `EXTERNAL_ACCESS` 程序集，则 `RESTORE` 或 `ATTACH DATABASE` 语句可以完成，但程序集可能加载失败。   
  若要加载程序集，必须更改或删除并重新创建每个程序集，以便使用证书或非对称密钥对程序集进行签名，这样的证书或密钥具有与服务器上的 `UNSAFE ASSEMBLY` 权限相应的登录名。 有关详细信息，请参阅 [CLR 严格安全性](../database-engine/configure-windows/clr-strict-security.md)。 

## <a name="previous-versions"></a> 先前版本  

- [SQL Server 2016 中数据库引擎功能的重大更改](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)

- [SQL Server 2014 中数据库引擎功能的重大更改](https://docs.microsoft.com/sql/database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016?view=sql-server-2014#SQL14)

#### <a name="archived-documentation-for-very-old-versions-of-sql-server"></a>较早版本的 SQL Server 的存档文档

[!INCLUDE[Archived documentation for very old versions of SQL Server](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>另请参阅  
 [SQL Server 2016 中不推荐使用的数据库引擎功能](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2016 中废止的数据库引擎功能](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [SQL Server 数据库引擎的向后兼容性](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [ALTER DATABASE 兼容级别 (Transact-SQL)](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  

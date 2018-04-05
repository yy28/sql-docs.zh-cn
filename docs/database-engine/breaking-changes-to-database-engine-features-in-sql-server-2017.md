---
title: SQL Server 2017 中数据库引擎功能的重大更改 | Microsoft Docs
description: SQL Server 2017 中数据库引擎功能的重大更改
ms.date: 04/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: database-engine
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- breaking changes 2017 [SQL Server]
ms.assetid: ''
caps.latest.revision: 1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0b560ce9771f1ce93a3dc4b6269d636e5e66df99
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2018
---
# <a name="breaking-changes-to-database-engine-features-in-includesssqlv14-mdincludessssqlv14-mdmd"></a>[!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] 中数据库引擎功能的重大更改
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]


  本主题介绍 [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)] 中的重大更改。 这些更改可能导致基于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的早期版本的应用程序、脚本或功能无法继续使用。 在进行升级时可能会遇到这些问题。  
  
## <a name="breaking-changes-in-includesssqlv14-mdincludessssqlv14-mdmdincludessdeincludesssde-mdmd"></a>[!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)] 中的重大更改  
  
-  CLR 在 .NET Framework 中使用代码访问安全性 (CAS)（不可再作为安全边界）。 引入叫做 `clr strict security` 的 `sp_configure` 选项（该选项以 [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)] 开头）以增强 CLR 程序集的安全性。 默认情况下启用 clr 严格安全性，并将 `SAFE` 和 `EXTERNAL_ACCESS` CLR 程序集视为标记为 `UNSAFE`。 可禁用 `clr strict security` 选项以实现后向兼容性，但不建议这样做。 禁用 `clr strict security` 后，使用 `PERMISSION_SET = SAFE` 创建的 CLR 程序集可以访问外部系统资源、调用非托管的代码以及获取“sysadmin”特权。 启用严格安全性后，未签名的任何程序集都将加载失败。 此外，如果数据库具有 `SAFE` 或 `EXTERNAL_ACCESS` 程序集，则 `RESTORE` 或 `ATTACH DATABASE` 语句可以完成，但程序集可能加载失败。   
  若要加载程序集，必须更改或删除并重新创建每个程序集，以便使用证书或非对称密钥对程序集进行签名，这样的证书或密钥具有与服务器上的 `UNSAFE ASSEMBLY` 权限相应的登录名。 有关详细信息，请参阅 [CLR 严格安全性](../database-engine/configure-windows/clr-strict-security.md)。 


  
## <a name="previous-versions"></a>先前版本  

-   [SQL Server 2016 中数据库引擎功能的重大更改](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)  
  
-   [SQL Server 2014 中数据库引擎功能的重大更改](https://msdn.microsoft.com/library/ms143179\(v=sql.120\))  
  
-   [SQL Server 2012 中数据库引擎功能的重大更改](https://msdn.microsoft.com/library/ms143179\(v=sql.110\))  
  
-   [SQL Server 2008 中数据库引擎功能的重大更改](https://msdn.microsoft.com/library/ms143179\(v=sql.100\))  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 2016 中不推荐使用的数据库引擎功能](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2016 中废止的数据库引擎功能](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [SQL Server 数据库引擎的向后兼容性](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [ALTER DATABASE 兼容级别 (Transact-SQL)](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  

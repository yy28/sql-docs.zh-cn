---
title: SQL Server 2014 中管理工具功能的重大更改 |Microsoft Docs
ms.custom: ''
ms.date: 11/27/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 3ff3fad8-b569-4516-bd58-5a3efeb537e2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0487b6ab0958e0b83d4e8e34be507b5b3211ac87
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936098"
---
# <a name="breaking-changes-to-management-tools-features-in-sql-server-2014"></a>SQL Server 2014 中管理工具功能的重大更改
  本主题介绍管理工具功能的重大更改。 这些更改可能导致基于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的早期版本的应用程序、脚本或功能无法继续使用。 在进行升级时可能会遇到这些问题。 有关详细信息，请参阅 [Use Upgrade Advisor to Prepare for Upgrades](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)。  
  
## <a name="breaking-changes-in-sssql14"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中的重大更改。  
 将很快提供相关信息。  
  
## <a name="breaking-changes-in-sssql11"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中的重大更改。  
  
### <a name="you-cannot-use-sssql11-management-tools-to-create-a-utility-control-point-on-a-sskilimanjaro-instance-of-sql-server"></a>不能使用 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 管理工具在 SQL Server 的 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 实例上创建实用工具控制点  
 若要在 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]实例上创建实用工具控制点，请使用 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 管理工具。  
  
### <a name="smo-has-been-reversioned-in-sssql11"></a>在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中复原了 SMO  
 使用 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 或早期版本的 SMO 开发的代码可能需要稍做更改才能针对 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 生成。 有关详细信息，请参阅 [Backward Compatibility in SMO](../relational-databases/server-management-objects-smo/backward-compatibility-in-smo.md)。  

## <a name="breaking-changes-in-sql-server-2005"></a><a name="previous-versions"></a>SQL Server 2005 中的重大更改  

[!INCLUDE[Archived documentation for very old versions of SQL Server](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>另请参阅  
 [向后兼容性](../../2014/getting-started/backward-compatibility.md)  
 [有关 SQL Server 2014 中管理工具功能的重大更改的详细信息](breaking-changes-to-database-engine-features-in-sql-server-2016.md?view=sql-server-2014)  
  
  

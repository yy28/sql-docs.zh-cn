---
title: 工具管理重大更改 SQL Server 2014 中的功能 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3ff3fad8-b569-4516-bd58-5a3efeb537e2
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 33e204958f9cea2db092f2a9c4b7d20648e4182c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027969"
---
# <a name="breaking-changes-to-management-tools-features-in-sql-server-2014"></a>SQL Server 2014 中管理工具功能的重大更改
  本主题介绍管理工具功能的重大更改。 这些更改可能导致基于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的早期版本的应用程序、脚本或功能无法继续使用。 在进行升级时可能会遇到这些问题。 有关详细信息，请参阅 [Use Upgrade Advisor to Prepare for Upgrades](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)。  
  
## <a name="breaking-changes-in-includesssql14includessssql14-mdmd"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中的重大更改。  
 将很快提供相关信息。  
  
## <a name="breaking-changes-in-includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中的重大更改。  
  
### <a name="you-cannot-use-includesssql11includessssql11-mdmd-management-tools-to-create-a-utility-control-point-on-a-includesskilimanjaroincludessskilimanjaro-mdmd-instance-of-sql-server"></a>不能使用 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 管理工具在 SQL Server 的 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 实例上创建实用工具控制点  
 若要在 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]实例上创建实用工具控制点，请使用 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 管理工具。  
  
### <a name="smo-has-been-reversioned-in-includesssql11includessssql11-mdmd"></a>SMO 已被重新修改了中的版本 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 使用 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 或早期版本的 SMO 开发的代码可能需要稍做更改才能针对 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 生成。 有关详细信息，请参阅 [Backward Compatibility in SMO](../relational-databases/server-management-objects-smo/backward-compatibility-in-smo.md)。  
  
## <a name="see-also"></a>请参阅  
 [后向兼容性](../../2014/getting-started/backward-compatibility.md)  
  
  
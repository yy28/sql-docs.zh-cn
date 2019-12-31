---
title: SQL Server 2014 中不推荐使用的 SQL Server 功能 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: fdc0c778-cc8d-42ab-8833-4deb4329f37a
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44fbab98aa017be66cd4dc369a713f44e8d248d5
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228220"
---
# <a name="deprecated-sql-server-features-in-sql-server-2014"></a>SQL Server 2014 中不推荐使用的 SQL Server 功能
  本主题介绍 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中仍然可用但不推荐使用的功能。 按照计划， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]未来版本将不再具有这些功能。 在新的应用程序中不应使用这些不推荐使用的功能。  
  
## <a name="features-not-supported-in-the-next-version-of-includessnoversionincludesssnoversion-mdmd"></a>下一版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中不支持的功能  
 下一版 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 将不再支持以下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]功能。 请不要在新的开发工作中使用这些功能，并尽快修改当前还在使用这些功能的应用程序。 功能名称列在跟踪事件中显示为 ObjectName，而在性能计数器和 sys.dm_os_performance_counters 中显示为 instance_name。 功能 ID 在跟踪事件中显示为 ObjectId。  
  
|类别|不推荐使用的功能|替代功能|功能名称|功能 ID|  
|--------------|------------------------|-----------------|------------------|----------------|  
|数据可编程性|[sys. soap_endpoints &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-soap-endpoints-transact-sql)|Windows Communications Foundation (WCF) 或 ASP.NET|本机 XML Web 服务|22|  
|数据可编程性|[sys. endpoint_webmethods &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-endpoint-webmethods-transact-sql)|Windows Communications Foundation (WCF) 或 ASP.NET|本机 XML Web 服务|23|  
  
### <a name="slipstream-functionality"></a>补充功能  
 [产品更新功能](/previous-versions/sql/sql-server-2012/hh231670(v=sql.110)?redirectedfrom=MSDN)是在 SQL Server 2012 中引入的，是 PCU1 中[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]提供的补充功能的扩展。 在 SQL Server 2014 中，推荐使用 "产品更新" 功能来 SQL Server 集成。 因此，不应再使用与原始滑功能关联的命令行参数/*PCUSource*和/*CUSource*。 这些参数将继续运行，但可能会在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]安装程序的未来版本中删除。 建议使用的参数是/*UpdateSource* ，它结合了原始滑参数的功能：/*PCUSource*和/*CUSource*。  
  
 有关 PCU1 中[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]提供的补充功能的详细信息，请参阅补充[SQL Server 更新](https://go.microsoft.com/fwlink/?LinkId=219945)（。https://go.microsoft.com/fwlink/?LinkId=219945)  
 有关如何使用/*UpdateSource*将 SQL Server 生成进行补充的信息，请参阅以下内容：
 
 - [如何使用更新的安装包修补 SQL Server 2012 安装程序（使用 UpdateSource 获取智能安装）](https://blogs.msdn.microsoft.com/jason_howell/2012/08/28/how-to-patch-sql-server-2012-setup-with-an-updated-setup-package-using-updatesource-to-get-a-smart-setup/)
 
 - [SQL Server 2012 安装程序刚刚获得更智能 .。。](https://techcommunity.microsoft.com/t5/SQL-Server-Support/SQL-Server-2012-Setup-just-got-smarter-8230/ba-p/317440)
 
## <a name="see-also"></a>另请参阅  
 [向后兼容性](../../2014/getting-started/backward-compatibility.md)  
  
  

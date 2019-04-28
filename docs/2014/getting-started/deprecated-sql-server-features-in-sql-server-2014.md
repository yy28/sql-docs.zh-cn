---
title: 不推荐使用 SQL Server 2014 中的 SQL Server 功能 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: fdc0c778-cc8d-42ab-8833-4deb4329f37a
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4abd066dd2fc971528468fb7104cb0c11e088150
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62843025"
---
# <a name="deprecated-sql-server-features-in-sql-server-2014"></a>SQL Server 2014 中不推荐使用的 SQL Server 功能
  本主题介绍 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中仍然可用但不推荐使用的功能。 按照计划， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]未来版本将不再具有这些功能。 在新的应用程序中不应使用这些不推荐使用的功能。  
  
## <a name="features-not-supported-in-the-next-version-of-includessnoversionincludesssnoversion-mdmd"></a>下一版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中不支持的功能  
 下一版 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 将不再支持以下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]功能。 请不要在新的开发工作中使用这些功能，并尽快修改当前还在使用这些功能的应用程序。 功能名称列在跟踪事件中显示为 ObjectName，而在性能计数器和 sys.dm_os_performance_counters 中显示为 instance_name。 功能 ID 在跟踪事件中显示为 ObjectId。  
  
|Category|不推荐使用的功能|替代功能|功能名称|功能 ID|  
|--------------|------------------------|-----------------|------------------|----------------|  
|数据可编程性|[sys.soap_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-soap-endpoints-transact-sql)|Windows Communications Foundation (WCF) 或 ASP.NET|本机 XML Web 服务|22|  
|数据可编程性|[sys.endpoint_webmethods &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-endpoint-webmethods-transact-sql)|Windows Communications Foundation (WCF) 或 ASP.NET|本机 XML Web 服务|23|  
  
### <a name="slipstream-functionality"></a>补充功能  
 产品更新功能将替换 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] PCU1 中提供的补充功能。 因此的命令行参数 /*PCUSource*和 /*CUSource*、 与补充应不再使用功能相关联。 这些参数将继续有效，但可能会在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安装程序的将来版本中删除。 /*UpdateSource*参数结合了 Slipstream 参数的功能 /*PCUSource*和 /*CUSource*。  
  
 有关详细信息中提供的补充功能[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]PCU1，请参阅[补充 SQL Server 更新](https://go.microsoft.com/fwlink/?LinkId=219945)(https://go.microsoft.com/fwlink/?LinkId=219945)。  
  
## <a name="see-also"></a>请参阅  
 [向后兼容性](../../2014/getting-started/backward-compatibility.md)  
  
  

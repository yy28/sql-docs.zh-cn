---
title: Analysis Services 配置-数据目录 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ef732855-b7af-4f40-a619-5573c1c354bb
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 4ff1cd03eb260d892c22c36285fa07d912994510
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66096812"
---
# <a name="analysis-services-configuration---data-directories"></a>Analysis Services 配置 - 数据目录
  下表中的默认目录是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程中可由用户配置的目录。 访问这些文件的权限授予本地管理员和安装过程中创建并预配的 SQLServerMSASUser$\< 实例 > 安全组成员。  
  
## <a name="uielement-list"></a>UIElement 列表  
  
|说明|默认目录|建议|  
|-----------------|-----------------------|---------------------|  
|数据根目录|C:\Program Files\Microsoft SQL Server\MSAS12。\<InstanceID> \Olap\data\|确保 \Program files\Microsoft SQL Server \ 文件夹受到有限权限的保护。 在许多配置中，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 性能取决于数据目录所在的存储区的性能。 请将此目录放置在附加到系统上的最高性能存储区中。 对于故障转移群集安装，应确保数据目录位于共享磁盘上。|  
|日志文件目录|C:\Program Files\Microsoft SQL Server\MSAS12。\<InstanceID> \olap\log\|这是[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]日志文件的目录，它包括 FlightRecorder 日志。 如果要延长网络流量记录器持续时间，请确保该日志目录有足够的空间。|  
|Temp 目录|C:\Program Files\Microsoft SQL Server\MSAS12。\<InstanceID> \Olap\temp\|将 Temp 目录放置在高性能存储子系统上。|  
|备份目录|C:\Program Files\Microsoft SQL Server\MSAS12。\<InstanceID> \olap\backup\|这是[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]默认备份文件的目录。 对于 PowerPivot for SharePoint 安装，这还是 PowerPivot 系统服务缓存 PowerPivot 数据文件的位置。<br /><br /> 确保设置合适的权限以防止数据丢失，并确保 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务的用户组具有写入备份目录的足够权限。 不支持对备份目录使用映射的驱动器。|  
  
## <a name="notes"></a>说明  
  
-   在 SharePoint 场上部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例将应用程序文件、数据文件和属性存储于内容数据库和服务应用程序数据库中。  
  
-   向现有安装添加功能时，不能更改以前安装的功能的位置，也不能为新功能指定该位置。  
  
-   如果指定非默认的安装目录，请确保安装文件夹对于此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例是唯一的。 此对话框中的任何目录都不应与其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的目录共享。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例中的[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件也应安装到单独的目录。  
  
-   在下列情况下，不能安装程序文件和数据文件：  
  
    -   在可移动磁盘驱动器上  
  
    -   在使用压缩的文件系统上  
  
    -   在系统文件所在的目录上  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 默认实例和命名实例的文件位置](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)  
  
  

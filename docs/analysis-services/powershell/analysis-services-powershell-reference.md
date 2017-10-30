---
title: "Analysis Services PowerShell 参考 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/21/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 6c435e40-bfaf-4073-8cef-bc3260602246
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7999198236f93a1c64ea731659017bce4efd3e55
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="analysis-services-powershell-reference"></a>Analysis Services PowerShell 参考

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]


  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中包含 PowerShell cmdlet [SqlServer 模块](https://www.powershellgallery.com/packages/SqlServer/21.0.17099)。 
  
>[!NOTE] 
> Azure Analysis Services 数据库操作使用相同的 sql Server 模块作为 SQL Server Analysis Services。 但是，并非所有的 cmdlet 为 Azure Analysis Services 支持。 若要了解详细信息，请参阅[使用 PowerShell 管理 Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-powershell)。
  
##  <a name="bkmk_cmdlets"></a> Analysis Services Cmdlet  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供了与 **Microsoft.AnalysisServices** 命名空间中的方法对应的 cmdlet。 下表描述每个 cmdlet，并提供指向相应 AMO 方法的链接。  
  
 如果想要使用 PowerShell 执行未在下表中表示的任务（例如，创建或同步某一数据库），则可为该操作编写一个 TMSL 或 XMLA 脚本，然后使用 **Invoke-ASCmd** cmdlet 执行该脚本。  
  
|Cmdlet|Description|等效的 AMO 方法|  
|------------|-----------------|----------------------------|  
|[Add-RoleMember cmdlet](../../analysis-services/powershell/add-rolemember-cmdlet.md)|向数据库角色添加成员。|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Add%2A>|  
|[Backup-ASDatabase cmdlet](../../analysis-services/powershell/backup-asdatabase-cmdlet.md)|备份 Analysis Services 数据库。|[Database.Backup](https://msdn.microsoft.com/library/microsoft.analysisservices.database.backup.aspx)|  
|[Invoke-ASCmd cmdlet](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)|以 XMLA 或 TSML (JSON) 格式执行查询或脚本。|<xref:Microsoft.AnalysisServices.Core.Server.Execute%2A>|  
|[Invoke-ProcessASDatabase](../../analysis-services/powershell/invoke-processasdatabase.md)|处理数据库。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessCube cmdlet](../../analysis-services/powershell/invoke-processcube-cmdlet.md)|处理多维数据集。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessDimension cmdlet](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)|处理维度。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessPartition cmdlet](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)|处理分区。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessTable cmdlet](../../analysis-services/powershell/invoke-processtable-cmdlet.md)|处理表格模型中，兼容性模式 1200年或更高版本中的表。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Merge-Partition cmdlet](../../analysis-services/powershell/merge-partition-cmdlet.md)|合并分区。|<xref:Microsoft.AnalysisServices.Partition.Merge%2A>|  
|[New-RestoreFolder cmdlet](../../analysis-services/powershell/new-restorefolder-cmdlet.md)|创建文件夹以便包含数据库备份。|<xref:Microsoft.AnalysisServices.RestoreFolder>|  
|[New-RestoreLocation cmdlet](../../analysis-services/powershell/new-restorelocation-cmdlet.md)|指定将数据库还原到其上的一个或多个远程服务器。|<xref:Microsoft.AnalysisServices.RestoreLocation>|  
|[Remove-RoleMember cmdlet](../../analysis-services/powershell/remove-rolemember-cmdlet.md)|从数据库角色中删除成员。|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Remove%2A>|  
|[Restore-ASDatabase cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)|还原服务器实例上的数据库。|<xref:Microsoft.AnalysisServices.Core.Server.Restore%2A>|  
  

  
  


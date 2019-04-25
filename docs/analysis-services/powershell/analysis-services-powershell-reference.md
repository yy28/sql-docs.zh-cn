---
title: Analysis Services PowerShell 参考 |Microsoft Docs
ms.date: 06/25/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 13ea15a23bbf6de6c50b494f709f65cae2f7c48b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62509831"
---
# <a name="analysis-services-powershell-reference"></a>Analysis Services PowerShell 参考
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中包含 PowerShell cmdlet [SqlServer 模块](https://www.powershellgallery.com/packages/SqlServer/21.0.17099)。 
  
>[!NOTE] 
> Azure Analysis Services 数据库操作与 SQL Server Analysis Services 使用相同的 SqlServer 模块。 但是，并非所有 cmdlet 在 Azure Analysis services 都支持。 若要了解详细信息，请参阅[使用 PowerShell 管理 Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-powershell)。
  
##  <a name="bkmk_cmdlets"></a> Analysis Services Cmdlet  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供了与 **Microsoft.AnalysisServices** 命名空间中的方法对应的 cmdlet。 下表描述每个 cmdlet，并提供指向相应 AMO 方法的链接。  
  
 如果想要使用 PowerShell 执行未在下表中表示的任务（例如，创建或同步某一数据库），则可为该操作编写一个 TMSL 或 XMLA 脚本，然后使用 **Invoke-ASCmd** cmdlet 执行该脚本。  
  
|Cmdlet|Description|等效的 AMO 方法|  
|------------|-----------------|----------------------------|  
|[Add-RoleMember cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/Add-RoleMember)|向数据库角色添加成员。|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Add%2A>|  
|[Backup-ASDatabase cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/backup-asdatabase)|备份 Analysis Services 数据库。|[Database.Backup](https://msdn.microsoft.com/library/microsoft.analysisservices.database.backup.aspx)|  
|[Invoke-ASCmd cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/invoke-ascmd)|以 XMLA 或 TSML (JSON) 格式执行查询或脚本。|<xref:Microsoft.AnalysisServices.Core.Server.Execute%2A>|  
|[Invoke-ProcessASDatabase](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processasdatabase)|处理数据库。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessCube cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processcube)|处理多维数据集。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessDimension cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processdimension)|处理维度。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessPartition cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processpartition)|处理分区。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessTable cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processtable)|处理表格模型中，兼容性模型 1200年或更高版本中的表。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Merge-Partition cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/merge-partition)|合并分区。|<xref:Microsoft.AnalysisServices.Partition.Merge%2A>|  
|[New-RestoreFolder cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/new-restorefolder)|创建文件夹以便包含数据库备份。|<xref:Microsoft.AnalysisServices.RestoreFolder>|  
|[New-RestoreLocation cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/new-restorelocation)|指定将数据库还原到其上的一个或多个远程服务器。|<xref:Microsoft.AnalysisServices.RestoreLocation>|  
|[Remove-RoleMember cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/remove-rolemember)|从数据库角色中删除成员。|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Remove%2A>|  
|[Restore-ASDatabase cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/restore-asdatabase)|还原服务器实例上的数据库。|<xref:Microsoft.AnalysisServices.Core.Server.Restore%2A>|  
  

  
  

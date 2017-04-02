---
title: "Analysis Services PowerShell 参考 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 6c435e40-bfaf-4073-8cef-bc3260602246
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Analysis Services PowerShell 参考
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包括 PowerShell 提供程序 (SQLAS) 和 cmdlet (SQLASCMDLETS)，以便可以使用 Windows PowerShell 导航、管理和查询 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象。 有关加载和使用该提供程序和 cmdlet 的详细信息，请参阅 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)。 有关如何在 PowerShell 中使用 AMO 类型来创建表格数据库的示例，请参阅 [AMO PowerShell Example](../../analysis-services/powershell/amo-powershell-example.md)。  
  
##  <a name="bkmk_cmdlets"></a> Analysis Services Cmdlet  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供了与 **Microsoft.AnalysisServices** 命名空间中的方法对应的 cmdlet。 下表描述每个 cmdlet，并提供指向相应 AMO 方法的链接。  
  
 如果想要使用 PowerShell 执行未在下表中表示的任务（例如，创建或同步某一数据库），则可为该操作编写一个 TMSL 或 XMLA 脚本，然后使用 **Invoke-ASCmd** cmdlet 执行该脚本。  
  
|Cmdlet|Description|等效的 AMO 方法|  
|------------|-----------------|----------------------------|  
|[Add-RoleMember cmdlet](../../analysis-services/powershell/add-rolemember-cmdlet.md)|向数据库角色添加成员。|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Add%2A>|  
|[Backup-ASDatabase cmdlet](../../analysis-services/powershell/backup-asdatabase-cmdlet.md)|备份 Analysis Services 数据库。|<xref:Microsoft.AnalysisServices.Database.Backup%2A>|  
|[Invoke-ASCmd cmdlet](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)|以 XMLA 或 TSML (JSON) 格式执行查询或脚本。|<xref:Microsoft.AnalysisServices.Server.Execute%2A>|  
|[Invoke-ProcessASDatabase](../../analysis-services/powershell/invoke-processasdatabase.md)|处理数据库。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessCube cmdlet](../../analysis-services/powershell/invoke-processcube-cmdlet.md)|处理多维数据集。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessDimension cmdlet](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)|处理维度。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessPartition cmdlet](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)|处理分区。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessTable cmdlet](../../analysis-services/powershell/invoke-processtable-cmdlet.md)|处理兼容性级别为 1200 或更高的表格模型中的表。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Merge-Partition cmdlet](../../analysis-services/powershell/merge-partition-cmdlet.md)|合并分区。|<xref:Microsoft.AnalysisServices.Partition.Merge%2A>|  
|[New-RestoreFolder cmdlet](../../analysis-services/powershell/new-restorefolder-cmdlet.md)|创建文件夹以便包含数据库备份。|<xref:Microsoft.AnalysisServices.RestoreFolder>|  
|[New-RestoreLocation cmdlet](../../analysis-services/powershell/new-restorelocation-cmdlet.md)|指定将数据库还原到其上的一个或多个远程服务器。|<xref:Microsoft.AnalysisServices.RestoreLocation>|  
|[Remove-RoleMember cmdlet](../../analysis-services/powershell/remove-rolemember-cmdlet.md)|从数据库角色中删除成员。|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Remove%2A>|  
|[Restore-ASDatabase cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)|还原服务器实例上的数据库。|<xref:Microsoft.AnalysisServices.Server.Restore%2A>|  
  
## 另请参阅  
 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Analysis Services 中表格模型的兼容级别](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Analysis Services 脚本语言（支持 XMLA 的 ASSL）](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)  
  
  
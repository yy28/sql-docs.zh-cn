---
title: "附加和分离 Analysis Services 数据库 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.ssmsimbi.AttachDatabase.f1
- sql13.asvs.ssms.attachdatabase.f1
- sql13.asvs.ssmsimbi.DetachDatabase.f1
- sql13.asvs.ssms.detachdatabase.f1
helpviewer_keywords:
- databases [Analysis Services], attach
- databases [Analysis Services], detach
ms.assetid: 41887413-2d47-49b8-8614-553cb799fb18
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f7cc88be76e8ad64d81465543ab4f463c98687e7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="attach-and-detach-analysis-services-databases"></a>附加和分离 Analysis Services 数据库
  在某些情况下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库管理员 (dba) 经常需要将数据库脱机一段时间，然后在同一服务器实例或其他服务器实例上将数据库恢复联机。 根据业务需要（例如，将数据库移到另一个磁盘以获得更好的性能、为数据库扩容获取空间或升级产品），经常需要进行上述操作。 对于上述所有情况，通过“附加”和“分离”命令，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dba 可以很容易地使数据库脱机和恢复联机。  
  
## <a name="attach-and-detach-commands"></a>附加和分离命令。  
 通过 **Attach** 命令可使已脱机的数据库恢复联机。 可以将该数据库附加到原始的服务器实例，也可以附加到另一个实例。 在附加数据库时，用户可以为该数据库指定 **ReadWriteMode** 设置。 使用 **Detach** 命令可使数据库与服务器脱机。  
  
## <a name="attach-and-detach-usage"></a>附加和分离命令的用法  
 **Attach** 命令用于使现有数据库结构联机。 如果该数据库是在 **ReadWrite** 模式下附加的，则只能将其附加到服务器实例一次。 但是，如果此数据库是在 **ReadOnly** 模式下附加的，则可以将其多次附加到不同的服务器实例。 但是，不能将同一数据库多次附加到同一服务器实例。 即使已将数据复制到不同的文件夹中，在尝试多次附加同一数据库时也会引发错误。  
  
> [!IMPORTANT]  
>  如果分离数据库时需要输入密码，则附加数据库时需要输入相同的密码。  
  
 **Detach** 命令用于使现有数据库结构脱机。 分离数据库时，应提供一个密码来保护机密的元数据。  
  
> [!IMPORTANT]  
>  若要保护数据文件的内容，应针对文件夹、子文件夹和数据文件使用访问控制列表。  
  
 分离数据库时，服务器会执行下列步骤。  
  
|分离读/写数据库|分离只读数据库|  
|--------------------------------------|-------------------------------------|  
|1) 服务器会对数据库上的 CommitExclusive 锁发出请求<br /><br /> 2) 服务器会等待，直到提交或回滚所有正在进行的事务<br /><br /> 3) 服务器会构建分离数据库必须具备的所有元数据<br /><br /> 4) 将数据库标记为已删除<br /><br /> 5) 服务器提交事务|1) 将数据库标记为已删除<br /><br /> 2) 服务器提交事务<br /><br /> 注意：不能更改只读数据库的分离密码。 如果为已包含密码的附加数据库提供密码参数，则会产生错误。|  
  
 **Attach** 和 **Detach** 命令必须作为单独的操作执行。 在同一事务中，不能将它们与其他操作一起执行。 同样， **Attach** 和 **Detach** 命令都是原子事务命令。 这意味着操作只有成功或失败两种情况。 数据库不会处于未完成的状态。  
  
> [!IMPORTANT]  
>  执行“分离”命令需要服务器或数据库管理员权限。  
  
> [!IMPORTANT]  
>  执行“附加”命令需要服务器管理员权限。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [移动 Analysis Services 数据库](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [数据库 Readwritemode](../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [切换 ReadOnly 和 ReadWrite 模式之间的 Analysis Services 数据库](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)   
 [分离元素](../../analysis-services/xmla/xml-elements-commands/detach-element.md)   
 [Attach 元素](../../analysis-services/xmla/xml-elements-commands/attach-element.md)  
  
  

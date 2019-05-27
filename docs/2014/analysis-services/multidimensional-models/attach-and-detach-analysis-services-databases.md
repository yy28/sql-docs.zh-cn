---
title: 附加和分离 Analysis Services 数据库 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssms.detachdatabase.f1
- sql12.asvs.ssms.attachdatabase.f1
- sql12.asvs.ssmsimbi.AttachDatabase.f1
- sql12.asvs.ssmsimbi.DetachDatabase.f1
helpviewer_keywords:
- databases [Analysis Services], attach
- databases [Analysis Services], detach
ms.assetid: 41887413-2d47-49b8-8614-553cb799fb18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4447f58baaa5ea88a48c67a9a32fcda77681d8d4
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66077489"
---
# <a name="attach-and-detach-analysis-services-databases"></a>附加和分离 Analysis Services 数据库
  在某些情况下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库管理员 (dba) 经常需要将数据库脱机一段时间，然后在同一服务器实例或其他服务器实例上将数据库恢复联机。 根据业务需要（例如，将数据库移到另一个磁盘以获得更好的性能、为数据库扩容获取空间或升级产品），经常需要进行上述操作。 对于上述所有情况的详细信息，`Attach`并`Detach`命令启用[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]dba 使数据库脱机并将其恢复联机状态后不费吹灰之力。  
  
## <a name="attach-and-detach-commands"></a>附加和分离命令。  
 通过 `Attach` 命令可使已脱机的数据库恢复联机。 可以将该数据库附加到原始的服务器实例，也可以附加到另一个实例。 在附加数据库时，用户可以为该数据库指定 **ReadWriteMode** 设置。 使用 `Detach` 命令可使数据库与服务器脱机。  
  
## <a name="attach-and-detach-usage"></a>附加和分离命令的用法  
 `Attach` 命令用于使现有数据库结构联机。 如果该数据库是在 `ReadWrite` 模式下附加的，则只能将其附加到服务器实例一次。 但是，如果此数据库是在 `ReadOnly` 模式下附加的，则可以将其多次附加到不同的服务器实例。 但是，不能将同一数据库多次附加到同一服务器实例。 即使已将数据复制到不同的文件夹中，在尝试多次附加同一数据库时也会引发错误。  
  
> [!IMPORTANT]  
>  如果分离数据库时需要输入密码，则附加数据库时需要输入相同的密码。  
  
 `Detach` 命令用于使现有数据库结构脱机。 分离数据库时，应提供一个密码来保护机密的元数据。  
  
> [!IMPORTANT]  
>  若要保护数据文件的内容，应针对文件夹、子文件夹和数据文件使用访问控制列表。  
  
 分离数据库时，服务器会执行下列步骤。  
  
|分离读/写数据库|分离只读数据库|  
|--------------------------------------|-------------------------------------|  
|1) 服务器会对数据库上的 CommitExclusive 锁发出请求<br />2) 服务器会等待，直到提交或回滚所有正在进行的事务<br />3) 服务器会构建分离数据库必须具备的所有元数据<br />4) 将数据库标记为已删除<br />5) 服务器提交事务|1) 将数据库标记为已删除<br />2) 服务器提交事务<br /><br /> <br /><br /> 注意：无法更改只读数据库的分离密码。 如果为已包含密码的附加数据库提供密码参数，则会产生错误。|  
  
 `Attach` 和 `Detach` 命令必须作为单独的操作执行。 在同一事务中，不能将它们与其他操作一起执行。 此外，`Attach`和`Detach`命令都是原子事务命令。 这意味着操作只有成功或失败两种情况。 数据库不会处于未完成的状态。  
  
> [!IMPORTANT]  
>  执行 `Detach` 命令需要服务器或数据库管理员权限。  
  
> [!IMPORTANT]  
>  执行 `Attach` 命令需要服务器管理员权限。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [移动 Analysis Services 数据库](move-an-analysis-services-database.md)   
 [数据库 ReadWriteMode](database-readwritemodes.md)   
 [在 ReadOnly 和 ReadWrite 模式之间切换 Analysis Services 数据库](switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)   
 [分离元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [附加元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)  
  
  

---
title: 数据库 Readwritemode |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], read/write
- databases [Analysis Services], read-only
ms.assetid: 03d7cb5c-7ff0-4e15-bcd2-7075d1b0dd69
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d775b8fbfb7d50b5db245073fdc52fc274638eb9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66075864"
---
# <a name="database-readwritemodes"></a>数据库 ReadWriteMode
  通常会出现这样的情况， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库管理员 (dba) 希望将读/写数据库更改为只读数据库，或者恰好相反。 通常根据业务需要进行相应的更改，例如：为制定解决方案和提高性能，在多个服务器之间共享同一数据库文件夹。 对于这些情况下，`ReadWriteMode`数据库属性[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]dba 可以轻松地更改数据库运行模式。  
  
## <a name="readwritemode-database-property"></a>ReadWriteMode 数据库属性  
 `ReadWriteMode` 数据库属性指定了数据库是处于读/写模式还是只读模式。 只可能有两个属性值。 在数据库处于只读模式时，不能对数据库应用更改或更新。 但是，在数据库处于读/写模式时，可能会出现更改和更新。 `ReadWriteMode` 数据库属性被定义为只读属性；只能通过 `Attach` 命令设置该属性。  
  
 在数据库处于只读模式时，存在一些限制，它们会影响数据库的允许操作的普通集合。 有关受限操作的信息，请参阅下表。  
  
|只读模式|受限操作|  
|-------------------|---------------------------|  
|XML/A 命令<br /><br /> <br /><br /> 注意：在执行这些命令之一时，引发错误。|`Create`<br /><br /> `Alter`<br /><br /> `Delete`<br /><br /> `Process`<br /><br /> `MergePartitions`<br /><br /> `DesignAggregations`<br /><br /> `CommitTransaction`<br /><br /> `Restore`<br /><br /> `Synchronize`<br /><br /> `Insert`<br /><br /> `Update`<br /><br /> `Drop`<br /><br /> <br /><br /> 注意：设置为只读的; 的数据库中允许单元写回但是，所做的更改无法提交。|  
|MDX 语句<br /><br /> <br /><br /> 注意：在执行这些语句之一时，引发错误。|`COMMIT TRAN`<br /><br /> `CREATE SESSION CUBE`<br /><br /> `ALTER CUBE`<br /><br /> `ALTER DIMENSION`<br /><br /> `CREATE DIMENSION MEMBER`<br /><br /> `DROP DIMENSION MEMBER`<br /><br /> `ALTER DIMENSION`<br /><br /> <br /><br /> 注意：Excel 用户不能使用数据透视表中的分组功能，因为该功能在内部实现的使用`CREATE SESSION CUBE`命令。|  
|DMX 语句<br /><br /> <br /><br /> 注意：在执行这些语句之一时，引发错误。|`CREATE [SESSION] MINING STRUCTURE`<br /><br /> `ALTER MINING STRUCTURE`<br /><br /> `DROP MINING STRUCTURE`<br /><br /> `CREATE [SESSION] MINING MODEL`<br /><br /> `DROP MINING MODEL`<br /><br /> `IMPORT`<br /><br /> `SELECT INTO`<br /><br /> `INSERT`<br /><br /> `UPDATE`<br /><br /> `DELETE`|  
|后台操作|禁用将修改数据库的所有后台操作。 这包括迟缓处理和主动缓存。|  
  
## <a name="readwritemode-usage"></a>ReadWriteMode 用法  
 `ReadWriteMode` 数据库属性将用作 `Attach` 数据库命令的一部分。 `Attach` 命令允许将数据库属性设置为 `ReadWrite` 或 `ReadOnly`。 因为 `ReadWriteMode` 数据库属性被定义为只读，所以不能直接更新该属性值。 通过将 `ReadWriteMode` 属性设置为 `ReadWrite` 可创建数据库。 不能在只读模式下创建数据库。  
  
 若要切换`ReadWriteMode`数据库之间的属性`ReadWrite`并`ReadOnly`，则必须发出一系列`Detach/Attach`命令。  
  
 除 `Attach` 外的所有数据库操作将保持 `ReadWriteMode` 数据库属性的当前状态。 例如，`Alter`、`Backup`、`Restore` 和 `Synchronize` 等操作会保留 `ReadWriteMode` 值。  
  
> [!NOTE]  
>  可以通过只读数据库创建本地多维数据集。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [附加和分离 Analysis Services 数据库](attach-and-detach-analysis-services-databases.md)   
 [移动 Analysis Services 数据库](move-an-analysis-services-database.md)   
 [分离元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [附加元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)  
  
  

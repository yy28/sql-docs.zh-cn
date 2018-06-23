---
title: 数据库 Readwritemode |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- databases [Analysis Services], read/write
- databases [Analysis Services], read-only
ms.assetid: 03d7cb5c-7ff0-4e15-bcd2-7075d1b0dd69
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f8a655c379f512f882534166a8c561524e02ce88
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024680"
---
# <a name="database-readwritemodes"></a>数据库 ReadWriteMode
  通常会出现这样的情况， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库管理员 (dba) 希望将读/写数据库更改为只读数据库，或者恰好相反。 通常根据业务需要进行相应的更改，例如：为制定解决方案和提高性能，在多个服务器之间共享同一数据库文件夹。 有关这些情况下，`ReadWriteMode`数据库属性使[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]dba 轻松更改数据库的运行模式。  
  
## <a name="readwritemode-database-property"></a>ReadWriteMode 数据库属性  
 `ReadWriteMode` 数据库属性指定了数据库是处于读/写模式还是只读模式。 只可能有两个属性值。 在数据库处于只读模式时，不能对数据库应用更改或更新。 但是，在数据库处于读/写模式时，可能会出现更改和更新。 `ReadWriteMode` 数据库属性被定义为只读属性；只能通过 `Attach` 命令设置该属性。  
  
 在数据库处于只读模式时，存在一些限制，它们会影响数据库的允许操作的普通集合。 有关受限操作的信息，请参阅下表。  
  
|只读模式|受限操作|  
|-------------------|---------------------------|  
|XML/A 命令<br /><br /> <br /><br /> 注意：如果执行下列命令之一，则产生错误。|`Create`<br /><br /> `Alter`<br /><br /> `Delete`<br /><br /> `Process`<br /><br /> `MergePartitions`<br /><br /> `DesignAggregations`<br /><br /> `CommitTransaction`<br /><br /> `Restore`<br /><br /> `Synchronize`<br /><br /> `Insert`<br /><br /> `Update`<br /><br /> `Drop`<br /><br /> <br /><br /> 注意：在设置为只读的数据库中允许单元写回；但是，不能提交更改。|  
|MDX 语句<br /><br /> <br /><br /> 注意：如果执行下列语句之一，则产生错误。|`COMMIT TRAN`<br /><br /> `CREATE SESSION CUBE`<br /><br /> `ALTER CUBE`<br /><br /> `ALTER DIMENSION`<br /><br /> `CREATE DIMENSION MEMBER`<br /><br /> `DROP DIMENSION MEMBER`<br /><br /> `ALTER DIMENSION`<br /><br /> <br /><br /> 注意： 因为通过使用在内部实现该功能，Excel 用户不能使用数据透视表中的分组功能`CREATE SESSION CUBE`命令。|  
|DMX 语句<br /><br /> <br /><br /> 注意：如果执行下列语句之一，则产生错误。|`CREATE [SESSION] MINING STRUCTURE`<br /><br /> `ALTER MINING STRUCTURE`<br /><br /> `DROP MINING STRUCTURE`<br /><br /> `CREATE [SESSION] MINING MODEL`<br /><br /> `DROP MINING MODEL`<br /><br /> `IMPORT`<br /><br /> `SELECT INTO`<br /><br /> `INSERT`<br /><br /> `UPDATE`<br /><br /> `DELETE`|  
|后台操作|禁用将修改数据库的所有后台操作。 这包括迟缓处理和主动缓存。|  
  
## <a name="readwritemode-usage"></a>ReadWriteMode 用法  
 `ReadWriteMode` 数据库属性将用作 `Attach` 数据库命令的一部分。 `Attach` 命令允许将数据库属性设置为 `ReadWrite` 或 `ReadOnly`。 因为 `ReadWriteMode` 数据库属性被定义为只读，所以不能直接更新该属性值。 通过将 `ReadWriteMode` 属性设置为 `ReadWrite` 可创建数据库。 不能在只读模式下创建数据库。  
  
 若要切换`ReadWriteMode`数据库之间的属性`ReadWrite`和`ReadOnly`，都必须发出一系列`Detach/Attach`命令。  
  
 所有数据库操作，除`Attach`，保留`ReadWriteMode`数据库处于其当前状态的属性。 例如，`Alter`、`Backup`、`Restore` 和 `Synchronize` 等操作会保留 `ReadWriteMode` 值。  
  
> [!NOTE]  
>  可以通过只读数据库创建本地多维数据集。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [附加和分离 Analysis Services 数据库](attach-and-detach-analysis-services-databases.md)   
 [移动 Analysis Services 数据库](move-an-analysis-services-database.md)   
 [分离元素](../xmla/xml-elements-commands/detach-element.md)   
 [Attach 元素](../xmla/xml-elements-commands/attach-element.md)  
  
  
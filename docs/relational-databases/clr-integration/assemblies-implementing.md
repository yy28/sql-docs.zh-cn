---
title: 实现的程序集 |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], implementing
ms.assetid: c228d7bf-a906-4f37-a057-5d464d962ff8
caps.latest.revision: 33
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0e295b80f737bbfcb3c9184974eb82e043da9b0b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="assemblies---implementing"></a>程序集的实现
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题提供有关以下方面的信息以帮助您在数据库中实现和使用程序集：  
  
-   创建程序集  
  
-   修改程序集  
  
-   删除、 禁用和启用程序集  
  
-   管理程序集版本  
  
## <a name="creating-assemblies"></a>创建程序集  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CREATE ASSEMBLY 语句在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中创建程序集或者使用程序集辅助编辑器在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中创建程序集。 此外，部署中的 SQL 服务器项目[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]为项目指定的数据库中注册程序集。 有关详细信息，请参阅 [Deploying CLR Database Objects](../../relational-databases/clr-integration/deploying-clr-database-objects.md)。  
  
 **使用 TRANSACT-SQL 创建程序集**  
  
-   [CREATE ASSEMBLY (Transact-SQL)](../../t-sql/statements/create-assembly-transact-sql.md)  
  
 **通过使用 SQL Server Management Studio 中创建一个程序集**  
  
-   [程序集属性&#40;常规页&#41;](../../relational-databases/clr-integration/assemblies-properties.md)  
  
## <a name="modifying-assemblies"></a>修改程序集  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ALTER ASSEMBLY 语句在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中修改程序集或者使用程序集辅助编辑器在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中修改程序集。 当要执行以下操作时，可以修改程序集：  
  
-   通过上载二进制的程序集的较新版本来更改程序集的实现。 有关详细信息，请参阅[管理程序集版本](#_managing)本主题中更高版本。  
  
-   更改程序集的权限集。 有关详细信息，请参阅[设计程序集](../../relational-databases/clr-integration/assemblies-designing.md)。  
  
-   更改程序集的可见性。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中可引用可见程序集。 不可以引用不可见程序集，即使它们已上载在数据库中。 默认情况下，上载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的程序集是可见的。  
  
-   添加或删除与程序集关联的调试文件或源文件。  
  
 **若要通过使用 TRANSACT-SQL 修改程序集**  
  
-   [ALTER ASSEMBLY (Transact-SQL)](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
 **若要通过使用 SQL Server Management Studio 修改程序集**  
  
-   [程序集属性&#40;常规页&#41;](../../relational-databases/clr-integration/assemblies-properties.md)  
  
## <a name="dropping-disabling-and-enabling-assemblies"></a>删除、禁用和启用程序集  
 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] DROP ASSEMBLY 语句或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 删除程序集。  
  
 **使用 TRANSACT-SQL 删除程序集**  
  
-   [DROP ASSEMBLY (Transact-SQL)](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **使用 SQL Server Management Studio 删除程序集**  
  
-   [删除对象](http://msdn.microsoft.com/library/49541441-179c-40d3-ba0c-01bcae545984)  
  
 默认情况下，不执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中创建的所有程序集。 你可以使用**启用 clr**选项**sp_configure**系统存储过程来禁用或启用的过程中上载的所有程序集执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 禁用程序集执行防止公共语言运行时 (CLR) 函数、存储过程、触发器、聚合和用户定义类型执行并使当前正在执行的那些停止执行。 禁用程序集执行并不禁用创建、更改或删除程序集的功能。 有关详细信息，请参阅[clr enabled 服务器配置选项](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)。  
  
 **若要禁用和启用执行程序集**  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
##  <a name="_managing"></a> 管理程序集版本  
 将程序集上载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例后，将在数据库系统目录中存储并管理该程序集。 中的程序集的定义进行任何更改[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]应传播到数据库目录中存储的程序集。  
  
 当必须修改程序集时，您必须发出 ALTER ASSEMBLY 语句以更新数据库中的程序集。 这将使该程序集更新为控制其实现的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 模块的最新副本。  
  
 ALTER ASSEMBLY 语句中的 WITH UNCHECKED DATA 子句指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 甚至刷新数据库中的持久化数据依赖的那些程序集。 特别地，如果存在以下任何内容，您必须指定 WITH UNCHECKED DATA：  
  
-   通过 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数或方法直接或间接引用程序集中的方法的持久化计算列。  
  
-   属于 CLR 用户定义类型且依赖于程序集的列，并且该类型实现的是 UserDefined（非 Native）序列化格式。  
  
> [!CAUTION]  
>  未指定 WITH UNCHECKED DATA 时，如果新的程序集版本对表、索引或其他持久性站点中的现有数据造成影响，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将尝试阻止 ALTER ASSEMBLY 执行。 但是，当 CLR 程序集更新时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不能保证计算列、索引、索引视图或表达式与基本例程和类型保持一致。 执行 ALTER ASSEMBLY 时一定要谨慎，以确保表达式的结果与程序集中存储的基于该表达式的值相互匹配。  
  
 只有的成员**db_owner**和**db_ddlowner**固定的数据库角色可以通过使用 WITH UNCHECKED DATA 子句执行 ALTER 运行程序集。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将消息（程序集对表中的未检查数据已修改）投递给 Windows 应用程序事件日志。 然后 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将任何包含依赖于程序集的数据的表标记为带有未检查数据的表。 **Has_unchecked_assembly_data**列**sys.tables**目录视图包含包含未选中状态的数据，使用 0 表示不包含未选中状态数据的表的表的值 1。  
  
 若要解决的未选中状态数据的完整性，可针对具有每个表运行 DBCC CHECKDB 与 EXTENDED_LOGICAL_CHECKS 未选中状态的数据。 如果 DBCC CHECKDB 与 EXTENDED_LOGICAL_CHECKS 失败，你必须删除不是有效或修改的程序集代码以便解决问题的表行，，然后发出其他 ALTER ASSEMBLY 语句。  
  
 ALTER ASSEMBLY 可更改程序集版本。 区域性和公钥标记的程序集保持不变。SQL Server 不允许使用相同的名称、 区域性和公钥注册的程序集的不同版本。  
  
### <a name="interactions-with-computer-wide-policy-for-version-binding"></a>与版本绑定的计算机范围的策略交互  
 如果通过使用发行者策略或计算机范围的管理员策略将存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的程序集的引用重定向到了特定版本，则必须执行以下两个操作之一：  
  
-   请确保此重定向到的新版本在数据库中。  
  
-   对计算机策略或发行者策略的外部策略文件的任何语句进行修改以确保它们引用数据库中的特定版本。  
  
 否则，将新程序集版本加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的尝试将失败。  
  
 **若要更新的程序集版本**  
  
-   [ALTER ASSEMBLY (Transact-SQL)](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
## <a name="see-also"></a>另请参阅  
 [程序集 & #40; 数据库引擎 & #41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [获取有关程序集的信息](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  

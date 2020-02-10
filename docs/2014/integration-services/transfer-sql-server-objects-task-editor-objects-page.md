---
title: 传输 SQL Server 对象任务编辑器（"对象" 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfersqlserverobjects.objects.f1
helpviewer_keywords:
- Transfer SQL Server Objects Task Editor
ms.assetid: 8cc09118-70ac-4013-8308-d87f8411ca0c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3ae231e933e30613d45fe00eaa99d6a2d5c9c772
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054869"
---
# <a name="transfer-sql-server-objects-task-editor-objects-page"></a>传输 SQL Server 对象任务编辑器（“对象”页）
  可以使用 **“传输 SQL Server 对象任务编辑器”** 对话框的 **“对象”** 页，指定用于将一个或多个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 对象从一个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例复制到另一个实例的属性。 可复制的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 对象的几个示例包括表、视图、存储过程和用户定义函数。 有关此任务的详细信息，请参阅 [Transfer SQL Server Objects Task](control-flow/transfer-sql-server-objects-task.md)。  
  
> [!NOTE]  
>  创建传输 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 对象任务的用户必须具有对源服务器对象的足够权限以选择对象进行复制，还必须具有访问这些对象将传输到的目标服务器数据库的权限。  
  
## <a name="static-options"></a>静态选项  
 **SourceConnection**  
 在列表中选择一个 SMO 连接管理器，或单击** \<"新建连接 ..." >** 以创建与源服务器的新连接。  
  
 **SourceDatabase**  
 选择要从源服务器上的哪个数据库复制对象。  
  
 **DestinationConnection**  
 在列表中选择一个 SMO 连接管理器，或单击** \<"新建连接 ..." >** 以创建与目标服务器的新连接。  
  
 **DestinationDatabase**  
 选择对象要复制到目标服务器上的哪个数据库。  
  
 **DropObjectsFirst**  
 选择复制前是否先在目标服务器上删除所选对象。  
  
 **IncludeExtendedProperties**  
 选择将对象从源服务器复制到目标服务器时是否包含扩展属性。  
  
 **CopyData**  
 选择将对象从源服务器复制到目标服务器时是否包含数据。  
  
 **ExistingData**  
 指定将数据复制到目标服务器的方式。 此属性具有下表所列的选项：  
  
|值|说明|  
|-----------|-----------------|  
|**全部**|将覆盖目标服务器上的数据。|  
|**附加**|从源服务器复制的数据将追加到目标服务器上的现有数据中。|  
  
> [!NOTE]  
>  只有在 **CopyData** 设置为 **True** 时， **ExistingData**选项才可用。  
  
 **CopySchema**  
 选择在传输 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 对象任务过程中是否复制架构。  
  
> [!NOTE]  
>  **CopySchema**仅适用于[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
 **UseCollation**  
 选择对象的传输是否应包含源服务器上指定的排序规则。  
  
 **IncludeDependentObjects**  
 选择复制所选对象时是否级联以包含依赖于所选复制对象的其他对象。  
  
 **CopyAllObjects**  
 选择该任务是复制指定源数据库中的所有对象还是仅复制所选对象。  如果此选项设置为 False，您就可以选择要传输的对象，并且在 **CopyAllObjects**部分中将显示动态选项。  
  
 **ObjectsToCopy**  
 展开 **ObjectsToCopy** 以指定应从源数据库复制到目标数据库的对象。  
  
> [!NOTE]  
>  仅当**CopyAllObjects**设置为**False**时， **ObjectsToCopy**才可用。  
  
 只有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]支持用于复制以下类型的对象的选项：  
  
 程序集  
  
 分区函数  
  
 分区方案  
  
 架构  
  
 用户定义聚合  
  
 用户定义类型  
  
 XML 架构集合  
  
 **CopyDatabaseUsers**  
 指定传输中是否应包含数据库用户。  
  
 **CopyDatabaseRoles**  
 指定传输中是否应包含数据库角色。  
  
 **CopySqlServerLogins**  
 指定传输中是否应包含 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登录名。  
  
 **CopyObjectLevelPermissions**  
 指定传输中是否应包含对象级权限。  
  
 **CopyIndexes**  
 指定传输中是否应包含索引。  
  
 **CopyTriggers**  
 指定传输中是否应包含触发器。  
  
 **CopyFullTextIndexes**  
 指定传输中是否应包含全文索引。  
  
 **CopyPrimaryKeys**  
 指定传输中是否应包含主键。  
  
 **CopyForeignKeys**  
 指定传输中是否应包含外键。  
  
 **GenerateScriptsInUnicode**  
 指定生成的传输脚本是否为 Unicode 格式。  
  
## <a name="dynamic-options"></a>动态选项  
  
### <a name="copyallobjects--false"></a>CopyAllObjects = False  
 **CopyAllTables**  
 选择该任务是复制指定源数据库中的所有表还是仅复制所选表。  
  
 **TablesList**  
 单击此项将打开“选择表”**** 对话框。  
  
 **CopyAllViews**  
 选择该任务是复制指定源数据库中的所有视图还是仅复制所选视图。  
  
 **ViewsList**  
 单击此项将打开“选择视图”**** 对话框。  
  
 **CopyAllStoredProcedures**  
 选择该任务是复制指定源数据库中的所有用户定义存储过程还是仅复制所选过程。  
  
 **StoredProceduresList**  
 单击此项将打开“选择存储过程”**** 对话框。  
  
 **CopyAllUserDefinedFunctions**  
 选择该任务是复制指定源数据库中的所有用户定义函数还是仅复制所选用户定义函数。  
  
 **UserDefinedFunctionsList**  
 单击此项将打开“选择用户定义函数”对话框。****  
  
 **CopyAllDefaults**  
 选择该任务是复制指定源数据库中的所有默认值还是仅复制所选默认值。  
  
 **DefaultsList**  
 单击此项将打开“选择默认值”对话框。****  
  
 **CopyAllUserDefinedDataTypes**  
 选择该任务是复制指定源数据库中的所有用户定义数据类型还是仅复制所选用户定义数据类型。  
  
 **UserDefinedDataTypesList**  
 单击此项将打开“选择用户定义数据类型”对话框。****  
  
 **CopyAllPartitionFunctions**  
 选择该任务是复制指定源数据库中的所有用户定义分区函数还是仅复制所选分区函数。 仅在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中支持。  
  
 **PartitionFunctionsList**  
 单击此项将打开“选择分区函数”对话框。****  
  
 **CopyAllPartitionSchemes**  
 选择该任务是复制指定源数据库中的所有分区方案还是仅复制所选分区方案。 仅在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中支持。  
  
 **PartitionSchemesList**  
 单击此项将打开“选择分区方案”对话框。****  
  
 **CopyAllSchemas**  
 选择该任务是复制指定源数据库中的所有架构还是仅复制所选架构。 仅在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中支持。  
  
 **SchemasList**  
 单击此项将打开“选择架构”对话框。****  
  
 **CopyAllSqlAssemblies**  
 选择该任务是复制指定源数据库中的所有 SQL 程序集还是仅复制所选 SQL 程序集。 仅在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中支持。  
  
 **SqlAssembliesList**  
 单击此项将打开“选择 SQL 程序集”对话框。****  
  
 **CopyAllUserDefinedAggregates**  
 选择该任务是复制指定源数据库中的所有用户定义聚合还是仅复制所选用户定义聚合。 仅在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中支持。  
  
 **UserDefinedAggregatesList**  
 单击此项将打开“选择用户定义聚合”对话框。****  
  
 **CopyAllUserDefinedTypes**  
 选择该任务是复制指定源数据库中的所有用户定义类型还是仅复制所选用户定义类型。 仅在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中支持。  
  
 **UserDefinedTypes**  
 单击此项将打开“选择用户定义类型”对话框。****  
  
 **CopyAllXmlSchemaCollections**  
 选择该任务是复制指定源数据库中的所有 XML 架构集合还是仅复制所选 XML 架构集合。 仅在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中支持。  
  
 **XmlSchemaCollectionsList**  
 单击此项将打开“选择 XML 架构集合”对话框。****  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 任务](control-flow/integration-services-tasks.md)   
 [&#40;常规页传输 SQL Server 对象任务编辑器&#41;](general-page-of-integration-services-designers-options.md)   
 [“表达式”页](expressions/expressions-page.md)   
 [用于大容量导入或大容量导出的数据格式 &#40;SQL Server&#41;](../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [安装 SQL Server 的安全注意事项](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  

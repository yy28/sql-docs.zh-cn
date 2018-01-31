---
title: "传输 SQL Server 对象任务 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transfersqlserverobjectstask.f1
- sql13.dts.designer.transfersqlserverobjects.general.f1
- sql13.dts.designer.transfersqlserverobjects.objects.f1
helpviewer_keywords:
- Transfer SQL Server Objects task [Integration Services]
ms.assetid: fe86d6e5-e415-406c-88f3-dc3ef71bd5f0
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d27b4617e47266a377d2412c79d126ea0cd6dc48
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="transfer-sql-server-objects-task"></a>传输 SQL Server 对象任务
  传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象任务在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例之间传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库中一种或多种类型的对象。 例如，该任务可以复制表和存储过程。 可以复制的对象的类型会因用作源的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本而异。 例如，只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库包括架构和用户定义聚合。  
  
## <a name="objects-to-transfer"></a>要传输的对象  
 可以复制指定数据库中的服务器角色、角色和用户以及这些传输的对象的权限。 通过随对象一起复制关联的用户、角色以及权限，您可以立即在目标服务器上对这些传输的对象进行操作。  
  
 下表列出了可以复制的对象的类型。  
  
|Object|  
|------------|  
|表|  
|视图|  
|存储过程|  
|用户定义函数|  
|默认值|  
|用户定义数据类型|  
|分区函数|  
|分区方案|  
|架构|  
|程序集|  
|用户定义聚合|  
|用户定义类型|  
|XML 架构集合|  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例中创建的用户定义类型 (UDT) 对公共语言运行时 (CLR) 程序集具有依赖关系。 如果使用传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象任务来传输 UDT，则还必须配置用于传输依赖对象的任务。 若要传输依赖对象，将 **IncludeDependentObjects** 属性设置为 **True**。  
  
### <a name="table-options"></a>表选项  
 在复制表时，可以指示在复制过程中要包含的与表相关的项的类型。 以下类型的项可以与相关表一起复制：  
  
-   索引  
  
-   触发器  
  
-   全文索引  
  
-   主键  
  
-   外键  
  
 您还可以指示该任务所生成的脚本是否为 Unicode 格式。  
  
## <a name="destination-options"></a>目标选项  
 您可以将传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象任务配置为在传输时包括架构名称、数据、所传输的对象的扩展属性以及依赖对象。 如果复制数据，则它可以替换或追加到现有数据。  
  
 某些选项只适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 例如，只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持架构。  
  
## <a name="security-options"></a>安全选项  
 传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象任务可以包括通过所传输的对象的源、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和权限所产生的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库级用户和角色。 例如，传输可以包括所传输的表的权限。  
  
## <a name="transfer-objects-between-instances-of-sql-server"></a>在 SQL Server 实例之间传输对象  
 传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象任务支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 源和目标。  
  
## <a name="events"></a>事件  
 该任务将引发报告已传输的对象的信息事件，而且在覆盖对象时还会引发警告事件。 信息事件还可以由截断数据库表这样的操作引发。  
  
 传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象任务并不报告对象传输的进度；它仅报告 0% 和 100 % 完成。  
  
## <a name="execution-value"></a>执行值  
 在任务的 **ExecutionValue** 属性中存储的执行值返回已传输的对象数。 通过将用户定义的变量分配给传输 SQL Server 对象任务的 **ExecValueVariable** 属性，包中的其他对象就可以访问有关对象传输的信息。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)和[在包中使用变量](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)。  
  
## <a name="log-entries"></a>日志项  
 传输 SQL Server 对象任务包括下列自定义日志项：  
  
-   TransferSqlServerObjectsTaskStartTransferringObjects   此日志项报告传输已经开始。 日志项包括开始时间。  
  
-   TransferSqlServerObjectsTaskFinishedTransferringObjects    此日志项报告传输已经完成。 日志项包括结束时间。  
  
 此外， **OnInformation** 事件的日志项报告属于为传输所选的对象类型的对象数、已经传输的对象数以及随表传输数据时截断表这样的操作。 覆盖目标上的每个对象时，都会写入 **OnWarning** 事件的日志项。  
  
## <a name="security-and-permissions"></a>安全性和权限  
 用户必须具有浏览源服务器上的对象的权限，同时必须具有在目标服务器上删除和创建对象的权限，此外用户还必须具有访问指定数据库和数据库对象的权限。  
  
## <a name="configuration-of-the-transfer-sql-server-objects-task"></a>配置传输 SQL Server 对象任务  
 传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象任务可以配置为传输所有对象，传输某种类型的所有对象，或者只传输某种类型的指定对象。 例如，可以选择只复制 AdventureWorks 数据库中的选定表。  
  
 如果传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象任务传输表，可指定随表一起复制、与表相关的对象的类型。 例如，您可以指定随表一起复制主键。  
  
 若要进一步增强所传输的对象的功能，您可以将传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象任务配置为在传输时包括架构名称、数据、所传输的对象的扩展属性以及依赖对象。 在复制数据时，您可以指定是替换现有数据还是追加到现有数据。  
  
 运行时，传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象任务使用两个 SMO 连接管理器连接到源服务器和目标服务器。 这两个 SMO 连接管理器与传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象任务分开配置，然后由传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象任务引用。 SMO 连接管理器指定服务器以及在访问该服务器时要使用的身份验证模式。 有关详细信息，请参阅 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题：  
  
-   [“表达式”页](../../integration-services/expressions/expressions-page.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-sql-server-objects-task"></a>以编程方式配置传输 SQL Server 对象任务  
 有关以编程方式设置这些属性的详细信息，请单击以下主题：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferSqlServerObjectsTask.TransferSqlServerObjectsTask>  
  
  
## <a name="transfer-sql-server-objects-task-editor-general-page"></a>传输 SQL Server 对象任务编辑器（“常规”页）
  可以使用 **“传输 SQL Server 对象任务编辑器”** 对话框的 **“常规”** 页，对传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象任务进行命名和说明。  
  
> [!NOTE]  
>  创建传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象任务的用户必须具有对源服务器对象的足够权限以选择对象进行复制，还必须具有访问这些对象将传输到的目标服务器数据库的权限。  
  
### <a name="options"></a>“常规”  
 **名称**  
 为传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象任务键入唯一的名称。 此名称用作任务图标中的标签。  
  
> [!NOTE]  
>  任务名称在一个包内必须是唯一的。  
  
 **Description**  
 键入传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象任务的说明。  
  
## <a name="transfer-sql-server-objects-task-editor-objects-page"></a>传输 SQL Server 对象任务编辑器（“对象”页）
  可以使用 **“传输 SQL Server 对象任务编辑器”** 对话框的 **“对象”** 页，指定用于将一个或多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象从一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例复制到另一个实例的属性。 可复制的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象的几个示例包括表、视图、存储过程和用户定义函数。  
  
> [!NOTE]  
>  创建传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象任务的用户必须具有对源服务器对象的足够权限以选择对象进行复制，还必须具有访问这些对象将传输到的目标服务器数据库的权限。  
  
### <a name="static-options"></a>静态选项  
 **SourceConnection**  
 从列表中选择 SMO 连接管理器，或单击“\<新建连接...>”，创建与源服务器的新连接。  
  
 **SourceDatabase**  
 选择要从源服务器上的哪个数据库复制对象。  
  
 **DestinationConnection**  
 从列表中选择 SMO 连接管理器，或单击“\<新建连接...>”，创建与目标服务器的新连接。  
  
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
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**替换**|将覆盖目标服务器上的数据。|  
|**追加**|从源服务器复制的数据将追加到目标服务器上的现有数据中。|  
  
> [!NOTE]  
>  只有在 **CopyData** 设置为 **True** 时， **ExistingData**选项才可用。  
  
 **CopySchema**  
 选择在传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象任务过程中是否复制架构。  
  
> [!NOTE]  
>  **CopySchema** 仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 **UseCollation**  
 选择对象的传输是否应包含源服务器上指定的排序规则。  
  
 **IncludeDependentObjects**  
 选择复制所选对象时是否级联以包含依赖于所选复制对象的其他对象。  
  
 **CopyAllObjects**  
 选择该任务是复制指定源数据库中的所有对象还是仅复制所选对象。  如果此选项设置为 False，您就可以选择要传输的对象，并且在 **CopyAllObjects**部分中将显示动态选项。  
  
 **ObjectsToCopy**  
 展开 **ObjectsToCopy** 以指定应从源数据库复制到目标数据库的对象。  
  
> [!NOTE]  
>  **CopyAllObjects** 设置为 **False** 时， **ObjectsToCopy**选项才可用。  
  
 只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持用于复制以下类型的对象的选项：  
  
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
 指定传输中是否应包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。  
  
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
  
### <a name="dynamic-options"></a>动态选项  
  
#### <a name="copyallobjects--false"></a>CopyAllObjects = False  
 **CopyAllTables**  
 选择该任务是复制指定源数据库中的所有表还是仅复制所选表。  
  
 **TablesList**  
 单击此项将打开“选择表”对话框。  
  
 **CopyAllViews**  
 选择该任务是复制指定源数据库中的所有视图还是仅复制所选视图。  
  
 **ViewsList**  
 单击此项将打开“选择视图”对话框。  
  
 **CopyAllStoredProcedures**  
 选择该任务是复制指定源数据库中的所有用户定义存储过程还是仅复制所选过程。  
  
 **StoredProceduresList**  
 单击此项将打开“选择存储过程”对话框。  
  
 **CopyAllUserDefinedFunctions**  
 选择该任务是复制指定源数据库中的所有用户定义函数还是仅复制所选用户定义函数。  
  
 **UserDefinedFunctionsList**  
 单击此项将打开“选择用户定义函数”对话框。  
  
 **CopyAllDefaults**  
 选择该任务是复制指定源数据库中的所有默认值还是仅复制所选默认值。  
  
 **DefaultsList**  
 单击此项将打开“选择默认值”对话框。  
  
 **CopyAllUserDefinedDataTypes**  
 选择该任务是复制指定源数据库中的所有用户定义数据类型还是仅复制所选用户定义数据类型。  
  
 **UserDefinedDataTypesList**  
 单击此项将打开“选择用户定义数据类型”对话框。  
  
 **CopyAllPartitionFunctions**  
 选择该任务是复制指定源数据库中的所有用户定义分区函数还是仅复制所选分区函数。 仅在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中支持。  
  
 **PartitionFunctionsList**  
 单击此项将打开“选择分区函数”对话框。  
  
 **CopyAllPartitionSchemes**  
 选择该任务是复制指定源数据库中的所有分区方案还是仅复制所选分区方案。 仅在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中支持。  
  
 **PartitionSchemesList**  
 单击此项将打开“选择分区方案”对话框。  
  
 **CopyAllSchemas**  
 选择该任务是复制指定源数据库中的所有架构还是仅复制所选架构。 仅在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中支持。  
  
 **SchemasList**  
 单击此项将打开“选择架构”对话框。  
  
 **CopyAllSqlAssemblies**  
 选择该任务是复制指定源数据库中的所有 SQL 程序集还是仅复制所选 SQL 程序集。 仅在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中支持。  
  
 **SqlAssembliesList**  
 单击此项将打开“选择 SQL 程序集”对话框。  
  
 **CopyAllUserDefinedAggregates**  
 选择该任务是复制指定源数据库中的所有用户定义聚合还是仅复制所选用户定义聚合。 仅在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中支持。  
  
 **UserDefinedAggregatesList**  
 单击此项将打开“选择用户定义聚合”对话框。  
  
 **CopyAllUserDefinedTypes**  
 选择该任务是复制指定源数据库中的所有用户定义类型还是仅复制所选用户定义类型。 仅在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中支持。  
  
 **UserDefinedTypes**  
 单击此项将打开“选择用户定义类型”对话框。  
  
 **CopyAllXmlSchemaCollections**  
 选择该任务是复制指定源数据库中的所有 XML 架构集合还是仅复制所选 XML 架构集合。 仅在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中支持。  
  
 **XmlSchemaCollectionsList**  
 单击此项将打开“选择 XML 架构集合”对话框。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 任务](../../integration-services/control-flow/integration-services-tasks.md)   
 [传输 SQL Server 对象任务编辑器（“常规”页）](../../integration-services/control-flow/transfer-sql-server-objects-task-editor-general-page.md)   
 [“表达式”页](../../integration-services/expressions/expressions-page.md)   
 [用于批量导入或导出的数据格式 (SQL Server)](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [安装 SQL Server 的安全注意事项](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  

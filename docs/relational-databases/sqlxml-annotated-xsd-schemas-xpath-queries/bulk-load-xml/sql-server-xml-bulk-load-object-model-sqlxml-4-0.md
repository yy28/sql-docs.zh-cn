---
title: SQL Server XML 大容量加载对象模型 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], object model
- ErrorLogFile property
- SGDropTables property
- SGUseID property
- KeepNulls property
- ConnectionCommand property
- SchemaGen property
- XMLFragment property
- SQLXMLBulkLoad object
- ForceTableLock property
- CheckConstraints property
- BulkLoad property
- TempFilePath property
- IgnoreDuplicateKeys property
- Transaction property
- KeepIdentity property
- ConnectionString property
- FireTriggers property
- Execute method
- XML Bulk Load [SQLXML], object model
ms.assetid: a9efbbde-ed2b-4929-acc1-261acaaed19d
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cdd0c4efafbab577aef1016d367ca2210ea3d863
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56011429"
---
# <a name="sql-server-xml-bulk-load-object-model-sqlxml-40"></a>SQL Server XML 大容量加载对象模型 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XML 大容量加载对象模型包含 SQLXMLBulkLoad 对象。 该对象支持以下方法和属性。  
  
## <a name="methods"></a>方法  
 Execute  
 通过使用作为参数提供的架构文件和数据文件（或流），大容量加载数据。  
  
## <a name="properties"></a>Properties  
 BulkLoad  
 指定是否应执行大容量加载。 此属性很有用，如果你想要只生成的架构 （请参阅按照 SchemaGen、 SGDropTables 和 SGUseID 属性），并且执行大容量加载。 此属性是一个布尔属性。 当此属性设置为 TRUE 时，XML 大容量加载将执行。 当此属性设置为 FALSE 时，XML 大容量加载将不执行。  
  
 默认值为 TRUE。  
  
 CheckConstraints  
 指定在 XML 大容量加载将数据插入列时是否应检查对该列指定的约束（例如，由于列之间的主键/外键关系而产生的约束）。 此属性是一个布尔属性。  
  
 在此属性设置为 TRUE 时，XML 大容量加载检查每个插入的值的约束（这意味着约束冲突将导致错误）。  
  
> [!NOTE]  
>  若要将此属性为 FALSE，您必须具有**ALTER TABLE**目标表的权限。 有关详细信息，请参阅 [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md)。  
  
 默认值是 FALSE。 在该值设置为 FALSE 时，XML 大容量加载在插入操作期间将忽略这些约束。 在当前实现中，您必须按照映射架构中的主键和外键关系的顺序定义表。 也就是说，具有主键的表必须在具有外键的相应表之前定义；否则，XML 大容量加载将失败。  
  
 请注意，如果 ID 传播正在进行，则此选项不适用并且约束检查将保持。 这将在 `KeepIdentity=False` 并且存在定义的关系（即，父级是标识字段并且在生成子级时值将提供给子级）发生。  
  
 ConnectionCommand  
 标识 XML 大容量加载应使用现有连接对象 （例如，ADO 或 ICommand 命令对象）。 您可以使用 ConnectionCommand 属性而不是使用 ConnectionString 属性指定连接字符串。 事务属性必须设置为 TRUE，如果使用 ConnectionCommand。  
  
 如果使用 ConnectionString 和 ConnectionCommand 属性，XML 大容量加载使用最后指定的属性。  
  
 默认值为 NULL。  
  
 ConnectionString  
 标识 OLE DB 连接字符串，该字符串提供建立与数据库实例的连接所必需的信息。 如果使用 ConnectionString 和 ConnectionCommand 属性，XML 大容量加载使用最后指定的属性。  
  
 默认值为 NULL。  
  
 ErrorLogFile  
 指定 XML 大容量加载将错误和消息记录到的文件名。 默认值为空字符串，在此情况下将不发生日志记录。  
  
 FireTriggers  
 指定在大容量加载操作期间是否应引发对目标表定义的触发器。 默认值为 FALSE。  
  
 在设置为 TRUE 时，在插入操作期间触发器将照常触发。  
  
> [!NOTE]  
>  若要将此属性为 FALSE，您必须具有**ALTER TABLE**目标表的权限。 有关详细信息，请参阅 [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md)。  
  
 请注意，如果 ID 传播正在进行，则此选项不适用并且触发器将保持。 这将在 `KeepIdentity=False` 并且存在定义的关系（即，父级是标识字段并且在生成子级时值将提供给子级）发生。  
  
 ForceTableLock  
 指定在大容量加载期间，XML 大容量加载将数据复制到的表是否应被锁定。 此属性是一个布尔属性。 在此属性设置为 TRUE 时，XML 大容量加载要求在大容量加载期间执行表锁定。 在此属性设置为 FALSE 时，XML 大容量加载在每次将记录插入到表中时要求表锁定。  
  
 默认值是 FALSE。  
  
 IgnoreDuplicateKeys  
 指定尝试在某一键列中插入重复值时应采取什么后续操作。 如果此属性设置为 TRUE 并且尝试在某一键列中插入具有重复值的记录，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将不插入该记录。 但它将插入随后的记录；这样，大容量加载操作将不会失败。 如果此属性设置为 FALSE，则尝试在某一键列中插入重复值时大容量加载将失败。  
  
 当 IgnoreDuplicateKeys 属性设置为 TRUE 时，对于每个记录的表中插入发出 COMMIT 语句。 这将降低性能。 该属性可以设置为 TRUE，仅事务属性设置为 FALSE，因为事务行为使用文件实现。  
  
 默认值是 FALSE。  
  
 KeepIdentity  
 指定如何处理源文件中标识类型列的值。 此属性是一个布尔属性。 在此属性设置为 TRUE 时，XML 大容量加载将在源文件中指定的值分配给标识列。 在该属性设置为 FALSE 时，大容量加载操作将忽略在源文件中指定的标识列值。 在此情况下，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将某一值分配给标识列。  
  
 如果大容量加载涉及作为外键的列，该外键引用存储 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 生成的值的标识列，则大容量加载会相应将这些标识值传播到外键列。  
  
 此属性的值适用于在大容量加载中涉及的所有列。 默认值为 TRUE。  
  
> [!NOTE]  
>  若要将此属性为 TRUE，必须具有**ALTER TABLE**目标表的权限。 否则，它必须设置为 FALSE 的值。 有关详细信息，请参阅 [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md)。  
  
 KeepNulls  
 指定哪些值将用于在 XML 文档中缺少相应属性或子元素的列。 此属性是一个布尔属性。 当此属性设置为 TRUE 时，XML 大容量加载将 Null 值分配给该列。 它并不分配在服务器上设置的该列的默认值（如果有）。 此属性的值适用于在大容量加载中涉及的所有列。  
  
 默认值是 FALSE。  
  
 SchemaGen  
 指定是否在执行大容量加载操作前创建必需的表。 此属性是一个布尔属性。 如果该属性设置为 TRUE，则创建在映射架构中标识的表（数据库必须存在）。 如果数据库中已存在一个或多个表，SGDropTables 属性确定是否要删除并重新创建这些预先存在的表。  
  
 SchemaGen 属性的默认值为 FALSE。 SchemaGen 不会创建新创建的表的 PRIMARY KEY 约束。 SchemaGen，但是，FOREIGN KEY 约束在数据库中创建如果可以找到匹配**sql: relationship**并**sql:key-字段**映射架构中的批注并且键字段由构成单个列。  
  
 请注意，是否 SchemaGen 属性设置为 TRUE 时，XML 大容量加载将以下事项：  
  
-   根据元素和属性名称创建必需的表。 因此，不采用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 保留字作为架构中的元素和属性名称十分重要。  
  
-   返回溢出指定使用的任何列的数据[sql:overflow-字段](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)中[xml 数据类型](../../../t-sql/xml/xml-transact-sql.md)格式。  
  
 SGDropTables  
 指定是否应删除并重新创建现有表。 SchemaGen 属性设置为 TRUE 时使用此属性。 如果 SGDropTables 为 FALSE 时，会保留现有的表。 在此属性为 TRUE 时，将删除并重新创建现有表。  
  
 默认值是 FALSE。  
  
 SGUseID  
 指定映射架构中的属性是否为标识**id**类型可在创建表时创建 PRIMARY KEY 约束。 SchemaGen 属性设置为 TRUE 时，请使用此属性。 SGUseID 为 TRUE，如果 SchemaGen 实用程序将使用特性为其**dt: type ="id"** 指定为主键列并添加相应的 PRIMARY KEY 约束创建表时。  
  
 默认值是 FALSE。  
  
 TempFilePath  
 指定文件路径，该路径中包含 XML 大容量加载为事务性大容量加载创建的临时文件。 （只有在 Transaction 属性设置为 TRUE 时，此属性才有用。）您必须确保[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用于 XML 大容量加载的帐户有权访问此路径。 如果未设置此属性，XML 大容量加载将 TEMP 环境变量上指定的位置中存储临时文件。  
  
 事务  
 指定大容量加载是否应作为事务实现，在此情况下，如果大容量加载失败，则确保回滚。 此属性是一个布尔属性。 如果此属性设置为 TRUE，则大容量加载将在事务上下文中发生。 仅当事务设置为 TRUE 时，TempFilePath 属性是很有用。  
  
> [!NOTE]  
>  如果在加载二进制数据 (例如，图像 bin.base64 XML 数据类型为二进制，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型)，事务属性必须设置为 FALSE。  
  
 默认值是 FALSE。  
  
 XMLFragment  
 指定源数据是否是 XML 片断。 XML 片段是没有单个顶级（根）元素的 XML 文档。 此属性是一个布尔属性。 如果源文件由 XML 片断构成，则此属性必须设置为 TRUE。  
  
 默认值是 FALSE。  
  
  

---
title: 创建、更改和删除 FileTable | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], altering
- FileTables [SQL Server], dropping
- FileTables [SQL Server], creating
ms.assetid: 47d69e37-8778-4630-809b-2261b5c41c2c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7ed2d476be0ba9a22b42e5c7e60789a4059ea73c
ms.sourcegitcommit: ffb87aa292fc9b545c4258749c28df1bd88d7342
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2019
ms.locfileid: "71816738"
---
# <a name="create-alter-and-drop-filetables"></a>创建、更改和删除 FileTable
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  说明如何创建新的 FileTable 或者更改或删除现有的 FileTable。  
  
##  <a name="BasicsCreate"></a> 创建 FileTable  
 FileTable 是专用的用户表，它具有预定义的固定架构。 此架构存储 FILESTREAM 数据、文件和目录信息以及文件属性。 有关 FileTable 架构的信息，请参阅 [FileTable Schema](../../relational-databases/blob/filetable-schema.md)。  
  
 可以使用 Transact-SQL 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]创建新的 FileTable。 由于 FileTable 有固定架构，您不必指定列的列表。 创建 FileTable 的简单语法允许您指定：  
  
-   目录名称。 在 FileTable 文件夹层次结构中，此表级目录将成为在数据库级别指定的数据库目录的子级以及在表中存储的文件或目录的父级。  
  
-   要用于 FileTable 的“名称”  列中文件名的排序规则名称。  
  
-   要用于 3 个主键的名称和自动创建的唯一约束。  
  
###  <a name="HowToCreate"></a> 如何：创建 FileTable  
 **使用 Transact-SQL 创建 FileTable**  
 通过调用带 **AS FileTable** 选项的 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md) 语句创建 FileTable。 由于 FileTable 有固定架构，您不必指定列的列表。 您可以为新的 FileTable 指定以下设置：  
  
1.  **FILETABLE_DIRECTORY**。 指定充当存储在 FileTable 中的所有文件和目录的根目录的目录。 此名称应在数据库的所有 FileTable 目录名称中唯一。 无论当前排序规则设置如何，唯一性比较都不区分大小写。  
  
    -   此值的数据类型为 **nvarchar(255)** ，并且使用 **Latin1_General_CI_AS_KS_WS**的固定排序规则。  
  
    -   您提供的目录名称必须符合文件系统对有效目录名称的要求。  
  
    -   此名称应在数据库的所有 FileTable 目录名称中唯一。 无论当前排序规则设置如何，唯一性比较都不区分大小写。  
  
    -   如果您创建 FileTable 时没有提供目录名称，则 FileTable 自身的名称将用作目录名称。  
  
2.  **FILETABLE_COLLATE_FILENAME**。 指定要应用于 FileTable 的“名称”  列的排序规则名称。  
  
    1.  指定的排序规则必须**不区分大小写**，以符合 Windows 文件命名语义。  
  
    2.  如果未提供 **FILETABLE_COLLATE_FILENAME**的值，或指定了 **database_default**，则该列继承当前数据库的排序规则。 如果当前数据库排序规则区分大小写，将引发错误， **CREATE TABLE** 操作将失败。  
  
3.  您还可以指定要用于 3 个主键的名称和自动创建的唯一约束。 如果您不提供名称，则系统会生成名称，如本主题后面所述。  

    -   **FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME**  
  
    -   **FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME**  
  
    -   **FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME**  
  
 **示例**  
  
 以下示例将创建一个新的 FileTable，并为 **FILETABLE_DIRECTORY** 和 **FILETABLE_COLLATE_FILENAME**指定用户定义的值。  
  
```sql  
CREATE TABLE DocumentStore AS FileTable  
    WITH (   
          FileTable_Directory = 'DocumentTable',  
          FileTable_Collate_Filename = database_default  
         );  
GO  
```  
  
 下面的示例也创建一个新的 FileTable。 由于没有指定用户定义的值，因此 **FILETABLE_DIRECTORY** 的值将成为 FileTable 的名称， **FILETABLE_COLLATE_FILENAME** 的值将成为 database_default，主键和唯一约束将收到系统生成的名称。  
  
```sql  
CREATE TABLE DocumentStore AS FileTable;  
GO  
```  
  
 **使用 SQL Server Management Studio 创建 FileTable**  
 在对象资源管理器中，展开所选数据库下的对象，然后右键单击“Tables”  文件夹，选择“新建 FileTable”  。  
  
 此选项将打开一个新的脚本窗口，其中包含一个 Transact-SQL 脚本模板，您可以自定义和运行此模板以创建 FileTable。 使用 **“查询”** 菜单上的 **“指定模板参数的值”** 选择可轻松指定脚本。  
  
###  <a name="ReqCreate"></a> 创建 FileTable 的要求和限制  
  
-   不能更改现有表以将其转换为 FileTable。  
  
-   先前在数据库级别指定的父目录还必须具有非 Null 值。 有关指定数据库级目录的信息，请参阅 [启用 FileTable 的先决条件](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)。  
  
-   由于一个 FileTable 包含一个 FILESTREAM 列，因此，FileTable 需要有效的 FILESTREAM 文件组。 可以指定有效的 FILESTREAM 文件组作为 **CREATE TABLE** 命令的一部分以创建 FileTable（可选）。 如果未指定文件组，则 FileTable 使用数据库的默认 FILESTREAM 文件组。 如果数据库没有 FILESTREAM 文件组，将引发错误。  
  
-   不能将表约束作为 CREATE TABLE…AS FILETABLE 语句的一部分创建  。 但是，您以后可以使用 **ALTER TABLE** 语句添加该约束。  
  
-   不能在 **tempdb** 数据库或任何其他系统数据库中创建 FileTable。  
  
-   不能将 FileTable 作为临时表创建。  
  
##  <a name="BasicsAlter"></a> 更改 FileTable  
 由于 FileTable 具有预定义的固定架构，您不能添加或更改它的列。 但是，可以将自定义索引、触发器、约束和其他选项添加到 FileTable。  
  
 有关使用 ALTER TABLE 语句启用或禁用 FileTable 命名空间（包括系统定义的约束）的信息，请参阅 [管理 FileTables](../../relational-databases/blob/manage-filetables.md)。  
  
###  <a name="HowToChange"></a> 如何：更改 FileTable 的目录  
 **使用 Transact-SQL 更改 FileTable 的目录**  
 调用 ALTER TABLE 语句并为 **FILETABLE_DIRECTORY** SET 选项提供一个有效的新值。  
  
 **示例**  
  
```sql  
ALTER TABLE filetable_name  
    SET ( FILETABLE_DIRECTORY = N'directory_name' );  
GO  
```  
  
 **使用 SQL Server Management Studio 更改 FileTable 的目录**  
 在对象资源管理器中，右键单击 FileTable，然后选择“属性”以打开“表属性”对话框。   在 **FileTable** 页上，为 **“FileTable 目录名称”** 输入新值。  
  
###  <a name="ReqAlter"></a> 更改 FileTable 的要求和限制  
  
-   你不能更改 **FILETABLE_COLLATE_FILENAME**的值。  
  
-   不能更改、删除或禁用 FileTable 的系统定义的列。  
  
-   不能将新的用户列、计算列或持久化计算列添加到 FileTable。  
  
##  <a name="BasicsDrop"></a> 删除 FileTable  
 可以使用 [DROP TABLE (Transact-SQL)](../../t-sql/statements/drop-table-transact-sql.md) 语句的普通语法删除 FileTable。  
  
 当您删除 FileTable 时，同时也会删除下列对象：  
  
-   此时还将删除 FileTable 的所有列以及与该表关联的所有对象，如索引、约束和触发器。  
  
-   FileTable 目录及其包含的子目录将从数据库的 FILESTREAM 文件和目录层次结构中消失。  
  
 如果 FileTable 的文件命名空间中有打开的文件句柄，DROP TABLE 命令将失败。 有关关闭打开的句柄的信息，请参阅 [管理 FileTable](../../relational-databases/blob/manage-filetables.md)。  
  
##  <a name="BasicsOtherObjects"></a> 创建 FileTable 时创建其他数据库对象  
 创建新的 FileTable 时，还会创建一些系统定义的索引和约束。 您不能更改或删除这些对象；仅当删除 FileTable 本身时，它们才消失。 若要查看这些对象的列表，请查询目录视图 [sys.filetable_system_defined_objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)。  
  
```sql  
--View all objects for all filetables, unsorted  
SELECT * FROM sys.filetable_system_defined_objects;  
GO  
  
--View sorted list with friendly names  
SELECT OBJECT_NAME(parent_object_id) AS 'FileTable', OBJECT_NAME(object_id) AS 'System-defined Object'  
    FROM sys.filetable_system_defined_objects  
    ORDER BY FileTable, 'System-defined Object';  
GO  
```  
  
 **创建新的 FileTable 时创建的索引**  
 创建新的 FileTable 时，还会创建以下系统定义的索引：  
  
|||  
|-|-|  
|**列**|**索引类型**|  
|[path_locator] ASC|主键，非聚集|  
|[parent_path_locator] ASC，<br /><br /> [name] ASC|唯一，非聚集|  
|[stream_id] ASC|唯一，非聚集|  
  
 **创建新的 FileTable 时创建的约束**  
 创建新的 FileTable 时，还会创建以下系统定义的约束：  
  
|约束|强制执行|  
|-----------------|--------------|  
|以下列的默认约束：<br /><br /> creation_time<br /><br /> is_archive<br /><br /> is_directory<br /><br /> is_hidden<br /><br /> is_offline<br /><br /> is_readonly<br /><br /> is_system<br /><br /> is_temporary<br /><br /> last_access_time<br /><br /> last_write_time<br /><br /> path_locator<br /><br /> stream_id|系统定义的默认约束强制采用指定列的默认值。|  
|检查约束|系统定义的检查约束强制执行下列要求：<br /><br /> 有效的文件名。<br /><br /> 有效的文件属性。<br /><br /> 父对象必须是目录。<br /><br /> 命名空间层次结构在文件操作过程中锁定。|  
  
 **系统定义的约束的命名约定**  
 上述系统定义的约束采用以下格式命名： **\<constraintType>_\<tablename>[\_\<columnname>]\_\<uniquifier>** ，其中：  
  
-   *<constraint_type>* 为 CK（检查约束）、DF（默认约束）、FK（外键）、PK（主键）或 UQ（唯一约束）。  
  
-   *\<uniquifier>* 是系统生成的字符串以使名称唯一。 此字符串中可能包含 FileTable 的名称和唯一标识符。  
  
## <a name="see-also"></a>另请参阅  
 [管理 FileTable](../../relational-databases/blob/manage-filetables.md)  
  
  

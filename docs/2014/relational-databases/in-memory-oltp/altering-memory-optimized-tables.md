---
title: 更改内存优化表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 690b70b7-5be1-4014-af97-54e531997839
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bcfa139cb854954d920a1148f3d5cebb907c61e4
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706559"
---
# <a name="altering-memory-optimized-tables"></a>更改内存优化表
  不支持对内存优化表执行 ALTER 操作。 其中包括更改 bucket_count、添加或删除索引、添加或删除列等操作。 本主题指导如何更新内存优化表。  
  
## <a name="updating-the-definition-of-a-memory-optimized-table"></a>更新内存优化表的定义  
 更新内存优化表的定义要求您使用更新的表定义创建一个新表，将数据复制到新表，然后使用新表启动。 除非该表是只读的，否则这要求停止表上的工作负荷以确保在执行数据复制时不对表进行更改。  
  
 以下过程概述了更新表所需的步骤。 在此示例中，更新时添加了一个索引。 此过程保留了表的名称，需要两次数据复制操作：一次是复制临时表，另一次是复制新表。 以同样的方式更改索引的 bucket_count 或添加/删除列。  
  
1.  停止表上的工作负荷。  
  
2.  生成表的脚本并将新索引添加到脚本。  
  
3.  为引用 T 的架构绑定对象（主要为本机编译的存储过程）及其权限生成脚本。  
  
     可使用以下查询查找引用表的架构绑定对象：  
  
    ```sql  
    declare @t nvarchar(255) = N'<table name>'  
  
    select r.referencing_schema_name, r.referencing_entity_name  
    from sys.dm_sql_referencing_entities (@t, 'OBJECT') as r join sys.sql_modules m on r.referencing_id=m.object_id  
    where r.is_caller_dependent = 0 and m.is_schema_bound=1;  
    ```  
  
     使用以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 可对存储过程的权限编写脚本：  
  
    ```sql  
    declare @sp nvarchar(255) = N'<procedure name>'  
    declare @permissions nvarchar(max) = N''  
  
    select @permissions += dp.state_desc + N' ' + dp.permission_name + N' ON ' +   
       quotename(schema_name(o.schema_id)) + N'.' + quotename(o.name) + N' TO ' +  
       quotename(u.name) + N'; ' + char(13)  
    from sys.database_permissions as dp  
  
    join sys.database_principals as u  
       on u.principal_id = dp.grantee_principal_id  
  
    join sys.objects as o  
       on o.object_id = dp.major_id  
    where dp.class = 1 /* object */  
       and dp.minor_id = 0 and o.object_id=object_id(@sp);  
  
    select @permissions  
    ```  
  
4.  创建表的副本并将数据从原始表复制到表的副本。 可以使用以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] <sup>1</sup>创建副本。  
  
    ```sql  
    select * into dbo.T_copy from dbo.T  
    ```  
  
     如果有足够的可用内存，则 `T_copy` 可以是内存优化表，这会使数据复制更快。<sup>2</sup>  
  
5.  删除引用原始表的架构绑定对象。  
  
6.  删除原始表。  
  
7.  使用包含新索引的脚本创建新表 (`T`)。  
  
8.  将数据从 `T_copy` 复制到 `T`。  
  
9. 重新创建引用的架构绑定对象并应用权限。  
  
10. 启动 `T` 上的工作负荷。  
  
 <sup>1</sup>请注意， `T_copy` 在此示例中，保存到磁盘。 如果 `T` 的备份可用，`T_copy` 可以为临时表或非持久表。  
  
 <sup>2</sup>对于，必须有足够的内存 `T_copy` 。 执行 `DROP TABLE` 后，不立即释放内存。 如果 `T_copy` 进行内存优化，需要有足够的内存用于新增的两个 `T` 副本。 如果 `T_copy` 是基于磁盘的表，仅需要有足够的内存用于新增的一个 `T` 副本，因为在删除旧版本的 `T` 后垃圾收集器需要同步。  
  
## <a name="changing-schema-powershell"></a>更改架构 (PowerShell)  
 以下 PowerShell 脚本通过对表和相关权限编写脚本来为架构更改做准备和生成。  
  
```powershell
prepare_schema_change.ps1 <serverName> <databaseName> <schemaName> <tableName>
```
  
 此脚本提取作为变量的表，并对对象及其权限编写脚本，然后引用当前文件夹中架构绑定的对象及其权限。 为更新输入表的架构总共生成了 7 个脚本：  
  
-   将数据复制到临时表（堆）。  
  
-   删除引用表的架构绑定对象。  
  
-   删除表。  
  
-   使用新架构重新创建表并重新应用权限。  
  
-   将数据从临时表复制到重新创建的表。  
  
-   重新创建引用表的架构绑定对象及其权限。  
  
-   删除临时表。  
  
 应更新步骤 4 的脚本以反映所需的架构更改。 如果表中的列发生更改，应根据需要更新第 5 步（从临时表复制数据）的脚本和第 6 步（重新创建存储过程）的脚本。  
  
```powershell
# Prepare for schema changes by scripting out the table, as well as associated permissions
# Usage: prepare_schema_change.ps1 server_name db_name schema_name table_name  
# stop execution once an error occurs  
$ErrorActionPreference="Stop"  
  
if($args.Count -le 3)  
{  
   throw "Usage prepare_schema_change.ps1 server_name db_name schema_name table_name"  
}  
  
$servername = $args[0]  
$database = $args[1]  
$schema = $args[2]  
$object = $args[3]  
  
$object_heap = "$object$(Get-Random)"  
  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.SMO") | Out-Null  
  
$server =  New-Object ("Microsoft.SqlServer.Management.SMO.Server") ($servername)  
$scripter = New-Object ("Microsoft.SqlServer.Management.SMO.Scripter") ($server)  
  
## initialize table variable  
$tableUrn = $server.Databases[$database].Tables[$object, $schema]  
if($tableUrn.Count -eq 0)  
{  
   throw "Table or database not found"  
}  
  
## initialize scripting object  
$scriptingOptions = New-Object ("Microsoft.SqlServer.Management.SMO.ScriptingOptions")
$scriptingOptions.Permissions = $True  
$scriptingOptions.ScriptDrops = $True  
  
$scripter.Options = $scriptingOptions;  
  
Write-Host "(1) Scripting SELECT INTO $object_heap for table [$object] to 1_copy_to_heap_for_$schema`_$object.sql"  
Echo "SELECT * INTO $schema.$object_heap FROM $schema.$object WITH (SNAPSHOT)" | Out-File "1_copy_to_heap_$schema`_$object.sql";  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(2) Scripting DROP for procs schema-bound to [$object] 2_drop_procs_$schema`_$object.sql"  
## query referencing schema-bound objects  
$dt = $server.Databases[$database].ExecuteWithResults("select r.referencing_schema_name, r.referencing_entity_name  
from sys.dm_sql_referencing_entities ('$schema.$object', 'OBJECT') as r join sys.sql_modules m on r.referencing_id=m.object_id  
where r.is_caller_dependent = 0 and m.is_schema_bound=1;")  
  
## initialize out file  
Echo "" | Out-File "2_drop_procs_$schema`_$object.sql"  
## loop through schema-bound objects  
ForEach ($t In $dt.Tables)  
{    
   ForEach ($r In $t.Rows)  
   {    
      ## script object   
      $so =  $server.Databases[$database].StoredProcedures[$r[1], $r[0]]  
      $scripter.Script($so) | Out-File -Append "2_drop_procs_$schema`_$object.sql"  
   }  
}  
Write-Host "--done--"  
Write-Host ""  
Write-Host "(3) Scripting DROP table for [$object] to 3_drop_table_$schema`_$object.sql"
$scripter.Script($tableUrn) | Out-File "3_drop_table_$schema`_$object.sql";
Write-Host "--done--"  
Write-Host ""  
  
## now script creates  
$scriptingOptions.ScriptDrops = $False  
  
Write-Host "(4) Scripting CREATE table and permissions for [$object] to !please_edit_4_create_table_$schema`_$object.sql"  
Write-Host "***** rename this script to 4_create_table.sql after completing the updates to the schema"
$scripter.Script($tableUrn) | Out-File "!please_edit_4_create_table_$schema`_$object.sql";  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(5) Scripting INSERT INTO table from heap and UPDATE STATISTICS for [$object] to 5_copy_from_heap_$schema`_$object.sql"  
Write-Host "[update this script if columns are added to or removed from the table]"  
Echo "INSERT INTO [$schema].[$object] SELECT * FROM [$schema].[$object_heap]; UPDATE STATISTICS [$schema].[$object] WITH FULLSCAN, NORECOMPUTE" | Out-File "5_copy_from_heap_$schema`_$object.sql";  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(6) Scripting CREATE PROC and permissions for procedures schema-bound to [$object] to 6_create_procs_$schema`_$object.sql"  
Write-Host "[update the procedure definitions if columns are renamed or removed]"  
## initialize out file  
Echo "" | Out-File "6_create_procs_$schema`_$object.sql"  
## loop through schema-bound objects  
ForEach ($t In $dt.Tables)  
{    
   ForEach ($r In $t.Rows)  
   {    
      ## script the schema-bound object  
      $so =  $server.Databases[$database].StoredProcedures[$r[1], $r[0]]  
      ForEach($s In $scripter.Script($so))  
        {  
            Echo $s | Out-File -Append "6_create_procs_$schema`_$object.sql"  
            Echo "GO" | Out-File -Append "6_create_procs_$schema`_$object.sql"  
        }  
   }  
}  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(7) Scripting DROP $object_heap to 7_drop_heap_$schema`_$object.sql"  
Echo "DROP TABLE $schema.$object_heap" | Out-File "7_drop_heap_$schema`_$object.sql";  
Write-Host "--done--"  
Write-Host ""  
```  
  
 以下 PowerShell 脚本执行在上一示例中脚本化的架构更改。 此脚本提取作为变量的表，并执行为该表和相关存储过程生成的架构更改脚本。  
  
 用法： execute_schema_change ps1 *server_name * * db_name `schema_name` table_name*  
  
```powershell
# stop execution once an error occurs  
$ErrorActionPreference="Stop"  
  
if($args.Count -le 3)  
{  
   throw "Usage execute_schema_change.ps1 server_name db_name schema_name table_name"  
}  
  
$servername = $args[0]  
$database = $args[1]  
$schema = $args[2]  
$object = $args[3]  
  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.SMO") | Out-Null  
  
$server =  New-Object ("Microsoft.SqlServer.Management.SMO.Server") ($servername)  
$database = $server.Databases[$database]  
$table = $database.Tables[$object, $schema]  
if($table.Count -eq 0)  
{  
   throw "Table or database not found"  
}  
  
$1 = Get-Item "1_copy_to_heap_$schema`_$object.sql"  
$2 = Get-Item "2_drop_procs_$schema`_$object.sql"  
$3 = Get-Item "3_drop_table_$schema`_$object.sql"  
$4 = Get-Item "4_create_table_$schema`_$object.sql"  
$5 = Get-Item "5_copy_from_heap_$schema`_$object.sql"  
$6 = Get-Item "6_create_procs_$schema`_$object.sql"  
$7 = Get-Item "7_drop_heap_$schema`_$object.sql"  
  
Write-Host "(1) Running SELECT INTO heap for table [$object] from 1_copy_to_heap_for_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $1.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(2) Running DROP for procs schema-bound from [$object] 2_drop_procs_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $2.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(3) Running DROP table for [$object] to 4_drop_table_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $3.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(4) Running CREATE table and permissions for [$object] from 4_create_table_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $4.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(5) Running INSERT INTO table from heap for [$object] and UPDATE STATISTICS from 5_copy_from_heap_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $5.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(6) Running CREATE PROC and permissions for procedures schema-bound to [$object] from 6_create_procs_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $6.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(7) Running DROP heap from 7_drop_heap_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $7.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
```  
  
## <a name="see-also"></a>另请参阅  
 [Memory-Optimized Tables](memory-optimized-tables.md)  

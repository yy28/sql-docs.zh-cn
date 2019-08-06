---
title: 复制到内存优化表订阅服务器 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
ms.assetid: 1a8e6bc7-433e-471d-b646-092dc80a2d1a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b9f58e472b0b6e6d164e45c2d1136c81bc4a46d6
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811227"
---
# <a name="replication-to-memory-optimized-table-subscribers"></a>复制到内存优化表订阅服务器
  充当事务复制订阅服务器的表（不包括对等事务复制）可以配置为内存优化表。 其他复制配置与内存优化表不兼容。  
  
## <a name="configuring-a-memory-optimized-table-as-a-subscriber"></a>将内存优化表配置为订阅服务器  
 若要讲内存优化表配置为订阅服务器，请执行以下步骤。  
  
 **创建和启用发布**  
  
1.  创建发布。  
  
2.  向发布添加项目。 对于 `@upd_cmd` 参数，请使用 SCALL 或 SQL 约定。  
  
    ```  
    EXEC sp_addarticle  
        @publication = N'Publication1',  
        @article = N'Mem_Table',  
        @source_owner = N'dbo',  
        @source_object = N'Mem_Table',  
        @type = N'logbased',  
        @description = null,  
        @creation_script = null,  
        @pre_creation_cmd = N'none',  
        @schema_option = 0x00000000080050DF,  
        @identityrangemanagementoption = N'manual',  
        @destination_table = N'Mem_Table',  
        @destination_owner = N'dbo',  
        @vertical_partition = N'false',  
        @ins_cmd = N'CALL sp_MSins_Mem_Table',  
        @del_cmd = N'CALL sp_MSdel_Mem_Table',  
        @upd_cmd = N'SCALL sp_MSupd_Mem_Table';  
    GO  
    ```  
  
 **生成快照并调整架构**  
  
1.  创建一个快照作业并生成快照。  
  
    ```  
    EXEC sp_addpublication_snapshot @publication = N'Publication1', @frequency_type = 1;  
    EXEC sp_startpublication_snapshot @publication = N'Publication1';  
    ```  
  
2.  导航到快照文件夹。 默认位置是 "C:\Program Files\Microsoft SQL Server\MSSQL12。实例 > \MSSQL\repldata\unc\XXX\YYYYMMDDHHMMSS\\"。 \<  
  
3.  找到 **。SCH-M**文件, 并在 Management Studio 中打开该表。 按如下所示更改表架构并且更新存储过程。  
  
     对在 IDX 文件中定义的索引进行求值。 修改 `CREATE TABLE` 以指定所需索引、约束、主键和内存优化语法。 对于内存优化表，索引列应为 NOT NULL，而字符类型的索引列必须为 Unicode 并且使用 BIN2 排序规则。 请参阅下面的示例：  
  
    ```  
    SET ANSI_PADDING ON;  
    GO  
  
    SET ANSI_NULLS ON;  
    GO  
  
    SET QUOTED_IDENTIFIER ON;  
    GO  
  
    CREATE TABLE [dbo].[Mem_Table]([c1] [int] NOT NULL,  
        [c2] [float] NOT NULL,  
        [c3] [decimal](10, 2) NOT NULL,  
        [c4] [nvarchar](5) COLLATE SQL_Latin1_General_CP850_BIN2 NOT NULL,  
        INDEX [hash_index_sample_memoryoptimizedtable_c2] HASH (c2) WITH (BUCKET_COUNT = 1024),  
        INDEX [index_sample_memoryoptimizedtable_c3] NONCLUSTERED ([c3]),  
        INDEX [nvarchar_index_sample_memoryoptimizedtable_c4] ([c4]),  
        CONSTRAINT [PK_sample_memoryoptimizedtable] PRIMARY KEY NONCLUSTERED ([c1])) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA);  
    GO  
    ```  
  
4.  在将 SCALL 约定用于 `@upd_cmd` 参数时，转到架构 (.SCH) 文件并且在 `create procedure [sp_MSupd_<SCHEMA><TABLE_NAME>]` 中更改表更新语句，以便删除主键列。  
  
     若要支持主键更新，请使用自定义更新存储过程替换主键更新语句，如下所示：  
  
    1.  选择缺失的列值（SCALL 仅提供涉及到更新操作的列）。  
  
    2.  删除现有记录。  
  
    3.  将新记录以及提供的新值（包括新主键）一起插入。  
  
     原始更新过程如下所示：  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                   @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    update [dbo].[Mem_Table] set  
                   [c1] = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
     如果主键始终不应在发布服务器上更新。 按如下所示对更新过程中这些列的更新进行注释：  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                   @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    update [dbo].[Mem_Table] set  
    --             [c1] = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
     若要允许支持主键更新，请按如下所示修改更新过程  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                    @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    select  
                   @c1 = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   @c2 = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   @c3 = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   @c4 = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    from [dbo].[Mem_Table] where [c1] = @pkc1  
    if @@rowcount <> 0 begin  
            delete [dbo].[Mem_Table] where [c1] = @pkc1  
            if @@rowcount <> 0  
                   insert into [dbo].[Mem_Table]([c1],  
                           [c2],  
                           [c3],  
                           [c4]) values (  
                           @c1,  
                           @c2,  
                           @c3,  
                           @c4  
                   )   
    end  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
5.  使用 "**提升为快照隔离**" 选项创建订阅服务器数据库, 并在使用非 Unicode 字符数据类型的情况下将默认排序规则设置为 Latin1_General_CS_AS_KS_WS。  
  
    ```  
    CREATE DATABASE [Sub]   
    CONTAINMENT = NONE   
    ON PRIMARY ( NAME = [Sub], FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub.mdf]),   
    FILEGROUP [mem] CONTAINS MEMORY_OPTIMIZED_DATA ( NAME = [mem],   
    FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub])  
    LOG ON ( NAME = [Sub_log], FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub.ldf])  
    COLLATE Latin1_General_CS_AS_KS_WS;  
  
    ALTER DATABASE [Sub] SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;  
    GO  
    ```  
  
6.  将架构应用于订阅服务器的数据库, 并保存架构以供将来使用。  
  
7.  加载发布服务器（源）数据写入订阅服务器。 在您添加订阅前，不应在发布服务器上更改数据。  可按如下所示使用 BCP：  
  
    ```  
    bcp Pub.dbo.Mem_Table out Mem_Table.bcp -S. -T -C1252 -n  
    bcp Sub.dbo.Mem_Table in Mem_Table.bcp -S. -T -C1252 -n  
    ```  
  
8.  重新配置项目以便禁用订阅服务器上的架构更改：  
  
    ```  
    EXEC sp_changearticle  
        @publication = N'Publication1',  
        @article = N'Mem_Table',  
        @property = N'schema_option',  
        @value = 0,  
        @force_invalidate_snapshot = 1,  
        @force_reinit_subscription = 1;  
    GO  
    ```  
  
 **不添加同步订阅**  
  
 添加非同步订阅。  
  
```  
EXEC sp_addsubscription  
    @publication = N' Publication1',  
    @subscriber = @@ServerName,  
    @destination_db = N'Sub',  
    @subscription_type = N'Push',  
    @sync_type = N'replication support only',  
    @article = N'all',  
    @update_mode = N'read only',  
    @subscriber_type = 0;  
GO  
```  
  
 内存优化表现在应该开始从发布服务器接收更新。  
  
## <a name="restrictions"></a>限制  
 仅支持单向事务复制。 不支持对等事务复制。  
  
 内存优化表无法发布。  
  
 分发服务器上的复制表无法配置为内存优化表。  
  
 合并复制无法包括内存优化表。  
  
 在订阅服务器上，在事务复制中涉及的表可以配置为内存优化表，但订阅服务器上的表必须满足针对内存优化表的要求。 这要求以下限制。  
  
-   若要在事务复制订阅服务器上创建内存优化表，必须手动修改用于创建内存优化表的快照架构文件。 有关详细信息, 请参阅[修改架构文件](#Schema)。  
  
-   根据内存优化表的行限制，复制到订阅服务器上的内存优化表的表限制为 8060 字节。  
  
-   复制到订阅服务器上的内存优化表的表限制为内存优化表允许的数据类型。 有关详细信息, 请参阅[支持的数据类型](../in-memory-oltp/supported-data-types-for-in-memory-oltp.md)。  
  
-   对于更新要复制到订阅服务器上内存优化表的表的主键，存在一些限制。 有关详细信息, 请参阅[将更改复制到主键](#PrimaryKey)。  
  
-   在内存优化表中不支持外键、唯一约束、触发器、架构修改、ROWGUIDCOL、计算列、数据压缩、别名数据类型、版本化和锁。 有关信息，请参阅 [内存中 OLTP 不支持的 T-SQL 构造](../in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md) 。  
  
##  <a name="Schema"></a> 修改架构文件  
  
-   不支持聚集索引。 将所有聚集索引更改为非聚集索引。  
  
-   索引键中的所有列都必须指定为 `NOT NULL`。  
  
-   如果使用内存优化表选项 `DURABILITY = SCHEMA_AND_DATA` ，则表必须具有非聚集主键索引。  
  
-   ANSI_PADDING 必须为 ON。  
  
##  <a name="PrimaryKey"></a>将更改复制到主键  
 内存优化表的主键无法更新。 若要复制订阅服务器上的主键更新，请修改更新存储过程以便将该更新作为删除和插入对提供。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 复制](sql-server-replication.md)  
  
  

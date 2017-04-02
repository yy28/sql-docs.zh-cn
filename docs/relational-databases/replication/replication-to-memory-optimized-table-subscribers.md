---
title: "复制到内存优化表订阅服务器 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/21/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1a8e6bc7-433e-471d-b646-092dc80a2d1a
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# 复制到内存优化表订阅服务器
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  用作快照和事务复制订阅服务器（不包括对等事务复制）的表可以配置为内存优化表。 其他复制配置与内存优化表不兼容。 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]及更高版本支持此功能。  
  
## <a name="two-configurations-are-required"></a>需要进行两项配置  
  
-   **配置订阅服务器数据库，以支持对内存优化表进行复制**  
  
     设置 **@memory_optimized** 属性 **true**, ，通过使用 [sp_addsubscription &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 或 [sp_changesubscription &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)。  
  
-   **配置项目以支持对内存优化表进行复制**  
  
     设置 `@schema_option = 0x40000000000` 为通过使用项目的选项 [sp_addarticle &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 或 [sp_changearticle &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)。  
  
#### <a name="to-configure-a-memory-optimized-table-as-a-subscriber"></a>将内存优化表配置为订阅服务器表  
  
1.  创建事务发布。 有关详细信息，请参阅 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
2.  向发布添加项目。 有关详细信息，请参阅 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)。  
  
     如果通过使用配置 [!INCLUDE[tsql](../../includes/tsql-md.md)] 设置 **@schema_option** 参数 **sp_addarticle** 存储过程   
    **0x40000000000**及更高版本支持此功能。  
  
3.  在项目属性窗口中，将“启用内存优化”  设置为“true” 。  
  
4.  启动快照代理作业以为此发布生成初始快照。 有关详细信息，请参阅 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
5.  此时，创建新订阅。 在“新建订阅向导”  中，将“内存优化订阅”  设置为“true” 。  
  
 内存优化表现在应该开始从发布服务器接收更新。  
  
#### <a name="reconfigure-an-existing-transaction-replication"></a>重新配置现有的事务复制  
  
1.  转到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的订阅属性，然后将“内存优化订阅”  设置为“true” 。 只有在重新初始化订阅之后，系统才会应用这些更改。  
  
     如果通过使用配置 [!INCLUDE[tsql](../../includes/tsql-md.md)] 设置新 **@memory_optimized** 参数 **sp_addsubscription** 存储为 true 的过程。  
  
2.  转到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的发布项目属性，然后将“启用内存优化”  设置为“true”。  
  
     如果通过使用配置 [!INCLUDE[tsql](../../includes/tsql-md.md)] 设置 **@schema_option** 参数 **sp_addarticle** 存储过程   
    **0x40000000000**及更高版本支持此功能。  
  
3.  内存优化表不支持聚集索引。 若要让复制能够通过在目标上将聚集索引转换成非聚集索引来处理此情况，请将“为内存优化项目将聚集索引转换成非聚集索引”  设置为“true”。  
  
     如果通过使用配置 [!INCLUDE[tsql](../../includes/tsql-md.md)] 设置 **@schema_option** 参数 **sp_addarticle** 存储过程  **0x0000080000000000**。  
  
4.  重新生成快照。  
  
5.  重新初始化订阅。  
  
## <a name="remarks-and-restrictions"></a>备注和限制  
 仅支持单向事务复制。 不支持对等事务复制。  
  
 内存优化表无法发布。  
  
 分发服务器上的复制表无法配置为内存优化表。  
  
 合并复制无法包括内存优化表。  
  
 在订阅服务器上，在事务复制中涉及的表可以配置为内存优化表，但订阅服务器上的表必须满足针对内存优化表的要求。 这要求以下限制。  
 
-   复制到订阅服务器上的内存优化表的表限制为内存优化表允许的数据类型。 有关详细信息，请参阅 [内存中 OLTP 支持的数据类型](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md)。  
  
-   内存优化表支持不是所有的 TRANSACT-SQL 功能。 请参阅 [内存中 OLTP 不支持 TRANSACT-SQL 构造](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md) 有关详细信息。  
  
##  <a name="a-nameschemaa-modifying-a-schema-file"></a><a name="Schema"></a> 修改架构文件  
  
-   如果使用内存优化表选项 `DURABILITY = SCHEMA_AND_DATA` ，则表必须具有非聚集主键索引。  
  
-   ANSI_PADDING 必须为 ON。  
  
## <a name="see-also"></a>另请参阅  
 [复制功能和任务](../../relational-databases/replication/replication-features-and-tasks.md)  
  
  
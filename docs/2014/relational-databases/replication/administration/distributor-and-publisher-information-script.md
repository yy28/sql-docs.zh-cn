---
title: 分发服务器和发布服务器信息脚本 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Publishers [SQL Server replication], information scripts
- Distributors [SQL Server replication], information scripts
ms.assetid: 8622db47-c223-48fa-87ff-0b4362cd069a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4695b53e52c9c63eaacb4f2f32c6bc9f65958213
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060832"
---
# <a name="distributor-and-publisher-information-script"></a>分发服务器和发布服务器信息脚本
  此脚本使用系统表和复制存储过程回答有关分发服务器和发布服务器上的对象的常见问题。 此脚本可按原样使用，也可以作为自定义脚本的基础。 此脚本可能需要做两处修改才能在您的环境中运行：  
  
-   将 `use AdventureWorks2012` 一行更改为使用您的发布数据库的名称。  
  
-   `--`从行中删除注释（） `exec sp_helparticle @publication='<PublicationName>'` ，并将替换 \<PublicationName> 为发布的名称。  
  
```  
--********** Execute at the Distributor in the master database **********--  
  
USE master;  
go  
  
--Is the current server a Distributor?  
--Is the distribution database installed?  
--Are there other Publishers using this Distributor?  
EXEC sp_get_distributor  
  
--Is the current server a Distributor?  
SELECT is_distributor FROM sys.servers WHERE name='repl_distributor' AND data_source=@@servername;  
  
--Which databases on the Distributor are distribution databases?  
SELECT name FROM sys.databases WHERE is_distributor = 1  
  
--What are the Distributor and distribution database properties?  
EXEC sp_helpdistributor;  
EXEC sp_helpdistributiondb;  
EXEC sp_helpdistpublisher;  
  
--********** Execute at the Publisher in the master database **********--  
  
--Which databases are published for replication and what type of replication?  
EXEC sp_helpreplicationdboption;  
  
--Which databases are published using snapshot replication or transactional replication?  
SELECT name as tran_published_db FROM sys.databases WHERE is_published = 1;  
--Which databases are published using merge replication?  
SELECT name as merge_published_db FROM sys.databases WHERE is_merge_published = 1;  
  
--What are the properties for Subscribers that subscribe to publications at this Publisher?  
EXEC sp_helpsubscriberinfo;  
  
--********** Execute at the Publisher in the publication database **********--  
  
USE AdventureWorks2012;  
go  
  
--What are the snapshot and transactional publications in this database?   
EXEC sp_helppublication;  
--What are the articles in snapshot and transactional publications in this database?  
--REMOVE COMMENTS FROM NEXT LINE AND REPLACE <PublicationName> with the name of a publication  
--EXEC sp_helparticle @publication='<PublicationName>';  
  
--What are the merge publications in this database?   
EXEC sp_helpmergepublication;  
--What are the articles in merge publications in this database?  
EXEC sp_helpmergearticle; -- to return information on articles for a single publication, specify @publication='<PublicationName>'  
  
--Which objects in the database are published?  
SELECT name AS published_object, schema_id, is_published AS is_tran_published, is_merge_published, is_schema_published  
FROM sys.tables WHERE is_published = 1 or is_merge_published = 1 or is_schema_published = 1  
UNION  
SELECT name AS published_object, schema_id, 0, 0, is_schema_published  
FROM sys.procedures WHERE is_schema_published = 1  
UNION  
SELECT name AS published_object, schema_id, 0, 0, is_schema_published  
FROM sys.views WHERE is_schema_published = 1;  
  
--Which columns are published in snapshot or transactional publications in this database?  
SELECT object_name(object_id) AS tran_published_table, name AS published_column FROM sys.columns WHERE is_replicated = 1;  
  
--Which columns are published in merge publications in this database?  
SELECT object_name(object_id) AS merge_published_table, name AS published_column FROM sys.columns WHERE is_merge_published = 1;  
```  
  
## <a name="see-also"></a>另请参阅  
 [复制管理员常见问题解答](frequently-asked-questions-for-replication-administrators.md)   
 [sp_get_distributor (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-get-distributor-transact-sql)   
 [sp_helparticle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helparticle-transact-sql)   
 [sp_helpdistributiondb (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql)   
 [sp_helpdistpublisher (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql)   
 [sp_helpdistributor (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql)   
 [sp_helpmergearticle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql)   
 [sp_helpmergepublication (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql)   
 [sp_helppublication (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)   
 [sp_helpreplicationdboption (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helpreplicationdboption-transact-sql)   
 [sp_helpsubscriberinfo (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql)   
 [sys.columns (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-columns-transact-sql)   
 [sys.databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [sys.procedures (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-procedures-transact-sql)   
 [sys.servers (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-servers-transact-sql)   
 [sys.tables (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql)   
 [sys.views (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-views-transact-sql)  
  
  

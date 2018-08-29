---
title: sp_adddistributiondb (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 04/30/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_adddistributiondb_TSQL
- sp_adddistributiondb
helpviewer_keywords:
- sp_adddistributiondb
ms.assetid: e9bad56c-d2b3-44ba-a4d7-ff2fd842e32d
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: db1cc4feb71c3b7c7bdc09e1c62f5fa1237a3d0d
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43029172"
---
# <a name="spadddistributiondb-transact-sql"></a>sp_adddistributiondb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建新的分发数据库并安装分发服务器架构。 分发数据库存储过程、架构以及用于复制的元数据。 此存储过程在分发服务器的主数据库中执行，以便创建分发数据库并安装启用复制分发所需的表和存储过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_adddistributiondb [ @database= ] 'database'   
    [ , [ @data_folder= ] 'data_folder' ]   
    [ , [ @data_file= ] 'data_file' ]   
    [ , [ @data_file_size= ] data_file_size ]   
    [ , [ @log_folder= ] 'log_folder' ]   
    [ , [ @log_file= ] 'log_file' ]   
    [ , [ @log_file_size= ] log_file_size ]   
    [ , [ @min_distretention= ] min_distretention ]   
    [ , [ @max_distretention= ] max_distretention ]   
    [ , [ @history_retention= ] history_retention ]   
    [ , [ @security_mode= ] security_mode ]   
    [ , [ @login= ] 'login' ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @createmode= ] createmode ]  
    [ , [ @from_scripting = ] from_scripting ] 
    [ , [ @deletebatchsize_xact = ] deletebatchsize_xact ] 
    [ , [ @deletebatchsize_cmd = ] deletebatchsize_cmd ] 
```  
  
## <a name="arguments"></a>参数  
 [  **@database=**]*数据库*  
 要创建的分发数据库的名称。 *数据库*是**sysname**，无默认值。 如果指定的数据库已经存在并且尚未标记为分发数据库，那么将安装启用分发所需的对象并将数据库标记为分发数据库。 如果指定的数据库已经作为分发数据库启用，则返回错误。  
  
 [  **@data_folder=**] *** * * data_folder*  
 用于存储分发数据库数据文件的目录的名称。 *data_folder*是**nvarchar(255)**，默认值为 NULL。 如果为 NULL，则使用该 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的数据目录，例如 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data`。  
  
 [  **@data_file=**] **'***data_file*****  
 数据库文件的名称。 *data_file*是**nvarchar(255)**，默认值为**数据库**。 如果为 NULL，存储过程将使用数据库名称来构造文件名。  
  
 [  **@data_file_size=**] *data_file_size*  
 初始数据文件大小，以兆字节 (MB) 为单位。 *data_file_size 我*s **int**，默认值为 5 MB。  
  
 [  **@log_folder=**] **'***log_folder*****  
 数据库日志文件所在目录的名称。 *log_folder*是**nvarchar(255)**，默认值为 NULL。 如果为 NULL，则使用该 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的数据目录，例如 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data`。  
  
 [  **@log_file=**] **'***log_file*****  
 日志文件的名称。 *log_file*是**nvarchar(255)**，默认值为 NULL。 如果为 NULL，存储过程将使用数据库名称来构造文件名。  
  
 [  **@log_file_size=**] *log_file_size*  
 初始日志文件大小，以兆字节 (MB) 为单位。 *log_file_size*是**int**，默认值为 0 MB，这意味着使用的最小日志创建的文件大小文件大小允许的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 [  **@min_distretention=**] *min_distretention*  
 从分发数据库中删除事务前的最小保持期，以小时为单位。 *min_distretention*是**int**，默认值为 0 小时。  
  
 [  **@max_distretention=**] *max_distretention*  
 删除事务前的最大保持期，以小时为单位。 *max_distretention*是**int**，默认值为 72 小时。 尚未接收到在最大分发保持期之前复制的命令的订阅将标记为非活动，并需要重新初始化。 针对每个非活动订阅发出 RAISERROR 21011。 值为**0**表示复制的事务不会存储在分发数据库。  
  
 [  **@history_retention=**] *history_retention*  
 历史记录的保留时间，以小时为单位。 *history_retention*是**int**，默认值为 48 小时。  
  
 [  **@security_mode=**] *security_mode*  
 同步时连接到分发服务器所使用的安全模式。 *security_mode*是**int**，默认值为 1。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证;**1**指定 Windows 集成身份验证。  
  
 [  **@login=**] **'***登录*****  
 连接到分发服务器以创建分发数据库时使用的登录名。 这是必需的如果*security_mode*设置为**0**。 login 的数据类型为 sysname，默认值为 NULL。  
  
 [  **@password=**] **'***密码*****  
 连接到分发服务器时使用的密码。 这是必需的如果*security_mode*设置为**0**。 *密码*是**sysname**，默认值为 NULL。  
  
 [  **@createmode=**] *createmode*  
 *createmode*是**int**，默认值为 1，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**1** （默认值）|CREATE DATABASE 或使用现有数据库，然后应用**instdist.sql**文件以创建分发数据库中的复制对象。|  
|**2**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 [  **@from_scripting =** ] *from_scripting*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
 
 [  **@deletebatchsize_xact=**] *deletebatchsize_xact*  
 指定要在从 MSRepl_Transactions 表过期的事务的清理过程中使用的批处理大小。 *deletebatchsize_xact*是**int**，默认值为 5000。 SQL Server 2017，跟在 SQL Server 2012 SP4 和 SQL Server 2016 SP2 中的版本中，首先引入了此参数。  

 [  **@deletebatchsize_cmd=**] *deletebatchsize_cmd*  
 指定要在 MSRepl_Commands 表中的过期命令的清理过程中使用的批处理大小。 *deletebatchsize_cmd*是**int**，默认值为 2000年。 SQL Server 2017，跟在 SQL Server 2012 SP4 和 SQL Server 2016 SP2 中的版本中，首先引入了此参数。 
 
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>Remarks  
 **sp_adddistributiondb**用于所有类型的复制。 但是，此存储过程只在分发服务器上运行。  
  
 必须通过执行配置分发服务器上[sp_adddistributor](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)之前执行**sp_adddistributiondb**。  
  
 运行**sp_adddistributor**在运行前先**sp_adddistributiondb**。  
  
## <a name="example"></a>示例  
  
```  
-- This script uses sqlcmd scripting variables. They are in the form  
-- $(MyVariable). For information about how to use scripting variables    
-- on the command line and in SQL Server Management Studio, see the   
-- "Executing Replication Scripts" section in the topic  
-- "Programming Replication Using System Stored Procedures".  
  
-- Install the Distributor and the distribution database.  
DECLARE @distributor AS sysname;  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @directory AS nvarchar(500);  
DECLARE @publicationDB AS sysname;  
-- Specify the Distributor name.  
SET @distributor = $(DistPubServer);  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
-- Specify the replication working directory.  
SET @directory = N'\\' + $(DistPubServer) + '\repldata';  
-- Specify the publication database.  
SET @publicationDB = N'AdventureWorks2012';   
  
-- Install the server MYDISTPUB as a Distributor using the defaults,  
-- including autogenerating the distributor password.  
USE master  
EXEC sp_adddistributor @distributor = @distributor;  
  
-- Create a new distribution database using the defaults, including  
-- using Windows Authentication.  
USE master  
EXEC sp_adddistributiondb @database = @distributionDB,   
    @security_mode = 1;  
GO  
  
-- Create a Publisher and enable AdventureWorks2012 for replication.  
-- Add MYDISTPUB as a publisher with MYDISTPUB as a local distributor  
-- and use Windows Authentication.  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
  
USE [distribution]  
EXEC sp_adddistpublisher @publisher=@publisher,   
    @distribution_db=@distributionDB,   
    @security_mode = 1;  
GO  
  
```  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_adddistributiondb**。  
  
## <a name="see-also"></a>请参阅  
 [配置发布和分发](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistributiondb &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [sp_helpdistributiondb (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [配置分发](../../relational-databases/replication/configure-distribution.md)  
  
  

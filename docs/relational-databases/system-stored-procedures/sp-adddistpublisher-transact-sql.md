---
title: sp_adddistpublisher (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adddistpublisher
- sp_adddistpublisher_TSQL
helpviewer_keywords:
- sp_adddistpublisher
ms.assetid: 04e15011-a902-4074-b38c-3ec2fc73b838
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2190e31245cde19eca4c5a47f21ac48e12f57f53
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771390"
---
# <a name="spadddistpublisher-transact-sql"></a>sp_adddistpublisher (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  配置发布服务器以使用指定的分发数据库。 此存储过程在分发服务器上的任何数据库中执行。 请注意, 在使用此存储过程之前, 必须先运行存储过程[sp_adddistributor &#40;&#41; transact-sql](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)和[sp_adddistributiondb &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) 。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_adddistpublisher [ @publisher= ] 'publisher'   
        , [ @distribution_db= ] 'distribution_db'   
    [ , [ @security_mode= ] security_mode ]   
    [ , [ @login= ] 'login' ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @working_directory= ] 'working_directory' ]   
    [ , [ @storage_connection_string= ] 'storage_connection_string']
    [ , [ @trusted= ] 'trusted' ]   
    [ , [ @encrypted_password= ] encrypted_password ]   
    [ , [ @thirdparty_flag = ] thirdparty_flag ]  
    [ , [ @publisher_type = ] 'publisher_type' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @publisher = ] 'publisher'`发布服务器名称。 *发布服务器*的**sysname**, 无默认值。  
  
`[ @distribution_db = ] 'distribution_db'`分发数据库的名称。 *distributor_db*的值为**sysname**, 无默认值。 复制代理使用该参数连接到发布服务器。  
  
`[ @security_mode = ] security_mode`实现的安全模式。 此参数仅供复制代理用于连接到排队更新订阅的发布服务器或非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *security_mode*的数据值为**int**, 可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**0**|分发服务器中的复制代理使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证连接到发布服务器。|  
|**1** （默认值）|分发服务器中的复制代理使用 Windows 身份验证连接到发布服务器。|  
  
`[ @login = ] 'login'`登录名。 如果*security_mode*为**0**, 则此参数是必需的。 login 的数据类型为 sysname，默认值为 NULL。 复制代理使用该参数连接到发布服务器。  
  
`[ @password = ] 'password']`密码。 *password*的值为**sysname**, 默认值为 NULL。 复制代理使用该参数连接到发布服务器。  
  
> [!IMPORTANT]  
>  不要使用空密码。 请使用强密码。  
  
`[ @working_directory = ] 'working_directory'`用于存储发布的数据和架构文件的工作目录的名称。 *working_directory*为**nvarchar (255)** , 默认为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]此实例的 ReplData 文件夹, 例如`C:\Program Files\Microsoft SQL Server\MSSQL\MSSQ.1\ReplData`。 名称应按 UNC 格式指定。  

 对于 Azure SQL 数据库, 请`\\<storage_account>.file.core.windows.net\<share>`使用。

`[ @storage_connection_string = ] 'storage_connection_string'`对于 SQL 数据库是必需的。 使用 Azure 门户中的 "存储 > 设置" 下的访问密钥。

 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]

`[ @trusted = ] 'trusted'`此参数已弃用, 提供此参数只是为了向后兼容。 *trusted*为**nvarchar (5)** , 将其设置为任何值, 但**false**将导致错误。  
  
`[ @encrypted_password = ] encrypted_password`不再支持设置*encrypted_password* 。 尝试将此**位**参数设置为**1**将导致错误。  
  
`[ @thirdparty_flag = ] thirdparty_flag`发布服务器是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时为。 *thirdparty_flag*为**bit**, 可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0** （默认值）|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据.|  
|**1**|非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。|  
  
`[ @publisher_type = ] 'publisher_type'`当发布服务器不[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是时指定发布服务器类型。 *publisher_type*为 sysname, 可以为以下值之一。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**<br /><br /> （默认值）|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器。|  
|**联手**|指定标准的 Oracle 发布服务器。|  
|**ORACLE 网关**|指定 Oracle 网关发布服务器。|  
  
 有关 Oracle 发布服务器与 Oracle 网关发布服务器之间的差异的详细信息, 请参阅[配置 Oracle 发布服务器](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 **sp_adddistpublisher**用于快照复制、事务复制和合并复制。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistpublisher-tran_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员才能执行**sp_adddistpublisher**。  
  
## <a name="see-also"></a>请参阅  
 [配置发布和分发](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistpublisher (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [配置分发](../../relational-databases/replication/configure-distribution.md)  
  
  

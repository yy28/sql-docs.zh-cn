---
title: sp_changedistpublisher （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedistpublisher_TSQL
- sp_changedistpublisher
helpviewer_keywords:
- sp_changedistpublisher
ms.assetid: 7ef5c89d-faaa-4f8e-aef7-00649ebc8bc9
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8aec9e25008c8dfe3b14bbe838f8122bb93fb756
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717405"
---
# <a name="sp_changedistpublisher-transact-sql"></a>sp_changedistpublisher (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  更改分发发布服务器的属性。 此存储过程在分发服务器上的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_changedistpublisher [ @publisher = ] 'publisher'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @storage_connection_string = ] 'storage_connection_string']
```  
  
## <a name="arguments"></a>自变量  
`[ @publisher = ] 'publisher'`发布服务器名称。 *发布服务器*的**sysname**，无默认值。  
  
`[ @property = ] 'property'`要更改的给定发布服务器的属性。 *属性*为**sysname** ，可以是下列值之一。  
  
`[ @value = ] 'value'`给定属性的值。 *值*为**nvarchar （255）**，默认值为 NULL。  
  
`[ @storage_connection_string = ] 'storage_connection_string'`对于 SQL 数据库托管实例是必需的，应匹配 Azure SQL 数据库存储卷的访问密钥。 


 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]
 
 下表说明了发布服务器的属性和这些属性的值。  
  
|Property|值|说明|  
|--------------|------------|-----------------|  
|**active**|true|激活发布服务器。|  
||**false**|停用发布服务器|  
|**distribution_db**||分发数据库的名称。|  
|**id**||登录名。|  
|**password**||提供的登录名的强密码。|  
|**security_mode**|**1**|连接发布服务器时，使用 Windows 身份验证。 *不能更改非* [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]*发布者。*|  
||**0**|连接发布服务器时，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。 *不能更改非* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]*发布者。*|  
|**working_directory**||用于存储发布的数据和架构文件的工作目录。|  
|NULL（默认值）||将打印所有可用的*属性*选项。| 
|**storage_connection_string**| 访问密钥 | Azure SQL 数据库托管实例数据库时工作目录的访问密钥。 
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_changedistpublisher**在所有类型的复制中使用。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员才能**sp_changedistpublisher**执行。  
  
## <a name="see-also"></a>另请参阅  
 [查看和修改分发服务器和发布服务器属性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

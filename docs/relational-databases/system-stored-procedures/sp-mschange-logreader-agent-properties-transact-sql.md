---
title: sp_MSchange_logreader_agent_properties (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_MSchange_logreader_agent_properties_TSQL
- sp_MSchange_logreader_agent_properties
helpviewer_keywords:
- sp_MSchange_logreader_agent_properties
ms.assetid: 925df9d3-a041-4046-8e17-c47f40edb86d
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: daf6a59d9d9a07393516de37868069b547690ff1
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43038027"
---
# <a name="spmschangelogreaderagentproperties-transact-sql"></a>sp_MSchange_logreader_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改在运行的日志读取器代理作业的属性[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更高版本分发服务器。 当发布服务器在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 实例上运行时，可使用此存储过程更改属性。 此存储过程在分发服务器上对分发数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_MSchange_logreader_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publisher_security_mode = ] publisher_security_mode  
        , [ @publisher_login = ] 'publisher_login'  
        , [ @publisher_password = ] 'publisher_password'   
        , [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
        , [ @publisher_type = ] 'publisher_type'  
```  
  
## <a name="arguments"></a>参数  
 [ **@publisher** = ] **'***publisher***'**  
 发布服务器的名称。 *发布服务器*是**sysname**，无默认值。  
  
 [  **@publisher_db=** ] **'***publisher_db*****  
 发布数据库的名称。 *publisher_db*是**sysname**，无默认值。  
  
 [ **@publisher_security_mode**=] *publisher_security_mode*  
 连接到发布服务器时代理所使用的安全模式。 *publisher_security_mode*是**smallint**，无默认值。  
  
 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。  
  
 **1**指定 Windows 身份验证。  
  
 [ **@publisher_login**=] **'***publisher_login*****  
 连接到发布服务器时所使用的登录名。 *publisher_login*是**sysname**，无默认值。 *publisher_login*时，必须指定*publisher_security_mode*是**0**。 如果*publisher_login*为 NULL 并*publisher_security_mode*是**1**，然后在指定的 Windows 帐户*job_login*将使用当连接到发布服务器。  
  
 [ **@publisher_password**=] **'***publisher_password*****  
 连接到发布服务器时所使用的密码。 *publisher_password*是**sysname**，无默认值。  
  
 [ **@job_login**=] **'***job_login*****  
 用于运行代理的 Windows 帐户的登录名。 *job_login*是**nvarchar(257)**，无默认值。 *这是无法更改为非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *发布服务器。*  
  
 [ **@job_password**=] **'***job_password*****  
 用于运行代理的 Windows 帐户的密码。 *job_password*是**sysname**，无默认值。  
  
 [ **@publisher_type**=] **'***publisher_type*****  
 当发布服务器未在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例中运行时指定该发布服务器类型。 *publisher_type*是**sysname**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器。|  
|**ORACLE**|指定标准的 Oracle 发布服务器。|  
|**ORACLE 网关**|指定 Oracle 网关发布服务器。|  
  
 有关 Oracle 发布服务器和 Oracle 网关发布服务器之间的差异的详细信息，请参阅[Oracle 发布概述](../../relational-databases/replication/non-sql/oracle-publishing-overview.md)。  
  
## <a name="remarks"></a>Remarks  
 **sp_MSchange_logreader_agent_properties**事务复制中使用。  
  
 执行时，必须指定所有参数**sp_MSchange_logreader_agent_properties**。 执行[sp_helplogreader_agent &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md)若要返回的日志读取器代理作业的当前属性。  
  
 更改代理登录名或密码之后，必须先停止并重新启动代理，然后更改才能生效。  
  
 发布服务器实例上的运行时[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更高版本，应使用[sp_changelogreader_agent](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)更改日志读取器代理的属性。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**分发服务器上的固定的服务器角色可以执行**sp_MSchange_logreader_agent_properties**。  
  
## <a name="see-also"></a>请参阅  
 [sp_addlogreader_agent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
  

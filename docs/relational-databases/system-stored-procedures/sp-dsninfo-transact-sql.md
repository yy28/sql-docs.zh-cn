---
title: sp_dsninfo （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dsninfo
- sp_dsninfo_TSQL
helpviewer_keywords:
- sp_dsninfo
ms.assetid: 34648615-814b-42bc-95a3-50e86b42ec4d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d7409d28b6a21a033c139c63ca6d6e7524e6ba50
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783767"
---
# <a name="sp_dsninfo-transact-sql"></a>sp_dsninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  从与当前服务器关联的分发服务器中返回 ODBC 或 OLE DB 数据源信息。 此存储过程在分发服务器上的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dsninfo [ @dsn =] 'dsn'   
    [ , [ @infotype =] 'info_type']   
    [ , [ @login =] 'login']   
    [ , [ @password =] 'password']  
    [ , [ @dso_type=] dso_type]  
```  
  
## <a name="arguments"></a>自变量  
`[ @dsn = ] 'dsn'`ODBC DSN 或 OLE DB 链接服务器的名称。 *dsn*的值为**varchar （128）**，无默认值。  
  
`[ @infotype = ] 'info_type'`要返回的信息的类型。 如果未指定*info_type*或指定 NULL，则返回所有信息类型。 *info_type*为**varchar （128）**，默认值为 NULL，可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**DBMS_NAME**|指定数据源供应商名称。|  
|**DBMS_VERSION**|指定数据源版本。|  
|**DATABASE_NAME**|指定数据库名。|  
|**SQL_SUBSCRIBER**|指定数据源可以是订阅服务器。|  
  
`[ @login = ] 'login'`数据源的登录名。 如果数据源包括登录名，则指定 NULL 或忽略该参数。 *login*的值为**varchar （128）**，默认值为 NULL。  
  
`[ @password = ] 'password'`登录名的密码。 如果数据源包括登录名，则指定 NULL 或忽略该参数。 *password*的值为**varchar （128）**，默认值为 NULL。  
  
`[ @dso_type = ] dso_type`数据源类型。 *dso_type*为**int**，可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1** （默认值）|ODBC 数据源|  
|**3**|OLE DB 数据源|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**信息类型**|**nvarchar （64）**|信息类型，如 DBMS_NAME、DBMS_VERSION、DATABASE_NAME 和 SQL_SUBSCRIBER。|  
|**值**|**nvarchar(512)**|关联的信息类型的值。|  
  
## <a name="remarks"></a>备注  
 **sp_dsninfo**在所有类型的复制中使用。  
  
 **sp_dsninfo**检索 ODBC 或 OLE DB 数据源信息，该信息显示数据库是否可用于复制或查询。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员才能**sp_dsninfo**执行。  
  
## <a name="see-also"></a>另请参阅  
 [sp_enumdsn &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-enumdsn-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

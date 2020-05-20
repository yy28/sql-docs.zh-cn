---
title: sp_getsubscriptiondtspackagename （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_getsubscriptiondtspackagename
- sp_getsubscriptiondtspackagename_TSQL
helpviewer_keywords:
- sp_getsubscriptiondtspackagename
ms.assetid: 606c40aa-2593-43af-9762-0f260bbb51f2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 65f26504c37ac9845a454994ad60ae462759909b
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827736"
---
# <a name="sp_getsubscriptiondtspackagename-transact-sql"></a>sp_getsubscriptiondtspackagename (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在将数据发送到订阅服务器之前，返回用于转换数据的 Data Transformation Services (DTS) 包名称。 此存储过程在发布服务器的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_getsubscriptiondtspackagename [ @publication = ] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'`发布的名称。 **"***发布***"** 的值为**sysname**，无默认值。  
  
`[ @subscriber = ] 'subscriber'`订阅服务器的名称。 *订阅服务器*的值为 sysname，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**new_package_name**|**sysname**|DTS 包的名称。|  
  
## <a name="remarks"></a>备注  
 **sp_getsubscriptiondtspackagename**用于快照复制和事务复制。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_getsubscriptiondtspackagename**。  
  
  

---
title: "dbo.sysproxylogin (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.sysproxylogin_TSQL
- sysproxylogin_TSQL
- dbo.sysproxylogin
- sysproxylogin
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxylogin system table
ms.assetid: 433d33cb-bdf2-47bb-af78-2a40b7c8dfce
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6235a99d6fa67fb00a84dbab315bd4f2355e37bc
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="dbosysproxylogin-transact-sql"></a>dbo.sysproxylogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  记录与各个 SQL Server 代理的代理帐户关联的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 此表存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的代理帐户的 ID。 此值对应于**proxy_id**中的列**sysproxies**表。|  
|**sid**|**varbinary(85)**|Microsoft Windows *security_identifier*为 SQL Server 登录名。|  
|**principal_id**|**int**|指定用户或组的 ID，此用户或组具有将代理帐户用于指定子系统步骤的权限。|  
|**flags**|**int**|登录类型：<br /><br /> **0** = Windows 用户或组，和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名。<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]固定的系统角色<br /><br /> **2** = **msdb**数据库角色|  
  
## <a name="remarks"></a>注释  
 只有的成员**sysadmin**固定的服务器角色可以访问此表。  
  
## <a name="see-also"></a>另请参阅  
 [dbo.sysproxies &#40;Transact SQL &#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)  
  
  

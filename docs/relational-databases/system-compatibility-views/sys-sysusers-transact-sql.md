---
title: sys.sysusers (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sysusers
- sys.sysusers_TSQL
- sysusers_TSQL
- sysusers
dev_langs:
- TSQL
helpviewer_keywords:
- sysusers system table
- sys.sysusers compatibility view
ms.assetid: 5f0e6a8d-c983-44f6-97e9-aab5bff67d18
caps.latest.revision: 36
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2450923afb141599da29d9c17cda7528e7b07111
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="syssysusers-transact-sql"></a>sys.sysusers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  包含一个行，每个[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 用户、 Windows 组、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用户，或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库中的角色。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**uid**|**int**|用户 ID，在此数据库中是唯一的。<br /><br /> 1 = 数据库所有者<br /><br /> 如果用户数和角色数超过 32,767，则发生溢出或返回 NULL。|  
|**status**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**名称**|**sysname**|用户名或组名，在此数据库中是唯一的。|  
|**sid**|**varbinary(85)**|此项的安全性标识符。|  
|**角色**|**varbinary(2048)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**createdate**|**datetime**|帐户的添加日期。|  
|**updatedate**|**datetime**|帐户的上次更改日期。|  
|**altuid**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 如果用户数和角色数超过 32,767，则发生溢出或返回 NULL。|  
|**password**|**varbinary(256)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**gid**|**int**|此用户所属的组 ID。 如果**uid**相同**gid**，此项定义一组。 如果组和用户的总数超过 32,767，则发生溢出或返回 NULL。|  
|**environ**|**varchar(255)**|保留。|  
|**hasdbaccess**|**int**|1 = 帐户具有数据库访问权。|  
|**islogin**|**int**|1 = 帐户是具有登录帐户的 Windows 组、Windows 用户或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户。|  
|**isntname**|**int**|1 = 帐户是 Windows 组或 Windows 用户。|  
|**isntgroup**|**int**|1 = 帐户是 Windows 组。|  
|**isntuser**|**int**|1 = 帐户是 Windows 用户。|  
|**issqluser**|**int**|1 = 帐户是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户。|  
|**isaliased**|**int**|1 = 帐户化名为另一个用户。|  
|**issqlrole**|**int**|1 = 帐户是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色。|  
|**isapprole**|**int**|1 = 帐户是应用程序角色。|  
  
## <a name="see-also"></a>另请参阅  
 [将系统表映射到系统视图&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [兼容性视图 (Transact SQL)](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  

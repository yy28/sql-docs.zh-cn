---
title: "catalog.update_master_address（SSISDB 数据库）| Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 52aef94f67ef1697731a1844f44f83ddaf0c4ccc
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="catalogupdatemasteraddress-ssisdb-database"></a>catalog.update_master_address（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

更新 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Master 终结点。

## <a name="syntax"></a>语法

```sql
catalog.update_master_address [@MasterAddress = ] masterAddress
```

## <a name="arguments"></a>参数
[ @MasterAddress = ] masterAddress  
Scale Out Master 终结点。 masterAddress 为 nvarchar。  

 ## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  

## <a name="permissions"></a>权限  
 此存储过程需要下列权限之一：  
   
-   ssis_admin 数据库角色的成员资格  
  
-   sysadmin 服务器角色的成员资格  
 

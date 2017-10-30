---
title: "catalog.update_master_address （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e5e560d6011370b3d56ba13c86608d2be3d0dc6e
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="catalogupdatemasteraddress-ssisdb-database"></a>catalog.update_master_address （SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

更新[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]缩放出主终结点。

## <a name="syntax"></a>语法

```sql
catalog.update_master_address [@MasterAddress = ] masterAddress
```

## <a name="arguments"></a>参数
[ @MasterAddress =] *masterAddress*  
缩放出主终结点。 *MasterAddress*是**nvarchar**。  

 ## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  

## <a name="permissions"></a>权限  
 此存储过程需要下列权限之一：  
   
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
 


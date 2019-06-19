---
title: catalog.update_master_address（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
author: haoqian
ms.author: haoqian
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: b120ee8d8744214119df9442a4901a5cf9295b13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65715689"
---
# <a name="catalogupdatemasteraddress-ssisdb-database"></a>catalog.update_master_address（SSISDB 数据库）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

更新 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Master 终结点。

## <a name="syntax"></a>语法

```sql
catalog.update_master_address [@MasterAddress = ] masterAddress
```

## <a name="arguments"></a>参数
[ @MasterAddress = ] masterAddress   
Scale Out Master 终结点。 masterAddress  为 nvarchar  。  

 ## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 None  

## <a name="permissions"></a>权限  
 此存储过程需要下列权限之一：  
   
-   **ssis_admin** 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格  
 

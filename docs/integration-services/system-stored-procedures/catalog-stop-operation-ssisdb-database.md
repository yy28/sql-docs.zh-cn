---
title: catalog.stop_operation（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 97fd9d22-03dd-4eda-8f6c-ba8b67acec68
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f7427a85fa3e8b6f65bb899d008a13f48008e4c0
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65715794"
---
# <a name="catalogstopoperation-ssisdb-database"></a>catalog.stop_operation（SSISDB 数据库）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中停止执行的验证或实例。  
  
## <a name="syntax"></a>语法  
  
```sql  
catalog.stop_operation [ @operation_id = ] operation_id  
```  
  
## <a name="arguments"></a>参数  
 [ @operation_id = ] operation_id  
 执行验证或实例的唯一标识符。 operation_id 为 bigint。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="permissions"></a>权限  
 此存储过程需要下列权限之一：  
  
-   针对执行验证或实例的 READ 和 MODIFY 权限  
  
-   **ssis_admin** 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
  
-   用户没有相应的权限  
  
-   操作标识符无效  
  
-   操作已停止  
  
## <a name="remarks"></a>Remarks  
 一次只能有一个用户应停止 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录的操作。 如果多个用户试图停止操作，则存储过程在第一次尝试时将返回成功（值 `0`），但后续尝试将引发错误。  
  
  

---
title: "catalog.stop_operation （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 97fd9d22-03dd-4eda-8f6c-ba8b67acec68
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 76a41be8ac6066a4f163b5049a758302d43d5219
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogstopoperation-ssisdb-database"></a>catalog.stop_operation（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中停止执行的验证或实例。  
  
## <a name="syntax"></a>语法  
  
```tsql  
stop_operation [ @operation_id = ] operation_id  
```  
  
## <a name="arguments"></a>参数  
 [ @operation_id =] *operation_id*  
 执行验证或实例的唯一标识符。 *Operation_id*是**bigint**。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   针对执行验证或实例的 READ 和 MODIFY 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
  
-   用户没有适当的权限  
  
-   操作标识符无效  
  
-   操作已停止  
  
## <a name="remarks"></a>注释  
 一次只能有一个用户应停止 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录的操作。 如果多个用户试图停止操作，则存储过程在第一次尝试时将返回成功（值 `0`），但后续尝试将引发错误。  
  
  

---
title: "catalog.set_worker_agent_property （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ddd2a534-6925-4d66-90e7-541c14f41de7
caps.latest.revision: 2
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: d0476bbb67cff44a05aed1441a31d679882b4cb3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/08/2017

---
# <a name="catalogsetworkeragentproperty-ssisdb-database"></a>catalog.set_worker_agent_property （SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

设置的属性[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]横向扩展辅助进程。

## <a name="syntax"></a>语法

```tsql
set_worker_agent_property [ @WorkerAgentId = ] WorkerAgentId, [ @PropertyName = ] PropertyName, [ @PropertyValue = ] PropertyValue 
```

## <a name="arguments"></a>参数
[ @WorkerAgentId =] *WorkerAgentId*  
辅助代理的横向扩展辅助进程的 id。 *WorkerAgentId*是**uniqueidentifier**。

[ @PropertyName =] *PropertyName*  
属性的名称。 *PropertyName*是**nvarchar(256)**。

[ @PropertyValue =] *PropertyValue*  
属性的值。 *PropertyValue*是**nvarchar (max)**。

## <a name="remarks"></a>注释
有效的属性名称为**DisplayName**，**说明**，**标记**。

## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 无  

## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色

## <a name="erros-and-warnings"></a>错误和警告
  下面的列表描述了一些可能引发错误或警告的情况：  
  
-   用户没有适当的权限 

-   辅助代理 id 不是有效的。

-   属性名称无效。

-   属性值不是 vilid。  

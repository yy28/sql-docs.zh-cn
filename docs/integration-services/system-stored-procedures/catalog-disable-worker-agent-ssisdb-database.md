---
title: "catalog.disable_worker_agent （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f19dc4c-a000-4318-8fe1-e80d56720e66
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 8f4a8cd24278742ffb13d16791ce5f1f3a95f301
ms.contentlocale: zh-cn
ms.lasthandoff: 10/20/2017

---
# <a name="catalogdisableworkeragent-ssisdb-database"></a>catalog.disable_worker_agent （SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

禁用与此工作 Master 出缩放的横向扩展辅助进程[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]目录。

## <a name="syntax"></a>语法

```sql
catalog.disable_worker_agent [@WorkerAgentId =] WorkerAgentId
```
## <a name="arguments"></a>参数
[@WorkerAgentId =] *WorkerAgentId*辅助代理 ID 的横向扩展辅助。 *WorkerAgentId*是**uniqueidentifier**。

## <a name="example"></a>示例
此示例将禁用缩放出工作线程上可用。

```sql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    MachineA    --

EXEC [catalog].[disable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```

## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 无  

## <a name="permissions"></a>Permissions  
 此存储过程需要下列权限之一：  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色 

## <a name="errors-and-warnings"></a>错误和警告
如果辅助角色的代理 ID 不是有效的则存储的过程将返回错误。


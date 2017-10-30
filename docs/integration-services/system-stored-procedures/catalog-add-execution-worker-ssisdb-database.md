---
title: "catalog.add_execution_worker （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d587cedd-6402-4d5c-9526-7cd25627a037
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8ce83f2678a1f3dcae6539f33beb33070b8e771b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="catalogaddexecutionworker-ssisdb-database"></a>catalog.add_execution_worker （SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

将添加[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]缩放出辅助到向外扩展中执行的实例。

## <a name="syntax"></a>語法

```sql
catalog.add_execution_worker [@execution_id = ] execution_id, [@workeragent_id = ] workeragent_id
```

## <a name="arguments"></a>参数
[ @execution_id =] *execution_id*  
 执行实例的唯一标识符。 *Execution_id*是**bigint**。  
 
[@workeragent_id =] *workeragent_id*  
横向扩展辅助进程工作代理 id。 *Workeragent_id*是**uniqueIdentifier**。

## <a name="return-code-value"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  

## <a name="permissions"></a>权限  
 此存储过程需要下列权限之一：  
  
-   针对执行实例的 READ 和 MODIFY 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
 
## <a name="errors-and-warnings"></a>错误和警告  
 下面的列表描述了一些可能引发错误或警告的情况：  
 
- 用户不具备适当的权限。

- 执行标识符不是有效的。

- 辅助代理 id 不是有效的。

- 执行不在向外扩展。

## <a name="see-also"></a>另请参阅
[在向外扩展中执行包](~/integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md)。



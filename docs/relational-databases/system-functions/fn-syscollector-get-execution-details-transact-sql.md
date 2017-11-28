---
title: "fn_syscollector_get_execution_details (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_syscollector_get_execution_details_TSQL
- fn_syscollector_get_execution_details
dev_langs: TSQL
helpviewer_keywords: fn_syscollector_get_execution_details function
ms.assetid: d59ddf0c-72c0-4c57-bc83-aef260e4e105
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bd44ed098f4dbf15e529df6cbe4026d065dfa2a5
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="fnsyscollectorgetexecutiondetails-transact-sql"></a>fn_syscollector_get_execution_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回与给定包的 package_execution_id 相匹配的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 日志 (sysssislog) 部分。 由包或其任务和容器在运行时生成的每个日志记录项在表中各占一行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
fn_syscollector_get_execution_details ( log_id )  
```  
  
## <a name="arguments"></a>参数  
 *log_id*  
 执行日志的本地唯一标识符。 *log_id*是**int**。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|id|**int**|日志记录项的唯一标识符。|  
|事件|**sysname**|生成日志记录项的事件的名称。|  
|computer|**nvarchar**|生成日志记录条目时运行包的计算机。|  
|运算符后的表达式|**nvarchar**|运行生成日志记录项的包的人员或代理的用户名。|  
|源 (source)|**nvarchar**|生成日志记录项的可执行文件的名称。|  
|sourceid|**uniqueidentifier**|生成日志记录项的可执行文件的 GUID。|  
|executionid|**uniqueidentifier**|生成日志记录条目的可执行文件的执行实例的 GUID。|  
|starttime|**datetime**|包开始运行时间。|  
|endtime|**datetime**|包完成的时间。|  
|datacode|**int**|用于标识与日志项关联的事件的整数值。 “0”指示事件未提供标识符。|  
|databytes|**image**|用于标识返回值的字节数组。|  
|message|**nvarchar**|事件以及与事件关联的信息的说明。|  
  
## <a name="permissions"></a>Permissions  
 需要选择权限**dc_operator**。  
  
## <a name="see-also"></a>另请参阅  
 [启用包日志记录在 SQL Server 数据工具](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)   
 [数据收集](../../relational-databases/data-collection/data-collection.md)  
  
  

---
title: sys.dm_external_script_requests | Microsoft Docs
ms.custom: ''
ms.date: 06/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_external_script_requests
- sys.dm_external_script_requests_TSQL
- dm_external_script_requests
- dm_external_script_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_external_script_requests dynamic management view
ms.assetid: e7e7c50f-b8b2-403c-b8c8-1955da5636c3
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6b73281b970940caced870dbf75c78946f9f559b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmexternalscriptrequests"></a>sys.dm_external_script_requests
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

为运行外部脚本的每个活动工作线程帐户都返回一行。
 
  
> [!NOTE] 
>  
>  只有在已安装并启用支持外部脚本执行的功能的情况下，此 DMV 才可用。 有关如何为 R 脚本执行此操作的信息，请参阅[设置 SQL Server R services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|external_script_request_id|**唯一标识符**|发送外部脚本请求的进程的 ID。 由于由接收的这对应于的进程 ID [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]|  
|language|**nvarchar**|表示支持的脚本语言的关键字。 当前仅支持 `R` 。|  
|degree_of_parallelism|**int**|数字，指示已创建的并行进程数。 此值可能与请求的并行进程数不同。|  
|external_user_name|**nvarchar**|在其下执行脚本的 Windows 工作线程帐户。|  
  
## <a name="permissions"></a>权限  
 需要针对服务器的 VIEW SERVER STATE 权限。  
  
> [!NOTE]
>   
>  运行外部脚本的用户必须具有额外权限 EXECUTE ANY EXTERNAL SCRIPT，但是，此 DMV 可由没有此权限的管理员使用。 
  
## <a name="remarks"></a>注释  

此视图可以使用脚本语言标识符进行筛选。

此视图还返回在其下运行脚本的工作线程帐户。 有关 R 脚本使用的工作线程帐户的信息，请参阅[修改 R 服务的用户帐户池](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)。

在 **external_script_request_id** 字段中返回的 GUID 还表示用于存储临时文件的受保护目录的文件名。 每个工作线程帐户（如 MSSQLSERVER01）都表示单个 SQL 登录名或 Windows 用户，可以用于运行多个脚本请求。 默认情况下，这些临时文件会在请求脚本完成之后进行清理。 如果需要在一段时期内保留这些文件以便进行调试，则可以按照本主题中所述来更改清理标志：[配置和管理高级分析扩展](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md)。  
 
此 DMV 仅监视活动进程，不能报告已完成的脚本。 如果需要跟踪脚本的持续时间，我们建议将计时信息添加到脚本并在脚本执行过程中进行捕获。


## <a name="examples"></a>示例  
  
### <a name="viewing-the-currently-active-r-scripts-for-a-particular-process"></a>查看特定进程的当前活动 R 脚本 
 下面的示例显示在当前实例上运行的外部脚本执行数。  
  
```  
SELECT external_script_request_id 
  , [language]
  , degree_of_parallelism
  , external_user_name
FROM sys.dm_external_script_requests; 
```  

结果  


external_script_request_id  |language  |degree_of_parallelism  |external_user_name  
---------|---------|---------|---------
183EE6FC-7399-4318-AA2E-7A6C68E435A8     |     R    |      1   |  MSSQLSERVER01       


  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [执行相关的动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)
[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
  


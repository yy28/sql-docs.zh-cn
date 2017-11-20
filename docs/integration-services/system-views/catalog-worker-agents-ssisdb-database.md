---
title: "catalog.worker_agents （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0bd0d827-e2f1-44fe-aa90-6bf922d68d16
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: d56af0ab150255c53746898a638a32112938755c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/08/2017

---
# <a name="catalogworkeragents-ssisdb-database"></a>catalog.worker_agents （SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

显示的信息[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]横向扩展辅助进程。

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|WorkerAgentId|**uniqueidentifier**|辅助代理 ID 的横向扩展辅助中。|
|IsEnabled|**bit**|是否启用缩放出工作线程。|
|DisplayName|**nvarchar(256)**|横向扩展辅助进程的显示名称。|
|Description|**nvarchar(256)**|横向扩展辅助进程的说明。|
|MachineName|**nvarchar(256)**|横向扩展辅助进程的计算机名称。|
|Tags|**nvarchar(max)**|横向扩展辅助进程的标记。|
|用户帐户|**nvarchar(256)**|运行了缩放出 Worker 服务的用户帐户。|
|LastOnlineTime|**datetimeoffset(7)**|上次缩放出工作线程处于联机状态的时间。|

## <a name="remarks"></a>注释
此视图显示每个横向扩展辅助角色连接到使用 SSISDB 目录出 Master 缩放行。

## <a name="permissions"></a>Permissions
此视图需要下列权限之一：

- 成员资格**ssis_admin**数据库角色

- 成员资格**ssis_cluster_executor**数据库角色

- 成员资格**sysadmin**服务器角色


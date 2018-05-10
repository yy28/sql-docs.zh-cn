---
title: catalog.worker_agents（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0bd0d827-e2f1-44fe-aa90-6bf922d68d16
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ce474c525f6819c3c70747b56fc2fbd7d1588737
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="catalogworkeragents-ssisdb-database"></a>catalog.worker_agents（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker 的相关信息。

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|WorkerAgentId|**uniqueidentifier**|Scale Out Worker 的 Worker 代理 ID。|
|IsEnabled|**bit**|是否启用 Scale Out Worker。|
|DisplayName|**nvarchar(256)**|Scale Out Worker 的显示名称。|
|Description|**nvarchar(256)**|Scale Out Worker 的相关说明。|
|MachineName|**nvarchar(256)**|Scale Out Worker 的计算机名称。|
|Tags|**nvarchar(max)**|Scale Out Worker 的标记。|
|UserAccount|**nvarchar(256)**|运行 Scale Out Worker 服务的用户帐户。|
|LastOnlineTime|**datetimeoffset(7)**|Scale Out Worker 上次联机的时间。|

## <a name="remarks"></a>Remarks
此视图对于使用 SSISDB 目录连接到 Scale Out Master 的每个 Scale Out Worker 显示一行。

## <a name="permissions"></a>权限
此视图需要下列权限之一：

- ssis_admin 数据库角色的成员资格

- **ssis_cluster_executor** 数据库角色的成员资格

- sysadmin 服务器角色的成员资格

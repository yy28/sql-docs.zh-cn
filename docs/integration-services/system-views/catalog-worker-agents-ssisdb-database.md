---
title: catalog.worker_agents（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0bd0d827-e2f1-44fe-aa90-6bf922d68d16
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f2678853d13436811b53b40473a04191625535db
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "71295135"
---
# <a name="catalogworker_agents-ssisdb-database"></a>catalog.worker_agents（SSISDB 数据库）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker 的相关信息。

|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|WorkerAgentId|**uniqueidentifier**|Scale Out Worker 的 Worker 代理 ID。|
|IsEnabled|**bit**|是否启用 Scale Out Worker。|
|DisplayName|**nvarchar(256)**|Scale Out Worker 的显示名称。|
|说明|**nvarchar(256)**|Scale Out Worker 的相关说明。|
|MachineName|**nvarchar(256)**|Scale Out Worker 的计算机名称。|
|Tags|**nvarchar(max)**|Scale Out Worker 的标记。|
|UserAccount|**nvarchar(256)**|运行 Scale Out Worker 服务的用户帐户。|
|LastOnlineTime|**datetimeoffset(7)**|Scale Out Worker 上次联机的时间。|

## <a name="remarks"></a>备注
此视图对于使用 SSISDB 目录连接到 Scale Out Master 的每个 Scale Out Worker 显示一行。

## <a name="permissions"></a>权限
此视图需要下列权限之一：

- **ssis_admin** 数据库角色的成员资格

- **ssis_cluster_executor** 数据库角色的成员资格

- **sysadmin** 服务器角色的成员资格

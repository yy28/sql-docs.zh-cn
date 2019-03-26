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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4102d6139594bb0fd8aa36ea6b038ae897213634
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58272340"
---
# <a name="catalogworkeragents-ssisdb-database"></a>catalog.worker_agents（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

显示 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker 的相关信息。

|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|WorkerAgentId|**uniqueidentifier**|Scale Out Worker 的 Worker 代理 ID。|
|IsEnabled|**bit**|是否启用 Scale Out Worker。|
|DisplayName|**nvarchar(256)**|Scale Out Worker 的显示名称。|
|描述|**nvarchar(256)**|Scale Out Worker 的相关说明。|
|MachineName|**nvarchar(256)**|Scale Out Worker 的计算机名称。|
|Tags|**nvarchar(max)**|Scale Out Worker 的标记。|
|UserAccount|**nvarchar(256)**|运行 Scale Out Worker 服务的用户帐户。|
|LastOnlineTime|**datetimeoffset(7)**|Scale Out Worker 上次联机的时间。|

## <a name="remarks"></a>Remarks
此视图对于使用 SSISDB 目录连接到 Scale Out Master 的每个 Scale Out Worker 显示一行。

## <a name="permissions"></a>权限
此视图需要下列权限之一：

- **ssis_admin** 数据库角色的成员资格

- **ssis_cluster_executor** 数据库角色的成员资格

- **sysadmin** 服务器角色的成员资格

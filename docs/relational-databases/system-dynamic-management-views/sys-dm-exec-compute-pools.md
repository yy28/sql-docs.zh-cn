---
title: sys.databases _dm_compute_pools （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, big-data-clusters
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_dm_compute_pools
- dm_dm_compute_pools_TSQL
- dm_dm_compute_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_dm_compute_pools dynamic management view
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 0b21f517b540c69822dd8b1da4aa6a4cf8b8616f
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532963"
---
# <a name="sysdm_dm_compute_pools-transact-sql"></a>sys.databases _dm_compute_pools （Transact-sql）
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|name|`sysname`|计算池的名称。 不可为 null。 返回默认计算池 `default`。 |
|compute_pool_id|`int`|池的唯一标识符。 此视图的键。|  
|位置|`sysname`|SQL 大数据群集中的控制器的终结点。 不可为 null。 |

## <a name="permissions"></a>权限

在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上，需要 `VIEW SERVER STATE` 权限。

## <a name="see-also"></a>另请参阅

[什么是 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)]](../../big-data-cluster/big-data-cluster-overview.md)？

---
title: sys. dm_cluster_endpoints （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, big-data-clusters
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_cluster_endpoints
- dm_cluster_endpoints_TSQL
- dm_cluster_endpoints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cluster_endpoints dynamic management view
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: b6ec5de74d2da2a94c25ef121abc0157348554d5
ms.sourcegitcommit: ef830f565ee07dc7d4388925cc3c86c5d2cfb4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2019
ms.locfileid: "74947059"
---
# <a name="sysdm_cluster_endpoints-transact-sql"></a>sys. dm_cluster_endpoints （Transact-sql）
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|name|`sysname`|在 SQL 大数据群集中外部公开的服务的名称。 终结点的唯一标识符。 此视图的键。 不可为 null。 |  
|description|`nvarchar(4000)`|服务说明。 不可为 null。 |
|endpoint|`sysname`|终结点 url 或连接属性。 不可为 null。 |
|protocol_desc|`sysname`|终结点协议说明 |

## <a name="permissions"></a>权限

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上， `VIEW SERVER STATE`需要权限。

## <a name="see-also"></a>另请参阅

[什么是[!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)] ](../../big-data-cluster/big-data-cluster-overview.md)？

---
title: LOCALDB_ERROR_INSTANCE_BUSY |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: 0ed9d0f8-3297-4e31-a3e9-4a827f381789
author: stevestein
ms.author: sstein
ms.openlocfilehash: e8f5eb6960a38b9aefc211530a1c29c0ccf8ae69
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246084"
---
# <a name="localdb_error_instance_busy"></a>LOCALDB_ERROR_INSTANCE_BUSY
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>详细信息  
  
| Attribute | 值 |
| --------- | ----- |
|产品名称|SQL Server|  
|事件 ID|274|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|无法执行本地数据库实例上请求的操作，因为指定的实例已被使用。 请停止该实例后重试。|  
  
## <a name="explanation"></a>说明  
 指定的实例正在运行。  
  
## <a name="user-action"></a>用户操作  
 停止指定的本地数据库运行时实例并重试。  
  
  

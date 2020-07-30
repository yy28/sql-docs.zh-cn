---
title: LOCALDB_ERROR_WAIT_TIMEOUT |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: e5b55efa-daa1-4c39-aa71-eeb7707ed601
author: stevestein
ms.author: sstein
ms.openlocfilehash: 49a7b10aa85d6a1cf3393a02904fdc346cfccd6a
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242537"
---
# <a name="localdb_error_wait_timeout"></a>LOCALDB_ERROR_WAIT_TIMEOUT
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>详细信息  
  
| Attribute | 值 |
| --------- | ----- |
|产品名称|SQL Server|  
|事件 ID|277|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|本地数据库实例 API 方法内发生超时。|  
  
## <a name="explanation"></a>说明  
 试图获取同步锁定时发生超时。  
  
## <a name="user-action"></a>用户操作  
 再次重试请求的操作。  
  
  

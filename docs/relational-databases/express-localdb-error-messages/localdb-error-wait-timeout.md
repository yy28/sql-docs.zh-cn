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
ms.openlocfilehash: 64a58f3a42464d38254c577b2ad0753621026154
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85641040"
---
# <a name="localdb_error_wait_timeout"></a>LOCALDB_ERROR_WAIT_TIMEOUT
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|277|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|本地数据库实例 API 方法内发生超时。|  
  
## <a name="explanation"></a>说明  
 试图获取同步锁定时发生超时。  
  
## <a name="user-action"></a>用户操作  
 再次重试请求的操作。  
  
  

---
title: LOCALDB_ERROR_WAIT_TIMEOUT |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: e5b55efa-daa1-4c39-aa71-eeb7707ed601
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ce9a092056fe8b1fd83d2be97efd5b827269d619
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34326468"
---
# <a name="localdberrorwaittimeout"></a>LOCALDB_ERROR_WAIT_TIMEOUT
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|277|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|本地数据库实例 API 方法内发生超时。|  
  
## <a name="explanation"></a>解释  
 试图获取同步锁定时发生超时。  
  
## <a name="user-action"></a>用户操作  
 再次重试请求的操作。  
  
  

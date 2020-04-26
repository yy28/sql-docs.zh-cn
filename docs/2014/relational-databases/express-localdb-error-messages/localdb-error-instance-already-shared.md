---
title: LOCALDB_ERROR_INSTANCE_ALREADY_SHARED |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: 35b4d6fa-ebb9-49d3-aaab-d4e37b6f3760
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5f562a0cbd489202d5dbab7de6ac0d19ebeef348
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/25/2020
ms.locfileid: "62519364"
---
# <a name="localdb_error_instance_already_shared"></a>LOCALDB_ERROR_INSTANCE_ALREADY_SHARED
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|284|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|指定的本地数据库实例已经共享。|  
  
## <a name="explanation"></a>说明  
 已使用不同的共享名称共享指定的本地数据库实例。  
  
## <a name="user-action"></a>用户操作  
 在使用不同的共享名称再次共享此共享实例之前，先取消共享此实例。  
  
  

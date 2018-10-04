---
title: LOCALDB_ERROR_INSTANCE_ALREADY_SHARED |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: 35b4d6fa-ebb9-49d3-aaab-d4e37b6f3760
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2296d4327eaf1214ae6ee39b85a89b65b466a2c9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47597825"
---
# <a name="localdberrorinstancealreadyshared"></a>LOCALDB_ERROR_INSTANCE_ALREADY_SHARED
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|284|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|指定的本地数据库实例已经共享。|  
  
## <a name="explanation"></a>解释  
 已使用不同的共享名称共享指定的本地数据库实例。  
  
## <a name="user-action"></a>用户操作  
 在使用不同的共享名称再次共享此共享实例之前，先取消共享此实例。  
  
  

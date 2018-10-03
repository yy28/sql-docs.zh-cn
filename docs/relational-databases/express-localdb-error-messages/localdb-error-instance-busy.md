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
manager: craigg
ms.openlocfilehash: 8f8b0dbd388c6a96f9f515732a4ff4d49a56b749
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47697985"
---
# <a name="localdberrorinstancebusy"></a>LOCALDB_ERROR_INSTANCE_BUSY
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|274|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|无法执行本地数据库实例上请求的操作，因为指定的实例已被使用。 请停止该实例后重试。|  
  
## <a name="explanation"></a>解释  
 指定的实例正在运行。  
  
## <a name="user-action"></a>用户操作  
 停止指定的本地数据库运行时实例并重试。  
  
  

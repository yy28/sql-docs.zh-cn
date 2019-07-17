---
title: LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: fa082dca-bf88-46e7-b61e-7ac8835a3493
author: stevestein
ms.author: sstein
ms.openlocfilehash: 93d770fde71fe51b06bfe8fc95b87d023765eb5d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127032"
---
# <a name="localdberrorunknownlanguageid"></a>LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|270|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|获取本地化的错误消息时出错。 “语言 ID”参数指定的语言未知。|  
  
## <a name="explanation"></a>解释  
 本地数据库运行时错误消息的请求的语言未知或不受支持。  
  
## <a name="user-action"></a>用户操作  
 尝试请求本地数据库运行时错误消息的支持的语言之一，或尝试请求默认语言。  
  
  

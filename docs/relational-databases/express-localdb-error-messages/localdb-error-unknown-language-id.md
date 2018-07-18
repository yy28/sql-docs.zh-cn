---
title: LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: fa082dca-bf88-46e7-b61e-7ac8835a3493
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7233b624053c2c707e8576ccf4cb23edcec1baa8
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34326038"
---
# <a name="localdberrorunknownlanguageid"></a>LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>詳細資料  
  
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
  
  

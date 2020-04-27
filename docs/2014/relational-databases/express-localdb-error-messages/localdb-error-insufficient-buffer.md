---
title: LOCALDB_ERROR_INSUFFICIENT_BUFFER |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: ff67bda8-7e5c-4b06-8d7b-9985b6059a98
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b16cd79186357dafd07fa5f0f19dee05b03722f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62990441"
---
# <a name="localdb_error_insufficient_buffer"></a>LOCALDB_ERROR_INSUFFICIENT_BUFFER
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|276|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|传递给本地数据库实例 API 方法的缓冲区太小。|  
  
## <a name="explanation"></a>说明  
 输入的缓冲区太小，并且没有要求截断。  
  
## <a name="user-action"></a>用户操作  
 提供指定大小的缓冲区。  
  
  

---
title: LOCALDB_ERROR_INSUFFICIENT_BUFFER |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: ff67bda8-7e5c-4b06-8d7b-9985b6059a98
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 48ea53756395c717ec716e35787371ada260d894
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016844"
---
# <a name="localdberrorinsufficientbuffer"></a>LOCALDB_ERROR_INSUFFICIENT_BUFFER
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|276|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|传递给本地数据库实例 API 方法的缓冲区太小。|  
  
## <a name="explanation"></a>解释  
 输入的缓冲区太小，并且没有要求截断。  
  
## <a name="user-action"></a>用户操作  
 提供指定大小的缓冲区。  
  
  
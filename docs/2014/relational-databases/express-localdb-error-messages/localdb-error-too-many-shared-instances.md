---
title: LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: c1595263-6264-4a43-9535-5eb76ece3a57
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0896f3e70e6c65a1fcd0de4169249fb622e6b5f8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85051075"
---
# <a name="localdb_error_too_many_shared_instances"></a>LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|287|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|共享的实例太多，无法生成唯一的用户实例名。 请取消共享某些现有共享实例。|  
  
## <a name="explanation"></a>说明  
 共享的实例太多，无法生成唯一的用户实例名。  
  
## <a name="user-action"></a>用户操作  
 取消共享一个或多个共享的本地数据库运行时实例，然后重试。  
  
  

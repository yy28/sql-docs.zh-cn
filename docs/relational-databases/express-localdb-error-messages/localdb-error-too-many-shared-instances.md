---
title: "LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: c1595263-6264-4a43-9535-5eb76ece3a57
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 70f2450686f7e20bb2e1aef321dbf22f31cb6ba9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="localdberrortoomanysharedinstances"></a>LOCALDB_ERROR_TOO_MANY_SHARED_INSTANCES
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|287|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|共享的实例太多，无法生成唯一的用户实例名。 请取消共享某些现有共享实例。|  
  
## <a name="explanation"></a>解释  
 共享的实例太多，无法生成唯一的用户实例名。  
  
## <a name="user-action"></a>用户操作  
 取消共享一个或多个共享的本地数据库运行时实例，然后重试。  
  
  

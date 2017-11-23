---
title: "LOCALDB_ERROR_NOT_INSTALLED |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e7912885-1c14-409b-9022-83ad4c36f3bd
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b512d9a5f24d514f34080d3805a23f222061cd29
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="localdberrornotinstalled"></a>LOCALDB_ERROR_NOT_INSTALLED
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|278|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|注意： 消息文本为空，因为此消息意味着整个 LocalDB API （包括将 HRESULT 映射到消息文本的 FormatMessage 函数） 不可用。|  
  
## <a name="explanation"></a>解释  
 计算机上没有安装本地数据库运行时。  
  
## <a name="user-action"></a>用户操作  
 安装本地数据库运行时，然后重试操作。  
  
  

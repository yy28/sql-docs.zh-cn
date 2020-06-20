---
title: LOCALDB_ERROR_NOT_INSTALLED |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: e7912885-1c14-409b-9022-83ad4c36f3bd
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1c64dcfc42522b8252edb94237bd4acc7c246083
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85051122"
---
# <a name="localdb_error_not_installed"></a>LOCALDB_ERROR_NOT_INSTALLED
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|278|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|**注意：** 消息文本为空，因为此消息意味着整个 LocalDB API （包括将 HRESULT 映射到消息文本的 FormatMessage 函数）不可用。|  
  
## <a name="explanation"></a>说明  
 计算机上没有安装本地数据库运行时。  
  
## <a name="user-action"></a>用户操作  
 安装本地数据库运行时，然后重试操作。  
  
  

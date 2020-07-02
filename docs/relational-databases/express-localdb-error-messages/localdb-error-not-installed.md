---
title: LOCALDB_ERROR_NOT_INSTALLED |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: e7912885-1c14-409b-9022-83ad4c36f3bd
author: stevestein
ms.author: sstein
ms.openlocfilehash: fc83ba06b9cf5efdf90253a1987140ac9877d8a0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85641448"
---
# <a name="localdb_error_not_installed"></a>LOCALDB_ERROR_NOT_INSTALLED
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|278|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|注意：消息文本为空，因为此消息意味着整个 LocalDB API （包括将 HRESULT 映射到消息文本的 FormatMessage 函数）不可用。|  
  
## <a name="explanation"></a>说明  
 计算机上没有安装本地数据库运行时。  
  
## <a name="user-action"></a>用户操作  
 安装本地数据库运行时，然后重试操作。  
  
  

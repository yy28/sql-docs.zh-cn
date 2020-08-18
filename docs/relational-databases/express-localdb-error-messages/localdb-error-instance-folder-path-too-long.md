---
description: LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG
title: LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: c178a308-8d99-47fc-8a49-5a480dc592f6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6d72cae123d37e561799285e4dbf7a21875fc5b9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88409513"
---
# <a name="localdb_error_instance_folder_path_too_long"></a>LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>详细信息  
  
| Attribute | 值 |
| --------- | ----- | 
|产品名称|SQL Server|  
|事件 ID|260|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|本地数据库实例文件夹的完整路径长度大于 MAX_PATH。 此实例必须存储在以下文件夹中：%% LOCALAPPDATA%% \ Microsoft\Microsoft SQL Server 本地 DB\Instances \\<实例名称 \> 。|  
  
## <a name="explanation"></a>说明  
 应在其中存储该实例的路径的长度超过 MAX_PATH。  
  
## <a name="user-action"></a>用户操作  
 创建长度小于 MAX_PATH 的新路径。  
  
  

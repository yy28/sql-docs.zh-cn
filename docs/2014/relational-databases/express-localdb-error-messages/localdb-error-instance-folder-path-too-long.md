---
title: LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: c178a308-8d99-47fc-8a49-5a480dc592f6
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 96b4deb3bf0c7d660779781f9d76aac785ca12ca
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37415126"
---
# <a name="localdberrorinstancefolderpathtoolong"></a>LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|260|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|本地数据库实例文件夹的完整路径长度大于 MAX_PATH。 该实例必须存储在文件夹： %%LOCALAPPDATA%%\Microsoft\Microsoft SQL Server 本地 DB\Instances\\< 实例名称\>。|  
  
## <a name="explanation"></a>解释  
 应在其中存储该实例的路径的长度超过 MAX_PATH。  
  
## <a name="user-action"></a>用户操作  
 创建长度小于 MAX_PATH 的新路径。  
  
  

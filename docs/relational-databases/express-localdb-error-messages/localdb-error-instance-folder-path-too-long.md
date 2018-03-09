---
title: LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: c178a308-8d99-47fc-8a49-5a480dc592f6
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 53a553f454b89133b083c03fa492effd8ec12e97
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2018
---
# <a name="localdberrorinstancefolderpathtoolong"></a>LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件識別碼|260|  
|事件來源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|訊息文字|本地数据库实例文件夹的完整路径长度大于 MAX_PATH。 实例必须存储在文件夹中： %%LOCALAPPDATA%%\Microsoft\Microsoft SQL Server 本地 DB\Instances\\< 实例名称\>。|  
  
## <a name="explanation"></a>解释  
 应在其中存储该实例的路径的长度超过 MAX_PATH。  
  
## <a name="user-action"></a>使用者動作  
 创建长度小于 MAX_PATH 的新路径。  
  
  

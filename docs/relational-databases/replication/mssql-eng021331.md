---
title: MSSQL_ENG021331 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021331 error
ms.assetid: 9acd75d9-fda1-44cd-ba17-20295ad53ea0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: fb0b11b081140cc7c76036b5a1585dbeca0b852a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68027671"
---
# <a name="mssqleng021331"></a>MSSQL_ENG021331
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|21331|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|无法将用户脚本文件复制到分发服务器。(%ls)|  
  
## <a name="explanation"></a>解释  
 手动初始化订阅，而由复制生成或在复制命令中指定的脚本无法保存在指定目录中时，会发生此错误。 权限问题可导致此错误：在不使用快照的情况下初始化订阅时，在发布服务器上运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的帐户对分发服务器上的快照文件夹必须具有写权限。  
  
## <a name="user-action"></a>用户操作  
 请确保已为快照文件夹指定正确的路径，并且在发布服务器上运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的帐户具有足够的权限。  
  
## <a name="see-also"></a>另请参阅  
 [指定快照选项](../../relational-databases/replication/snapshot-options.md)   
 [错误和事件参考（复制）](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [初始化事务订阅（不使用快照）](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  

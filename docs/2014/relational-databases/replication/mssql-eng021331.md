---
title: MSSQL_ENG021331 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021331 error
ms.assetid: 9acd75d9-fda1-44cd-ba17-20295ad53ea0
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4bab3ee3277554b3e3846e95c17f44e1cc937a17
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37298077"
---
# <a name="mssqleng021331"></a>MSSQL_ENG021331
    
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
  
## <a name="see-also"></a>请参阅  
 [指定默认快照位置 (SQL Server Management Studio)](specify-the-default-snapshot-location-sql-server-management-studio.md)   
 [错误和事件参考（复制）](errors-and-events-reference-replication.md)   
 [初始化事务订阅（不使用快照）](initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  

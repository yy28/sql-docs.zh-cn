---
title: MSSQLSERVER_3437 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3437 (Database Engine error)
ms.assetid: b38216e2-b650-43bd-97af-061d54f60031
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 62fcf4360a9b5eefc971bf0f5443a9e9e96004aa
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3437"></a>MSSQLSERVER_3437
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|3437|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|NODTC|  
|消息正文|在恢复数据库 '%.*ls' 时出错。 无法连接到 Microsoft 分布式事务处理协调器 (MS DTC) 以检查事务 %S_XID 的完成状态。 请修复 MS DTC，然后再次运行恢复操作。|  
  
## <a name="explanation"></a>解释  
在数据库关闭时，使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分布式事务处理协调器 (MS DTC) 的一项或多项分布式事务尚未完成。 由于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不能连接到 MS DTC 以完成或回退事务，所以该数据库的恢复失败。  
  
## <a name="user-action"></a>用户操作  
若要恢复该数据库，必须首先解决 MS DTC 存在的问题。 若要调查 MS DTC 存在的问题，请检查 Windows 事件日志。 如果无法解决 MS DTC 问题和恢复数据库，请还原数据库备份。  
  


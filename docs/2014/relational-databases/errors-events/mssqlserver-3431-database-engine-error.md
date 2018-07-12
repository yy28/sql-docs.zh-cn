---
title: MSSQLSERVER_3431 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 3431 (Database Engine error)
ms.assetid: 9541217f-e5c6-4a12-a19a-006058f1d3f3
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 02724ea8bf358294af5e5dcd6c8f549d80010391
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37426456"
---
# <a name="mssqlserver3431"></a>MSSQLSERVER_3431
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|3431|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|UNRESOLVED_XACT|  
|消息正文|无法恢复数据库 '%.*ls' (数据库 ID 为 %d)，因为事务结果尚未解析。 Microsoft 分布式事务处理协调器 (MS DTC) 事务已准备好，但 MS DTC 无法确定解析方法。 若要进行解析，请修复 MS DTC，从完整备份进行还原，或者修复数据库。|  
  
## <a name="explanation"></a>解释  
 在数据库关闭时，使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分布式事务处理协调器 (MS DTC) 的一项或多项分布式事务尚未完成。 此数据库的恢复失败，因为没有来自 MS DTC 的详细信息，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法完成事务或回退事务。  
  
## <a name="user-action"></a>用户操作  
 若要恢复该数据库，必须首先解决 MS DTC 存在的问题。 若要调查 MS DTC 存在的问题，请检查 Windows 事件日志。 如果无法解决 MS DTC 问题和恢复数据库，请还原数据库备份。  
  
  

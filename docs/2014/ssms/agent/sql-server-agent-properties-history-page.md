---
title: SQL Server 代理属性（“历史记录”页）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.history.f1
ms.assetid: dc73734c-b3c3-407f-bbd1-8714b4fa47b0
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 46a62984a55b5141f66fb459b42274fe3ca94c1d
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43818183"
---
# <a name="sql-server-agent-properties-history-page"></a>SQL Server 代理属性（“历史记录”页）
  使用此页可以查看和修改用于管理 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务历史记录日志的设置。  
  
## <a name="options"></a>选项  
 **限制作业历史记录日志的大小**  
 对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理在日志中保留的作业历史记录信息量设置限制。  
  
 **作业历史记录日志的最大大小(行)**  
 设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理保留的最大行数。 如果日志包含的行数增大到此数值，则在输入新行时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理会删除日志中最早的行。  
  
 **每个作业的最大作业历史记录行数**  
 设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理为每个作业保留的最大行数。 如果特定作业历史记录包含的行数增大到此数值，则在输入新行时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理会删除日志中最早的行。  
  
 **删除代理历史记录**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理将删除在日志中保留的时间超过指定时间长度的项。 这是用来删除历史记录的一次性操作。 如果需要重复发生的作业，则创建并安排具有清除作业的维护计划。  
  
 **保留时间超过**  
 设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理将保留项多久。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 代理错误日志](sql-server-agent-error-log.md)  
  
  

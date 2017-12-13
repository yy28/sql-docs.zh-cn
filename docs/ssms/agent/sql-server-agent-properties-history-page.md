---
title: "SQL Server 代理属性（“历史记录”页）| Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.agent.history.f1
ms.assetid: dc73734c-b3c3-407f-bbd1-8714b4fa47b0
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 624f225d6ee4f8b00831f1ce0201538c5047e60e
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="sql-server-agent-properties-history-page"></a>SQL Server 代理属性（“历史记录”页）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 使用此页可以查看和修改用于管理 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理服务历史记录日志的设置。  
  
## <a name="options"></a>选项  
**限制作业历史记录日志的大小**  
对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理在日志中保留的作业历史记录信息量设置限制。  
  
**作业历史记录日志的最大大小(行)**  
设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理保留的最大行数。 如果日志包含的行数增大到此数值，则在输入新行时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理会删除日志中最早的行。  
  
**每个作业的最大作业历史记录行数**  
设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理为每个作业保留的最大行数。 如果特定作业历史记录包含的行数增大到此数值，则在输入新行时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理会删除日志中最早的行。  
  
**删除代理历史记录**  
指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理将删除在日志中保留的时间超过指定时间长度的项。 这是用来删除历史记录的一次性操作。 如果需要重复发生的作业，则创建并安排具有清除作业的维护计划。  
  
**保留时间超过**  
设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理将保留项多久。  
  
## <a name="see-also"></a>另请参阅  
[SQL Server 代理错误日志](../../ssms/agent/sql-server-agent-error-log.md)  
  

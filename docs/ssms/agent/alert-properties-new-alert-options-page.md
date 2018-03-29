---
title: 警报属性 - 新建警报（“选项”页）| Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ag.alert.options.f1
ms.assetid: 6e4f41aa-832d-46ba-b6b5-cf1d3b15d33f
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0f86a156d1e7f659e5460d92d80454eb34a4644a
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
---
# <a name="alert-properties---new-alert-options-page"></a>警报属性 - 新建警报（“选项”页）
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此页可以查看和修改 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理警报的选项。  

## <a name="options"></a>“常规”  
**电子邮件**  
在电子邮件通知中包括事件错误文本（如果有的话）。  
  
**寻呼程序**  
在寻呼程序通知中包括事件错误文本（如果有的话）。  
  
**Net send**  
在 net send 通知中包括事件错误文本（如果有的话）。  
  
**要发送的其他通知消息**  
键入要包括在通知消息中的任何其他文本。  
  
**两次响应之间的延迟时间**  
为重复发生的事件指定延迟时间。 某些事件可能会在短期内频繁发生。 在这种情况下，您可能需要知道事件已经发生，但不希望针对每一事件做出响应。 使用此选项可以指定超时时间。如果设定了延迟时间，在警报响应某个事件之后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理将等待指定的延迟时间，然后再响应，而不管在延迟时间内该事件发生与否。  
  
**Minutes**  
指定延迟时间（分钟）。 若要在每次发生事件时均予以响应，请指定 0 分和 0 秒。  
  
**Seconds**  
指定延迟时间（秒）。 若要在每次发生事件时均予以响应，请指定 0 分和 0 秒。  
  
## <a name="see-also"></a>另请参阅  
[警报](../../ssms/agent/alerts.md)  
  

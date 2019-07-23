---
title: SQL Server 代理属性（“高级”页）| Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.advanced.f1
ms.assetid: a4d798ee-4c18-40d4-b6af-63d17503738c
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a427b41e5f1269a4f59fd69257f54bdbd61a3050
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265366"
---
# <a name="sql-server-agent-properties-advanced-page"></a>SQL Server 代理属性（“高级”页）
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此页可以查看和修改 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务的高级属性。  
  
## <a name="options"></a>选项  
**SQL Server 事件转发**  
此类别中的选项可用来激活和配置事件转发功能。  
  
**将事件转发到其他服务器**  
将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理事件转发到其他服务器。  
  
**Server**  
选择要将事件转发到的服务器的名称。  
  
**未处理的事件**  
仅将未处理的事件转发到指定的服务器。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理仅转发警报未对其响应的事件。  
  
**所有事件**  
转发所有事件。 当本地实例中的某个警报响应该事件时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理将转发该事件并处理此警报。  
  
**如果事件的严重性不低于**  
仅转发严重级别不低于指定级别的事件。  
  
**空闲 CPU 条件**  
此类别中的选项定义一些条件，在这些条件下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理运行那些“空闲 CPU”计划安排的作业。  
  
**定义空闲 CPU 条件**  
定义 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理认为 CPU 处于空闲状态的条件。  
  
**CPU 平均使用率低于**  
CPU 平均使用率，在低于该使用率时，CPU 被认为处于空闲状态。  
  
**并且保持低于此级别**  
CPU 平均占用时间量必须低于指定的级别， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理才可按照“空闲 CPU”计划运行作业。  
  
## <a name="see-also"></a>另请参阅  
[创建计划并将计划附加到作业](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
[管理事件](../../ssms/agent/manage-events.md)  
  

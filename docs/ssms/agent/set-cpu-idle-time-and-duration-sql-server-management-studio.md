---
title: 设置 CPU 空闲时间和持续时间 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- CPU [SQL Server], idle conditions
- time [SQL Server], CPU idle and duration
- duration of CPU idle [SQL Server]
- SQL Server Agent, CPU idle conditions
- idle time [SQL Server]
ms.assetid: 8647b465-d899-4cc7-9640-134a506d0a2e
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 43ae32554b49df98f6e6ed4118b897e65d4f2246
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33041084"
---
# <a name="set-cpu-idle-time-and-duration-sql-server-management-studio"></a>设置 CPU 空闲时间和持续时间 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主题说明如何在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]定义服务器的 CPU 空闲条件。 CPU 空闲定义会影响 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理对事件的响应方式。 例如，假设将 CPU 空闲条件定义为 CPU 平均使用率低于 10% 并在此级别保持 10 分钟。 那么，如果将作业定义为在服务器 CPU 达到空闲条件时执行，则当 CPU 使用率低于 10% 并在该级别保持 10 分钟后，作业将开始执行。 如果作业对服务器的性能具有显著影响，如何定义 CPU 空闲条件将变得非常重要。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-set-cpu-idle-time-and-duration"></a>设置 CPU 空闲时间和持续时间  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的实例，然后展开该实例。  
  
2.  右键单击“SQL Server 代理”，再单击“属性”，然后选择“高级”页。  
  
3.  在 **“空闲 CPU 条件”** 下，执行下列操作：  
  
    -   选中 **“定义空闲 CPU 条件”**。  
  
    -   在“CPU 平均使用率低于”（对于所有 CPU 而言）框中指定百分比。 此选项设置 CPU 必须低于什么使用率级别才能变为空闲状态。  
  
    -   在 **“并且保持低于此级别”** 框中指定秒数。 此选项设置 CPU 最小使用率必须保持多长时间 CPU 才能变为空闲状态。  
  

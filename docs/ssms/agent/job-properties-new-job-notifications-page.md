---
title: 作业属性 - 新建作业（“通知”页）| Microsoft Docs
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
f1_keywords:
- sql13.ag.job.notifications.f1
ms.assetid: ed393cbd-4496-4399-a177-e5baa92fb689
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 110e9c0e597b9e9f482dc101bbb71d8cf93fceed
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="job-properties---new-job-notifications-page"></a>作业属性 - 新建作业（“通知”页）
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此页可以设置在作业完成时 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理要执行的操作。  
  
## <a name="options"></a>“常规”  
**电子邮件**  
选择此选项将在作业完成时发送电子邮件。 选择此选项后，选择要通知的操作员以及触发该通知的条件：“当作业成功时”；“当作业失败时”；或“当作业完成时”。  
  
**第**  
选择此选项将在作业完成时将电子邮件发送到操作员的寻呼程序。 选择此选项后，指定要通知的操作员以及触发该通知的条件：“当作业成功时”；“当作业失败时”；或“当作业完成时”。  
  
**Net send**  
选择此选项将在作业完成时通过 net send 通知操作员。 选择此选项后，指定要通知的操作员以及触发该通知的条件：“当作业成功时”；“当作业失败时”；或“当作业完成时”。  
  
**写入 Windows 应用程序事件日志**  
选择此选项将在作业完成时将条目写入到应用程序事件日志中。 选择此选项后，指定导致写入条目的条件：“当作业成功时”；“当作业失败时”；或“当作业完成时”。  
  
**自动删除作业**  
选择此选项将在作业完成时删除该作业。 选择此选项后，指定触发删除作业的条件：“当作业成功时”；“当作业失败时”；或“当作业完成时”。  
  
## <a name="see-also"></a>另请参阅  
[执行作业](../../ssms/agent/implement-jobs.md)  
[如何配置 SQL Server 代理邮件以使用数据库邮件 (SQL Server Management Studio)](http://msdn.microsoft.com/en-us/4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce)  
  

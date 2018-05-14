---
title: 设置作业执行关闭 (SQL Server Management Studio) | Microsoft Docs
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
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
- SQL Server Agent jobs, execution shutdowns
ms.assetid: ac23e88f-53fc-41de-bb16-0c27c002d5a5
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5b85b37b7bde8853528e5de026c565a2e36fbf24
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="set-job-execution-shutdown-sql-server-management-studio"></a>Set Job Execution Shutdown (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主题说明如何使用 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 中设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理自己结束之前，[!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 代理等待作业执行完的时间。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [Security](#Security)  
  
-   **若要设置 SQL Server 代理作业的关闭时间，可使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
默认情况下， **sysadmin** 固定服务器角色的成员可设置在 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 中设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理等待作业执行完的时间。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-set-job-execution-shutdown"></a>设置作业执行关闭  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开要设置作业执行关闭间隔的服务器。  
  
2.  右键单击“SQL Server 代理”，然后选择“属性”。  
  
3.  在 **“选择页”**下，选择 **“作业系统”**。  
  
4.  设置“关闭超时间隔(秒)”以延长或缩短关闭超时间隔。 这决定了在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理本身结束之前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理等待作业执行完成的时间长度。  
  

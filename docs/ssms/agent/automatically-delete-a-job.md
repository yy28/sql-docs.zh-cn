---
title: 自动删除作业 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- dropping jobs
- SQL Server Agent jobs, removing
- automatic job removal
- jobs [SQL Server Agent], deleting
- deleting jobs
- removing jobs
ms.assetid: 92dbb6da-5919-4bde-9354-d454e9ea3da0
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 376eed288247c15c4ca751fe42694cc243f1a73a
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67688858"
---
# <a name="automatically-delete-a-job"></a>Automatically Delete a Job
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主题说明如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 SQL Server 管理对象在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中将 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理配置为在作业成功、失败或完成时自动将其删除。  
  
作业响应可确保数据库管理员知道作业完成的时间和作业运行频率。 典型的作业响应包括：  
  
-   使用电子邮件、电子寻呼或 **net send** 消息通知操作员。  
  
    如果操作员必须执行后续操作，应使用其中的某种作业响应。 例如，当一个备份作业成功地完成之后，必须通知操作员取出备份磁带并将其存放在安全处。  
  
-   将事件消息写入 Windows 应用程序日志。  
  
    只能对失败的作业使用这种响应。  
  
-   自动删除作业。  
  
    如果确信不需要再次运行该作业，可以使用这种作业响应。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [安全性](#Security)  
  
-   **若要指定作业响应，可使用：**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [SQL Server 管理对象](#SMO)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Security"></a>安全性  
有关详细信息，请参阅[实现 SQL Server 代理安全性](../../ssms/agent/implement-sql-server-agent-security.md)。  
  
## <a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-automatically-delete-a-job"></a>自动删除作业  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的实例，然后展开该实例。  
  
2.  展开 **“SQL Server 代理”** ，展开 **“作业”** ，右键单击要编辑的作业，再单击 **“属性”** 。  
  
3.  选择 **“通知”** 页。  
  
4.  选中 **“自动删除作业”** ，并选择以下某项：  
  
    -   单击 **“当作业成功时”** 以在作业成功完成时删除作业状态。  
  
    -   单击 **“当作业失败时”** 以在作业失败时删除作业。  
  
    -   单击 **“当作业完成时”** 以删除作业，而不管完成状态如何。  
  
## <a name="SMO"></a>使用 SQL Server 管理对象  
**自动删除作业**  
  
通过使用所选的编程语言（如 Visual Basic、Visual C# 或 PowerShell）来使用 **Job** 类的 **DeleteLevel** 属性。 有关详细信息，请参阅 [SQL Server 管理对象 (SMO)](https://msdn.microsoft.com/library/ms162169.aspx)。  
  

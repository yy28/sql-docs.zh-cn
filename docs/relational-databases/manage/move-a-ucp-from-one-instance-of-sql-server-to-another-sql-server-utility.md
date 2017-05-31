---
title: "将 UCP 从 SQL Server 的一个实例移到另一个实例（SQL Server 实用工具）| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b402fd9e-0bea-4c38-a371-6ed7fea12e96
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5f8aaa0f8b094fe17f9cac1e88d5bffc75edb1ac
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="move-a-ucp-from-one-instance-of-sql-server-to-another-sql-server-utility"></a>将 UCP 从 SQL Server 的一个实例移到另一个实例（SQL Server 实用工具）
  本主题说明如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中将实用工具控制点 (UCP) 从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的一个实例移到另一个实例。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="move-a-ucp-from-one-instance-of-sql-server-to-another"></a>将 UCP 从 SQL Server 的一个实例移到另一个实例。  
  
1.  在将成为新 UCP 的新宿主实例的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上创建该新的 UCP。 有关详细信息，请参阅[创建 SQL Server 实用工具控制点（SQL Server 实用工具）](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)。  
  
2.  如果已经在您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的任何实例设置了非默认的策略设置，则记录策略阈值，以便您可以在新的 UCP 上重新创建它们。 在将实例添加到新的 UCP 时应用默认策略。 如果默认策略在起作用，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具列表视图将在 **“策略类型”** 列中显示 **“全局”** 。  
  
3.  从旧的 UCP 中删除所有托管实例。 有关详细信息，请参阅 [从 SQL Server 实用工具中删除 SQL Server 的实例](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md)。  
  
4.  从旧的 UCP 备份实用工具管理数据仓库 (UMDW)。 文件名是 Sysutility_mdw_\<GUID>_DATA，数据库默认位置是 \<System drive>:\Program Files\Microsoft SQL Server\MSSQL10_50.<UCP_Name>\MSSQL\Data\\，其中，\<System drive> 通常为 C:\ 驱动器。 有关详细信息，请参阅 [通过备份和还原来复制数据库](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)。  
  
5.  将 UMDW 的备份还原到新 UCP。 有关详细信息，请参阅 [通过备份和还原来复制数据库](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)。  
  
6.  将实例注册到新的 UCP 中，使它们由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具管理。 有关详细信息，请参阅 [注册 SQL Server 实例（SQL Server 实用工具）](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)的一个实例移到另一个实例。  
  
7.  根据需要，为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的托管实例实现自定义策略定义。  
  
8.  等待大约 1 小时，以便数据收集和聚合操作完成。  
  
9. 若要刷新数据，请在“实用工具资源管理器”中右键单击“托管实例”节点，然后选择“刷新”。 列表视图数据将显示在 **“实用工具资源管理器”** 内容窗格中。 有关详细信息，请参阅[查看资源运行状况策略结果（SQL Server 实用工具）](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 实用工具的功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [注册 SQL Server 实例（SQL Server 实用工具）](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)  
  
  

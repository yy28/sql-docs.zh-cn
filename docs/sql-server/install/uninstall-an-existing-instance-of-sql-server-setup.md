---
title: 卸载现有 SQL Server 实例（安装程序）| Microsoft Docs
ms.custom: ''
ms.date: 01/27/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- removing instances of SQL Server
- uninstalling instances of SQL Server
- removing SQL Server
- instances of SQL Server, uninstalling
- uninstalling SQL Server
ms.assetid: 3c64b29d-61d7-4b86-961c-0de62261c6a1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5bea9587b92e1452891e24475cc33a8baeec437b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38049115"
---
# <a name="uninstall-an-existing-instance-of-sql-server-setup"></a>卸载现有 SQL Server 实例（安装程序）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

 > 有关与以前版本的 SQL Server 相关的内容，请参阅[卸载现有 SQL Server 实例（安装程序）](https://msdn.microsoft.com/en-US/library/ms143412(SQL.120).aspx)。

  本文介绍如何卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的独立实例。 执行本文中提供的步骤，还可以准备系统以便重新安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
>**重要说明！** 若要卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例，您必须是拥有“作为服务登录”权限的本地管理员。  
  
> **注意：** 若要卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集，请使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序提供的删除节点功能分别删除每个节点。 有关详细信息，请参阅[在 SQL Server 故障转移群集中添加或删除节点（安装程序）](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
 卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，请注意以下重要方案：  
  
-   从内存大小为最小必需物理内存量的计算机中删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件前，请确保有足够大小的页文件。 页文件大小必须等于物理内存量的两倍。 虚拟内存不足会导致无法完全删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   如果有多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 将在删除 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的最后一个实例后自动卸载。  
  
     如果您要卸载 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的所有组件，则必须从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] “控制面板” **中的** “程序和功能” **手动卸载**Browser 组件。  
  
1.  卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会删除在安装过程期间添加的 tempdb 数据文件。 如果带有 tempdb_mssql_*.ndf 名称模式的文件存在于系统数据库目录中，它们会被删除。  
  
### <a name="before-you-uninstall"></a>卸载之前  
  
1.  **备份您的数据。** 尽管这不是必需的步骤，但您可能希望按照当前的状态保存数据库。 可能还希望保存对系统数据库所做的更改。 无论哪种情况，请确保先备份数据，再卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 或者，将所有数据和日志文件的副本保存在 MSSQL 文件夹以外的文件夹中。 卸载期间 MSSQL 文件夹将被删除。  
  
     必须保存的文件包括以下数据库文件：  
  
    -   Master.mdf  
  
    -   Mastlog.ldf  
  
    -   Model.mdf  
  
    -   Modellog.ldf  
  
    -   Msdbdata.mdf  
  
    -   Msdblog.ldf  
  
    -   Mssqlsystemresource.mdf  
  
    -   Mssqlsustemresource.ldf  
  
    -   Tempdb.mdf  
  
    -   Templog.ldf  
  
    -   ReportServer[$InstanceName] 这是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的默认数据库。  
  
    -   ReportServer[$InstanceName]TempDB 这是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的默认临时数据库。  
  
2.  **删除本地安全组。** 卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，应先删除用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件的本地安全组。  
  
3.  **停止所有的**  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **服务。** 建议先停止所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务，然后再卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件的本地安全组。 活动的连接可能会使卸载过程无法成功完成。  
  
4.  **使用具有适当权限的帐户。** 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户或具有同等权限的帐户登录到服务器。 例如，可以使用本地 Administrators 组的成员帐户登录到服务器。  
  
### <a name="to-uninstall-an-instance-of-includessnoversionincludesssnoversion-mdmd"></a>To Uninstall an Instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  若要开始卸载过程，请转到 **“控制面板”** ，然后选择 **“程序和功能”**。  
  
2.  右键单击“SQL Server 2016”，然后选择“卸载”。 然后单击 **“删除”**。 此时将启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导。  
  
     将运行安装程序支持规则以验证您的计算机配置。 若要继续，请单击 **“下一步”**。  
  
3.  在“选择实例”页上，使用下拉框指定要删除的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，或者指定与仅删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共享功能和管理工具相对应的选项。 若要继续，请单击 **“下一步”**。  
  
4.  在“选择功能”页上指定要从指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例中删除的功能。  
  
     将运行删除规则以验证是否可以成功完成删除操作。  
  
5.  在 **“准备删除”** 页上查看要卸载的组件和功能的列表。 单击 **“删除”** 开始卸载  
  
6.  在卸载最后一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例后，与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 关联的其他程序仍显示在 **“程序和功能”** 的程序列表中。 但是，如果关闭 **“程序和功能”**，则下次打开 **“程序和功能”** 时，将会刷新程序列表以仅显示仍实际安装的程序。  
  
### <a name="if-the-uninstallation-fails"></a>如果卸载失败  
  
1.  如果卸载过程没有成功完成，请尝试修复造成卸载失败的问题。 以下文章可帮助您了解卸载失败的原因：  
  
    -   [如何在安装日志文件中识别 SQL Server 2008 安装问题](http://support.microsoft.com/kb/955396/en-us)  
  
    -   [查看和读取 SQL Server 安装程序日志文件](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
2.  如果无法修复卸载失败的原因，可与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 支持部门联系。 在某些情况下（如无意间删除了重要文件），则在计算机上重新安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前，可能需要重新安装操作系统。  
  
## <a name="see-also"></a>另请参阅  
 [查看和读取 SQL Server 安装程序日志文件](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  

---
title: 使用将数据库添加到可用性组向导 (SQL Server Management Studio) |Microsoft 文档
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.adddatabasewizard.f1
helpviewer_keywords:
- Availability Groups [SQL Server], wizards
- Availability Groups [SQL Server], databases
ms.assetid: 81e5e36d-735d-4731-8017-2654673abb88
caps.latest.revision: 23
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 2eae2dbc1f6031b18f6edf3a92e65d05d56b4ff2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129965"
---
# <a name="use-the-add-database-to-availability-group-wizard-sql-server-management-studio"></a>使用“将数据库添加到可用性组向导”(SQL Server Management Studio)
  使用“将数据库添加到可用性组向导”可帮助您将一个或多个数据库添加到现有的 AlwaysOn 可用性组。  
  
> [!NOTE]  
>  有关使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 PowerShell 将次要副本添加到数据库的信息，请参阅 [将数据库添加到可用性组 (SQL Server)](availability-group-add-a-database.md)。  
  
 **本主题内容：**  
  
-   **开始之前：**  
  
     [先决条件和限制](#Prerequisites)  
  
     [Security](#Security)  
  
-   **若要添加数据库，请使用：**[将数据库添加到可用性组向导 (SQL Server Management Studio)](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
 如果你从未向可用性组添加数据库，请参阅中的"可用性数据库"部分[先决条件、 限制和 AlwaysOn 可用性组的建议&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)。  
  
###  <a name="Prerequisites"></a> 先决条件、限制和建议  
  
-   您必须连接到承载当前主副本的服务器实例。  
  
-   如果数据库进行了加密或者数据库甚至包含数据库加密密钥 (DEK)，则您无法使用 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 或 [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] 将该数据库添加到某一可用性组。 即使已对加密的数据库进行了解密，其日志备份也可能包含加密的数据。 在此情况下，在该数据库上完整的初始数据同步可能会失败。 其原因在于，还原日志操作可能要求数据库加密密钥 (DEK) 使用的证书，但该证书可能不可用。  
  
     **为使解密的数据库可添加到可用性组使用向导：**  
  
    1.  创建主数据库的日志备份。  
  
    2.  创建主数据库的完整数据库备份。  
  
    3.  在承载辅助副本的服务器实例上，还原数据库备份。  
  
    4.  从主数据库创建新的日志备份。  
  
    5.  在辅助数据库上还原此日志备份。  
  
-   **使用完全初始数据同步的先决条件**  
  
    -   在承载可用性组的副本的每个服务器实例上，所有数据库文件路径都必须完全相同。  
  
    -   没有任何主数据库名称可存在于承载辅助副本的任何服务器实例上。 这意味着尚没有任何新的辅助数据库可以存在。  
  
    -   为了使该向导创建并访问备份，需要指定网络共享。 对于主副本，用于启动 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 的帐户必须对网络共享具有读写文件系统权限。 对于辅助副本，该帐户必须具有对网络共享区的读权限。  
  
     如果您无法使用该向导执行完全初始数据同步，则需要手动准备您的辅助数据库。 您可以在运行该向导之前或之后进行准备。 有关详细信息，请参阅 [为可用性组手动准备辅助数据库 (SQL Server)](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)中创建和配置 AlwaysOn 可用性组。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用“将数据库添加到可用性组向导”(SQL Server Management Studio)  
 **使用“将数据库添加到可用性组向导”**  
  
1.  在对象资源管理器中，连接到承载可用性组的主副本的服务器实例，然后展开服务器树。  
  
2.  依次展开 **“AlwaysOn 高可用性”** 节点和 **“可用性组”** 节点。  
  
3.  右键单击要向其添加数据库的可用性组，然后选择“添加数据库”命令。 该命令将启动“将数据库添加到可用性组向导”。  
  
4.  在 **“选择数据库”** 页上，选择一个或多个数据库。 有关详细信息，请参阅[选择数据库页&#40;新建可用性组向导将添加数据库向导&#41;](select-databases-page-new-availability-group-wizard-and-add-database-wizard.md)。  
  
5.  在 **“选择初始数据同步”** 页上，选择如何创建新的辅助数据库并将其联接到可用性组。 选择下列选项之一：  
  
    -   **Full**  
  
         如果你的环境满足自动启动初始数据同步的要求，则选择此选项（有关详细信息，请参阅本主题前面的 [先决条件、限制和建议](#Prerequisites)）。  
  
         如果选择 **“完全”**，则在创建可用性组后，向导会尝试将每个主数据库及其事务日志备份到网络共享，并在每个承载辅助副本的服务器实例上还原备份。 然后，该向导将每个辅助数据库联接到可用性组。  
  
         在“指定可由所有副本访问的共享网络位置”字段中，指定承载副本的所有服务器都具有读写访问权限的备份共享。 日志备份将是您的日志备份链的一部分。 适当地存储日志备份文件。  
  
        > [!IMPORTANT]  
        >  有关所需文件系统权限的详细信息，请参阅本主题中前面的 [先决条件](#Prerequisites)部分。  
  
    -   **仅联接**  
  
         如果在将承载辅助副本的服务器实例上手动准备了辅助数据库，则可以选择此选项。 该向导将每个现有辅助数据库联接到可用性组。  
  
    -   **跳过初始数据同步**  
  
         如果要使用您自己的数据库和主数据库的日志备份，请选择此选项。 有关详细信息，请参阅[启动 AlwaysOn 辅助数据库的数据移动 (SQL Server)](start-data-movement-on-an-always-on-secondary-database-sql-server.md)。  
  
     有关详细信息，请参阅[选择初始数据同步页&#40;AlwaysOn 可用性组向导&#41;](select-initial-data-synchronization-page-always-on-availability-group-wizards.md)。  
  
6.  在 **“连接到现有的辅助副本”** 页上，如果承载该可用性组的可用性副本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例全部作为相同用户帐户中的某个服务运行，则单击 **“全部连接”**。 如果任何服务器实例作为不同帐户下的某个服务运行，则单击每个服务器实例名称右侧的各个 **“连接”** 按钮。  
  
     有关详细信息，请参阅[连接到现有的辅助副本页&#40;添加副本向导和添加数据库向导&#41;](connect-to-existing-secondary-replicas-page.md)。  
  
7.  **“验证”** 页验证在此向导中指定的值是否满足新建可用性组向导的要求。 若要进行更改，可以单击 **“上一页”** 以返回前面的向导页，更改一个或多个值。 单击 **“下一步”** 返回到 **“验证”** 页，然后单击 **“重新运行验证”**。  
  
     有关详细信息，请参阅[验证页&#40;AlwaysOn 可用性组向导&#41;](validation-page-always-on-availability-group-wizards.md)。  
  
8.  在 **“摘要”** 页上，查看您为新的可用性组进行的选择。 若要进行更改，请单击 **“上一步”** 以返回到相应页。 在进行更改后，单击 **“下一步”** 以返回到 **“摘要”** 页。  
  
     有关详细信息，请参阅[摘要页&#40;AlwaysOn 可用性组向导&#41;](summary-page-always-on-availability-group-wizards.md)。  
  
     如果您满意所做的选择，可以选择单击“脚本”以创建向导将执行的步骤的脚本。 然后，若要创建和配置新的可用性组，请单击 **“完成”**。  
  
9. **“进度”** 页将显示创建可用性组的各步骤（配置端点、创建可用性组和将辅助副本联接到该组）的进度。  
  
     有关详细信息，请参阅[进度页&#40;AlwaysOn 可用性组向导&#41;](progress-page-always-on-availability-group-wizards.md)。  
  
10. 在这些步骤完成后， **“结果”** 页将显示各步骤的结果。 如果所有这些步骤都成功，则新的可用性组得到了完全配置。 如果任何步骤导致错误，您可能需要手动完成配置。 有关给定错误的原因的信息，请单击 **“结果”** 列中关联的“错误”链接。  
  
     完成向导后，单击 **“关闭”** 以退出安装向导。  
  
     有关详细信息，请参阅[“结果”页（AlwaysOn 可用性组向导）](results-page-always-on-availability-group-wizards.md)。  
  
11. 如果在所有辅助数据库上未自动启动初始数据同步，则需要配置任何尚未加入的辅助数据库。 有关详细信息，请参阅[启动 AlwaysOn 辅助数据库的数据移动 (SQL Server)](start-data-movement-on-an-always-on-secondary-database-sql-server.md)。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [为可用性组手动准备辅助数据库 (SQL Server)](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [将辅助数据库联接到可用性组 (SQL Server)](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [先决条件、 限制和 AlwaysOn 可用性组的建议&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [将数据库添加到可用性组 (SQL Server)](availability-group-add-a-database.md)   
 [启动 AlwaysOn 辅助数据库上的数据移动&#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)   
 [将数据库添加到可用性组 (SQL Server)](availability-group-add-a-database.md)  
  
  
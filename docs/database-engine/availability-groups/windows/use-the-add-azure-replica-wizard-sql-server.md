---
title: 使用“添加 Azure 副本向导”(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.addreplicawizard.azurereplica.f1
ms.assetid: b89cc41b-07b4-49f3-82cc-bc42b2e793ae
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: c5dfd05448d59a26ded4672f27ae4ec8ebbdd926
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803428"
---
# <a name="use-the-add-azure-replica-wizard-sql-server"></a>使用“添加 Azure 副本向导”(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  通过使用“添加 Azure 副本向导”，你可以在混合 IT 环境中创建新的 Windows Azure VM，将它配置为新的或现有 Always On 可用性组的辅助副本。  
  

##  <a name="BeforeYouBegin"></a> 开始之前  
 如果你从未向可用性组添加过任何可用性副本，请参阅 [针对 AlwaysOn 可用性组的先决条件、限制和建议 (SQL Server)](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)中的“服务器实例”与“可用性组和副本”部分。  
  
##  <a name="Prerequisites"></a> 先决条件  
  
-   您必须连接到承载当前主副本的服务器实例。  
  
-   您必须有混合 IT 环境，其中的本地子网有 Windows Azure 站点到站点 VPN。 有关详细信息，请参阅 [在管理门户中配置站点到站点 VPN](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create)。  
  
-   可用性组必须包含本地可用性副本。  
  
-   到可用性组侦听器的客户端必须具有 Internet 连接，才能在可用性组故障转移到 Windows Azure 副本时保持与侦听器的连接。  
  
-   **使用完全初始数据同步的先决条件** 为了使该向导创建并访问备份，需要指定网络共享。 对于主副本，用于启动 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 的帐户必须对网络共享具有读写文件系统权限。 对于辅助副本，该帐户必须具有对网络共享区的读权限。  
  
     如果您无法使用该向导执行完全初始数据同步，则需要手动准备您的辅助数据库。 您可以在运行该向导之前或之后进行准备。 有关详细信息，请参阅 [为可用性组手动准备辅助数据库 (SQL Server)](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)或 PowerShell 将辅助数据库联接到 Always On 可用性组。  
  
##  <a name="Permissions"></a> 权限  
 对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。  
  
 如果要允许“将副本添加到可用性组向导”管理数据库镜像端点，还需要 CONTROL ON ENDPOINT 权限。  
  
##  <a name="SSMSProcedure"></a> 使用“添加 Azure 副本向导”(SQL Server Management Studio)  
 可以从 [“指定副本”页](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md)启动“添加 Azure 副本向导”。 有两种方法可以打开此页：  
  
-   [使用可用性组向导 (SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [使用“将副本添加到可用性组向导”(SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
 启动“添加 Azure 副本向导”后，按以下步骤操作：  
  
1.  首先，为您的 Windows Azure 订阅下载管理证书。 单击“下载”  打开登录页面。  
  
2.  使用你的 Microsoft 帐户或组织帐户登录到 Microsoft Azure。 Microsoft 或组织帐户采用电子邮件地址格式，如 HYPERLINK "mailto:patc@contoso.com" patc@contoso.com。 有关 Azure 凭据的详细信息，请参阅 [Microsoft 组织帐户常见问题](https://technet.microsoft.com/jj592903) 和 [组织帐户登录问题的疑难解答](https://support.microsoft.com/kb/2756852)。  
  
3.  然后单击 **“连接”** 连接到您的订阅。 连接后，下拉列表用 Windows Azure 参数进行填充，例如 **“虚拟网络”** 和 **“虚拟网络子网”** 。  
  
4.  为将承载新辅助副本的 Windows Azure 虚拟机指定设置：  
  
     图像  
     要用于 Windows Azure 虚拟机的 SQL Server 图像的名称  
  
     VM 大小  
     Windows Azure 虚拟机的大小。  
  
     VM 名称  
     Windows Azure 虚拟机的 DNS 名称。  
  
     VM 用户名  
     Windows Azure 虚拟机默认管理员的用户名  
  
     VM 管理员密码（和确认密码）  
     Windows Azure 虚拟机默认管理员的密码  
  
     虚拟网络  
     要放置 Windows Azure 虚拟机的虚拟网络  
  
     虚拟网络子网  
     要放置 Windows Azure 虚拟机的虚拟网络子网  
  
     域  
     要联接 Windows Azure 虚拟机的 Active Directory (AD) 域  
  
     域用户名  
     用于将 Windows Azure 虚拟机联接到域的 AD 用户名  
  
     Password  
     用于将 Windows Azure 虚拟机联接到域的密码  
  
5.  单击 **“确定”** 提交设置并退出“添加 Azure 副本向导”。  
  
6.  对任意新副本继续 [“指定副本”页](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md) 的剩余配置步骤。  
  
     完成“可用性组向导”或“将副本添加到可用性组向导”后，配置过程在 Windows Azure 执行所有操作，创建新的 VM，将其联接到 AD 域，添加到 Windows 群集，启用 Always On 高可用性，并将新副本添加到可用性组。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [将辅助副本添加到可用性组 (SQL Server)](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组概述 (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [针对 AlwaysOn 可用性组的先决条件、限制和建议 (SQL Server)](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [将辅助副本添加到可用性组 (SQL Server)](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  

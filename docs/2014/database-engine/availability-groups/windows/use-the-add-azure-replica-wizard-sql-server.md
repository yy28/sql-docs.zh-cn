---
title: 使用“添加 Azure 副本向导”(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.addreplicawizard.azurereplica.f1
ms.assetid: b89cc41b-07b4-49f3-82cc-bc42b2e793ae
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 85f5dc758a6f9243fc553f597687552fdb22a481
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154404"
---
# <a name="use-the-add-azure-replica-wizard-sql-server"></a>使用“添加 Azure 副本向导”(SQL Server)
  使用 "添加 Azure 副本" 向导来帮助你在混合 IT 中创建新的 Azure VM, 并将其配置为新的或现有 AlwaysOn 可用性组的辅助副本。  
  
-   **开始之前：**  
  
     [先决条件](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **要添加副本，请使用：** [添加 Azure 副本向导 (SQL Server Management Studio)](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
 如果你从未向可用性组添加过任何可用性副本, 请参阅[针对 AlwaysOn 可用性组&#40;SQL 的先决条件、限制和建议中的 "服务器实例" 和 "可用性组和副本" 部分服务器&#41;](prereqs-restrictions-recommendations-always-on-availability.md)。  
  
###  <a name="Prerequisites"></a> 先决条件  
  
-   您必须连接到承载当前主副本的服务器实例。  
  
-   你必须具有混合 IT 环境, 其中本地子网具有 Azure 的站点到站点 VPN。 有关详细信息，请参阅 [在管理门户中配置站点到站点 VPN](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create)。  
  
-   可用性组必须包含本地可用性副本。  
  
-   如果可用性组侦听器要在可用性组故障转移到 Azure 副本时保持与侦听器的连接, 则这些客户端必须能够连接到 Internet。  
  
-   **使用完全初始数据同步的先决条件** 为了使该向导创建并访问备份，需要指定网络共享。 对于主副本，用于启动 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 的帐户必须对网络共享具有读写文件系统权限。 对于辅助副本，该帐户必须具有对网络共享区的读权限。  
  
     如果您无法使用该向导执行完全初始数据同步，则需要手动准备您的辅助数据库。 您可以在运行该向导之前或之后进行准备。 有关详细信息，请参阅 [为可用性组手动准备辅助数据库 (SQL Server)](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)中创建和配置 AlwaysOn 可用性组。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 请参阅 [Security](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md#Security)  
  
##  <a name="SSMSProcedure"></a> 使用“添加 Azure 副本向导”(SQL Server Management Studio)  
 可以从 [“指定副本”页](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md)启动“添加 Azure 副本向导”。 有两种方法可以打开此页：  
  
-   [使用可用性组向导 (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [使用“将副本添加到可用性组向导”(SQL Server Management Studio)](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
 启动“添加 Azure 副本向导”后，按以下步骤操作：  
  
1.  首先, 请下载 Azure 订阅的管理证书。 单击“下载”打开登录页面。  
  
2.  在登录页中, 登录到 Azure 订阅。 登录后，向导会在您的本地计算机上安装管理证书。 下次使用此向导时会自动加载此管理证书。 如果您下载了多个管理证书，可以单击 **“...”** 按钮选择要使用的证书。  
  
3.  然后单击 **“连接”** 连接到您的订阅。 连接后, 下拉列表将用 Azure 参数填充, 例如**虚拟网络**和**虚拟网络子网**。  
  
4.  指定将承载新辅助副本的 Azure VM 的设置:  
  
     图像  
     要用于 Azure VM 的 SQL Server 映像的名称  
  
     VM 大小  
     Azure VM 的大小  
  
     VM 名称  
     Azure VM 的 DNS 名称  
  
     VM 用户名  
     Azure VM 的默认管理员的用户名  
  
     VM 管理员密码（和确认密码）  
     Azure VM 的默认管理员的密码  
  
     虚拟网络  
     要在其中放置 Azure VM 的虚拟网络  
  
     虚拟网络子网  
     要在其中放置 Azure VM 的虚拟网络子网  
  
     Domain  
     要加入 Azure VM 的 Active Directory (AD) 域  
  
     域用户名  
     用于将 Azure VM 加入到域的 AD 用户名  
  
     Password  
     用于将 Azure VM 加入到域的密码  
  
5.  单击 **“确定”** 提交设置并退出“添加 Azure 副本向导”。  
  
6.  对任意新副本继续 [“指定副本”页](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md) 的剩余配置步骤。  
  
     完成 "可用性组向导" 或 "将副本添加到可用性组向导" 后, 配置过程将在 Azure 中执行所有操作来创建新的 VM, 将其加入 AD 域, 将其添加到 Windows 群集, 启用 AlwaysOn 高可用性, 并将新副本添加到可用性组。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [将辅助副本添加到可用性组 (SQL Server)](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组&#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性组&#40;的先决条件、限制和建议 SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [将辅助副本添加到可用性组 (SQL Server)](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  

---
title: "连接到其他计算机（SQL Server 配置管理器）| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: connections [SQL Server], other computers
ms.assetid: c4c1e94f-4f5f-431e-8b5b-d5ff97baf723
caps.latest.revision: "40"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e2e1053f5def6f941e82d050f117c3814776787d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="scm-services---connect-to-another-computer"></a>SCM 服务 - 连接到其他计算机
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]本主题说明如何在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中连接到其他计算机。 按照第一个过程执行操作，打开 Windows 的“计算机管理” [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理控制台 (mmc)，连接到该计算机，然后展开“服务和应用程序”树。 遵循第二个过程，创建一个包含到远程计算机中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器的链接的文件。  
  
> [!NOTE]  
>  远程连接时，某些程序无法由配置管理器执行。  
  
 若要在其他计算机上启动、停止、暂停或恢复服务，也可以连接到安装有 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的服务器，右键单击此服务器或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理，然后单击需要的操作。  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-connect-to-another-computer-with-windows-computer-management"></a>使用 Windows 的“计算机管理”连接到另一台计算机  
  
1.  在“开始”  菜单上，右键单击“我的电脑” ，再单击“管理”   
  
2.  在“计算机管理” 中，右键单击“计算机管理（本地）” ，再单击“连接到另一台计算机” 。  
  
3.  在 **“选择计算机”** 对话框中的 **“另一台计算机”** 文本框中，键入想要管理的计算机名，然后单击 **“确定”**。  
  
     “计算机管理”将显示运行在远程计算机上的服务。 顶级节点更改为“计算机管理”\<远程计算机>。  
  
4.  在控制台树中，依次展开 **“服务和应用程序”**、 **“SQL Server 配置管理器”** 来管理远程计算机的服务。  
  
#### <a name="to-save-a-link-to-sql-server-configuration-manager-for-another-computer"></a>将链接保存到其他计算机的 SQL Server 配置管理器中  
  
1.  在 **“开始”** 菜单上，单击 **“运行”**。  
  
2.  在“打开”  框中，键入 **mmc -a** ，以作者模式打开 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理控制台。  
  
3.  在“文件”  菜单上，单击“添加/删除管理单元” 。  
  
4.  在“添加/删除管理单元”  窗口中，单击“添加” 。  
  
5.  在“添加独立管理单元”  窗口中，单击“计算机管理”  ，再单击“添加” 。  
  
6.  在 **“计算机管理”** 窗口中，单击 **“其他计算机”**，键入要管理的远程计算机的名称，再单击 **“完成”**。  
  
7.  在“添加单独管理单元”  窗口中，单击“关闭” 。  
  
8.  在“添加/删除管理单元”  窗口中，单击“确定” 。  
  
9. 依次展开“计算机管理（\<计算机名称>）”和“服务和应用程序”。  
  
10. 右键单击“SQL Server 配置管理器” ，再单击“从此处新建窗口” 。  
  
11. 在 **“窗口”** 菜单上，单击 **“控制台根节点”**，切换回第一个窗口，并删除该窗口。  
  
12. 在“文件”  菜单上，单击“另存为” ，使用文件扩展名为 **.msc** 的相应文件名将文件保存到目标文件夹。 关闭 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理控制台。  
  
13. 若要打开目标计算机中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器，请双击此文件。 如果需要，则在桌面上或 **“开始”** 菜单中保存到此文件的链接。  
  
> [!CAUTION]  
>  当使用远程计算机中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器时，计算机名称不是显而易见的，因此可能会错误地停止或配置不正确的计算机。 在 **“服务”** 选项卡上，选中 **“主机名”** 复选框以在修改服务前确认计算机名称。  
  
## <a name="see-also"></a>另请参阅  
 [在 SQL Server 工具中将 WMI 配置为显示服务器状态](http://msdn.microsoft.com/library/7e97197b-ed4d-40d1-9a52-9ab1d92401d7)  
  
  

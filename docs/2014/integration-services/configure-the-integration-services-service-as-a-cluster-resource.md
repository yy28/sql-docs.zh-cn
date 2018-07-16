---
title: 将 Integration Services 服务配置为群集资源 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 367835aa-9855-4791-a989-b3d08402ad4c
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b524b2c570b3fac16403565716aaea36a31a7f24
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37223763"
---
# <a name="configure-the-integration-services-service-as-a-cluster-resource"></a>将 Integration Services 服务配置为群集资源
  对于那些认为将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务配置为群集资源所带来的优点大于缺点的客户，本节包含必要的配置说明。 但是， [!INCLUDE[msCoName](../includes/msconame-md.md)] 不建议将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务配置为群集资源。  
  
 若要将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务配置为群集资源，您需要完成以下任务。  
  
-   在群集上安装 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 。  
  
     若要在群集上安装 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ，必须将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 安装在群集的每个节点上。  
  
-   将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 配置为群集资源。  
  
     在将 Integration Services 安装在群集的每个节点上之后，需要将 Integration Services 配置为群集资源。 在将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务配置为群集资源时，可以向与 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]相同或不同的资源组中添加该服务。 下表描述了在选择资源组时可能存在的优缺点。  
  
    |当 Integration Services 和 SQL Server 位于同一个资源组中时|当 Integration Services 和 SQL Server 位于不同的资源组中时|  
    |-----------------------------------------------------------------------------|-------------------------------------------------------------------------------|  
    |客户端计算机可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 来管理存储在 msdb 数据库中的包，因为 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 和 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务运行于同一台虚拟服务器上。 此配置避免了双跃点方案中的委托问题。|客户端计算机不能使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 来管理存储在 msdb 数据库中的包。 客户端可以连接到运行 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务的虚拟服务器。 但是，客户端计算机不能将用户的凭据委托给运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的虚拟服务器。 这称作双跃点方案。|  
    |[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务在 CPU 和其他计算机资源方面能够与其他 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服务竞争。|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务在 CPU 和其他计算机资源方面不能与其他 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服务竞争，因为不同的节点上配置了不同的资源组。|  
    |将包加载和保存到 msdb 数据库的速度会加快，生成的网络通信流量会较少，因为这两项服务运行于同一台计算机上。|将包加载和保存到 msdb 数据库的速度可能会减慢，生成的网络通信流量会较多。|  
    |这两项服务同时联机或脱机。|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务可以在 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 处于脱机状态时联机。 因此，存储在 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的 msdb 数据库中的包不可用。|  
    |[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务不能根据需要快速移动到另一个节点。|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务可以根据需要更快地移动到另一个节点。|  
  
     在确定了要向哪个资源组添加 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]之后，必须在该组中将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 配置为群集资源。  
  
-   配置 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务和包存储区。  
  
     在将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 配置为群集资源之后，必须针对群集内每个节点上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务，修改配置文件的位置和内容。 这些修改会使得配置文件和包存储区在发生故障转移时对于所有的节点可用。 在修改配置文件的位置和内容之后，必须将该服务联机。  
  
-   将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务作为群集资源联机。  
  
 在群集或任何服务器上配置 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务后，可能需要配置 DCOM 权限才能从客户端计算机连接到该服务。 有关详细信息，请参阅[连接到远程 Integration Services 服务器（SSIS 服务）](../../2014/integration-services/connect-to-a-remote-integration-services-server-ssis-service.md)。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务不能委托凭据。 因此，在满足下列条件时，不能使用 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 来管理存储在 msdb 数据库中的包：  
  
-   [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 运行于不同的服务器或虚拟服务器上。  
  
-   运行 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的客户端是第三台计算机。  
  
 客户端可以连接到运行 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务的虚拟服务器。 但是，客户端计算机不能将用户的凭据委托给运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的虚拟服务器。 这称作双跃点方案。  
  
### <a name="to-install-integration-services-on-a-cluster"></a>在群集上安装 Integration Services  
  
1.  安装并配置具有一个或更多节点的群集。  
  
2.  （可选）安装群集服务（如 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]）。  
  
3.  在群集的每个节点上安装 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 。  
  
### <a name="to-configure-integration-services-as-a-cluster-resource"></a>将 Integration Services 配置为群集资源  
  
1.  打开 **“群集管理器”**。  
  
2.  在控制台树中选择 Groups 文件夹。  
  
3.  在结果窗格中，选择计划添加 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]的组：  
  
    -   若要将 Integrations Services 作为群集资源添加到与 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]相同的资源组中，请选择 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所属的组。  
  
    -   若要将 Integrations Services 作为群集资源添加到不同于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的组中，请选择 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所属的组以外的组。  
  
4.  在 **“文件”** 菜单上，指向 **“新建”**，再单击 **“资源”**。  
  
5.  在“资源向导”的 **“新资源”** 页上，键入名称并选择 **“一般服务”** 作为 **“服务类型”**。 不要更改 **“组”** 的值。 单击“下一步” 。  
  
6.  在 **“可能的所有者”** 页上，将群集的节点作为可能的资源所有者来添加或删除。 单击“下一步” 。  
  
7.  若要添加依赖关系，请在 **“依赖关系”** 页上的 **“可用资源”** 下选择一项资源，然后单击 **“添加”**。 对于故障转移情况， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和用来存储 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包的共享磁盘应在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 联机前重新联机。 在选择依赖关系之后，单击 **“下一步”**。  
  
     有关详细信息，请参阅 [Add Dependencies to a SQL Server Resource](../sql-server/failover-clusters/windows/add-dependencies-to-a-sql-server-resource.md)。  
  
8.  在“一般服务参数”  页上，输入 **MsDtsServer** 作为服务名。 单击“下一步” 。  
  
9. 在 **“注册表复制”** 页上单击 **“添加”** ，以添加用来标识 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务的配置文件位置的注册表项。 此文件必须位于 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务所在资源组中的共享磁盘上。  
  
10. 在“注册表项”对话框中，键入 SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile。 单击 **“确定”**，然后单击 **“完成”**。  
  
     [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务现已添加为群集资源。  
  
### <a name="to-configure-the-integration-services-service-and-package-store"></a>配置 Integration Services 服务和包存储区  
  
1.  在 %ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.ini.xml 中找到该配置文件。 将该文件复制到已添加 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务的组的共享磁盘上。  
  
2.  在共享磁盘上，创建一个名为 **Packages** 的新文件夹来充当包存储区。 为适当的用户和组授予对这个新文件夹的“列出文件夹”和“写入”权限。  
  
3.  在共享磁盘上，用文本编辑器或 XML 编辑器打开配置文件。 更改的值`ServerName`的虚拟名称的元素[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中相同的资源组。  
  
4.  更改的值`StorePath`元素的完全限定路径**包**在上一步中在共享磁盘上创建文件夹。  
  
5.  将注册表中的 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile** 值更新为共享磁盘上服务配置文件的完全限定路径和文件名。  
  
### <a name="to-bring-the-integration-services-service-online"></a>将 Integration Services 服务联机  
  
-   在“群集管理器”中选择 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务，单击右键，然后在弹出菜单中选择“联机”。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务现已作为群集资源联机。  
  
  

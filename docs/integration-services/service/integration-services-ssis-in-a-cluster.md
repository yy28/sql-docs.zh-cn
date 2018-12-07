---
title: 群集中的 Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0216266d-d866-4ea2-bbeb-955965f4d7c2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 714136a95b47626b0d8db0875a6b3d72402a472f
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52407344"
---
# <a name="integration-services-ssis-in-a-cluster"></a>群集中的 Integration Services (SSIS)
  建议不要对 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 进行聚类分析，因为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务不是群集服务或群集感知服务，而且不支持从一个群集节点故障转移到另一个节点。 因此，在群集环境内，应当在群集的每个节点上安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 并将其作为一个独立服务来启动。  
  
 虽然 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务不是群集服务，但您可以在将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务单独安装在群集的每个节点上之后，手动将该服务配置为作为群集资源运行。  
  
 但是，如果您建立群集硬件环境的目的是实现高可用性，那么，不将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置为群集资源也可以实现此目标。  若要从群集中的其他任何节点管理该群集中某一节点上的包，请在群集的每个节点上修改 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的配置文件。 可以修改每个配置文件，使其指向包所存储到的所有可用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 本解决方案提供大多数客户所需的高可用性，而不会带来在将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置为群集资源时可能遇到的问题。 有关如何更改此配置文件的详细信息，请参阅 [Integration Services 服务（SSIS 服务）](../../integration-services/service/integration-services-service-ssis-service.md)。  
  
 了解 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的角色对于就如何在群集环境中配置该服务做出明智决定至关重要。 有关详细信息，请参阅 [Integration Services 服务（SSIS 服务）](../../integration-services/service/integration-services-service-ssis-service.md)。  
  
## <a name="disadvantages"></a>缺点
 将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置为群集资源的一些潜在缺点包括：  
  
-   **发生故障转移时，正在运行的包不会重启。**
    
    可以通过从检查点重新启动包来从包失败中恢复。 可以从检查点重新启动，而不必将服务配置为群集资源。 有关详细信息，请参阅 [通过使用检查点重新启动包](../../integration-services/packages/restart-packages-by-using-checkpoints.md)。  
  
-   在不同于 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的资源组中配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务时，不能使用客户端计算机上的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 来管理存储在 msdb 数据库中的包。 在这个双跃点方案中， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务不能委托凭据。  
  
-   如果群集内有多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源组包括 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务，则故障转移可能会导致意外的结果。 请考虑下面的方案。 组 1 运行于节点 A 上，其中包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务。组 2 运行于节点 B 上，其中也包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务。组 2 故障转移到节点 A。由于 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务是单实例服务，因此尝试在节点 A 上启动 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的另一个实例时将失败。 尝试故障转移到节点 A 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务是否也失败取决于组 2 中 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的配置。 如果 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置为影响资源组中的其他服务，那么，由于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务失败，因此正在故障转移的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务也将失败。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务配置为不影响资源组中的其他服务，则该服务将能够故障转移到节点 A。除非组 2 中的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置为不影响资源组中的其他服务，否则，当正在故障转移的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务失败时，正在故障转移到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务也将失败。  

## <a name="configure-the-service-as-a-cluster-resource"></a>将服务配置为群集资源
对于那些认为将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置为群集资源所带来的优点大于缺点的客户，本节包含必要的配置说明。 但是， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 不建议将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置为群集资源。  
  
 若要将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置为群集资源，您需要完成以下任务。  
  
-   在群集上安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 。  
  
     若要在群集上安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ，必须将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 安装在群集的每个节点上。  
  
-   将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 配置为群集资源。  
  
     在将 Integration Services 安装在群集的每个节点上之后，需要将 Integration Services 配置为群集资源。 在将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置为群集资源时，可以向与 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]相同或不同的资源组中添加该服务。 下表描述了在选择资源组时可能存在的优缺点。  
  
    |当 Integration Services 和 SQL Server 位于同一个资源组中时|当 Integration Services 和 SQL Server 位于不同的资源组中时|  
    |-----------------------------------------------------------------------------|-------------------------------------------------------------------------------|  
    |客户端计算机可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 来管理存储在 msdb 数据库中的包，因为 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务运行于同一台虚拟服务器上。 此配置避免了双跃点方案中的委托问题。|客户端计算机不能使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 来管理存储在 msdb 数据库中的包。 客户端可以连接到运行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的虚拟服务器。 但是，客户端计算机不能将用户的凭据委托给运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的虚拟服务器。 这称作双跃点方案。|  
    |[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务在 CPU 和其他计算机资源方面能够与其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务竞争。|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务在 CPU 和其他计算机资源方面不能与其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务竞争，因为不同的节点上配置了不同的资源组。|  
    |将包加载和保存到 msdb 数据库的速度会加快，生成的网络通信流量会较少，因为这两项服务运行于同一台计算机上。|将包加载和保存到 msdb 数据库的速度可能会减慢，生成的网络通信流量会较多。|  
    |这两项服务同时联机或脱机。|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务可以在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 处于脱机状态时联机。 因此，存储在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的 msdb 数据库中的包不可用。|  
    |[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务不能根据需要快速移动到另一个节点。|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务可以根据需要更快地移动到另一个节点。|  
  
     在确定了要向哪个资源组添加 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]之后，必须在该组中将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 配置为群集资源。  
  
-   配置 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务和包存储区。  
  
     在将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 配置为群集资源之后，必须针对群集内每个节点上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务，修改配置文件的位置和内容。 这些修改会使得配置文件和包存储区在发生故障转移时对于所有的节点可用。 在修改配置文件的位置和内容之后，必须将该服务联机。  
  
-   将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务作为群集资源联机。  
  
 在群集或任何服务器上配置 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务后，可能需要配置 DCOM 权限才能从客户端计算机连接到该服务。 有关详细信息，请参阅 [Integration Services 服务（SSIS 服务）](../../integration-services/service/integration-services-service-ssis-service.md)。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务不能委托凭据。 因此，在满足下列条件时，不能使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 来管理存储在 msdb 数据库中的包：  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 运行于不同的服务器或虚拟服务器上。  
  
-   运行 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的客户端是第三台计算机。  
  
 客户端可以连接到运行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的虚拟服务器。 但是，客户端计算机不能将用户的凭据委托给运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的虚拟服务器。 这称作双跃点方案。  
  
### <a name="to-install-integration-services-on-a-cluster"></a>在群集上安装 Integration Services  
  
1.  安装并配置具有一个或更多节点的群集。  
  
2.  （可选）安装群集服务（如 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]）。  
  
3.  在群集的每个节点上安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 。  
  
### <a name="to-configure-integration-services-as-a-cluster-resource"></a>将 Integration Services 配置为群集资源  
  
1.  打开 **“群集管理器”**。  
  
2.  在控制台树中选择 Groups 文件夹。  
  
3.  在结果窗格中，选择计划添加 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的组：  
  
    -   若要将 Integrations Services 作为群集资源添加到与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]相同的资源组中，请选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所属的组。  
  
    -   若要将 Integrations Services 作为群集资源添加到不同于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的组中，请选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所属的组以外的组。  
  
4.  在 **“文件”** 菜单上，指向 **“新建”**，再单击 **“资源”**。  
  
5.  在“资源向导”的“新资源”页上，键入名称并选择“一般服务”作为“服务类型”。 不要更改 **“组”** 的值。 单击“下一步” 。  
  
6.  在 **“可能的所有者”** 页上，将群集的节点作为可能的资源所有者来添加或删除。 单击“下一步” 。  
  
7.  若要添加依赖关系，请在 **“依赖关系”** 页上的 **“可用资源”** 下选择一项资源，然后单击 **“添加”**。 对于故障转移情况， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和用来存储 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的共享磁盘应在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 联机前重新联机。 在选择依赖关系之后，单击 **“下一步”**。  
  
     有关详细信息，请参阅 [Add Dependencies to a SQL Server Resource](../../sql-server/failover-clusters/windows/add-dependencies-to-a-sql-server-resource.md)。  
  
8.  在“一般服务参数”  页上，输入 **MsDtsServer** 作为服务名。 单击“下一步” 。  
  
9. 在 **“注册表复制”** 页上单击 **“添加”** ，以添加用来标识 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的配置文件位置的注册表项。 此文件必须位于 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务所在资源组中的共享磁盘上。  
  
10. 在“注册表项”对话框中，键入 SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile。 单击 **“确定”**，然后单击 **“完成”**。  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务现已添加为群集资源。  
  
### <a name="to-configure-the-integration-services-service-and-package-store"></a>配置 Integration Services 服务和包存储区  
  
1.  在 %ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.ini.xml 中找到该配置文件。 将该文件复制到已添加 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的组的共享磁盘上。  
  
2.  在共享磁盘上，创建一个名为 **Packages** 的新文件夹来充当包存储区。 为适当的用户和组授予对这个新文件夹的“列出文件夹”和“写入”权限。  
  
3.  在共享磁盘上，用文本编辑器或 XML 编辑器打开配置文件。 将 **ServerName** 元素的值更改为同一资源组中虚拟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的名称。  
  
4.  将 **StorePath** 元素的值更改为上一步骤中在共享磁盘上所创建的 **Packages** 文件夹的完全限定路径。  
  
5.  将注册表中的 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile** 值更新为共享磁盘上服务配置文件的完全限定路径和文件名。  
  
### <a name="to-bring-the-integration-services-service-online"></a>将 Integration Services 服务联机  
  
-   在“群集管理器”中选择 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务，单击右键，然后在弹出菜单中选择“联机”。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务现已作为群集资源联机。  
  
  

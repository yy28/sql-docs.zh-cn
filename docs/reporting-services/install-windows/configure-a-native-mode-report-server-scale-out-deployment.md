---
title: 配置本机模式报表服务器扩展部署 | Microsoft Docs
ms.date: 11/29/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], deployments
- deploying [Reporting Services], scale-out deployment model
- scale-out deployments [Reporting Services]
ms.assetid: b30d0308-4d9b-4f85-9f83-dece4dcb2775
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 65182936a6ea686b7b0089827ce1fb2f26e86b98
ms.sourcegitcommit: 1800fc15075bb17b50d0c18b089d8a64d87ae726
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2019
ms.locfileid: "66500583"
---
# <a name="configure-a-native-mode-report-server-scale-out-deployment"></a>配置本机模式报表服务器扩展部署

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE [ssrs-appliesto-pbirs](../../includes/ssrs-appliesto-pbirs.md)]

Reporting Services 本机模式支持扩展部署模式。该模式允许运行共享单个报表服务器数据库的多个报表服务器实例。 扩展部署用来增加报表服务器的可扩展性，以处理更多的并发用户和更大的报表执行负载， 还可用来在特定服务器上专门处理交互式报表或计划报表。

对于 Power BI 报表服务器，为确保其良好性能，需要在负载均衡器上为任何横向扩展环境配置客户端关联（有时称为粘滞会话）。  
  
对于 SQL Server 2016 Reporting Services 及更早版本，SharePoint 模式报表服务器利用 SharePoint 产品基础结构进行横向扩展。通过将更多的 SharePoint 模式报表服务器添加到 SharePoint 场来执行 SharePoint 模式扩展。 有关 SharePoint 模式中的扩展的信息，请参阅[向场中添加另一个报表服务器（SSRS 扩展）](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)。  

> [!NOTE]
> 自 SQL Server 2016 之后，不再提供 Reporting Services 与 SharePoint 的集成这一功能。
 
  在以下情形中使用“扩展部署”  ：  
  
-   作为对服务器群集中的多个报表服务器进行负载平衡的必备条件。 在可以对多个报表服务器进行负载平衡之前，必须首先将它们配置为共享同一报表服务器数据库。  
  
-   通过使用一个服务器处理交互式报表同时使用另一个服务器处理计划的报表，将报表服务器应用程序分段置于不同的计算机上。 在此情况下，每个服务器实例均按照共享报表服务器数据库中存储的同一报表服务器内容来处理不同类型的请求。  
  
 **扩展部署中包括：**  
  
-   两个或多个共享单个报表服务器数据库的报表服务器实例。  
  
-   （可选）一个用来将交互式用户负载分布到多个报表服务器实例上的网络负载平衡 (NLB) 群集。  
  
 如果将 Reporting Services 部署到 NLB 群集上，则需要确保在报表服务器 URL 的配置中使用 NLB 虚拟服务器名称，并将这些服务器配置为共享同一个视图状态。  
  
 Reporting Services 不参与 Microsoft Cluster Services 群集。 但是，可以在属于故障转移群集的数据库引擎实例上创建报表服务器数据库。  
  
 **若要计划、安装和配置扩展部署，请按照下列步骤操作：**  
  
-   请查看[使用安装向导安装 SQL Server（安装程序）](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)，获取有关如何安装报表服务器实例的说明。  
  
-   如果打算在网络负载平衡 (NLB) 群集上承载扩展部署，则应当在配置扩展部署之前配置 NLB 群集。 有关详细信息，请参阅 [在网络负载平衡群集上配置报表服务器](../../reporting-services/report-server/configure-a-report-server-on-a-network-load-balancing-cluster.md)。  
  
-   请查阅此主题中的过程以了解有关如何共享报表服务器数据库并将报表服务器联接到扩展部署的说明。  
  
     这些过程说明如何配置双节点报表服务器扩展部署。 重复本主题中所述的步骤可向部署中添加其他报表服务器节点。  
  
    -   使用安装程序安装将与扩展部署联接的每个报表服务器实例。  
  
         为避免在将服务器实例连接到共享数据库时出现数据库兼容错误，应确保所有实例都为同一版本。 例如，如果使用 SQL Server 2016 报表服务器实例创建报表服务器数据库，则同一部署中的其他所有实例也必须为 SQL Server 2016 实例。  
  
    -   使用 Reporting Services 配置管理器将每个报表服务器连接到共享数据库。 您一次只能连接并配置一台报表服务器。  
  
    -   使用 Reporting Services 配置工具将新的报表服务器实例联接到已经与报表服务器数据库连接的第一个报表服务器实例来完成扩展。  
  
## <a name="to-install-a-sql-server-instance-to-host-the-report-server-databases"></a>安装 SQL Server 实例以承载报表服务器数据库  
  
1.  在将承载报表服务器数据库的计算机上安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 至少需要安装 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
2.  如有必要，请针对报表服务器启用远程连接。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的某些版本在默认情况下不允许进行远程 TCP/IP 和 Named Pipes 连接。 若要确认是否允许进行远程连接，请使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器，然后查看目标实例的网络配置设置。 如果远程实例还是一个命名实例，请验证目标服务器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务是否已启用且正在运行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 可提供用于连接到命名实例的端口号。 

## <a name="service-accounts"></a>服务帐户

在处理扩展部署时，用于 Reporting Services 实例的服务帐户非常重要。 部署 Reporting Services 实例时，应执行以下操作之一。

**选项 1：** 应使用相同的域用户帐户为服务帐户配置所有的 Reporting Services 实例。

**选项 2：** 需要向每个单独的服务帐户（无论是否为域帐户）授予 SQL Server 数据库实例内的 dbadmin 权限，该数据库实例正在托管 ReportServer 目录数据库。

如果已配置不同于上述任一选项的配置，则在使用 SQL 代理修改任务时可能会遇到间歇性故障。 在编辑报表订阅时，这会作为错误同时显示在 Reporting Services 日志和 Web 门户中。

```
An error occurred within the report server database.  This may be due to a connection failure, timeout or low disk condition within the database.
``` 

会间歇性出现的问题为只有创建了 SQL 代理任务的服务器将有权查看、删除或编辑项。 如果不执行上述选项之一，则只有在负载均衡器将对该订阅的所有请求发送到创建了 SQL 代理任务的服务器时，操作才会成功。 
  
## <a name="to-install-the-first-report-server-instance"></a>安装第一个报表服务器实例  
  
1.  安装属于部署内容的第一个报表服务器实例。 安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]时，请在“报表服务器安装选项”页上选择 **“安装但不配置服务器”** 选项。  
  
2.  启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具。  
  
3.  配置报表服务器 Web 服务 URL、Web 门户 URL 和报表服务器数据库。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的[配置报表服务器（Reporting Services 本机模式）](../../reporting-services/report-server/configure-a-report-server-reporting-services-native-mode.md)。  
  
4.  验证报表服务器是否正常运行。 有关详细信息，请参阅 [联机丛书中的](../../reporting-services/install-windows/verify-a-reporting-services-installation.md) 验证 Reporting Services 安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="to-install-and-configure-the-second-report-server-instance"></a>安装并配置第二个报表服务器实例  
  
1.  运行安装程序以在另一台计算机上安装第二个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例，或在同一台计算机上将其安装为命名实例。 在安装 Reporting Services 时，请在“报表服务器安装选项”页上选择 **“安装但不配置服务器”** 选项。  
  
2.  启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具，然后连接到刚安装的新实例。  
  
3.  将报表服务器连接到用于第一个报表服务器实例的数据库：  
  
    1.  选择“数据库”打开“数据库”页  。  
  
    2.  选择“更改数据库”  。  
  
    3.  选择“选择现有报表服务器数据库”  。  
  
    4.  键入承载您要使用的报表服务器数据库的 SQL Server 数据库引擎实例的服务器名称。 此服务器必须是上述说明中连接到的服务器。  
  
    5.  选择“测试连接”，然后选择“下一步”   。  
  
    6.  在“报表服务器数据库”中，选择为第一个报表服务器创建的数据库，然后选择“下一步”   。 默认名称为 ReportServer。 请勿选择 ReportServerTempDB；它仅用于在处理报表时存储临时数据。 如果数据库列表为空，请重复前四个步骤以建立服务器连接。  
  
    7.  在“凭据”页中，选择报表服务器将用于连接到报表服务器数据库的帐户类型和凭据。 可以使用与第一个报表服务器实例相同的凭据，也可以使用其他凭据。 选择“下一步”  。  
  
    8.  选择“摘要”，然后选择“完成”   。  
  
4.  配置报表服务器“Web 服务 URL”  。 先不要测试该 URL。 在报表服务器联接到扩展部署后，该 URL 才会解析。  
  
5.  配置“Web 门户 URL”  。 先不要测试 URL，也不要试图验证部署。 报表服务器在联接到扩展部署后才可用。  
  
## <a name="to-join-the-second-report-server-instance-to-the-scale-out-deployment"></a>将第二个报表服务器实例联接到扩展部署  
  
1.  打开 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具，然后连接到第一个报表服务器实例。 由于已将第一个报表服务器初始化为执行可逆加密操作，因此它可用于将其他报表服务器实例联接到扩展部署。  
  
2.  单击“扩展部署”打开“扩展部署”页  。 您会看到两个条目，分别对应于连接到报表服务器数据库的两个报表服务器实例。 第一个报表服务器实例应已联接。 第二个报表服务器应在“等待联接”。 如果您在自己的部署中没有看到类似的条目，请确认您已连接到已配置和初始化为使用报表服务器数据库的第一个报表服务器。  
  
     ![“扩展部署”页的部分屏幕快照](../../reporting-services/install-windows/media/scaloutscreen.gif "“扩展部署”页的部分屏幕快照")  
  
3.  在“扩展部署”页上，选择等待联接部署的报表服务器实例，然后选择“添加服务器”  。  
  
    > [!NOTE]  
    >  **问题：** 尝试将一个 Reporting Services 报表服务器实例联接到横向扩展部署时，可能遇到类似“拒绝访问”的错误消息。  
    >   
    >  **解决方法：** 从第一个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例备份 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 加密密钥并将该密钥还原到第二个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器。 然后将第二个服务器联接到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 扩展部署。  
  
4.  现在应能验证两个报表服务器实例是否都正常运行。 若要验证第二个实例，可以使用 Reporting Services 配置工具连接到报表服务器，然后单击“Web 服务 URL”或“Web 门户 URL”   。  
  
 如果计划在负载平衡服务器群集中运行报表服务器，则需要进行额外配置。 有关详细信息，请参阅 [在网络负载平衡群集上配置报表服务器](../../reporting-services/report-server/configure-a-report-server-on-a-network-load-balancing-cluster.md)。  

## <a name="next-steps"></a>后续步骤

[配置服务帐户](configure-the-report-server-service-account-ssrs-configuration-manager.md)
[配置 URL](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[创建本机模式报表服务器数据库](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
[配置报表服务器 URL](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
[配置报表服务器数据库连接](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[添加和删除扩展部署的加密密钥](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
[管理 Reporting Services 本机模式报表服务器](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  

更多疑问？ [请访问 Reporting Services 论坛](https://go.microsoft.com/fwlink/?LinkId=620231)

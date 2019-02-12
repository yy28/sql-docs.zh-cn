---
title: Reporting Services 中的 SharePoint 库传递 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], report delivery
- delivering reports [Reporting Services]
- subscriptions [Reporting Services], SharePoint library delivery
ms.assetid: cb4e4f71-f2d5-475a-9284-ea324c93c7de
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e6e98f8a1989193fba440ad7e8574d409c3a4996
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56038248"
---
# <a name="sharepoint-library-delivery-in-reporting-services"></a>Reporting Services 中的 SharePoint 库传递
  配置为 SharePoint 集成模式的报表服务器包含可用于向 SharePoint 库中发送报表的传递扩展插件。  
  
 若要使用 SharePoint 传递扩展插件，必须在 SharePoint 站点上的应用程序页中创建一个订阅，然后选择 **“SharePoint 文档库”** 作为传递类型。 不能为在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或报表管理器中创建的订阅使用 SharePoint 传递扩展插件。  
  
> [!NOTE]  
>  如果报表服务器在本机模式下运行，则传递扩展插件不支持将报表传递到 SharePoint 站点。 如果尝试通过编程方式为本机模式报表服务器调用传递扩展插件，则服务器将返回 `rsDeliveryExtensionNotFound` 错误，并在报表服务器日志文件中记录 `rsOperationNotSupportedSharePointMode` 错误。  
  
## <a name="requirements"></a>要求  
 关于将呈现的报表传递到库的要求包括以下几点：  
  
-   必须将报表服务器配置为 SharePoint 集成模式。  
  
-   必须在报表服务器上安装和配置 SharePoint 传递扩展插件。  
  
-   报表必须是报表定义 (.rdl) 文件。 不能通过订阅传递其他报表服务器内容类型，如模型或资源。 不能订阅使用模型作为数据源的特别报告。  
  
-   报表必须使用已存储凭据。 无论对于何种传递类型，这都是对报表创建订阅的必备条件。  
  
-   目标必须是 SharePoint 库。 选择目标库时，必须选择位于同一 SharePoint 站点上的库。 不能将报表传递到位于相同网站集内的其他服务器或其他站点。  
  
 传递报表的过程中不传递属性和元数据。 首次传递报表时，报表会继承包含该报表的文件夹或列表的安全设置。 如果您随后修改安全设置或设置报表属性，这些设置会保留不变。 订阅仅刷新存储在指定位置的报表。  
  
## <a name="sharepoint-permissions"></a>SharePoint 权限  
 若要创建订阅，必须对报表拥有“查看项”权限。 若要传递报表，必须对要传入报表的库拥有“添加项”权限。  
  
## <a name="how-to-create-modify-and-delete-subscriptions"></a>如何创建、修改和删除订阅  
  
1.  转到从中访问报表的 SharePoint 站点。  
  
2.  选择报表，单击它旁边的向下箭头，然后选择 **“管理订阅”**。  
  
3.  单击 **“创建”**、 **“编辑”** 或 **“删除”**。  
  
 有关“管理订阅”列表的状态消息中显示有关订阅的当前信息，包括订阅是否成功以及上次运行订阅的日期和时间。  
  
## <a name="setting-delivery-options"></a>设置传递选项  
 可以为将报表传递到 SharePoint 库的订阅设置下列传递选项。  
  
 呈现输出格式  
 指定用以传递报表的应用程序格式。 在传递报表前使用该格式呈现报表。 您选择的输出格式将确定默认文件扩展名。  
  
 可从中进行选择的输出格式列表包含报表服务器上安装的一组呈现扩展插件。  
  
 请注意，不能指定仅供内部使用的输出格式，也不能指定在 SharePoint 集成模式下运行的报表服务器不支持的输出格式。 这些格式包括 Null、RGDI 和 HTMLOWC。  
  
 文件名和扩展名  
 指定要在目标库中为报表显示的文件名和扩展名。 如果不指定文件扩展名，则报表服务器会根据报表输出格式创建一个扩展名。 此值是必需的。 文件名中不得包含下列字符：: \ / * ? " \< > | # { } %  
  
 标题  
 为目标库中的报表指定可选的 `Title` 属性。 该属性是库中存储的所有项的标准属性。 用户可以指定在 SharePoint 站点上查看库内容时是显示还是隐藏该属性。  
  
 路径  
 指定一个指向 SharePoint 库的完全限定 URL，包括 SharePoint Web 应用程序和站点。 例如： <http://mySharePointWeb/MySite/MyDocLib>; 其中"<http://mySharePointWeb>"指示 Web 应用程序，"MySite"是 SharePoint 站点，并"MyDocLib"是可传递报表的位置的 SharePoint 库。  
  
 不能指定页、站点或列表。 目标容器必须是同一站点上或同一场中的库。  
  
 覆盖选项  
 指定处理订阅时是否使用更新的版本替换具有相同名称和扩展名的文件。 如果希望使用更新的版本替换现有文件，请选择 **“覆盖”** 。 如果不希望订阅替换文件，请选择 **“无”** 。 在这种情况下，如果存在具有目标名称和扩展名的文件，则不进行传递。 如果希望通过在文件名末尾追加数字来添加同一文件的连续版本，请选择 **“Autoincrement”** 。  
  
 自动复制  
 如果使用自动复制功能将一个文件的最新版本自动复制到多个位置，在启用“覆盖”的情况下则会复制此文件。 如果您使用了**Autoincrement**或**None**，则传递将失败并`rsDeliveryError`将发生错误。  
  
## <a name="see-also"></a>请参阅  
 [创建和管理 SharePoint 模式报表服务器的订阅](create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)   
 [订阅和传递 (Reporting Services)](subscriptions-and-delivery-reporting-services.md)   
 [为报表数据源指定凭据和连接信息](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  

---
title: PowerPivot 管理面板和使用情况数据 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 541c8b1f-c6c2-423d-a97d-65c379967e0c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cf132a6cd6e15002b36ba7ecdced512e3686e433
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748899"
---
# <a name="powerpivot-management-dashboard-and-usage-data"></a>PowerPivot 管理面板和使用情况数据
  PowerPivot 管理面板是 SharePoint 管理中心中预定义报表和 Web 部件的集合，可以帮助您管理 SQL Server PowerPivot for SharePoint 部署。 管理面板提供了与服务器运行状况、工作簿活动以及数据刷新相关的信息。 该面板使用的数据来自于 SharePoint 使用情况数据集合。  
  
 [先决条件](#prereq)  
  
 [仪表板的各个部分概述](#items)  
  
 [打开 PowerPivot 管理面板](#open)  
  
 [在仪表板中的源数据](#sourcedata)  
  
 [编辑 PowerPivot 面板](#edit)  
  
 [为 PowerPivot 管理面板创建自定义报表](#reports)  
  
##  <a name="prereq"></a> 先决条件  
 您必须是服务管理员才能为您管理的 PowerPivot 服务应用程序打开 PowerPivot 管理面板。  
  
##  <a name="items"></a> “面板”各个部分的概述  
 PowerPivot 管理面板包含用于深化到特定信息类别的 Web 部件和嵌入式报表。 下面的列表介绍面板的每个部分：  
  
|面板|Description|  
|---------------|-----------------|  
|基础结构 - 服务器运行状况|显示 CPU 使用情况、内存消耗量和查询响应时间随时间推移而变化的趋势，以便您可以评估系统资源是接近最大容量还是未充分利用。|  
|操作|包含指向管理中心中其他页的链接，包括当前服务应用程序、服务应用程序的列表和使用情况日志记录。|  
|工作簿活动 - 图表|有关数据访问频率的报表。 您可以了解每天或每周与 PowerPivot 数据源建立连接的频率。|  
|工作簿活动 - 列表|有关数据访问频率的报表。 您可以了解每天或每周与 PowerPivot 数据源建立连接的频率。|  
|数据刷新 - 最近的活动|有关数据刷新作业（包括运行失败的作业）的状态的报表。 此报表针对在应用程序级别执行的数据刷新操作提供了一个组合视图。 管理员可以快速查看为整个 PowerPivot 服务应用程序定义的数据刷新作业的数目。|  
|数据刷新 - 最近的失败|列出未成功完成数据刷新的 PowerPivot 工作簿。|  
|报表|包含指向可以在 Excel 中打开的报表的链接。|  
  
##  <a name="open"></a> 打开 PowerPivot 管理面板  
 面板中一次显示一个 PowerPivot 服务应用程序的信息。 您可以从两个不同的位置打开管理面板。  
  
### <a name="open-the-dashboard-from-general-application-settings"></a>从“常规应用程序设置”打开面板  
  
1.  在管理中心的 **“常规应用程序设置”** 组中，单击 **“PowerPivot 管理面板”**。  
  
2.  在主页上，选择您要查看其操作数据的 PowerPivot 服务应用程序。  
  
### <a name="open-the-dashboard-from-a-powerpivot-service-application"></a>从 PowerPivot 服务应用程序中打开该面板  
  
1.  在管理中心的 **“应用程序管理”** 中，单击 **“管理服务应用程序”**。  
  
2.  单击 PowerPivot 服务应用程序的名称。 PowerPivot 管理面板显示当前服务应用程序的操作数据。  
  
### <a name="change-the-current-service-application"></a>更改当前服务应用程序。  
 在管理面板中更改当前 PowerPivot 服务应用程序：  
  
1.  在 PowerPivot 管理面板顶部，记下名称的当前服务应用程序，例如**默认 PowerPivot 服务应用程序**。  
  
2.  在 **“操作”** 面板中单击 **“列出服务应用程序”**。  
  
3.  单击要查看管理面板报表的 PowerPivot 服务应用程序的名称。  
  
##  <a name="sourcedata"></a> 面板中的源数据  
 面板、报表和 Web 部件显示的数据来自于一个内部数据模型，而该数据模型则从系统和 PowerPivot 应用程序数据库请求这些数据。 这个内部数据模型嵌入在一个承载于管理中心站点的 PowerPivot 工作簿中。 该数据模型的结构是固定的。 虽然可以使用 PowertPivot 工作簿作为数据源来创建新报表，但您不得以破坏使用该数据源的预定义报表的方式修改结构。  
  
 有关如何收集数据的详细信息，请参阅以下主题：  
  
-   [PowerPivot 使用情况数据集合](power-pivot-usage-data-collection.md)  
  
-   [配置使用情况数据收集&#40;PowerPivot for SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
 为了捕获有关 PowerPivot 服务器系统的数据，请验证为每个 PowerPivot 服务应用程序启用了事件消息传递、数据刷新历史记录和其他使用情况历史记录。 在服务器正常操作过程中收集的服务器和使用情况数据是最终完成此内部数据模型的源数据。 **注意：** 如果您关闭事件或使用情况历史记录，则组合报表将不完整或出错。  
  
##  <a name="edit"></a> 编辑 PowerPivot 面板  
 如果您具有面板开发或自定义方面的专业知识，则可以编辑此面板以加入新的 Web 部件。 还可以编辑包含在面板中的 Web 部件属性。  
  
##  <a name="reports"></a> 为 PowerPivot 管理面板创建自定义报表  
 出于报告目的，PowerPivot 使用情况数据和历史记录保留在一个与面板一起创建和配置的内部 PowerPivot 工作簿中。 如果默认报表未提供所需信息，您可以在 Excel 中基于该工作簿创建自定义报表。 如果您以后升级或卸载 PowerPivot 解决方案文件，该工作簿和您创建的任何自定义报表都会保留。 工作簿和报表存储在管理中心站点的 PowerPivot 管理库中。 默认情况下此库不可见，但您可以使用“网站操作”下的“查看所有网站内容”操作来查看此库。  
  
 为帮助开始进行自定义报表制作，PowerPivot 管理面板提供了一个 Office 数据连接 (.odc) 文件连接到源工作簿。 例如，您可以在 Excel 中使用 .odc 文件来创建其他报表。  
  
> [!NOTE]  
>  编辑文件以尝试使用在 Excel 中的.odc 文件时出现以下错误："数据源初始化失败"。 自动生成的 .odc 文件包含 MSOLAP OLE DB 访问接口不支持的一个参数。 以下说明介绍了用于删除这些参数的办法。  
  
 您必须是场或服务管理员，才能生成基于管理中心内的 PowerPivot 工作簿的报表。  
  
1.  打开 PowerPivot 管理面板。  
  
2.  滚动到页底部的 **“报表”** 部分。  
  
3.  单击 **“PowerPivot 管理数据”**。  
  
4.  将 .odc 文件保存到本地文件夹。  
  
5.  在文本编辑器中打开 .odc 文件。  
  
6.  在 `<odc:ConnectionString>` 元素中，滚动至行尾并删除 `Embedded Data=False`，然后删除 `Edit Mode=0`。 如果字符串中的最后一个字符为分号，则立即删除它。  
  
7.  保存文件。 其余步骤取决于您使用的 PowerPivot 和 Excel 的版本。  
  
8.  1.  启动 Excel 2013  
  
    2.  在 **PowerPivot** 功能区中，单击 **“管理”**。  
  
    3.  单击 **“获取外部数据”** ，然后单击 **“现有连接”**。  
  
    4.  如果看到 .ODC 文件，请单击它。 如果看不到 .ODC 文件，请单击 **“浏览更多”** ，然后在文件路径中指定 .odc 文件。  
  
    5.  单击 **“打开”**。  
  
    6.  单击 **“测试连接”** 以验证连接成功。  
  
    7.  单击键入连接的名称，然后单击 **“下一步”**。  
  
    8.  在指定 MDX 查询中，单击**设计**以打开 MDX 查询设计器以组合您要使用的数据**如果你看到错误消息**"编辑模式的属性名称格式不正确。"，验证你的编辑。ODC 文件。  
  
    9. 单击 **“确定”** ，然后单击 **“完成”**。  
  
    10. 创建数据透视表或数据透视图报表以便在 Excel 中直观显示数据。  
  
9. 1.  启动 Excel 2010。  
  
    2.  在 PowerPivot 功能区中，单击 **“启动 PowerPivot 窗口”**。  
  
    3.  在 PowerPivot 窗口的“设计”功能区中，单击 **“现有连接”**。  
  
    4.  单击 **“浏览更多”**。  
  
    5.  在文件路径中，指定 .odc 文件。  
  
    6.  单击 **“打开”**。 此时，将使用指向包含使用情况数据的 PowerPivot 工作簿的连接字符串启动“表导入向导”。  
  
    7.  单击 **“测试连接”** 以确认您具有访问权限。  
  
    8.  输入连接的友好名称，然后单击 **“下一步”**。  
  
    9. 在“指定 MDX 查询”中，单击 **“设计”** 打开 MDX 查询设计器以组合您要使用的数据，然后创建数据透视表或数据透视图报表以便在 Excel 中直观显示数据。  
  
## <a name="see-also"></a>请参阅  
 [使用 SharePoint 2010 的 PowerPivot 数据刷新](../powerpivot-data-refresh-with-sharepoint-2010.md)   
 [配置使用情况数据收集&#40;PowerPivot for SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  

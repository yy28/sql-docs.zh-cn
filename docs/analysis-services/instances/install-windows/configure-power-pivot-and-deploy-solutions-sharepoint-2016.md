---
title: "配置 Power Pivot 和部署解决方案 (SharePoint 2016) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 18a48995-639f-4782-8b17-6caa5769bb5f
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b0e3fa74aed98e00a64a155a8fb43d2cc6db3e1f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="configure-power-pivot-and-deploy-solutions-sharepoint-2016"></a>配置 Power Pivot 和部署解决方案 (SharePoint 2016)
  本主题介绍如何部署和配置 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 中 [!INCLUDE[SPS2016](../../../includes/sps2016-md.md)] 功能的中间层增强功能，包括 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 库、计划数据刷新、管理面板和数据提供程序。 运行 **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2016 配置** 工具以便完成以下任务：  
  
-   部署 SharePoint 解决方案文件。  
  
-   创建 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务应用程序。  
  
-   有关后端服务和在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 模式下安装 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务器的信息，请参阅 [在 PowerPivot 模式下安装 Analysis Services](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)。  
  
 有关安装信息[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]for SharePoint 2016 配置工具，请参阅[安装或卸载 Power Pivot for SharePoint 外接程序 (SharePoint 2016)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016.md)。  
  
 本主题包含以下各节：  
  
 [运行 Power Pivot for SharePoint 2016 配置](#bkmk_run_configuration_tool)  
  
 [验证 Power Pivot 配置](#bkmk_verify_powerpivot)  
  
 [解决问题](#bkmk_troubleshoot_issues)  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2016|  
  
##  <a name="bkmk_run_configuration_tool"></a> 运行 Power Pivot for SharePoint 2016 配置  
 **注意：** 若要完成下列步骤，您必须是场管理员。 如果您看到与以下内容类似的错误消息：  
  
-   “该用户不是场管理员。 请解决验证问题并重试。”  
  
 以安装了 SharePoint 的帐户登录或将安装帐户配置为 SharePoint 管理中心网站的主管理员。  
  
1.  在“开始”菜单中，选择“所有程序”，然后依次选择 [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]、“配置工具”和“[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] For SharePoint 2016 配置”。 只有在本地服务器上安装了 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 后，才会列出工具。  
  
2.  选择“配置或修复 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint”，然后选择“确定”。  
  
3.  该工具将运行验证以验证 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 的当前状态和完成配置所需的步骤。 将窗口放大为实际大小。 您应该在该窗口的底部看到一个菜单栏，其中包含 **“验证”**、 **“运行”**和 **“退出”** 命令。  
  
4.  在 **“参数”** 选项卡上：  
  
    1.  **默认帐户用户名**：输入默认帐户的域用户帐户。 此帐户将用于设置服务，包括 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务应用程序池。 不要指定 Network Service 或 Local System 之类的内置帐户。 该工具将阻止指定内置帐户的配置。  
  
    2.  **数据库服务器**：您可以使用 SharePoint 场支持的 SQL Server 数据库引擎。  
  
    3.  **通行短语**：输入密码。 如果您在创建新的 SharePoint 场，则在您向该 SharePoint 场中添加新的服务器或应用程序时，将使用该通行短语。 如果该场已存在，则输入允许您向该场添加服务器应用程序的通行短语。  
  
    4.  在左窗口中单击 **“创建网站集”** 。 请注意 **“网址 URL”** ，以便您可以在后面的步骤中引用它。 如果 SharePoint 服务器尚未配置，则配置向导默认使用 Web 应用程序，并且将网站集 URL 默认为 `http://[ServerName]`的根。 若要修改这些默认设置，请在左窗口中查看以下页： **“创建默认的 Web 应用程序”** 和 **“部署 Web 应用程序解决方案”**。  
  
5.  或者，查看用于完成各操作的剩余输入值。 单击左窗口中的每个操作以查看操作的详细信息。 有关每个输入值的详细信息，请参阅本主题中 [配置或修复 Power Pivot for SharePoint 2010（Power Pivot 配置工具）](http://msdn.microsoft.com/en-us/d61f49c5-efaa-4455-98f2-8c293fa50046) 中的“用于配置服务器的输入值”部分。  
  
6.  您还可以删除不想在此时处理的任何操作。 例如，如果你想要在以后配置 Secure Store Service，请选择“配置 Secure Store Service” ，然后取消选中“在任务列表中包括此操作” 复选框。  
  
7.  选择“验证”  以便检查该工具是否有足够的信息来处理列表中的操作。 如果看到验证错误，请单击左窗格中的警告查看验证错误的详细信息。 更正任何验证错误，然后再次选择“验证”  。  
  
8.  选择“运行”  来处理该任务列表中的所有操作。 请注意， **“运行”** 将在您验证操作之后才可用。 如果“运行”  未启用，请首先选择“验证”  。  
  
 有关详细信息，请参阅 [配置或修复 Power Pivot for SharePoint 2010（Power Pivot 配置工具）](http://msdn.microsoft.com/en-us/d61f49c5-efaa-4455-98f2-8c293fa50046)  
  
##  <a name="bkmk_verify_powerpivot"></a> 验证 Power Pivot 配置  
 **服务：**  
  
1.  在管理中心的“系统设置”中，选择“管理服务器上的服务” 。  
  
2.  确认“SQL Server [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 系统服务”已启动。  
  
 **场功能：**  
  
1.  在管理中心的“系统设置”中，选择“管理场功能” 。  
  
2.  验证 **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 集成功能**状态为“活动”。  
  
 **网站集功能：**  
  
1.  浏览到您通过使用配置工具创建的网站 URL。  
  
     选择**设置**![SharePoint 设置](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 设置")，然后单击**站点设置**。  
  
     选择“网站集功能” 。  
  
2.  确认**[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 针对网站集的功能集成**状态为“活动”。  
  
 **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务应用程序：**  
  
1.  在管理中心的“应用程序管理” 中，选择“管理服务应用程序” 。  
  
2.  确认服务应用程序状态为 **“已启动”**。 默认名称为**默认的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务应用程序”**。  
  
     选择服务应用程序的名称以打开服务应用程序，然后打开其 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 管理面板。 第一次使用时，面板要花几分钟的加载时间。  
  
 有关详细信息，请参阅 [Verify a Power Pivot for SharePoint Installation](../../../analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md)。  
  
##  <a name="bkmk_troubleshoot_issues"></a> 解决问题  
 为了协助解决问题，最好验证诊断日志记录已启用。  
  
1.  在 SharePoint 管理中心中，单击“监视”  ，然后选择“配置使用情况和运行状况数据收集” 。  
  
2.  确认选择了 **“启用使用情况数据收集”** 。  
  
3.  验证是否选择了以下事件：  
  
    -   针对教育遥测的使用情况字段的定义  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 连接  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 加载数据使用情况  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 查询使用情况  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 卸载数据使用情况  
  
4.  确认选择了 **“启用运行状况数据收集”** 。  
  
5.  选择“确定”。  
  
 有关解决数据刷新问题的详细信息，请参阅[解决 Power Pivot 数据刷新问题](http://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx) (http://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx)。  
  
 有关配置工具的详细信息，请参阅 [Power Pivot Configuration Tools](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)。  
  
  

---
title: 新的订阅或编辑订阅页 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: e02d6529-ce67-4305-b7f0-433997e99c21
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a6194516bfc230c73df928bda5095c106776beff
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56030128"
---
# <a name="new-subscription-or-edit-subscription-page-report-manager"></a>“新建订阅”或“编辑订阅”页（报表管理器）
  使用“新建订阅”或“编辑订阅”页，可为报表创建新订阅或修改报表的现有订阅。 此页包含的选项取决于您的角色分配。 具有高级权限的用户可以使用附加选项。  
  
 以无人参与的方式运行的报表支持订阅。 报表必须最起码使用已存储的凭据或不使用凭据。 如果报表使用参数，则必须指定默认值。 如果更改报表执行设置或删除参数属性使用的默认值，订阅可能进入非活动状态。 有关详细信息，请参阅 [创建和管理本机模式报表服务器的订阅](../../2014/reporting-services/create-manage-subscriptions-native-mode-report-servers.md)。  
  
> [!NOTE]  
>  并非在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的每个版本中均提供此功能。 有关的各版本支持的功能列表[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请参阅[SQL Server 2014 各个版本支持的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
### <a name="to-open-the-new-subscription-or-edit-subscription-page"></a>打开“新建订阅”或“编辑订阅”页  
  
1.  打开报表管理器，找到要添加订阅的报表。  
  
2.  悬停在该报表之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，执行以下步骤之一：  
  
    -   单击 **“管理”**。 这会打开该报表的“常规”属性页。 然后，选择 **“订阅”** 选项卡。在工具栏中，单击 **“新建订阅”** 或选择要编辑的现有订阅并单击 **“编辑”**。  
  
    -   单击 **“订阅”**。 这会打开该报表的 **“新建订阅”** 页。  
  
## <a name="options"></a>选项  
 **传递方式**  
 选择用于分发报表的传递扩展插件。 根据选定的传递扩展插件，会显示下列设置：  
  
-   电子邮件订阅提供了电子邮件用户所熟悉的字段（例如， **“收件人”**、 **“主题”** 和 **“优先级”** 字段）。 指定 **“包括报表”** 可以嵌入或附加报表，而指定 **“包括链接”** 可以将 URL 包括在报表中。 指定 **“呈现格式”** 可以选择附加报表或嵌入报表的显示格式。  
  
-   文件共享订阅提供了允许您指定目标位置的字段。 您可以将任何报表传递到文件共享位置。 但是，支持交互式功能的报表（包括支持深化以及支持行和列的矩阵报表）将以静态文件的形式呈现。 无法查看静态文件中的深化行和深化列。 必须以通用命名约定 (UNC) 格式指定文件共享名 (例如， \\\mycomputer\public\myreportfiles)。 不能在路径名的末尾包含反斜杠。 报表文件将以基于呈现格式的文件格式进行传递（例如，如果选择 **Excel**，则报表以 .xls 文件格式进行传递）。  
  
 传递扩展插件的可用性取决于其是否在报表服务器上进行了安装和配置。 报表服务器电子邮件是默认的传递扩展插件，但是使用前必须先行配置。 文件共享传递不需要配置，但是使用前必须定义一个共享文件夹。  
  
## <a name="subscription-processing-options"></a>订阅处理选项  
 使用这些设置可以定义导致处理订阅的条件。 某些选项仅可用于使用参数的报表或作为报表执行快照运行的报表。  
  
 **刷新报表内容时**  
 选择此选项可以订阅定期刷新的报表快照。 只有在订阅作为报表执行快照运行的报表时才显示此选项。 报表执行快照的内容通常定期刷新。 对于以此模式运行的报表，可以定义在刷新快照时进行订阅。  
  
 **预定的报表运行何时完成**  
 创建计划以确定何时处理订阅。  
  
 **根据共享计划**  
 选择处理订阅的预定义计划。  
  
 **输入参数值**  
 如果订阅具有参数的报表，请使用此选项。 此选项仅可用于参数化报表。 订阅参数化报表时，可以指定一些参数值，用于创建通过订阅传递的报表版本。 例如，您可以指定区域代码以选择特定区域的销售数据。 如果不指定值，将使用默认值。  
  
## <a name="see-also"></a>请参阅  
 [为电子邮件传递配置报表服务器&#40;SSRS 配置管理器&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)   
 [报表管理器（SSRS 本机模式）](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [创建、修改和删除计划](subscriptions/create-modify-and-delete-schedules.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)  
  
  

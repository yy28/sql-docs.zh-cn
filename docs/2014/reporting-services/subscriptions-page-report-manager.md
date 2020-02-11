---
title: 订阅页（报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: cf3a6bd0-e0b2-4875-a532-63ef34cfa860
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eec92d7c58b68b14374666f65489f145fa863422
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66101088"
---
# <a name="subscriptions-page-report-manager"></a>“订阅”页（报表管理器）
  使用“订阅”页可以列出当前报表或共享数据源的所有订阅。 如果有足够的权限（指“管理所有订阅”任务），则可以查看所有用户的订阅。 否则，此页仅显示您所拥有的订阅。  
  
> [!NOTE]  
>  其他页也包含订阅信息。 有关详细信息，请参阅["我的订阅" 页 &#40;报表管理器&#41;](../../2014/reporting-services/my-subscriptions-page-report-manager.md)在一个位置访问所有订阅，或者在 "新建订阅"[或 "编辑订阅" 页 &#40;报表管理器&#41;](../../2014/reporting-services/new-subscription-or-edit-subscription-page-report-manager.md)创建或编辑订阅。  
  
 某些选项只有在存在要处理的现有订阅时才可见。 如果在没有定义任何订阅的情况下从报表访问此页，则此页上仅显示 **“新建订阅”** 和 **“新建数据驱动订阅”** 选项。  
  
 必须确认报表数据源使用的是存储凭据，才能创建新订阅。 使用“数据源”属性页可以存储凭据。 有关详细信息，请参阅 "[数据源属性" 页 &#40;报表管理器&#41;](../../2014/reporting-services/data-sources-properties-page-report-manager.md)。  
  
> [!NOTE]  
>  并非在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的每个版本中均提供此功能。 有关各个版本支持的功能列表[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请参阅 SQL Server 2014 的各个[版本支持的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
### <a name="to-open-the-subscriptions-page-for-report"></a>打开报表的“订阅”页  
  
1.  打开报表管理器，找到您要查看或配置订阅的报表。  
  
2.  悬停在该报表之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“管理”** 。 这会打开该报表的“常规”属性页。  
  
4.  选择 **“订阅”** 选项卡。  
  
## <a name="options"></a>选项  
 **删除**  
 单击此选项可删除订阅。 删除订阅之前，必须选中要删除的每个订阅旁边的复选框。  
  
 **新订阅**  
 单击此选项可创建当前报表的新订阅。 此按钮在报表使用存储的凭据或不使用凭据时启用。 当通过共享数据源打开订阅页时，此按钮不可用。  
  
 **“新建数据驱动订阅”**  
 单击此选项可通过命令或查询针对包含此信息的数据存储区生成订阅服务器列表和传递选项。 此按钮在报表使用存储的凭据或不使用凭据时启用。 当通过共享数据源打开订阅页时，此按钮不可用。  
  
 **编辑**  
 单击此选项可查看或编辑说明。  
  
 **报告**  
 从共享数据源打开此页时，此列标识为其定义了订阅的报表。 
  **“文件夹”** 列用于标识报表位置。  
  
 **说明**  
 显示订阅的说明。  
  
 **界限**  
 标识导致订阅运行的条件。 
  **TimedSubscription** 触发器基于定义订阅运行时间的计划。 
  **SnapshotUpdated** 触发器基于对报表快照的更新操作。  
  
 **所有者**  
 显示创建订阅的用户的名称。  
  
 **上次运行时间**  
 显示上次处理订阅的时间。  
  
 **Status**  
 显示订阅的状态。 通常，状态值为“新建”或订阅上次运行的日期和时间。  
  
 当订阅包括指向不再有效的加密值（即指向用于运行报表的已存储凭据）的指针时，将出现“错误数据”状态值。 在报表服务器上重新创建用于对数据进行加密和解密的对称密钥后，现有的加密值将无法使用。  
  
 如果订阅已停用，将无法对其进行处理。 若要更新订阅并使其可操作，请先打开订阅，然后保存即可。  
  
## <a name="see-also"></a>另请参阅  
 [报表管理器（SSRS 本机模式）](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [在纯模式下创建、修改和删除标准订阅 &#40;Reporting Services&#41;](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [创建、修改和删除计划](subscriptions/create-modify-and-delete-schedules.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)  
  
  

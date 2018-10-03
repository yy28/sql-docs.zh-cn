---
title: 快照选项属性页 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f6641f59-5267-4f57-8957-63b93d1a9679
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4342504d0d62f2c611c680c58fcdeae1f046f29b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078097"
---
# <a name="snapshot-options-properties-page-report-manager"></a>“快照选项”属性页（报表管理器）
  使用“快照选项”属性页可以计划将报表快照添加到报表历史记录的时间，以及设置报表历史记录中存储的报表快照的数量限制。  
  
> [!NOTE]  
>  并非在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的每个版本中均提供此功能。 有关的各版本支持的功能列表[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请参阅[其他数据库服务](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md#Add_DBServices)。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
### <a name="to-open-the-snapshot-options-properties-page-for-a-report"></a>打开报表的“快照选项”属性页  
  
1.  打开报表管理器，找到您要配置报表快照属性的报表。  
  
2.  悬停在该报表之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“管理”**。 这会打开该报表的“常规”属性页。  
  
4.  选择 **“快照选项”** 选项卡。  
  
## <a name="options"></a>选项  
 **允许手动创建报表历史记录**  
 选中此复选框可以根据需要将快照添加到报表历史记录中。 选中此复选框后，“历史记录”页上将显示 **“新建快照”** 按钮。  
  
 **在报表历史记录中存储所有报表执行快照**  
 选中此复选框可以根据报表执行属性将您生成的报表快照添加到报表历史记录中。 您可以设置报表执行属性以便从生成的快照运行报表。 设置此报表历史记录属性后，您可以将一段时间内生成的所有报表快照的副本放置在报表历史记录中，以跟踪这些报表快照。  
  
 **使用以下计划将快照添加到报表历史记录**  
 选中此复选框可以按计划将快照添加到报表历史记录中。 您可以创建专门用于此用途的计划，也可以选择包含您所需的计划信息的预定义共享计划。  
  
 **选择要保留快照的数**  
 从以下选项中进行选择，以控制保留在报表历史记录中的报表数。 各个报表的报表历史记录设置可以不同。  
  
-   选择 **“使用默认设置”** 可以保留默认设置。 报表服务器管理员控制报表历史记录存储的主设置。 如果选择此选项，将从该主设置获取保留的快照数。  
  
-   选择 **“不限制报表历史记录中保留的快照数”** 可以保留所有的报表历史记录快照。 要减少报表历史记录的大小，必须手动删除快照。  
  
-   选择 **“限制报表历史记录的副本数”** 可以保留设定数量的快照。 到达限制后，将从报表历史记录中删除较旧的副本以便为新副本腾出空间。  
  
 报表历史记录存储在报表服务器数据库中。 如果要保留大型报表或许多报表的历史记录，请考虑限制报表历史记录的量，以帮助管理报表服务器数据库的磁盘空间要求。  
  
 **应用**  
 单击此选项可保存所做的更改。  
  
## <a name="see-also"></a>请参阅  
 [将快照添加到报表历史记录&#40;报表管理器&#41;](report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [报表管理器&#40;SSRS 本机模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [创建、 修改和删除报表历史记录中的快照](report-server/create-modify-and-delete-snapshots-in-report-history.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)  
  
  

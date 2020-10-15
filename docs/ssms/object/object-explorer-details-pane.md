---
description: 对象资源管理器详细信息窗格
title: 对象资源管理器详细信息窗格
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.summary.general.f1
- sql13.swb.summary.report.f1
helpviewer_keywords:
- object search [SQL Server], Object Explorer
- Object Explorer
- object search [SQL Server]
- searching objects [SQL Server]
ms.assetid: b963e3c2-dc9e-4d38-bd28-2e00fe9e0e47
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 846c2707e5fe04e080460241e41df0ebf7ec8329
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037184"
---
# <a name="object-explorer-details-pane"></a>对象资源管理器详细信息窗格
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
对象资源管理器详细信息是 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的一个组件，它提供服务器中所有对象的表格视图，并显示一个用于管理这些对象的用户界面。 对象资源管理器的功能根据服务器的类型稍有不同，但一般都包括用于数据库的开发功能和用于所有服务器类型的管理功能。  
  
默认情况下，“对象资源管理器详细信息”窗格在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 是可见的。 如果看不到对象资源管理器，请在“视图”**** 菜单上单击“对象资源管理器详细信息”**** 或按 **F7**。  
  
> [!NOTE]  
> [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 显示的数据采用启动 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 时有效的 Microsoft Windows 的“区域和语言选项”的格式。 重新启动 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 可以反映更新的设置。  
  
## <a name="object-explorer-details"></a>对象资源管理器详细信息  
对象资源管理器详细信息可用于在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的文件夹和对象中导航。 在 32 位操作系统上, 对象资源管理器只能显示 64,000 个对象。 必须选择某个图标才能访问其他对象。  
  
对象资源管理器详细信息包括一个工具栏，其中包含下表中所述的图标。 只有适当的时候这些图标才可用。  
  
|图标|操作|  
|--------|----------|  
|**后退**|移动到对象资源管理器详细信息中显示的前几个项。 如果以前的显示内容是搜索操作的结果，则重新运行搜索。|  
|**前进**|选择“后退”**** 操作后，移动到下一个屏幕。|  
|**Up**|转到父对象或父文件夹。|  
|**同步**|将对象资源管理器的焦点设置为对象资源管理器详细信息中的选定对象。|  
|**筛选器**|如果有，显示对象的可配置子集。|  
|**“刷新”**|刷新对象资源管理器详细信息中的显示内容。|  
|**搜索**|提供一个区域，用于输入某些数据库对象的搜索词。|  
  
### <a name="column-header-selections"></a>列标题选择  
对象资源管理器详细信息具有可选择的列。 您可以右键单击任何列标题并选中希望显示的项。 您的选择将保留在您导航的不同对象上。 当您退出并重新启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]时，会保留每个用户的选择。  
  
> [!CAUTION]  
> 显示某些对象类型（如数据库）的所有列可能导致大型对象集的显示呈现略微减慢。  
  
### <a name="sorting"></a>排序  
单击列标题一次，可按该列进行排序。 再次单击同一个列标题，可按该列进行反向排序。 对于对象和文件夹范围内的每个用户将保留排序选择，重新启动 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 时也会保留。  
  
### <a name="filtering"></a>Filtering  
可以使用对象资源管理器详细信息工具栏上的“筛选器”**** 图标，筛选对象资源管理器详细信息中显示的某些对象列表。 在可以进行筛选时，将启用该图标。  
  
### <a name="details-pane"></a>“详细信息”窗格  
对象资源管理器详细信息的最底部区域包含一个窗格，用于显示所选对象的某些详细信息。 如果选择多个对象，则只显示对象的计数。 在该窗格中选择项后，单击“复制”**** 图标可将显示的文本复制到剪贴板。  
  
向下箭头键将所选内容移至列表中的下一项。 向上箭头键将所选内容移至列表中的上一项。 按住箭头键将快速通过这些项。 所选内容将停止在属性列表的底部或顶部。  
  
键入属性名称的第一个字符会将所选内容移到以该字符开头的下一属性。  
  
当在多列中排列属性时，使用向左箭头键和向右箭头键可以移到相邻列。  
  
若要将属性值复制到剪贴板中，可以使用以下键盘组合键：  
  
-   Ctrl+C 将复制属性值。  
  
-   Ctrl+Shift+C 复制属性名称和具有 Tab 分隔符的属性值。  
  
在“对象资源管理器详细信息”属性窗格中使用右键单击菜单可以将所有属性或者所有属性和名称复制到剪贴板。  
  
若要在字段宽度无法完全显示某一属性值时显示该属性值，请将属性指针停留在该值上或者将 UI 焦点设置于该属性值以便激活具有整个属性值的工具提示。 当用户以长属性值为焦点时，辅助功能屏幕阅读器将报告完整的属性值。  
  
如果属性窗格中属性的数目超过了在内容区域中适合的数目，一个滚动条将出现在属性窗格的右侧。 使用滚动条可以调整内容区域中属性值的视图。  
  
### <a name="multiple-object-selection"></a>多重对象选择  
对象资源管理器详细信息支持多重对象选择。 例如，如果在对象资源管理器中选择了表，则在“对象资源管理器详细信息”窗口中按住 **Ctrl** 键，即可选择多个表，右键单击这些表，然后选择“删除”**** 或“生成表脚本”****，可立即对所有所选表执行操作。 标准复制命令可将显示的文本复制到剪贴板。  
  
## <a name="sql-server-object-search"></a>SQL Server 对象搜索  
通配符  
  
-   支持标准通配符字符。 例如，搜索 **dm_os%counters** 会返回 dm_os_memory_cache_counters 和 dm_os_performance_counters。 有关详细信息，请参阅 [如何使用通配符搜索](../scripting/search-text-with-wildcards.md)。  
  
搜索范围  
  
-   每次搜索的范围是对象资源管理器树中的当前焦点。 例如，如果对象资源管理器焦点在一个数据库上，则搜索 **dm_os%counters** 会返回该数据库中的 dm_os_memory_cache_counters 和 dm_os_performance_counters。 如果对象资源管理器焦点在“数据库”节点上，则会搜索所有数据库，并返回动态视图的多个实例。  
  
大型集合  
  
-   搜索大型对象集可能需要很长时间，并且会降低服务器性能。  
  
## <a name="see-also"></a>另请参阅  
[对象资源管理器](../../ssms/object/object-explorer.md)  

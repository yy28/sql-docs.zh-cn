---
title: 缓存刷新选项 （报表管理器） |Microsoft 文档
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 227da40c-6bd2-48ec-aa9c-50ce6c1ca3a6
caps.latest.revision: 11
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 5d5a2bd4683e70523275c8da191bc74cd4de28d6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124050"
---
# <a name="cache-refresh-options-report-manager"></a>缓存刷新选项（报表管理器）
  使用“缓存刷新选项”页可以创建使用报表或共享数据集数据的临时副本预加载缓存的计划。 刷新计划包括计划和指定或覆盖参数值的选项。 对于共享数据集，不能覆盖标记为只读的参数值。 在刷新选项页中，可以创建和使用多个刷新计划。  
  
 通过“内容管理员”、“我的报表”和“发布者”默认角色分配，您可以添加、删除、更改和查看缓存刷新计划的相关报表和共享数据集。  
  
> [!NOTE]  
>  并非在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的每个版本中均提供此功能。 有关支持的版本的功能的列表[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请参阅[支持的 SQL Server 2014 的版本功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="to-open-the-cache-refresh-plan-properties-page-for-a-report-or-shared-dataset"></a>打开报表或共享数据集的“缓存刷新计划”属性页  
  
1.  打开报表管理器，找到您要配置缓存刷新计划属性的报表或共享数据集。  
  
2.  悬停在该报表或共享数据集之上，然后单击下拉箭头。  
  
3.  在下拉列表中，单击 **“管理”**。 此时，将打开 **“常规”** 属性页。  
  
4.  单击 **“缓存刷新计划”** 选项卡。  
  
5.  若要创建新的缓存计划，请单击 **“新建缓存刷新计划”**。  
  
    > [!NOTE]  
    >  必须启用并启动 SQL Server 代理服务，才能创建缓存刷新计划。  
  
6.  若要创建缓存计划的副本然后对其自定义，请单击 **“根据现有内容新建”**。  
  
## <a name="cache-refresh-options"></a>缓存刷新选项  
 **删除**  
 删除所有当前所选的刷新计划。  
  
 **从现有新**  
 仅当选择一个缓存刷新计划时启用此选项。 此选项将创建一个新的刷新计划，该计划是从原始计划复制而来。 将打开缓存刷新计划页，其中预先填充了所选计划的详细信息。 然后，您可以修改刷新计划选项并用新说明保存该计划。  
  
 **新的缓存刷新计划**  
 单击以创建要在当前缓存刷新选项中使用的新刷新计划。  
  
 **编辑**  
 选择此选项可以编辑当前刷新计划。  
  
## <a name="cache-refresh-plan-options"></a>缓存刷新计划选项  
 **Description**  
 指定缓存刷新计划的说明。  
  
 **特定于项的计划**  
 选择此选项可以创建仅供此项使用的计划。  
  
 **配置**  
 单击此选项可打开用于指定频率信息的“计划”页。  
  
 有关详细信息，请参阅[新计划： 编辑计划页&#40;报表管理器&#41;](../../2014/reporting-services/new-schedule-edit-schedule-page-report-manager.md)。  
  
 **共享的计划**  
 选择此选项可以选择现有计划。  
  
 有关详细信息，请参阅[Create，Modify，and Delete Schedules](subscriptions/create-modify-and-delete-schedules.md)。  
  
 **@\<** *参数* **>**  
 指定参数值的一个组合。 只有在当前数据集或报表有参数时，才会显示此部分。  
  
 请参阅下一节中的 [指定参数](#Parameters) 。  
  
 **使用默认值**  
 选择此选项可以使用此参数的预定义默认值。  
  
##  <a name="Parameters"></a> 指定参数  
 若要创建缓存刷新计划，每个报表或共享数据集参数必须赋值。 如果报表或共享数据集项在定义中未指定默认值，您必须指定一个值。 如果默认值存在，则不需要在此处提供值。 如果提供了值，该值将覆盖默认值。  
  
 若要指定参数值的多个组合，请为每个组合创建单独的缓存刷新计划。  
  
 如果对报表或共享数据集的参数进行添加、更改和删除，将会影响缓存刷新计划。 如果为报表添加具有默认值的参数、删除参数或更改共享数据集参数的数据类型或只读选项，所做的更改将在下次处理缓存刷新计划时生效。  
  
### <a name="shared-dataset-parameters"></a>共享数据集参数  
 对于共享数据集，以下信息是从共享数据集定义派生的：  
  
-   **名称** ：指定查询参数的名称。  
  
-   **类型** ：指定查询参数的数据类型。 由于此数据类型在数据访问接口处理数据集查询前是未知的，直到处理共享数据集时才进行数据类型验证。  
  
-   **可以为 Null** ：指定 NULL 是否是有效值。  
  
-   **只读** ：指定此参数是否在共享数据集定义中被标记为只读。 只读参数不会出现在缓存刷新选项的参数列表中，在共享数据集定义中必须为其指定默认值。  
  
-   **默认值** ：在共享数据集定义中指定的默认值。 查询参数可以是多值的。 若要覆盖默认值，请在文本框提示区域中键入新值。  
  
 如果共享数据集定义中为参数指定了 **“从查询中省略”** 选项，则不必提供默认值。 此标志表示不在查询中使用数据集参数。 例如，该参数出现在共享数据集定义中，因为它是仅在数据集筛选器中使用的报表参数。  
  
 若要查看或更改数据集参数选项，必须编辑共享数据集定义。 有关详细信息，请参阅[管理共享数据集](report-data/manage-shared-datasets.md)。  
  
### <a name="report-parameters"></a>报表参数  
 对于报表，在成功创建一个缓存刷新计划前，每个参数值必须是有效的。 必须键入或选择每个报表参数的默认值。 您设置的值将覆盖在报表服务器上定义的报表参数默认值。  
  
 参数必须符合在报表服务器上的参数属性中指定的要求。 例如，如果属性 AllowBlank 为报表参数为 false，空字符串不是有效的值。  
  
 若要查看或更改报表参数选项，必须在报表中编辑报表参数，或在报表服务器上独立编辑。 有关详细信息，请参阅[报表参数概念&#40;报表生成器和 SSRS&#41;](report-design/report-parameters-concepts-report-builder-and-ssrs.md)。  
  
## <a name="conditions-that-cause-a-cache-refresh-plan-to-be-inactive"></a>导致缓存刷新计划处于非活动状态的情况  
 下列情况可能导致共享数据集或报表缓存刷新计划处于非活动状态。  
  
-   共享数据集缓存或报表缓存选项被禁用。  
  
-   所需的参数值没有定义、无效或缺失。 在处理报表前，报表的所有查询都必须有效。 对于具有子报表的报表，首先处理所有数据集查询（包括子报表的数据集）。 如果存在无法成功处理的数据集，报表将无法运行。  
  
## <a name="conditions-that-cause-a-cache-refresh-plan-to-be-reactivated"></a>导致缓存刷新计划重新激活的情况  
 计划处于非活动状态后，执行以下操作之一可以触发缓存刷新计划的评估：  
  
-   更改计划的选项。  
  
-   启用与刷新计划关联的共享数据集或报表的缓存。  
  
-   清除或选择与刷新计划关联的数据集查询参数的只读选项，然后将新的定义保存到报表服务器。  
  
## <a name="see-also"></a>请参阅  
 [项级任务](security/tasks-and-permissions-item-level-tasks.md)   
 [报表管理器&#40;SSRS 本机模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)   
 [缓存报表 (SSRS)](report-server/caching-reports-ssrs.md)   
 [管理共享数据集](report-data/manage-shared-datasets.md)  
  
  
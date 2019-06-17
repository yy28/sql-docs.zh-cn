---
title: 查看或更改收集组计划 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.dc.collectionsetprop.uploads.f1
- sql13.swb.dc.collectionsetprop.description.f1
- sql13.swb.dc.collectionsetprop.general.f1
helpviewer_keywords:
- collection sets [SQL Server], changing schedules
- schedules [SQL Server], changing collection set
- collection sets [SQL Server], viewing schedules
- schedules [SQL Server], viewing collection set
ms.assetid: 26336c98-78c5-414f-8d6a-574fc3af60c4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 328786411c61c5d92d25786b05dacb907b17114a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62645490"
---
# <a name="view-or-change-collection-set-schedules-sql-server-management-studio"></a>查看或更改收集组计划 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]查看或更改收集组计划。  
  
 收集模式（缓存或非缓存）决定变更计划的方式。 缓存模式使用不同的计划进行收集和上载。 非缓存模式使用同一计划进行收集和上载。 每个系统数据收集组的收集模式类型如下：  
  
-    “磁盘使用情况”使用非缓存收集模式。  
  
-   **“查询统计信息”** 使用缓存收集模式。  
  
-   **“服务器活动”** 使用缓存收集模式。  
  
### <a name="to-view-collection-set-schedules"></a>查看收集组计划  
  
1.  在对象资源管理器中，依次展开 **“管理”** 节点、 **“数据收集”** 和 **“系统数据收集组”** 。  
  
2.  右键单击收集组名称，然后单击“属性”[以便打开](#CollectionSet)“数据收集组属性”对话框。   
  
### <a name="to-change-the-schedules-for-a-cached-mode-collection-set"></a>更改缓存模式收集组的计划  
  
1.  在对象资源管理器中，依次展开 **“管理”** 节点、 **“数据收集”** 和 **“系统数据收集组”** 。  
  
2.  右键单击使用缓存模式的收集组（如“查询统计信息”），然后单击“属性”以便打开“[数据收集组属性](#CollectionSet)”对话框。    
  
3.  可以在 **“常规”** 页上更改收集频率。 为此，请按照下列步骤进行操作：  
  
    1.  在详细信息窗格中，双击  “收集项”表中的**Collection items**“收集频率(秒)”列中显示的数字。  
  
    2.  若要提高或降低收集频率，请键入一个更小或更大的数字，然后按 Enter 存储这个新值。  
  
4.  若要更改收集组的现有上载计划，请按照下列步骤进行操作：  
  
    1.  单击 **“上载”** 页。  
  
    2.  在详细信息窗格中，单击 **“选取”** 。  
  
         将打开 **“为作业选取计划”** 对话框。 可用的计划以表的形式出现。  
  
    3.  单击包含所需计划的行。 例如，若要将计划更改为每隔 5 分钟运行一次，请单击其中的计划名称为 **CollectorSchedule_Every_5min**的行。  
  
        > [!NOTE]  
        >  可以单击 **“属性”** 打开选定计划的 **“作业计划属性”** 对话框，以查看和编辑该计划的属性。 可使用此对话框来更改计划信息，例如频率。  
        >   
        >  除了修改现有计划外，还可以通过单击 **“上载”** 页上的 **“新建”** 来创建新的上载计划。 此操作将打开 **“新建作业计划”** 对话框，可使用该对话框来创建自定义计划。  
  
    4.  完成对该计划的配置后，请单击 **“确定”** 。  
  
         您所做的更改将出现在 **“上载”** 页上。  
  
5.  单击 **“确定”** 以保存对收集频率和上载计划所做的更改，并关闭 **“数据收集组属性”** 对话框。  
  
### <a name="to-change-the-schedule-for-a-non-cached-mode-collection-set"></a>更改非缓存模式收集组的计划  
  
1.  在对象资源管理器中，依次展开 **“管理”** 节点、 **“数据收集”** 和 **“系统数据收集组”** 。  
  
2.  右键单击使用非缓存模式的收集组（如  “磁盘使用情况”），然后单击  “属性”以便打开[数据收集组属性](#CollectionSet)对话框。  
  
     **“数据收集组属性”** 对话框将显示收集组属性的分页视图。  
  
3.  若要更改该收集组的计划，请单击 **“选取”** 。  
  
     将打开 **“为作业选取计划”** 对话框。 可用的计划以表的形式显示。  
  
4.  单击包含所需计划的行。 例如，若要将计划更改为每隔 5 分钟运行一次，请单击其中的计划名称为 **CollectorSchedule_Every_5min**的行。  
  
    > [!NOTE]  
    >  可以单击 **“属性”** 打开选定计划的 **“作业计划属性”** 对话框，以查看和编辑该计划的属性。 可使用此对话框来更改计划信息，例如频率。  
    >   
    >  除了修改现有计划外，还可以通过单击 **“常规”** 页上的 **“新建”** 来创建新的收集和上载计划。 此操作将打开 **“新建作业计划”** 对话框。  
  
5.  完成对该计划的配置后，请单击 **“确定”** 。  
  
6.  单击 **“确定”** 保存更改并关闭 **“数据收集组属性”** 对话框。  
  
####  <a name="CollectionSet"></a> “数据收集组属性”对话框  
 **“常规”页**  
  
 使用此页可以配置数据的收集和上载方式、配置计划以及配置数据在管理数据仓库中的保持期。 此页还提供了收集组的相关信息，如收集器类型、收集频率以及用于收集组的输入参数。  
  
 **名称**  
 显示此页引用的收集组的名称。  
  
 **数据收集和上载**  
 指定收集数据并将其上载到管理数据仓库的方式。 选取下列选项之一。  
  
|||  
|-|-|  
|**不缓存。按照相同的计划收集和上载数据。**|选择此选项后，请指定以下选项之一：<br /><br /> **计划**。 按计划收集和上载数据。 单击 **“选取”** 可从预定义的计划列表中进行选择，或单击 **“新建”** 创建新计划。<br /><br /> **按需**。 按需收集和上载数据。|  
|**已缓存。按照一组收集频率收集数据并对其进行缓存。按照单独的计划上载缓存的数据。**|按照指定的收集频率收集数据并对其进行缓存。 按照单独的计划上载收集的数据。|  
  
 **收集项**  
 显示收集组中的收集项。 以下是针对每个收集项提供的信息：  
  
-   **名称**  
  
-   **收集器类型**  
  
-   **收集频率** （秒）。 如果将 **“数据收集和上载”** 配置为缓存，则可以编辑此字段。 双击此单元格可设置收集频率。  
  
 **输入参数**  
 显示用于收集组的输入参数。  
  
 **运行身份**  
 指定用来运行收集组的帐户。 默认情况下，此帐户为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户。 如果定义了代理帐户，则此列表中包含可用代理帐户的名称。  
  
 **设置收集的数据将在管理数据仓库中保留的时间。**  
 指定收集的数据保留的时间。 选取下列选项之一。  
  
|||  
|-|-|  
|**数据保留时间**|默认情况下选择此选项，并且默认保持期为 14 天。|  
|**无限期保留数据**|对数据保留的时间长度没有限制。|  
  
 **“上载”页**  
  
 使用此页可以为由此收集组收集的数据配置上载计划。  
  
> [!NOTE]  
>  仅当已为  “数据收集和上传”配置了  “已缓存”选项时才启用此选项卡。  
  
 **Server**  
 显示承载管理数据仓库的服务器的名称。 有关详细信息。请参阅[配置管理数据仓库 (SQL Server Management Studio)](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)。  
  
 **管理数据仓库**  
 显示管理数据仓库的名称。 有关详细信息。请参阅[配置管理数据仓库 (SQL Server Management Studio)](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)。  
  
 **上次上载时间**  
 显示为收集组完成的上次上载的日期和时间信息。  
  
 **上载计划**  
 指定收集组的上载计划。 如果启用，请单击 **“选取”** 从预定义的计划列表中进行选择，或单击 **“新建”** 创建新计划。  
  
 **“说明”页**  
  
 使用此页可以查看此属性页引用的收集组的说明。  
  
## <a name="see-also"></a>另请参阅  
 [管理数据收集](../../relational-databases/data-collection/manage-data-collection.md)   
 [“数据收集”](../../relational-databases/data-collection/data-collection.md)  
  
  

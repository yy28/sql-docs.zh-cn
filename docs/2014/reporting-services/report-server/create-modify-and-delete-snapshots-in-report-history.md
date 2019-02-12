---
title: 创建、修改和删除报表历史记录中的快照 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- snapshots [Reporting Services]
- report snapshots [Reporting Services]
ms.assetid: 5aebbbfa-a8db-462d-8ab9-746fad9525f0
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: c607291cd2675e454861aa4c79da608d8bcaba1b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56010959"
---
# <a name="create-modify-and-delete-snapshots-in-report-history"></a>创建、修改和删除报表历史记录中的快照
  报表历史记录是报表快照的集合。 通过添加和删除快照或修改影响报表历史记录存储的属性，可以对报表历史记录进行维护。 您可以手动或按计划创建报表历史记录。  
  
 若要创建报表历史记录，您的角色分配必须包括“管理报表历史记录”任务。 若要查看报表历史记录，您的角色分配必须包括“查看报表”任务。 报表历史记录对有权访问该报表的所有用户均可用。 不能针对部分用户有选择地启用或禁用报表历史记录。  
  
 报表历史记录中的快照按其创建日期和时间进行标识， 而日期和时间则基于查询的执行时间。  
  
## <a name="creating-snapshots-in-report-history"></a>在报表历史记录中创建快照  
 对于所有可在无人参与情况下运行的报表，可以手动或按计划间隔为其创建快照。 若要在无人参与的情况下运行，报表必须使用已存储凭据或根本不使用凭据。 此外，如果报表使用参数，则必须指定运行报表时所用的默认值。 可以在报表的属性页中指定已存储凭据和参数值。 有关详细信息，请参阅[参数属性页（报表管理器）](../parameters-properties-page-report-manager.md)。  
  
 创建报表快照后，以下元素将随报表快照一起存储在报表服务器数据库中：  
  
-   结果集（即通过报表的“数据源”属性页中指定的凭据检索到的报表数据）。  
  
-   创建快照时的基础报表定义。 如果在生成快照后修改了报表定义，所做更改不会反映在快照中。  
  
-   用于获取或筛选结果集的参数值。  
  
-   嵌入的资源，如图像。 链接到报表的外部资源不与报表快照一同存储。  
  
 报表历史记录的创建方式以及可以存储的报表快照数由相应设置确定。  
  
 如果报表出错，则不会创建快照。 生成警告但仍能运行的报表可以用来生成快照。  
  
## <a name="modifying-properties-and-deleting-report-history"></a>修改属性和删除报表历史记录  
 报表快照一旦生成就无法修改。 但是，您可以采用删除报表历史记录的方法来修改属性。  
  
 可采用以下方法删除报表历史记录：  
  
-   手动删除单个或成组快照。  
  
     您可以从报表管理器的“历史记录”页中删除快照。 导航到报表，单击“历史记录”，选中要删除的快照旁边的复选框，再单击 **“删除”**。  
  
-   降低报表历史记录限值以减少存储的快照数。 可以为报表服务器或特定报表设置报表历史记录限值。 如果降低限值，将从历史记录中删除最早的快照。  
  
 不能通过大容量操作来删除报表服务器上存储的所有报表历史记录。  
  
 删除报表时将同时删除报表历史记录。 例如，如果删除月销售情况报表，代之以新报表，则与该报表关联的所有报表历史记录也将随之删除。 但是，如果移动报表，所有报表历史记录也将随之移动。  
  
## <a name="see-also"></a>请参阅  
 [创建报表历史记录（SharePoint 集成模式下的 Reporting Services）](create-report-history-reporting-services-in-sharepoint-integrated-mode.md)   
 [报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)   
 [报表服务器内容管理（SSRS 本机模式）](report-server-content-management-ssrs-native-mode.md)   
 [向报表历史记录添加快照（报表管理器）](add-a-snapshot-to-report-history-report-manager.md)   
 [限制报表历史记录（报表管理器）](../reports/limit-report-history-report-manager.md)  
  
  

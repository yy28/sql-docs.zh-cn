---
title: 用于 Microsoft Excel 的 Master Data Services 外接程序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 33d9c8fc-9602-494d-b9ab-8f0f42785974
caps.latest.revision: 17
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a5d6efd6aa45886aa87fdd5db5f51ae3682e45ad
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37273083"
---
# <a name="master-data-services-add-in-for-microsoft-excel"></a>用于 Microsoft Excel 的 Master Data Services 外接程序
  与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]，可以将引用数据的主列表分发给你组织中使用 Excel 的每个人。 可通过安全权限来确定用户可以查看和更新的数据。  
  
 可以将筛选过的数据列表从 MDS 加载到 Excel 中，从中按照处理任何其他数据的方式来处理加载的数据。 处理完成后，您可以将数据发布回 MDS，这是集中存储数据的位置。  
  
 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 如果您是管理员，则可以使用 来创建实体和属性，并向其中加载数据。 这样就不必使用任何其他工具将数据加载到模型中。  
  
 在 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，您可以先使用 Data Quality Services (DQS) 来匹配数据，然后再将其加载到 MDS 中。 这有助于防止 MDS 中的数据重复。  
  
> [!IMPORTANT]  
>  在将 Master Data Services 和 Data Quality Services 升级到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] CTP2 后，您可以使用用于 Excel 的 Master Data Services 外接程序的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 版本继续进行。 但是，在升级到 SQL Server 2014 CTP2 后，用于 Excel 的 Master Data Services 外接程序的任何早期版本都无法使用。 您可以下载[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]SP1 版本的 Master Data Services 外接程序从 excel[此处](http://go.microsoft.com/fwlink/?LinkId=328664)。  
  
## <a name="terms"></a>术语  
 使用该外接程序时，您可能会遇到以下术语。  
  
-   *MDS repository* 是所有主数据的存储位置。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 它是一个配置用于存储 MDS 数据的  数据库。 若要使用该存储库中的数据，需要将数据加载到 Excel 中；处理完数据后，需要将更改发布回该存储库。 管理员可以向该存储库添加新的实体和属性。  
  
-   *MDS-managed data* 是存储在 MDS 存储库中并加载到 Excel 中的数据，该数据在 Excel 中显示为突出显示的行。 您可以向工作表添加非 MDS 管理的数据，刷新 MDS 管理的数据时并不会影响非 MDS 管理的数据。  
  
-   *model* 是一种数据容器。 可以为这些容器创建多个版本，并且通常最新版本是最近创建的。 有关详细信息，请参阅[模型 (Master Data Services)](../models-master-data-services.md)。  
  
-   *entity* 是一个数据列表。 您可以将实体视作数据库中的表。  例如，Color 实体可能包含一个颜色列表。 有关详细信息，请参阅[实体 (Master Data Services)](../entities-master-data-services.md)。  
  
-   *member* 是数据行。 每个实体都包含成员。 **Blue**就是成员的一个示例。 有关详细信息，请参阅[成员 (Master Data Services)](../members-master-data-services.md)。  
  
-   *attribute* 是数据列。 每个成员都具有属性。 例如，“Blue”成员的“代码”属性是“B”有关属性的详细信息，请参阅[属性 (Master Data Services)](../attributes-master-data-services.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 创建指向  存储库的连接。|[连接到 MDS 存储库（用于 Excel 的 MDS 外接程序）](connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|将 MDS 管理的数据加载到 Excel 中。|[将数据从 MDS 加载到 Excel](export-data-to-excel-from-master-data-services.md)|  
|保存快捷查询，用于在将来打开当前显示的 MDS 管理的数据。|[保存快捷查询文件（用于 Excel 的 MDS 外接程序）](save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|与他人共享快捷方式。|[通过电子邮件发送快捷查询文件（用于 Excel 的 MDS 外接程序）](email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|查看对成员所做的所有更改。|[查看成员的所有批注或事务（用于 Excel 的 MDS 外接程序）](view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
|在发布新数据之前，确定是否存在重复。|[匹配相似数据（用于 Excel 的 MDS 外接程序）](match-similar-data-mds-add-in-for-excel.md)|  
|将数据从工作表发布到 MDS 存储库中。|[数据从 Excel 发布到 MDS &#40;MDS add-in for Excel&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|在工作表中创建包含数据的新实体。 （仅限管理员）|[创建实体（用于 Excel 的 MDS 外接程序）](create-an-entity-mds-add-in-for-excel.md)|  
|创建基于域的属性（也称为约束列表）。 （仅限管理员）|[创建基于域的属性（用于 Excel 的 MDS 外接程序）](create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|设置用于在用于 Excel 的 Master Data Services 外接程序中加载和发布数据的属性。 （仅限管理员）|[设置用于 Excel 的 Master Data Services 外接程序的属性](setting-properties-for-master-data-services-add-in-for-excel.md)|  
  
## <a name="related-content"></a>相关内容  
  
-   [连接（用于 Excel 的 MDS 外接程序）](connections-mds-add-in-for-excel.md)  
  
-   [加载数据&#40;MDS add-in for Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [快捷查询文件（用于 Excel 的 MDS 外接程序）](shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [用于 Excel 的 MDS 外接程序中的数据质量匹配](data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
-   [发布数据&#40;MDS add-in for Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
-   [生成模型（用于 Excel 的 MDS 外接程序）](building-a-model-mds-add-in-for-excel.md)  
  
-   [安全性 (Master Data Services)](../security-master-data-services.md)  
  
  

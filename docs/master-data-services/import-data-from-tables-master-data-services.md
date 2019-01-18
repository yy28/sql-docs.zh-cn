---
title: 从表中导入数据 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: ad5b83b1-8e40-4ef8-9ba8-4ea17a58b672
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 29d0b40b947bc9a19839005cfc81c9ed3446b318
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52759969"
---
# <a name="import-data-from-tables-master-data-services"></a>从表导入数据 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  你可以添加数据并将数据批量更改为 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中的模型。  
  
 **先决条件**  
  
-   必须有权将数据插入到 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库中的 stg. \<name>_Leaf、stg. \<name>_Consolidated、stg. \<name>_Relationship 表。  
  
-   必须有权执行 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库中的 stg.udp_\<name>_Leaf、stg.udp\_\<name>_Consolidated 或 \_\<name>_Relationship 存储过程。  
  
-   模型的状态不能是“已提交” 。  
  
 **添加、更新和删除 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库中的数据**  
  
1.  准备要导入 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库中相应临时表的成员，包括必需字段的提供值。 有关临时表的概述，请参阅[概述：导入表中数据 (Master Data Services)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)  
  
    -   叶成员的表为 stg.\<name>_Leaf，其中 \<name> 指代相应的实体。 有关所需字段的信息，请参阅[叶成员临时表 (Master Data Services)](../master-data-services/leaf-member-staging-table-master-data-services.md)  
  
    -   合并成员的表为 stg.\<name>_Consolidated。 有关所需字段的信息，请参阅[合并成员临时表 (Master Data Services)](../master-data-services/consolidated-member-staging-table-master-data-services.md)。  
  
    -   用于移动显式层次结构中成员的位置的表为 stg.\<name>_Relationship。 有关所需字段的信息，请参阅[关系临时表 (Master Data Services)](../master-data-services/relationship-staging-table-master-data-services.md)。  
  
         有关移动显式层次结构中成员的概述，请参阅[概述：导入表中数据 (Master Data Services)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)。  
  
    -   使用 **ImportType** 字段值来指定你要创建新的成员、停用成员或删除成员。 有关这些值的详细信息，请参阅[叶成员临时表 (Master Data Services)](../master-data-services/leaf-member-staging-table-master-data-services.md)和[合并成员临时表 (Master Data Services)](../master-data-services/consolidated-member-staging-table-master-data-services.md)。  
  
         有关停用和删除成员的概述，请参阅[概述：导入表中数据 (Master Data Services)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)。  
  
2.  打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 并为自己的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库连接到数据库引擎实例。  
  
     有关更多信息，请参见 [SQL Server Management Studio](https://msdn.microsoft.com/library/66a6b7b1-de6a-4161-82bd-98ded486947b)。  
  
3.  使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 导入和导出向导将数据导入到临时表。  
  
     有关更多信息，请参见 [SQL Server Import and Export Wizard](~/integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)。  
  
4.  通过执行下列任一操作，将数据从临时表加载 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 表  
  
    -   运行临时表（想要移动数据到的目标位置）相对应的临时存储过程。  
  
         有关临时存储过程和临时表的概述，请参阅[概述：导入表中数据 (Master Data Services)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)。 有关临时存储过程参数以及代码示例的详细信息，请参阅[临时存储过程 (Master Data Services)](../master-data-services/staging-stored-procedure-master-data-services.md)。  
  
    -   使用主数据管理的“集成管理”  功能区域。  
  
         “临时批处理”  页上，在下拉列表中选择向其添加数据的模型，然后单击“开始批处理” 。 “状态”  字段将指示执行批处理的状态。 有关状态的详细信息，请参阅[导入状态 (Master Data Services)](../master-data-services/import-statuses-master-data-services.md)。  
  
         ![主数据管理器中的“临时批处理”页](../master-data-services/media/mds-stagingbatchespage.png "Staging Batches Page in Master Data Manager")  
  
         按照 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中的“临时批处理间隔”设置所确定的间隔启动临时过程。 有关详细信息，请参阅[系统设置 (Master Data Services)](../master-data-services/system-settings-master-data-services.md)。  
  
5.  查看在临时过程中出现的错误。 有关详细信息，请参阅[查看临时过程中出现的错误 (Master Data Services)](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)和[临时过程错误 (Master Data Services)](../master-data-services/staging-process-errors-master-data-services.md)。  
  
6.  根据业务规则对数据进行验证。  
  
     在主数据管理器中，导航到模型的“资源管理器”  功能区域，然后应用业务规则以验证数据。 有关详细信息，请参阅[业务规则验证特定成员 (Master Data Services)](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)。 同时可以使用存储过程来验证数据。 有关详细信息，请参阅 [验证存储过程 (Master Data Services)](../master-data-services/validation-stored-procedure-master-data-services.md)。  
  
     使用临时表加载数据时，不会自动根据业务规则验证数据。 有关执行何种验证以及何时执行的详细信息，请参阅[验证 (Master Data Services)](../master-data-services/validation-master-data-services.md)。  
  
  

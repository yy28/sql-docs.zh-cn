---
title: 添加、更新和删除数据（Master Data Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b6295ead-bd2f-49dd-8756-35c6afb59648
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a12c6dd3b0691d62f5509a363311b1deb1584078
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972287"
---
# <a name="add-update-and-delete-data-master-data-services"></a>添加、更新和删除数据 (Master Data Services)
  你可以添加数据并将数据批量更改为 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中的模型。  
  
 **先决条件**  
  
-   您必须有权将数据插入 stg.<name。 \<name>_Leaf stg.<name。 \<name>_Consolidated stg.<name。 \<name>数据库中的 _Relationship 表 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 。  
  
-   您必须具有 \<name> 在数据库中执行 udp_ stg.<name _Leaf、stg.<name \_ \<name> _Consolidated 或 stg.<name \_ \<name> _Relationship 存储过程 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 的权限。  
  
-   模型的状态不能是“已提交” ****。  
  
 **添加、更新和删除 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库中的数据**  
  
1.  准备要导入 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库中相应临时表的成员，包括必需字段的提供值。 有关临时表的概述，请参阅[数据导入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)  
  
    -   对于叶成员，表是 stg.<name。 \<name>_Leaf，其中 \<name> 指对应的实体。 有关所需字段的信息，请参阅[叶成员临时表 (Master Data Services)](../../2014/master-data-services/leaf-member-staging-table-master-data-services.md)  
  
    -   对于合并成员，表是 stg.<name。 \<name>_Consolidated。 有关所需字段的信息，请参阅[合并成员临时表 (Master Data Services)](../../2014/master-data-services/consolidated-member-staging-table-master-data-services.md)。  
  
    -   为了移动显式层次结构中成员的位置，表是 stg.<name。 \<name>_Relationship。 有关所需字段的信息，请参阅[关系临时表 (Master Data Services)](../../2014/master-data-services/relationship-staging-table-master-data-services.md)。  
  
         有关移动显式层次结构中的成员的概述，请参阅[数据导入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)。  
  
    -   使用 **ImportType** 字段值来指定你要创建新的成员、停用成员或删除成员。 有关这些值的详细信息，请参阅[叶成员临时表 (Master Data Services)](../../2014/master-data-services/leaf-member-staging-table-master-data-services.md)和[合并成员临时表 (Master Data Services)](../../2014/master-data-services/consolidated-member-staging-table-master-data-services.md)。  
  
         有关停用和删除成员的概述，请参阅[数据导入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)。  
  
2.  打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 并为自己的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库连接到数据库引擎实例。  
  
     有关详细信息，请参阅[SQL Server Management Studio](../ssms/sql-server-management-studio-ssms.md)。  
  
3.  使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 导入和导出向导将数据导入到临时表。  
  
     有关更多信息，请参见 [SQL Server Import and Export Wizard](../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。  
  
4.  通过执行下列任一操作，将数据从临时表加载 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 表  
  
    -   运行临时表（想要移动数据到的目标位置）相对应的临时存储过程。  
  
         有关临时存储过程和临时表的概述，请参阅[数据导入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)。 有关临时存储过程参数以及代码示例的详细信息，请参阅[临时存储过程 (Master Data Services)](../../2014/master-data-services/staging-stored-procedure-master-data-services.md)。  
  
    -   使用主数据管理的“集成管理” **** 功能区域。  
  
         “临时批处理” **** 页上，在下拉列表中选择向其添加数据的模型，然后单击“开始批处理” ****。 “状态” **** 字段将指示执行批处理的状态。 有关状态的详细信息，请参阅[导入状态 (Master Data Services)](../../2014/master-data-services/import-statuses-master-data-services.md)。  
  
         ![主数据管理器中的“临时批处理”页](../../2014/master-data-services/media/mds-staging-batches.png "主数据管理器中的“临时批处理”页")  
  
         按照 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中的“临时批处理间隔”设置所确定的间隔启动临时过程。**** 有关详细信息，请参阅[系统设置 (Master Data Services)](../../2014/master-data-services/system-settings-master-data-services.md)。  
  
5.  查看在临时过程中出现的错误。 有关详细信息，请参阅[查看在临时过程中出现的错误 &#40;Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md)并在[临时过程错误 &#40;Master Data Services&#41;](../../2014/master-data-services/staging-process-errors-master-data-services.md)。  
  
6.  根据业务规则对数据进行验证。  
  
     在主数据管理器中，导航到模型的“资源管理器” **** 功能区域，然后应用业务规则以验证数据。 有关详细信息，请参阅[业务规则验证特定成员 (Master Data Services)](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)。 同时可以使用存储过程来验证数据。 有关详细信息，请参阅 [验证存储过程 (Master Data Services)](../../2014/master-data-services/validation-stored-procedure-master-data-services.md)。  
  
     使用临时表加载数据时，不会自动根据业务规则验证数据。 有关执行何种验证以及何时执行的详细信息，请参阅[验证 (Master Data Services)](../../2014/master-data-services/validation-master-data-services.md)。  
  
## <a name="see-also"></a>另请参阅  
 [数据导入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)  
  
  

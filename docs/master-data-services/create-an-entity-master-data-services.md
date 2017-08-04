---
title: "创建实体 (Master Data Services) |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- entities [Master Data Services], creating
- creating entities [Master Data Services]
ms.assetid: d9a6a51e-7b53-4785-a118-3baeb7ca2d48
caps.latest.revision: 9
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2766ad2cb250200e7fbb3f19f96eab7b5f748a9a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="create-an-entity-master-data-services"></a>创建实体 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，创建一个实体以便包含成员及其属性。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
-   模型必须存在。 有关详细信息，请参阅[创建模型 (Master Data Services)](../master-data-services/create-a-model-master-data-services.md)。  
  
### <a name="to-create-an-entity"></a>创建实体  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  在“管理模型”  页上，从网格中选择要为其创建实体的模型，然后单击“实体” 。  
  
3.  在“管理实体”  页上，单击“添加” 。  
  
4.  在“名称”  框中，键入实体的名称。  
  
5.  根据需要，在“说明”  字段中，键入实体说明。  
  
6.  根据需要，在“临时表名称”  框中，键入临时表的名称。  
  
     如果不填写此字段，则会使用实体名称。  
  
    > [!TIP]  
    >  使用模型名称作为临时表名称的一部分，例如 Modelname_Entityname。 这便于在数据库中查找表。 有关临时表的详细信息，请参阅[概述：导入表中数据 (Master Data Services)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)。  
  
7.  对于“事务日志类型”字段，请在下拉列表中选择事务日志类型。  
  
     有关详细信息，请参阅[更改实体事务日志类型 (Master Data Services)](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)  
  
8.  可选。 选中 **“自动创建代码值”** 复选框。 有关详细信息，请参阅[自动创建代码 (Master Data Services)](../master-data-services/automatic-code-creation-master-data-services.md)。  
  
9. 可选。 选择“启用数据压缩”  复选框。 默认情况下，系统将打开行压缩。 有关详细信息，请参阅 [Data Compression](../relational-databases/data-compression/data-compression.md)。  
  
10. 单击 **“保存”**。  
  
## <a name="grid-columns"></a>网格列  
 对于创建的每个实体，系统都会在网格中添加一行（其中包含十三列）。 下面介绍了这些列。  
  
|名称|Description|  
|----------|-----------------|  
|状态|实体状态。 单击“保存”  时，将显示下图，指示实体正在更新。<br /><br /> ![更新状态的图标](../master-data-services/media/mds-statusicon-updating.png "更新状态的图标")<br /><br /> 如果在创建或编辑实体时出错，将显示下面的图像。<br /><br /> ![错误状态的图标](../master-data-services/media/mds-statusicon-error.png "错误状态的图标")<br /><br /> 如果状态为“正常”，则将显示下面的图像。<br /><br /> ![正常状态的图标](../master-data-services/media/mds-statusicon-ok.png "正常状态的图标")|  
|名称|实体名称。|  
|Description|实体说明。|  
|临时表|用于存储数据的表的前缀名称。|  
|事务日志类型|实体的事务日志类型。|  
|自动创建代码|指定是否启用自动代码创建。|  
|Data Compression|指定是否为实体启用数据压缩。|  
|是否是同步目标|指定实体是否为同步关系的目标。|  
|是否已启用层次结构|指定是否为显式层次结构启用了实体。 如果为实体创建了至少一个显式层次结构，则此列将显示“是”。|  
|创建者|创建实体的用户的用户名。|  
|创建时间|创建实体的日期和时间。|  
|更新者|上次更新实体的用户的用户名。|  
|更新时间|上次更新实体的日期和时间。|  
  
## <a name="next-steps"></a>后续步骤  
  
-   [创建文本属性 (Master Data Services)](../master-data-services/create-a-text-attribute-master-data-services.md)  
  
-   [创建基于域的属性 (Master Data Services)](../master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
-   [创建文件属性 (Master Data Services)](../master-data-services/create-a-file-attribute-master-data-services.md)  
  
## <a name="see-also"></a>另请参阅  
 [实体 (Master Data Services)](../master-data-services/entities-master-data-services.md)   
 [显式层次结构 &#40;Master Data Services &#41;](../master-data-services/explicit-hierarchies-master-data-services.md)   
 [编辑实体 &#40;Master Data Services &#41;](../master-data-services/edit-an-entity-master-data-services.md)   
 [删除实体 (Master Data Services)](../master-data-services/delete-an-entity-master-data-services.md)  
  
  

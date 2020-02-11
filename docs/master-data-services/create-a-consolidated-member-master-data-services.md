---
title: 创建合并成员
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating consolidated members [Master Data Services]
- members [Master Data Services], creating consolidated members
- consolidated members [Master Data Services], creating
ms.assetid: 431ab2d2-5517-4372-9980-142b05427c08
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bcca8ec5850b7f787fa4fcb99f2c009a77b56b48
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "73729611"
---
# <a name="create-a-consolidated-member-master-data-services"></a>创建合并成员 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]在中，在您想要显式层次结构的父节点时创建合并成员。 如果你要批量添加数据，请改用临时表。 有关详细信息，请参阅[导入表中数据 (Master Data Services)](../master-data-services/import-data-from-tables-master-data-services.md)  
  
## <a name="prerequisites"></a>必备条件  
 若要执行此过程：  
  
-   您必须有权访问 "**资源管理器**" 功能区域。  
  
-   对于要向其中添加成员的实体，你必须至少具有对合并模型对象的“更新” **** 权限，同时你还需要具有对实体下的合并类型的“创建权限” **** 。  
  
### <a name="to-create-a-consolidated-member"></a>创建合并成员  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 主页上，从“模型” **** 列表中选择模型。  
  
2.  
  **
  ** 从“版本”列表中，选择某一版本。  
  
3.  
  **
  **单击“资源管理器”。  
  
4.  
  **
  ** 从菜单栏中，指向“层次结构”，然后单击您要将合并成员添加到的层次结构的名称。  
  
5.  
  **
  ** 在网格上方，选择 **“合并成员”** 或“层次结构中的所有合并成员”选项。  
  
6.  在左侧窗格中，选择要在其下创建合并成员的根节点或合并成员。  
  
7.  单击“添加”  。  
  
8.  在右侧窗格中，填写字段。  
  
9. 可选。 
  **
  ** 在“批注”框中，键入有关添加成员原因的注释。 有权访问成员的所有用户都可以查看批注。  
  
10. 单击“确定”。   
  
## <a name="see-also"></a>另请参阅  
 [创建显式层次结构 &#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [&#40;Master Data Services 创建叶成员&#41;](../master-data-services/create-a-leaf-member-master-data-services.md)   
 [成员 &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [显式层次结构 &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
  

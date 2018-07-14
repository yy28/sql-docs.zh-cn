---
title: 使属性组对用户可见 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b2f6cc27-dbc9-4f3f-961e-e81e76375248
caps.latest.revision: 3
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 94507eb6cae0db3206a02b43062871140d5f21c7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37223639"
---
# <a name="make-an-attribute-group-visible-to-users-master-data-services"></a>使属性组对用户可见 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，当您想要用户在 **“资源管理器”** 功能区域中将选项卡置于网格上方时，使属性组对于用户或组是可见的。  
  
 创建属性组时，对除创建者之外的所有用户自动隐藏它。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
-   必须至少存在一个属性组。 有关详细信息，请参阅[创建属性组&#40;Master Data Services&#41;](../../2014/master-data-services/create-an-attribute-group-master-data-services.md)。  
  
### <a name="to-make-an-attribute-group-visible-to-users"></a>使属性组对用户可见  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  上**模型视图**页上，从菜单栏中，依次指向**管理**然后单击**属性组**。  
  
3.  从 **“模型”** 列表中，选择某一模型。  
  
4.  从 **“实体”** 列表中，选择某一实体。  
  
5.  单击加号以展开**叶组**，**合并组**，或**集合组**，具体取决于你想要使可见的组的类型。  
  
6.  单击加号以便展开要使其可见的组。  
  
7.  单击任一**用户**或**组**，取决于您要使组对用户或组可见。  
  
8.  单击**编辑所的选项**。  
  
9. 单击用户或中的组**可用**框，然后单击**添加**箭头。 若要全部添加，请单击 **“全部添加”** 箭头。  
  
10. 单击 **“保存”**。  
  
## <a name="see-also"></a>请参阅  
 [属性组&#40;Master Data Services&#41;](../../2014/master-data-services/attribute-groups-master-data-services.md)   
 [创建属性组&#40;Master Data Services&#41;](../../2014/master-data-services/create-an-attribute-group-master-data-services.md)  
  
  

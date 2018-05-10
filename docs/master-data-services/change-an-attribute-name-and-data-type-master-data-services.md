---
title: 更改属性名称和数据类型 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], changing name
ms.assetid: d348f238-f59d-41c7-ad20-3ccd55bfd9e5
caps.latest.revision: 9
author: leolimsft
ms.author: lle
manager: erikre
ms.openlocfilehash: d823a7c716eb0c7dfc4097d0c7287fd571c39aef
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="change-an-attribute-name-and-data-type-master-data-services"></a>更改属性名称和数据类型 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，可以更改属性的名称。  
  
## <a name="prerequisites"></a>必备条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
### <a name="to-change-an-attribute-name-and-type"></a>更改属性名称和类型  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  在“管理模型”  页上，从网格中选择一个模型，然后单击“实体” 。  
  
3.  在“管理实体”  页上，选择要为其创建属性的实体所在的行。  
  
4.  单击 **“属性”**。  
  
5.  在“管理属性”  页上，执行下列操作之一。  
  
    -   如果是叶成员的属性，请从“成员类型”  列表框中选择“叶”  。  
  
    -   如果属性是针对合并成员，则从“成员类型”  列表框中选择“合并”  。  
  
    -   如果是集合的属性，请从“成员类型”  列表框中选择“集合”  。  
  
6.  选择要编辑的属性所在的行，然后单击“编辑” 。  
  
7.  在 **“名称”** 框中，键入属性的新名称。 有关不可用作属性名称的单词列表，请参阅[保留字 (Master Data Services)](../master-data-services/reserved-words-master-data-services.md)。  
  
8.  在“属性类型”  列表中，选择其他类型。  
  
9. 单击 **“保存”**。  
  
## <a name="see-also"></a>另请参阅  
 [创建文本属性 (Master Data Services)](../master-data-services/create-a-text-attribute-master-data-services.md)   
 [删除属性 &#40;Master Data Services&#41;](../master-data-services/delete-an-attribute-master-data-services.md)   
 [属性 (Master Data Services)](../master-data-services/attributes-master-data-services.md)  
  
  

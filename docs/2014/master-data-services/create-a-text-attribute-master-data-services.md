---
title: 创建文本属性 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], creating text attributes
- creating text attributes [Master Data Services]
ms.assetid: cd8b57de-364d-42a3-9273-c1c6b992bb40
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a58aaee32970b157b70a9f6a7c9477c18d9f19a7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62924930"
---
# <a name="create-a-text-attribute-master-data-services"></a>创建文本属性 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，在您希望用户输入文本字符串作为属性值时创建文本属性。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
-   要为其创建属性的实体必须存在。 有关详细信息，请参阅[创建实体 (Master Data Services)](../../2014/master-data-services/create-an-entity-master-data-services.md)。  
  
### <a name="to-create-a-text-attribute"></a>创建文本属性  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  在 **“模型视图”** 页上，从菜单栏中，指向 **“管理”** ，然后单击 **“实体”**。  
  
3.  在 **“实体维护”** 页上，从 **“模型”** 列表中，选择某一模型。  
  
4.  为您要为其创建属性的实体选择行。  
  
5.  单击 **“编辑所选实体”**。  
  
6.  在 **“编辑实体”** 页上：  
  
    -   如果属性是针对叶成员的，则在 **“叶成员属性”** 窗格中，单击 **“添加叶属性”**。  
  
    -   如果属性是针对合并成员的，则在 **“合并成员属性”** 窗格中，单击 **“添加合并属性”**。  
  
    -   如果属性是针对集合的，则在 **“集合属性”** 窗格中，单击 **“添加集合属性”**。  
  
7.  在 **“添加属性”** 页上，选择 **“自由格式”** 选项。  
  
8.  在 **“名称”** 框中，键入属性的名称。 有关不可用作属性名称的单词列表，请参阅[保留字 (Master Data Services)](../../2014/master-data-services/reserved-words-master-data-services.md)。  
  
9. 在 **“显示像素宽度”** 框中，键入要在 **“资源管理器”** 网格中显示的属性列的宽度。  
  
10. 从 **“数据类型”** 列表中，选择 **“文本”**。  
  
11. 在 **“长度”** 框中，键入允许的最大字符数。  
  
12. 根据需要，选择 **“启用更改跟踪”** 可以跟踪对属性组的更改。 有关详细信息，请参阅[向更改跟踪组添加属性 (Master Data Services)](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)。  
  
13. 单击 **“保存属性”**。  
  
14. 在 **“实体维护”** 页上，单击 **“保存实体”**。  
  
## <a name="see-also"></a>请参阅  
 [属性 (Master Data Services)](../../2014/master-data-services/attributes-master-data-services.md)   
 [更改属性名称&#40;Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [创建基于域的属性 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [创建文件属性 (Master Data Services)](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
  

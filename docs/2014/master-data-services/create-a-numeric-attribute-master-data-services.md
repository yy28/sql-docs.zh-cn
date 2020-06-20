---
title: 创建数字属性 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], creating number attributes
- creating number attributes [Master Data Services]
ms.assetid: c0dbb6d8-ba78-485a-a40d-6d5cb7e75d0a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 9e56d68cc46da72de21f07559b7ccb2aa9ac6fda
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971777"
---
# <a name="create-a-numeric-attribute-master-data-services"></a>创建数字属性 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，在您希望用户输入数字作为属性值时创建数字属性。  
  
> [!NOTE]  
>  数字属性存在一些限制。 有关详细信息，请参阅 [属性 (Master Data Services)](attributes-master-data-services.md)。  
  
## <a name="prerequisites"></a>必备条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)。  
  
-   要为其创建属性的实体必须存在。 有关详细信息，请参阅[创建实体 (Master Data Services)](../../2014/master-data-services/create-an-entity-master-data-services.md)。  
  
### <a name="to-create-a-numeric-attribute"></a>创建数字属性  
  
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
  
10. 从 **“数据类型”** 列表中，选择 **“数字”**。  
  
11. 在 **“小数位数”** 框中，键入小数点后可以输入的位数。  
  
12. 从 "**输入掩码**" 列表中，选择负数的格式。  
  
13. 根据需要，选择 **“启用更改跟踪”** 可以跟踪对属性组的更改。 有关详细信息，请参阅 [向更改跟踪组添加属性 (Master Data Services)](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md) 。  
  
14. 单击 **“保存属性”**。  
  
15. 在 **“实体维护”** 页上，单击 **“保存实体”**。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;Master Data Services&#41;](attributes-master-data-services.md)   
 [更改属性名称 &#40;Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [创建基于域的属性 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [创建文件属性 (Master Data Services)](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
  

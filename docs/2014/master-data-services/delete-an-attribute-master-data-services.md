---
title: 删除属性 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], deleting
- deleting attributes [Master Data Services]
ms.assetid: ec3e66f7-0e35-43d7-a80d-64899948ebfe
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 93b3867a55c66ebc5a0a26bc211104d63b01692f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84962007"
---
# <a name="delete-an-attribute-master-data-services"></a>删除属性 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，当您希望永久删除某个属性以及所有关联的属性值时，可以删除此属性。  
  
## <a name="prerequisites"></a>必备条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
### <a name="to-delete-an-attribute"></a>删除属性  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  在 **“模型视图”** 页上，从菜单栏中，指向 **“管理”** ，然后单击 **“实体”**。  
  
3.  在 **“实体维护”** 页上，从 **“模型”** 列表中，选择某一模型。  
  
4.  为包含您要删除的属性的实体选择行。  
  
5.  单击 **“编辑所选实体”**。  
  
6.  在 "**编辑实体**" 页上，单击要删除的属性。  
  
    > [!NOTE]  
    >  不能删除 Name 或 Code 属性。  
  
7.  单击 "**删除所选属性**"。  
  
8.  在确认对话框中，单击 **“确定”**。  
  
9. 在附加确认对话框中，单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)   
 [基于域的属性 &#40;Master Data Services&#41;](../../2014/master-data-services/domain-based-attributes-master-data-services.md)   
 [Master Data Services 创建文本属性 &#40;&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)   
 [创建基于域的属性 (Master Data Services)](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
  

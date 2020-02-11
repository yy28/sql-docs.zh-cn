---
title: 排除业务规则 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], excluding
ms.assetid: bdbc9df0-23f7-40b9-8aba-4445c1482580
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8f18e047b11bee4093ce7a6e494c1ae1bf3d0ada
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "65483387"
---
# <a name="exclude-a-business-rule-master-data-services"></a>排除业务规则 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，如果您不希望永久删除业务规则，而又不希望针对此规则验证数据，则可以排除该规则。  
  
## <a name="prerequisites"></a>必备条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
### <a name="to-exclude-a-business-rule"></a>排除业务规则  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  从菜单栏中，指向 **“管理”** ，然后单击 **“业务规则”**。  
  
3.  在 **“业务规则维护”** 页上，从 **“模型”** 列表中，选择某一模型。  
  
4.  从 **“实体”** 列表中，选择某一实体。  
  
5.  从 "**成员类型**" 列表中，选择成员的类型。  
  
6.  从 **“属性”** 列表中，选择某一属性或保持默认值 **“全部”**。  
  
7.  在网格中的业务规则行中，选中 "**排除**" 列中的复选框。 "**状态**" 列中的值为 "**排除待定**"。  
  
8.  单击 **“发布业务规则”**。  
  
9. 在确认对话框中，单击 **“确定”**。 "**状态**" 列中的值已**排除**。  
  
## <a name="see-also"></a>另请参阅  
 [删除业务规则 &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-business-rule-master-data-services.md)   
 [创建和发布业务规则 &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [业务规则 &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  

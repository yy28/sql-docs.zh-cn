---
title: 更改业务规则名称 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- business rules [Master Data Services], changing name
ms.assetid: cffcae43-a208-443f-9f43-a0ec9e05f79c
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b70b2ee10b092be94df67c13be09944824546b77
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013874"
---
# <a name="change-a-business-rule-name-master-data-services"></a>更改业务规则名称 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，当分配的业务规则名称不能满足您的业务需要时，可以更改此名称。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
-   业务规则必须存在。 有关详细信息，请参阅[创建和发布业务规则 (Master Data Services)](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)。  
  
### <a name="to-change-the-name-of-a-business-rule"></a>更改业务规则的名称  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  从菜单栏中，指向 **“管理”** ，然后单击 **“业务规则”**。  
  
3.  在 **“业务规则维护”** 页上，从 **“模型”** 列表中，选择某一模型。  
  
4.  从 **“实体”** 列表中，选择某一实体。  
  
5.  从**成员类型**列表中，选择一种类型的成员。  
  
6.  从 **“属性”** 列表中，选择某一属性或保持默认值 **“全部”**。  
  
7.  在网格中，业务规则的行中双击**名称**字段。  
  
8.  为业务规则键入名称。  
  
9. 按 Enter。  
  
10. 单击 **“发布业务规则”**。  
  
11. 在确认对话框中，单击 **“确定”**。 规则的状态将更改为 **“活动”**。  
  
## <a name="see-also"></a>请参阅  
 [业务规则&#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
---
title: 向业务规则添加多个条件 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], multiple conditions
ms.assetid: 5f0f6958-6cf2-444b-bdcd-05b887637a0b
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 2f9f8114186aa3593f2218037add9a0611a8fe23
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52792949"
---
# <a name="add-multiple-conditions-to-a-business-rule-master-data-services"></a>向业务规则添加多个条件 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，在您想要采用更复杂的规则时，可以向业务规则添加多个 **AND** 或 **OR** 条件。  
  
> [!NOTE]  
>  如果您创建使用 **OR** 运算符的业务规则，则考虑为可以独立进行计算的每个条件语句都创建单独的规则。 然后，您可以根据需要排除规则，提供更高的灵活性以及更便于排除故障。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
-   业务规则必须存在。 有关详细信息，请参阅[创建和发布业务规则 (Master Data Services)](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)。  
  
### <a name="to-add-multiple-conditions-to-a-business-rule"></a>向业务规则添加多个条件  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  从菜单栏中，指向 **“管理”** ，然后单击 **“业务规则”**。  
  
3.  在 **“业务规则维护”** 页上，从 **“模型”** 列表中，选择某一模型。  
  
4.  从 **“实体”** 列表中，选择某一实体。  
  
5.  从**成员类型**列表中，选择一种类型的成员。  
  
6.  从 **“属性”** 列表中，选择某一属性或保持默认值 **“全部”**。  
  
7.  单击要编辑的业务规则所对应的行。  
  
8.  单击 **“编辑所选业务规则”**。  
  
9. 在中**组件**窗格中，展开**逻辑运算符**节点。  
  
10. 单击**AND**或**OR**将其拖到**如果**窗格的**AND**标签。  
  
11. 在 **“组件”** 窗格中，展开 **“条件”** 节点。  
  
12. 单击某一条件并将其拖到**IF**窗格中，为**AND**或**OR**步骤 10 中的标签。  
  
13. 在中**特性**窗格中，单击某一属性，并将其拖到**编辑条件**窗格的**选择属性**标签。  
  
14. 在中**编辑条件**窗格中，完成必填的字段。  
  
15. 在 **“编辑条件”** 窗格中，单击 **“保存项”**。  
  
16. （可选） 若要添加更多条件，从**组件**窗格中，拖动**AND**或**OR**到任何**AND**或**OR**中**如果**窗格。 然后执行步骤 13-15。  
  
    > [!TIP]  
    >  若要删除条件，单击名称条件的然后在**编辑条件**窗格中，单击**删除项**。  
  
## <a name="see-also"></a>请参阅  
 [业务规则 (Master Data Services)](../../2014/master-data-services/business-rules-master-data-services.md)   
 [更改业务规则名称 &#40;Master Data Services&#41;](../../2014/master-data-services/change-a-business-rule-name-master-data-services.md)   
 [配置业务规则以发送通知 (Master Data Services)](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  

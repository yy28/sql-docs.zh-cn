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
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 54ab01033fc65f829f2a06bb5cbad8fc9e4d08f7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "65480184"
---
# <a name="add-multiple-conditions-to-a-business-rule-master-data-services"></a>向业务规则添加多个条件 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，在您想要采用更复杂的规则时，可以向业务规则添加多个 **AND** 或 **OR** 条件。  
  
> [!NOTE]  
>  如果您创建使用 **OR** 运算符的业务规则，则考虑为可以独立进行计算的每个条件语句都创建单独的规则。 然后，您可以根据需要排除规则，提供更高的灵活性以及更便于排除故障。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
-   业务规则必须存在。 有关详细信息，请参阅[创建和发布业务规则 (Master Data Services)](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)。  
  
### <a name="to-add-multiple-conditions-to-a-business-rule"></a>向业务规则添加多个条件  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  从菜单栏中，指向 **“管理”** ，然后单击 **“业务规则”**。  
  
3.  在 **“业务规则维护”** 页上，从 **“模型”** 列表中，选择某一模型。  
  
4.  从 **“实体”** 列表中，选择某一实体。  
  
5.  从 "**成员类型**" 列表中，选择成员的类型。  
  
6.  从 **“属性”** 列表中，选择某一属性或保持默认值 **“全部”**。  
  
7.  单击要编辑的业务规则所对应的行。  
  
8.  单击 **“编辑所选业务规则”**。  
  
9. 在 "**组件**" 窗格中，展开 "**逻辑运算符**" 节点。  
  
10. 单击 " **AND** " 或 " **or** "，然后将其拖到 " **IF** " 窗格**和**"标签"。  
  
11. 在 **“组件”** 窗格中，展开 **“条件”** 节点。  
  
12. 单击某个条件并将其拖到 " **IF** " 窗格，将**其添加到**步骤10中的 " **and** " 或 "标签"。  
  
13. 在 "**属性**" 窗格中，单击某个属性，然后将其拖到 "**编辑条件**" 窗格的 "**选择属性**" 标签。  
  
14. 在 "**编辑条件**" 窗格中，填写所有必填字段。  
  
15. 在 **“编辑条件”** 窗格中，单击 **“保存项”**。  
  
16. （可选）若要添加更多条件，**请在 "** **组件**" 窗格中，将 "and"**和** **"or" 拖到 any** **and**或 or in **IF**窗格中。 然后执行步骤 13-15。  
  
    > [!TIP]  
    >  若要删除某个条件，请单击该条件的名称，然后在 "**编辑条件**" 窗格中，单击 "**删除项**"。  
  
## <a name="see-also"></a>另请参阅  
 [业务规则 &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [更改业务规则名称 &#40;Master Data Services&#41;](../../2014/master-data-services/change-a-business-rule-name-master-data-services.md)   
 [配置业务规则以发送通知 (Master Data Services)](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  

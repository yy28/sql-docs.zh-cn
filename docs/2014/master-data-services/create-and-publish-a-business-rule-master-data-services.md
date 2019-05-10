---
title: 创建和发布业务规则 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], creating
- creating business rules [Master Data Services]
ms.assetid: 6961d636-4d69-468e-81f7-8d0be6a4a039
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2b52be0b8c76333b069c018415ff698f13f824ae
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65479888"
---
# <a name="create-and-publish-a-business-rule-master-data-services"></a>创建和发布业务规则 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，创建业务规则以便确保您的主数据的精确性。 创建规则后，必须首先发布它，然后才能将该规则应用于数据。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
### <a name="to-create-and-publish-a-business-rule"></a>创建和发布业务规则  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  从菜单栏中，指向 **“管理”** ，然后单击 **“业务规则”**。  
  
3.  在 **“业务规则维护”** 页上，从 **“模型”** 列表中，选择某一模型。  
  
4.  从 **“实体”** 列表中，选择某一实体。  
  
5.  从 **“成员类型”** 列表中，为要应用于的业务规则选择成员类型。  
  
6.  从 **“属性”** 列表中，选择某一属性或保持默认值 **“全部”**。  
  
7.  单击 **“添加业务规则”**。  
  
8.  单击 **“编辑所选业务规则”**。  
  
9. 在 **“组件”** 窗格中，展开 **“条件”** 节点。  
  
10. 单击某一条件并将其拖到**IF**窗格中的**条件**标签。  
  
    > [!TIP]  
    >  可以通过右键单击并选择从你的业务规则中删除项目**删除**。  
  
11. 在中**特性**窗格中，单击某一属性，并将其拖到**编辑条件**窗格的**选择属性**标签。  
  
12. 在中**编辑条件**窗格中，完成必填的字段。  
  
13. 在 **“编辑条件”** 窗格中，单击 **“保存项”**。  
  
14. 在 **“组件”** 窗格中，展开 **“操作”** 节点。  
  
15. 单击某一操作，然后将其拖到 **THEN** 窗格的 **“操作”** 标签。  
  
16. 在 **“属性”** 窗格中，单击某一属性并且将其拖到 **“编辑操作”** 窗格的 **“选择属性”** 标签。  
  
17. 在 **“编辑操作”** 窗格中，完成必填字段。  
  
18. 在 **“编辑操作”** 窗格中，单击 **“保存项”**。  
  
19. 也可以向规则添加多个条件。 有关详细信息，请参阅 [向业务规则添加多个条件 (Master Data Services)](../../2014/master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)。  
  
20. 单击 **“上一步”**。  
  
21. 或者，在“业务规则维护”页上，对于包含业务规则的行，双击“名称”、“说明”或“通知”列中的单元以便更新值。  
  
    > [!NOTE]  
    >  仅针对包括验证操作的规则发送通知。  
  
22. 单击 **“发布业务规则”**。  
  
23. 在确认对话框中，单击 **“确定”**。 规则的状态将更改为 **“活动”**。  
  
## <a name="next-steps"></a>后续步骤  
  
-   通过以下过程之一将业务规则应用到数据：  
  
    -   [针对业务规则验证特定成员 (Master Data Services)](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [针对业务规则验证版本 (Master Data Services)](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>请参阅  
 [配置业务规则以发送通知 (Master Data Services)](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)   
 [更改业务规则名称 (Master Data Services)](../../2014/master-data-services/change-a-business-rule-name-master-data-services.md)   
 [向业务规则添加多个条件 (Master Data Services)](../../2014/master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)  
  
  

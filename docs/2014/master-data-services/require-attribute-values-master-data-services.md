---
title: 要求属性值 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], requiring attribute values
- attributes [Master Data Services], requiring values
ms.assetid: a360ef13-0c34-43b8-a87e-2f5d8732d30e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 03f868d679f1d51dbb672cfdab5dbeaa2b4fc8a1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "65478865"
---
# <a name="require-attribute-values-master-data-services"></a>要求属性值 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，在您想要确保主数据完整时要求属性值。  
  
> [!NOTE]  
>  缺少基于域的属性值的成员不显示在基于那些关系的派生层次结构中。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
### <a name="to-require-attribute-values"></a>要求属性值  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  从菜单栏中，指向 **“管理”** ，然后单击 **“业务规则”**。  
  
3.  在 **“业务规则维护”** 页上，从 **“模型”** 列表中，选择某一模型。  
  
4.  从 **“实体”** 列表中，选择某一实体。  
  
5.  从 **“成员类型”** 列表中，为要应用于的业务规则选择成员类型。  
  
6.  从 **“属性”** 列表中，选择某一属性或保持默认值 **“全部”**。  
  
7.  单击 **“添加业务规则”**。  
  
8.  单击 **“编辑所选业务规则”**。  
  
9. 在 **“组件”** 窗格中，展开 **“操作”** 节点。  
  
10. 单击 "**是必需**的，然后将其拖到" **THEN** "窗格的"**操作**"标签。  
  
11. 在 **“属性”** 窗格中，单击某一属性并且将其拖到 **“编辑操作”** 窗格的 **“选择属性”** 标签。  
  
12. 在 **“编辑操作”** 窗格中，单击 **“保存项”**。  
  
13. 单击 **“上一步”**。  
  
14. 或者，在“业务规则维护”**** 页上，对于包含业务规则的行，双击“名称”****、“说明”**** 或“通知”**** 列中的单元以便更新值。  
  
15. 单击 **“发布业务规则”**。  
  
16. 在确认对话框中，单击 **“确定”**。 规则的状态将更改为 **“活动”**。  
  
## <a name="next-steps"></a>后续步骤  
  
-   通过以下过程之一将业务规则应用到数据：  
  
    -   [针对业务规则验证特定成员 (Master Data Services)](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [针对业务规则验证版本 (Master Data Services)](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>另请参阅  
 [业务规则 &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [派生层次结构 (Master Data Services)](../../2014/master-data-services/derived-hierarchies-master-data-services.md)  
  
  

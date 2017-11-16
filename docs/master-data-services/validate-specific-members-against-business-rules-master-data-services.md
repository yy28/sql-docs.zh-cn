---
title: "针对业务规则验证特定成员 (Master Data Services) | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- applying business rules [Master Data Services]
- business rules [Master Data Services], applying to select members
ms.assetid: 2288ef43-5392-47ea-b651-ec25e5692a14
caps.latest.revision: "7"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 69010f902b98ebdcb3fe1ad0f503e276ed64c08f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="validate-specific-members-against-business-rules-master-data-services"></a>针对业务规则验证特定成员 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，在您想要根据业务规则更新或验证成员的子级时，可以有选择地应用业务规则。  
  
> [!NOTE]  
>  如果想要将业务规则应用于某个模型版本中的所有成员，请参阅 [针对业务规则验证版本 (Master Data Services)](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-    您必须有权访问“资源管理器”功能区域。  
  
-   对于您要将业务规则应用于的模型对象，您必须至少具有 **“更新”** 权限。  
  
### <a name="to-apply-business-rules-selectively"></a>有选择地应用业务规则  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 主页上，从“模型”下拉列表中，选择某一模型。  
  
2.  从“版本”下拉列表中，选择某一版本。  
  
3.  单击“资源管理器”选项卡。   
  
4.  从菜单栏中指向 **“实体”** ，然后单击包含要将规则应用于的成员的实体名称。  
  
5.  单击“应用规则”。  业务规则仅应用于在网格中显示的成员。  
  
## <a name="see-also"></a>另请参阅  
 [针对业务规则验证版本 (Master Data Services)](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)   
 [业务规则 (Master Data Services)](../master-data-services/business-rules-master-data-services.md)  
  
  

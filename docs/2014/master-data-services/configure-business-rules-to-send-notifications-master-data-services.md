---
title: 配置业务规则以发送通知 (Master Data Services) | Microsoft Docs
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
- business rules [Master Data Services], configuring notifications
- e-mail [Master Data Services], configuring business rules
- notifications [Master Data Services], configuring business rules
ms.assetid: b24f7b11-ab53-4642-999c-e17b543b3558
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 2d0c5d66a15ba476806df39792206c47a31bb26d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016386"
---
# <a name="configure-business-rules-to-send-notifications-master-data-services"></a>配置业务规则以发送通知 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，当您要向用户通知有关属性值更改时，请配置业务规则以发送通知。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域和 **“用户和组权限”** 功能区域。 如果您对 **“用户和组权限”** 功能区域没有权限，则无法查看要向其发送通知的用户和组的列表。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
-   使用验证操作的业务规则必须已经存在。 有关详细信息，请参阅[创建和发布业务规则 (Master Data Services)](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)。  
  
-   接收通知的用户或组对未能通过验证的属性必须至少具有“只读”权限。 显式或隐式拒绝对属性的权限的用户或组将接收电子邮件，但将无法访问 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中的属性。  
  
-   如果将邮件发送到组，则组中只有已访问了 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 的成员才会获得电子邮件。  
  
### <a name="to-configure-business-rules-to-send-notifications"></a>配置业务规则以发送通知  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  从菜单栏中，指向 **“管理”** ，然后单击 **“业务规则”**。  
  
3.  在 **“业务规则维护”** 页上，从 **“模型”** 列表中，选择某一模型。  
  
4.  从 **“实体”** 列表中，选择某一实体。  
  
5.  从**成员类型**列表中，选择一种类型的成员。  
  
6.  从 **“属性”** 列表中，选择某一属性或保持默认值 **“全部”**。  
  
7.  在网格中，业务规则的行中双击**通知**字段。  
  
8.  从子菜单上，单击要发送到电子邮件通知的用户或组。  
  
## <a name="next-steps"></a>后续步骤  
  
-   通过以下过程之一将业务规则应用到数据：  
  
    -   [针对业务规则验证特定成员&#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [针对业务规则验证版本&#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
-   按如下方式配置电子邮件协议：  
  
    -   [配置电子邮件通知&#40;Master Data Services&#41;](../../2014/master-data-services/configure-email-notifications-master-data-services.md)  
  
## <a name="see-also"></a>请参阅  
 [通知&#40;Master Data Services&#41;](../../2014/master-data-services/notifications-master-data-services.md)   
 [配置电子邮件通知&#40;Master Data Services&#41;](../../2014/master-data-services/configure-email-notifications-master-data-services.md)  
  
  
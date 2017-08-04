---
title: "配置电子邮件通知 (Master Data Services) |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- e-mail [Master Data Services], configuring
- notifications [Master Data Services], configuring notifications
ms.assetid: 4241a6ab-7465-471b-9890-57c6b572037e
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 10139480120dffc47c93d36022b7c15e196a2a76
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="configure-email-notifications-master-data-services"></a>配置电子邮件通知 (Master Data Services)
  当您希望 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 自动发送电子邮件时，请配置通知电子邮件。  
  
### <a name="to-configure-notifications"></a>配置通知  
  
1.  在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中的 **“数据库”** 页上，选择您的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库。  
  
2.  在 **“系统设置”** 部分中，单击 **“创建配置文件”**。  
  
3.  填写所有必填字段。 有关详细信息，请参阅[“创建数据库邮件配置文件和帐户”对话框（Master Data Services 配置管理器）](../master-data-services/create-database-mail-profile-and-account-dialog-box.md)。  
  
4.  单击 **“确定”**。  
  
    > [!NOTE]  
    >  在配置通知之后，您无法使用 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 进行更改。 必须直接在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库中直接进行更改。 有关详细信息，请参阅 [Database Mail Configuration Objects](../relational-databases/database-mail/database-mail-configuration-objects.md)。  
  
## <a name="next-steps"></a>后续步骤  
  
-   [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中有多个设置可以影响通知。 可以在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中或直接在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库的“系统设置”表中调整这些设置。 有关详细信息，请参阅[系统设置 (Master Data Services)](../master-data-services/system-settings-master-data-services.md)。  
  
## <a name="see-also"></a>另请参阅  
 [通知 & #40;Master Data Services & #41;](../master-data-services/notifications-master-data-services.md)   
 [电子邮件通知故障排除 (Master Data Services)](http://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-email-notifications-master-data-services.aspx)   
 [配置业务规则以发送通知 & #40;Master Data Services & #41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  

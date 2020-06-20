---
title: 通知 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- notifications [Master Data Services]
- notifications [Master Data Services], about notifications
- e-mail [Master Data Services]
- e-mail [Master Data Services], about e-mail notifications
ms.assetid: d7ad32d5-9fe5-48fd-8c61-0b00c0aff082
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6891bba64da82a1a83f5ea4a44bf3fa1f52ddd67
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971157"
---
# <a name="notifications-master-data-services"></a>通知 (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]可以配置为在业务规则验证失败时发送电子邮件通知或模型版本的状态发生更改。  
  
## <a name="how-notifications-are-sent"></a>如何发送通知  
 在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中配置通知。 通知通过使用承载数据库的实例上的数据库邮件发送电子邮件 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 。 有关数据库邮件的详细信息，请参阅 [机丛书中的](../relational-databases/database-mail/database-mail-configuration-objects.md) 数据库邮件配置对象 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 部分。  
  
## <a name="when-notifications-are-sent"></a>何时发送通知  
 配置通知后，可以在以下实例中发送自动化的电子邮件通知。  
  
|实例|说明|  
|--------------|-----------------|  
|数据未能通过业务规则验证|各个业务规则还必须配置为在属性值未能通过业务规则验证时发送电子邮件。 有关详细信息，请参阅 [配置业务规则以发送通知 (Master Data Services)](configure-business-rules-to-send-notifications-master-data-services.md)中配置通知。|  
|模型版本状态更改|每当模型版本的状态更改时，作为模型管理员的用户将自动收到通知。 有关详细信息，请参阅[管理员 &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)。|  
  
## <a name="system-settings"></a>系统设置  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中有多个设置可以影响通知。 可以在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中或直接在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库的“系统设置”表中调整这些设置。 有关详细信息，请参阅[系统设置 (Master Data Services)](../../2014/master-data-services/system-settings-master-data-services.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|配置 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 以发送电子邮件通知。|[配置电子邮件通知 (Master Data Services)](../../2014/master-data-services/configure-email-notifications-master-data-services.md)|  
|配置 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 以在属性值更改时发送通知。|[配置业务规则以发送通知 (Master Data Services)](configure-business-rules-to-send-notifications-master-data-services.md)|  
  
## <a name="related-content"></a>相关内容  
  
-   [业务规则 (Master Data Services)](../../2014/master-data-services/business-rules-master-data-services.md)  
  
-   [版本 (Master Data Services)](../../2014/master-data-services/versions-master-data-services.md)  
  
-   [电子邮件通知故障排除 (Master Data Services)](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-email-notifications-master-data-services.aspx)  
  
  

---
title: "通知 (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "通知 [Master Data Services]"
  - "通知 [Master Data Services], 关于通知"
  - "电子邮件 [Master Data Services]"
  - "电子邮件 [Master Data Services], 关于电子邮件通知"
ms.assetid: d7ad32d5-9fe5-48fd-8c61-0b00c0aff082
caps.latest.revision: 15
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 15
---
# 通知 (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 可以配置为当业务规则验证失败、模型版本状态更改或变更集状态更改时发送电子邮件通知。  
  
## 如何发送通知  
 在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中配置通知。 通过使用承载 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]实例上的“数据库邮件”，在邮件中发送通知。 有关数据库邮件的详细信息，请参阅 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 机丛书中的[数据库邮件配置对象](../relational-databases/database-mail/database-mail-configuration-objects.md)部分。  
  
## 何时发送通知  
 配置通知后，可以在以下实例中发送自动化的电子邮件通知。  
  
|实例|Description|  
|--------------|-----------------|  
|数据未能通过业务规则验证|各个业务规则还必须配置为在属性值未能通过业务规则验证时发送电子邮件。 通知包含以下信息。<br /><br /> Model<br /><br /> 版本<br /><br /> 实体<br /><br /> 成员代码<br /><br /> 失败的业务规则<br /><br /> 链接到其属性值未通过业务规则的成员<br /><br /> 通知发出的时间<br /><br /> 有关详细信息，请参阅[配置业务规则以发送通知 (Master Data Services)](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)。|  
|模型版本状态更改|每当模型版本的状态更改时，作为模型管理员的用户将自动收到通知。 通知包含以下信息。<br /><br /> Model<br /><br /> 版本<br /><br /> 版本的先前和当前状态<br /><br /> 通知发出的时间<br /><br /> 有关详细信息，请参阅[管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。|  
|变更集状态更改|实体的变更集状态每次发生更改时，均需要审批，实体管理员和/或更改集的所有者会自动收到通知。 通知包含以下信息。<br /><br /> Model<br /><br /> 版本<br /><br /> 变更集名称<br /><br /> 先前状态<br /><br /> 当前状态<br /><br /> 用于应用变更集以便查看和修改挂起更改的链接。<br /><br /> 有关详细信息，请参阅[变更集 (Master Data Services)](../master-data-services/changesets-master-data-services.md)。|  
  
## 系统设置  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中有多个设置可以影响通知。 可以在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中或直接在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库的“系统设置”表中调整这些设置。 有关详细信息，请参阅[系统设置 (Master Data Services)](../master-data-services/system-settings-master-data-services.md)。  
  
## 相关任务  
  
|任务说明|主题|  
|----------------------|-----------|  
|配置 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 以发送电子邮件通知。|[配置电子邮件通知 (Master Data Services)](../master-data-services/configure-email-notifications-master-data-services.md)|  
|配置 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 以在属性值更改时发送通知。|[配置业务规则以发送通知 (Master Data Services)](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
  
## 相关内容  
  
-   [业务规则 (Master Data Services)](../master-data-services/business-rules-master-data-services.md)  
  
-   [版本 (Master Data Services)](../master-data-services/versions-master-data-services.md)  
  
-   [电子邮件通知故障排除 (Master Data Services)](http://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-email-notifications-master-data-services.aspx)  
  
  
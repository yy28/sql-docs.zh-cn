---
title: 通知 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
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
manager: craigg
ms.openlocfilehash: de89d59c6205dd2ab0789492a746b925fa74b5c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65486036"
---
# <a name="notifications-master-data-services"></a>通知 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 可以配置为当业务规则验证失败、模型版本状态更改或变更集状态更改时发送电子邮件通知。  
  
## <a name="how-notifications-are-sent"></a>如何发送通知  
 在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中配置通知。 通过使用承载 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 实例上的“数据库邮件”，在邮件中发送通知。 有关数据库邮件的详细信息，请参阅 [机丛书中的](../relational-databases/database-mail/database-mail-configuration-objects.md) 数据库邮件配置对象 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 部分。  
  
## <a name="when-notifications-are-sent"></a>何时发送通知  
 配置通知后，可以在以下实例中发送自动化的电子邮件通知。  
  
|实例|Description|  
|--------------|-----------------|  
|数据未能通过业务规则验证|各个业务规则还必须配置为在属性值未能通过业务规则验证时发送电子邮件。 通知包含以下信息。<br /><br /> “模型”<br /><br /> 版本<br /><br /> 实体<br /><br /> 成员代码<br /><br /> 失败的业务规则<br /><br /> 链接到其属性值未通过业务规则的成员<br /><br /> 通知发出的时间<br /><br /> 有关详细信息，请参阅 [配置业务规则以发送通知 (Master Data Services)](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)中配置通知。|  
|模型版本状态更改|每当模型版本的状态更改时，作为模型管理员的用户将自动收到通知。 通知包含以下信息。<br /><br /> “模型”<br /><br /> 版本<br /><br /> 版本的先前和当前状态<br /><br /> 通知发出的时间<br /><br /> 有关详细信息，请参阅 [管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。|  
|变更集状态更改|实体的变更集状态每次发生更改时，均需要审批，实体管理员和/或更改集的所有者会自动收到通知。 通知包含以下信息。<br /><br /> “模型”<br /><br /> 版本<br /><br /> 变更集名称<br /><br /> 先前状态<br /><br /> 当前状态<br /><br /> 用于应用变更集以便查看和修改挂起更改的链接。<br /><br /> 有关详细信息，请参阅[变更集 (Master Data Services)](../master-data-services/changesets-master-data-services.md)。|  
  
## <a name="system-settings"></a>系统设置  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中有多个设置可以影响通知。 可以在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中或直接在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库的“系统设置”表中调整这些设置。 有关详细信息，请参阅[系统设置 (Master Data Services)](../master-data-services/system-settings-master-data-services.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|配置 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 以发送电子邮件通知。|[配置电子邮件通知 (Master Data Services)](../master-data-services/configure-email-notifications-master-data-services.md)|  
|配置 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 以在属性值更改时发送通知。|[配置业务规则以发送通知 (Master Data Services)](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
  
## <a name="related-content"></a>相关内容  
  
-   [业务规则 (Master Data Services)](../master-data-services/business-rules-master-data-services.md)  
  
-   [版本 (Master Data Services)](../master-data-services/versions-master-data-services.md)  
  
-   [电子邮件通知故障排除 (Master Data Services)](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-email-notifications-master-data-services.aspx)  
  
  

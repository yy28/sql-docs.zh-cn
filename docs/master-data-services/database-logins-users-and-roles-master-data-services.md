---
title: "数据库登录名、用户和角色 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [Master Data Services], database roles
- database [Master Data Services], users
- security [Master Data Services], database users
- database [Master Data Services], roles
- database [Master Data Services], logins
- security [Master Data Services], database logins
ms.assetid: 72ee383e-a619-461b-9f9d-1cac162ab0c5
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c22d739812318cf6c29559164df18fc4c07fe834
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2018
---
# <a name="database-logins-users-and-roles-master-data-services"></a>数据库登录名、用户和角色 (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 包括在承载 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 数据库的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 实例上自动安装的登录名、用户和角色。 不应对这些登录名、用户和角色做任何修改。  
  
## <a name="logins"></a>登录名  
  
|登录|Description|  
|-----------|-----------------|  
|**mds_dlp_login**|允许创建 UNSAFE 程序集。 有关详细信息，请参阅 [Creating an Assembly](../relational-databases/clr-integration/assemblies/creating-an-assembly.md)。<br /><br /> -具有随机生成的密码的禁用的登录名。<br /><br /> - 映射到 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库的 dbo。<br /><br /> - 对于 msdb，mds_clr_user 映射到此登录名。|  
|**mds_email_login**|用于通知的启用的登录名。<br /><br /> 对于 msdb 和 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库，mds_email_user 映射到此登录名。|  
  
## <a name="msdb-users"></a>msdb 用户  
  
|用户|Description|  
|----------|-----------------|  
|**mds_clr_user**|未使用。 映射到 mds_dlp_login。|  
|**mds_email_user**|用于通知。<br /><br /> - 映射到 mds_email_login。<br /><br /> - 是角色 DatabaseMailUserRole 的成员。|  
  
## <a name="master-data-services-database-users"></a>Master Data Services 数据库用户  
  
|用户|Description|  
|----------|-----------------|  
|**mds_email_user**|用于通知。<br /><br /> - 具有针对 mdm 架构的 SELECT 权限。<br /><br /> - 具有针对 mdm.MemberGetCriteria 用户定义的表类型的 EXECUTE 权限。<br /><br /> - 具有针对 mdm.udpNotificationQueueActivate 存储过程的 EXECUTE 权限。|  
|**mds_schema_user**|拥有 mdm 和 mdq 架构。 默认架构为 mdm。<br /><br /> 不具有映射到它的登录名。|  
|**mds_ssb_user**|用于执行 Service Broker 任务。<br /><br /> -具有针对所有架构的 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE 权限。<br /><br /> -不具有映射到它的登录名。|  
  
## <a name="master-data-services-database-role"></a>Master Data Services 数据库角色  
  
|角色|Description|权限|  
|----------|-----------------|-----------------|  
|**mds_exec**|此角色包含创建 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] Web 应用程序并且为应用程序池指定帐户时在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中指定的帐户。|针对所有架构的 EXECUTE 权限。<br /><br /> <br /><br /> 针对以下表的 ALTER、INSERT 和 SELECT 权限：<br /><br /> mdm.tblStgMember<br /><br /> mdm.tblStgMemberAttribute<br /><br /> mdm.tbleStgRelationship<br /><br /> <br /><br /> 针对以下表的 SELECT 权限：<br /><br /> mdm.tblUser<br /><br /> mdm.tblUserGroup<br /><br /> mdm.tblUserPreference<br /><br /> <br /><br /> 针对以下视图的 SELECT 权限：<br /><br /> mdm.viw_SYSTEM_SECURITY_NAVIGATION<br /><br /> mdm.viw_SYSTEM_SECURITY_ROLE_ACCCESSCONTROL<br /><br /> mdm.viw_SYSTEM_SECURITY_ROLE_ACCCESSCONTROL_MEMBER<br /><br /> mdm.viw_SYSTEM_SECURITY_USER_MODEL|  
  
## <a name="schemas"></a>架构  
  
|角色|Description|  
|----------|-----------------|  
|**mdm**|包含除了在 mdq 架构中包含的函数之外的所有 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库和 Service Broker 对象。|  
|**mdq**|包含与基于正则表达式或相似性筛选成员结果相关的以及用于设置通知电子邮件格式的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库函数。|  
|**stg**|包含与临时过程有关的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库表、存储过程和视图。 不要删除任何这些对象。 有关临时过程的详细信息，请参阅[概述：导入表中数据 (Master Data Services)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)。|  
  
## <a name="see-also"></a>另请参阅  
 [数据库对象安全性 (Master Data Services)](../master-data-services/database-object-security-master-data-services.md)  
  
  

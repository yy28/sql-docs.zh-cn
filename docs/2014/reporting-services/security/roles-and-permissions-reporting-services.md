---
title: 角色和权限 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- access controls [Reporting Services]
- permissions [Reporting Services], about permissions
- security [Reporting Services], identity and access control
- authentication [Reporting Services]
- permissions [Reporting Services]
- security [Reporting Services], role-based
- identity [Reporting Services]
ms.assetid: eea655fe-43ed-418d-8233-b288a8f4daa4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0e6098a51afde04164e3ef0dfa5e5297457b4440
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101799"
---
# <a name="roles-and-permissions-reporting-services"></a>角色和权限 (Reporting Services)
  Reporting Services 提供身份验证子系统和基于角色的授权模型。 身份验证和授权模型取决于相应的报表服务器是在本机模式下运行还是在 SharePoint 模式下运行。 如果报表服务器是 SharePoint 部署的一部分，则 SharePoint 权限将确定哪些用户对此报表服务器具有访问权限。  
  
## <a name="identity-and-access-control-for-native-mode"></a>本机模式下的标识和访问控制  
 默认的身份验证基于 Windows 身份验证和集成安全性。 可以更改身份验证设置以允许报表服务器对不同的身份验证请求作出响应，甚至可以用您提供的自定义身份验证扩展插件替换默认安全功能。  
  
 授权基于分配给主体的角色。 每个角色由一组相关任务组成，这些任务又由一组相关操作组成。 例如， **“管理报表”** 任务授予对以下报表服务器操作的访问权限：查看报表、添加报表、更新报表、删除报表、计划报表和更新报表属性。  
  
## <a name="identity-and-access-control-for-sharepoint-mode"></a>SharePoint 模式下的标识和访问控制  
 在 SharePoint 集成模式下，身份验证和授权都在请求到达报表服务器之前在 SharePoint 站点处理。 根据身份验证的配置方式，来自 SharePoint 站点的请求包含安全标记或可信用户名。 为 SharePoint 用户和组设置的权限授予对置于 SharePoint 库中的报表服务器项的访问权限。  
  
## <a name="in-this-section"></a>本节内容  
 [授予对本机模式报表服务器的权限](granting-permissions-on-a-native-mode-report-server.md)  
 介绍基于角色的授权模型，该模型提供对内容和操作的访问权限。  
  
 [在 SharePoint 站点上授予对报表服务器项的权限](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
 说明如何使用 SharePoint 组、权限级别和权限来控制对报表服务器的访问权限。  
  
## <a name="see-also"></a>另请参阅  
 [针对报表服务器的身份验证](authentication-with-the-report-server.md)   
 [授予对本机模式报表服务器的权限](granting-permissions-on-a-native-mode-report-server.md)  
  
  

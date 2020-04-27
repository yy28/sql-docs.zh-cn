---
title: 系统级任务 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- system-level tasks [Reporting Services]
ms.assetid: 7023b388-40b2-4590-b227-115cf380a1e7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3c1785e927bf2d2b90322c90f2adace4555047af
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101535"
---
# <a name="system-level-tasks"></a>系统级任务
  系统级任务是与应用于整个报表服务器站点的操作相关的权限的集合。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 还包括应用于特定项的项级任务。 有关详细信息，请参阅 [项级任务](tasks-and-permissions-item-level-tasks.md)。 有关任务和权限总体情况的详细信息，请参阅 [Tasks and Permissions](tasks-and-permissions.md)。  
  
> [!NOTE]  
>  如果以编程方式使用这些任务，则必须使用支持系统级任务的方法。 有关详细信息，请参阅 <xref:ReportService2010.ReportingService2010.ListTasks%2A> 和 <xref:ReportService2010.ReportingService2010.ListRoles%2A>。  
  
## <a name="permissions-in-system-level-tasks"></a>系统级任务中的权限  
 下表给出了各个系统任务的权限集合。 所列出的权限仅供参考，目的是为每个任务的可用功能提供更准确的说明。  
  
|任务|权限|  
|----------|-----------------|  
|执行报表定义|执行报表定义（权限和任务名称相同）|  
|生成事件|生成事件|  
|管理作业|读取系统属性<br /><br /> 更新系统属性|  
|管理报表服务器属性|读取系统属性<br /><br /> 更新系统属性|  
|管理角色|创建角色<br /><br /> 删除角色<br /><br /> 读取角色属性<br /><br /> 更新角色属性|  
|管理共享计划|创建计划|  
|管理报表服务器安全性|读取系统安全策略<br /><br /> 更新系统安全策略|  
|查看报表服务器属性|读取系统属性|  
|查看共享计划|读取计划|  
  
## <a name="see-also"></a>另请参阅  
 [授予对本机模式报表服务器的权限](granting-permissions-on-a-native-mode-report-server.md)  
  
  

---
title: 设置角色 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c7e9db15-89f2-4d4d-8860-1e64c5821c4d
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: b1cf8c6f8442fc69669c10106f671040733e48ef
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66092225"
---
# <a name="setup-role"></a>安装角色
  使用此页可以指定是使用“功能选择”页来分别选择各项功能，还是使用安装角色来进行安装。  
  
 `setup role`是实现预定义 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置所需全部功能和共享组件的固定选择集。  
  
## <a name="options"></a>选项  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]功能安装**  
 选择此选项可分别选择各项功能和共享组件。 实例功能包括数据库引擎服务、Analysis Services（本机模式）和 Reporting Services。  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]PowerPivot for SharePoint**  
 选择此选项可以在 SharePoint 2010 场中安装 Analysis Services 服务器组件。 此选项在场中部署 PowerPivot 系统服务和 Analysis Services 服务器，同时支持对包含嵌入式 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据的已发布 Excel 工作簿进行查询和数据处理。  
  
 如果需要使用关系数据库引擎实例在 SharePoint 场中承载数据库，可以选择在安装中添加关系数据库引擎实例。 如果已配置场，则不必选择。  
  
 安装完成后，必须使用以下方法之一配置软件：PowerPivot 配置工具、PowerShell cmdlet 或 SharePoint 2010 管理中心。 与以往的版本相比，安装程序不再执行 PowerPivot 安装的任何配置任务。  
  
 基于角色的安装不包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerPivot for Excel 客户端应用程序。 将单独安装此客户端应用程序。  
  
 **所有功能以及默认值**  
 选择此安装角色将安装此版本提供的所有功能。 请注意，从该角色中排除 PowerPivot for SharePoint。 您必须使用 PowerPivot for SharePoint 安装角色来安装该功能。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 配置为使用 **NT AUTHORITY\NETWORK SERVICE** 帐户开始。 将当前用户设置为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**sysadmin** 角色的成员。 此选项设置的值可以通过指定其他命令行参数来覆盖。  
  
 当操作系统不是域控制器时，默认情况下，数据库引擎和 Reporting Services 将使用 NTAUTHORITY\NETWORK SERVICE 帐户，Integration Services 将使用 NTAUTHORITY\NETWORK SERVICE 帐户，而 SQL 全文筛选器后台程序启动器将使用 NTAUTHORITY\LOCAL SERVICE 帐户。  
  
## <a name="see-also"></a>另请参阅  
 [安装 PowerPivot for SharePoint](https://go.microsoft.com/fwlink/?LinkId=206906)   
 [硬件和软件要求（PowerPivot for SharePoint](https://go.microsoft.com/fwlink/?LinkId=216823)   
 [功能选择](../../../2014/sql-server/install/feature-selection.md)  
  
  

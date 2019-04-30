---
title: Analysis Services 配置 – 帐户设置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services configuration
- account provisioning
ms.assetid: 169b1af2-6fe2-467f-8ca4-919f24c620ce
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 095709115c15e770b8ad54678d4a359ab4b04ac8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63215155"
---
# <a name="analysis-services-configuration---account-provisioning"></a>Analysis Services 配置 – 帐户设置
  使用此页可以设置服务器节点，并向要求对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 进行不受限访问的用户或服务授予管理权限。 安装程序不会自动将本地 Windows 组 BUILTIN\Administrators 添加到要安装的实例的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器管理员角色。 如果您想要将本地管理员组添加到服务器管理员角色，则必须显式指定该组。  
  
 如果您正在安装 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]，确保将管理权限授予负责在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 场中部署 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 服务器的 SharePoint 场管理员或服务管理员。 有关详细信息[!INCLUDE[ssGeminiMTS](../../includes/ssgeminimts-md.md)]安装和服务帐户要求，请参阅[安装与 SharePoint 的 SQL Server BI 功能&#40;PowerPivot 和 Reporting Services&#41;](../../../2014/sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)。  
  
## <a name="options"></a>选项  
 **服务器模式** - 服务器模式指定可部署到服务器的 Analysis Services 数据库的类型。 服务器模式在安装过程中确定，之后不能修改。 各模式是互斥的，也就是说，您需要两个 Analysis Services 实例，它们配置为不同的模式，以便同时支持典型 OLAP 和表格模型解决方案。  
  
 **指定管理员** - 必须为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例指定至少一个服务器管理员。 您指定的用户或组将成为所安装的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的服务器管理员角色的成员。 这些都必须是与安装该软件的计算机处于同一域中的 Windows 域用户帐户。  
  
> [!NOTE]  
>  用户帐户控制 (UAC) 是一个 Windows 安全功能，它要求在运行管理操作或应用程序之前，先由管理员专门审批。 由于 UAC 在默认情况下处于打开状态，因此系统将提示您允许需要提升权限的特定操作。 您可以配置 UAC 来更改默认行为，或针对特定程序自定义 UAC。 有关 UAC 和 UAC 配置的详细信息，请参阅 [User Account Control Step by Step Guide](https://go.microsoft.com/fwlink/?linkid=196350)（用户帐户控制分步指南）和 [User Account Control (Wikipedia)](https://go.microsoft.com/fwlink/?linkid=196351)（用户帐户控制 (Wikipedia)）。  
  
## <a name="see-also"></a>请参阅  
 [配置服务帐户&#40;Analysis Services&#41;](../../../2014/analysis-services/instances/configure-service-accounts-analysis-services.md)   
 [配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  

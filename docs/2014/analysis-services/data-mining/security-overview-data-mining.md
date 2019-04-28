---
title: 安全性概述 （数据挖掘） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- security [Analysis Services - data mining], about security
ms.assetid: 387bde00-bcf3-4612-b27b-f9f608dbf71e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 85a208cdc973cf4e54bb0a68020182d41eb798f3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62733037"
---
# <a name="security-overview-data-mining"></a>安全性概述（数据挖掘）
  可以在多个级别对 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 进行保护。 您必须保护每个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例及其数据源，以确保只有经过授权的用户具有所选维度、挖掘模型以及数据源的读或读/写权限。 您还必须保护基础数据源以防止未经授权的用户恶意破坏敏感商业信息。 以下主题说明了保护 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的过程。  
  
##  <a name="bkmk_Architecture"></a> 安全体系结构  
 查看以下资源以了解 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例的基本安全体系结构，包括 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 是如何使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 身份验证来对用户访问进行身份验证的。  
  
-   [安全角色（Analysis Services - 多维数据）](../multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)  
  
-   [安全属性](../server-properties/security-properties.md)  
  
-   [配置服务帐户 (Analysis Services)](../instances/configure-service-accounts-analysis-services.md)  
  
-   [授予对对象和操作的访问权限 (Analysis Services)](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
##  <a name="bkmk_Logon"></a> 为 Analysis Services 配置登录帐户  
 您必须为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 选择相应的登录帐户，并为该帐户指定权限。 同时，还必须确保 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 登录帐户只拥有执行必要任务所需的必要权限，其中包括基础数据源的相应权限。  
  
 对于数据挖掘，与查看或查询模型相比，您需要一组不同的权限来生成和处理模型。 针对模型进行预测是一种查询，不需要管理权限。  
  
##  <a name="bkmk_Instance"></a> 保护 Analysis Services 实例  
 其次，您必须保护 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 计算机、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 计算机上的 Windows 操作系统、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 本身以及 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用的数据源。  
  
##  <a name="bkmk_Access"></a> 配置对 Analysis Services 的访问权限  
 设置和定义 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例的授权用户时，您需要决定哪些用户还应具有管理特定数据库对象的权限，哪些用户能够查看对象的定义或浏览模型，以及哪些用户能够直接访问数据源。  
  
##  <a name="bkmk_DMspecial"></a> 数据挖掘的特殊注意事项  
 若要使分析人员或开发人员能够创建和测试数据挖掘模型，必须向分析人员或开发人员授予对存储挖掘模型的数据库的管理权限。 这样，数据挖掘分析人员或开发人员就可以创建或删除与数据挖掘无关的其他对象，包括由其他分析人员或开发人员创建并要使用的数据挖掘对象或数据挖掘解决方案中不包含的 OLAP 对象。  
  
 相应地，在创建数据挖掘解决方案时，您必须平衡好分析人员或开发人员开发、测试和优化模型的需要与其他用户的需要，并采取措施对现有数据库对象进行保护。 一种可能的方法是创建独立的数据挖掘专用数据库或为每位分析人员创建单独的数据库。  
  
 尽管创建模型需要最高级别的权限，但您可以使用基于角色的安全措施，控制用户为进行其他操作而访问数据挖掘模型，例如处理、浏览或查询。 创建角色时，您可设置特定于数据挖掘对象的权限。 任何角色成员用户都将自动具有与该角色关联的所有权限。  
  
 此外，数据挖掘模型还会经常引用包含敏感信息的数据源。 如果挖掘结构和挖掘模型已配置为允许用户从模型钻取结构中的数据，则您必须采取预防措施来屏蔽敏感信息，或限制具有基础数据的访问权限的用户。  
  
 如果使用 Integration Services 包清理数据、更新挖掘模型或进行预测，则必须确保 Integration Services 服务拥有存储有模型的数据库的相应权限，以及源数据的相应权限。  
  
## <a name="see-also"></a>请参阅  
 [角色和权限 (Analysis Services)](../multidimensional-models/roles-and-permissions-analysis-services.md)  
  
  

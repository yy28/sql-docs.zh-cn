---
title: 服务器配置实用工具（Excel 数据挖掘外接程序） |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 28435f86-5cec-4a1e-9b7d-b2069c1ddddb
author: minewiskan
ms.author: owend
ms.openlocfilehash: f8a2006947cf4e4bffee0365ffbbf0b3b1c76bbf
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940728"
---
# <a name="server-configuration-utility-data-mining-add-ins-for-excel"></a>服务器配置实用工具（Excel 数据挖掘外接程序）
  在安装 Excel 数据挖掘外接程序时，还会安装服务器配置实用工具，并将在首次打开外接程序时运行。本主题介绍如何使用实用程序连接到实例 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，并设置用于处理数据挖掘模型的数据库。  
  

  
##  <a name="step-1-connect-to-analysis-services"></a><a name="bkmk_step1"></a>步骤1：连接到 Analysis Services  
 选择提供数据挖掘算法并存储您的数据挖掘模型的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器。  
  
 在创建连接以启用数据挖掘时，应选择可使用数据挖掘模型进行试验的服务器。 我们建议您在服务器上创建新数据库并将该数据库专用于数据挖掘，或请求管理员为您准备数据挖掘服务器。 这样您可以构建模型而不会影响其他服务的性能。  
  
 请注意用于数据挖掘的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器不需要位于您的源数据所在的同一服务器上。  
  
 **服务器名称**  
 键入包含将用于数据挖掘的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的服务器名称。  
  
 **身份验证**  
 指定身份验证方法。 Windows 身份验证对于连接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 是必需的，除非您的管理员配置了通过 HTTPPump 访问服务器。  
  
##  <a name="step-2-allow-temporary-models"></a><a name="bkmk_step2"></a>步骤2：允许临时模型  
 在您可以使用外接程序前，必须更改 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器属性以允许创建临时挖掘模型。  
  
 临时挖掘模型也称为 "*会话模型*"。 这是因为只能在当前会话处于打开状态时存储模型。 关闭到服务器的连接后，将结束会话，会话期间所使用的所有模型都会被删除。  
  
 使用会话挖掘模型不会影响服务器上的存储空间，不过创建数据挖掘模型所需的开销可能会影响服务器的性能。  
  
 该向导首先检测您指定的服务器上的设置。 如果服务器已经允许临时挖掘模型，则可以单击 "**下一步**" 继续。 该向导还提供有关如何在指定的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器上启用临时挖掘模型的说明，或如何向 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 管理员发送请求的说明。  
  
##  <a name="step-3-create-database-for-add-in-users"></a><a name="bkmk_step3"></a>步骤3：为外接程序用户创建数据库  
 在设置和配置向导的此页上，您可以创建专用于数据挖掘的新数据库，或选择现有 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库。  
  
> [!WARNING]  
>  数据挖掘需要在多维模式下运行的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例。 表格模式不支持数据挖掘。  
  
 我们建议您创建专用于数据挖掘的单独数据库。 这允许您使用数据挖掘模型进行实验，而不影响其他解决方案对象。  
  
 如果您选择 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例上的现有数据库，请注意如果使用外接程序创建模型且该名称的模型已存在，则可能覆盖现有模型。  
  
 **创建新的数据库**  
 选择此选项可以在所选服务器上创建新数据库。 数据挖掘数据库将存储您的数据源、挖掘结构和挖掘模型。  
  
 **数据库名称**  
 键入新数据库的名称。 如果该名称未被使用，将为您创建它。  
  
 **使用现有数据库**  
 选择此选项可以使用现有 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库。  
  
 **Database**  
 如果您选择了使用现有数据库的选项，必须从列表中选择该数据库名称。  
  
##  <a name="step-4-give-add-in-users-appropriate-permissions"></a><a name="bkmk_step4"></a>步骤4：向外接程序用户授予适当的权限  
 您必须确保您（和其他任何将使用外接程序的用户）拥有浏览、编辑、处理或创建数据挖掘结构和模型所必需的权限。  
  
 默认情况下，使用外接程序时需要进行集成的 Windows 身份验证。  
  
 **将数据库管理权限授予外接程序用户**  
 选择此选项将授予所列用户对数据库的管理访问权限。  
  
> [!NOTE]  
>  这些权限仅应用于 "**数据库名称**" 框中列出的数据库。  
  
 **数据库名称**  
 显示所选数据库的名称。  
  
 **指定要添加的用户或组**  
 选择将对要用于数据挖掘的数据库有访问权限的登录名。  
  
 **添加**  
 单击此项可打开一个对话框，在其中可添加用户或组。  
  
 **删除**  
 单击此项可从具有管理权限的用户列表中删除所选用户或组。  
  
  

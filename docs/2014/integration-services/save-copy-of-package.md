---
title: 保存包的副本 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.savecopyas.f1
helpviewer_keywords:
- Save Copy of Package dialog box
ms.assetid: 7b44c0d7-d8fa-4491-8836-0899f621d3a8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0e28fec1fb562c5ba6ed28ad615f40ada5fc2db9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766789"
---
# <a name="save-copy-of-package"></a>保存包的副本
  可以使用 **中的** “保存包的副本” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]对话框，将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包的副本从 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 保存到其他位置，并根据需要修改包的保护级别。  
  
## <a name="options"></a>选项  
 **包位置**  
 选择要在其中保存包副本的存储位置的类型。 可用选项包括：  
  
 **SQL Server**  
  
 **文件系统**  
  
 **SSIS 包存储区**  
  
 **Server**  
 键入服务器名称或从列表中选择一个服务器。 只有当存储位置为 **SQL Server** 或 **“SSIS 包存储区”** 时，此选项才可用。  
  
 **身份验证**  
 选择 Windows 身份验证或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证。 只有在存储位置为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]时，此选项才可用。  
  
> [!IMPORTANT]  
>  请尽可能使用 Windows 身份验证。  
  
 **身份验证类型**  
 选择身份验证类型。  
  
 **用户名**  
 如果使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证，请提供用户名。  
  
 **密码**  
 如果使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证，请提供密码。  
  
 **包路径**  
 键入包路径，或单击浏览 **（...）** 按钮，然后定位存储包的文件夹。  
  
 **保护级别**  
 单击浏览 **（...）** 按钮，然后更新中的保护级别**包保护级别**对话框。 有关详细信息，请参阅 [“包和项目保护级别”对话框](../../2014/integration-services/package-and-project-protection-level-dialog-box.md)。  
  
## <a name="see-also"></a>请参阅  
 [“导入包”对话框 UI 参考](../../2014/integration-services/import-package-dialog-box-ui-reference.md)   
 [“导出包”对话框 UI 参考](../../2014/integration-services/export-package-dialog-box-ui-reference.md)   
 [保存包](save-packages.md)   
 [导入和导出包（SSIS 服务）](../../2014/integration-services/import-and-export-packages-ssis-service.md)  
  
  

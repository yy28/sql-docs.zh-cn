---
title: "\"导出包\" 对话框 UI 参考 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.dtsserver.exportpackage.f1
helpviewer_keywords:
- Export Package dialog box
ms.assetid: 3742fe8a-ef57-444d-b2fb-cb25d16bae97
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c1cca0a2761f87d6f4f3837df1e9a0bdcc5b91a4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66058913"
---
# <a name="export-package-dialog-box-ui-reference"></a>“导出包”对话框 UI 参考
  可以使用 **中的** “导出包” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]对话框，将 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包导出到其他位置并根据需要修改包的保护级别。  
  
## <a name="options"></a>选项  
 **包位置**  
 选择要将包导出到的存储区的类型。 提供了以下选项：  
  
 **SQL Server**  
  
 **文件系统**  
  
 **SSIS 包存储**  
  
 **Server**  
 键入服务器名称或从列表中选择一个服务器。  
  
 **身份验证**  
 选择 Windows 身份验证或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证。 只有在存储位置为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]时，此选项才可用。  
  
> [!IMPORTANT]  
>  请尽可能使用 Windows 身份验证。  
  
 **身份验证类型**  
 选择身份验证类型。  
  
 **用户名**  
 如果使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证，请提供用户名。  
  
 **权限**  
 如果使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证，请提供密码。  
  
 **包路径**  
 键入包路径，或单击浏览按钮 (…)，然后定位存储包的文件夹****。  
  
 **保护级别**  
 单击浏览按钮 (…)，然后在“包保护级别”对话框中更新保护级别********。 有关详细信息，请参阅[“包和项目保护级别”对话框](../../2014/integration-services/package-and-project-protection-level-dialog-box.md)。  
  
## <a name="see-also"></a>另请参阅  
 [保存包的副本](../../2014/integration-services/save-copy-of-package.md)   
 ["导入包" 对话框 UI 参考](../../2014/integration-services/import-package-dialog-box-ui-reference.md)   
 [保存包](save-packages.md)   
 [&#40;SSIS 服务导入和导出包&#41;](../../2014/integration-services/import-and-export-packages-ssis-service.md)  
  
  

---
title: 导入包对话框 UI 参考 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.dtsserver.importpackage.f1
helpviewer_keywords:
- Import Package dialog box
ms.assetid: 0e5fb127-c7ff-4dfa-b90e-d9bcf0ce763b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3e36fae15f6f4220565bcc3d14c0e125ca6818f0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058080"
---
# <a name="import-package-dialog-box-ui-reference"></a>“导入包”对话框 UI 参考
  可以使用 **中的** “导入包” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]对话框，导入 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包以及设置或修改包的保护级别。  
  
## <a name="options"></a>选项  
 **包位置**  
 选择要向其中导入包的存储位置的类型。 可用选项包括：  
  
 **SQL Server**  
  
 **文件系统**  
  
 **SSIS 包存储区**  
  
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
  
 **密码**  
 如果使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证，请提供密码。  
  
 **包路径**  
 键入包的路径，或单击浏览按钮 (…) 并查找包  。  
  
 **包名称**  
 可以根据需要对包进行重命名。 默认名称是要导入的包的名称。  
  
 **保护级别**  
 单击浏览按钮 (…)，然后在“包保护级别”对话框中更新保护级别   。 有关详细信息，请参阅 [“包和项目保护级别”对话框](../../2014/integration-services/package-and-project-protection-level-dialog-box.md)。  
  
## <a name="see-also"></a>请参阅  
 [保存包的副本](../../2014/integration-services/save-copy-of-package.md)   
 [“导出包”对话框 UI 参考](../../2014/integration-services/export-package-dialog-box-ui-reference.md)   
 [保存包](save-packages.md)   
 [导入和导出包（SSIS 服务）](../../2014/integration-services/import-and-export-packages-ssis-service.md)  
  
  

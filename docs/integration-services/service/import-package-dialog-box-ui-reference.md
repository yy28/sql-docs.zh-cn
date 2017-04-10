---
title: "“导入包”对话框 UI 参考 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.dtsserver.importpackage.f1"
helpviewer_keywords: 
  - "“导入包”对话框"
ms.assetid: 0e5fb127-c7ff-4dfa-b90e-d9bcf0ce763b
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# “导入包”对话框 UI 参考
  可以使用 **中的** “导入包” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]对话框，导入 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包以及设置或修改包的保护级别。  
  
## 选项  
 **包位置**  
 选择要向其中导入包的存储位置的类型。 可用选项包括：  
  
 **SQL Server**  
  
 **文件系统**  
  
 **SSIS 包存储区**  
  
 **Server**  
 键入服务器名称或从列表中选择一个服务器。  
  
 **身份验证**  
 选择 Windows 身份验证或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。 只有在存储位置为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，此选项才可用。  
  
> [!IMPORTANT]  
>  请尽可能使用 Windows 身份验证。  
  
 **身份验证类型**  
 选择身份验证类型。  
  
 **用户名**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，请提供用户名。  
  
 **密码**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，请提供密码。  
  
 **包路径**  
 键入包的路径，或单击浏览按钮 **(…)** 并查找包。  
  
 **包名称**  
 可以根据需要对包进行重命名。 默认名称是要导入的包的名称。  
  
 **保护级别**  
 单击浏览按钮 **(…)**，然后在“包保护级别”对话框中更新保护级别。 有关详细信息，请参阅[“包和项目保护级别”对话框](../../integration-services/packages/package-and-project-protection-level-dialog-box.md)。  
  
## 另请参阅  
 [保存包的副本](../Topic/Save%20Copy%20of%20Package.md)   
 [“导出包”对话框 UI 参考](../../integration-services/service/export-package-dialog-box-ui-reference.md)   
 [保存包](../../integration-services/save-packages.md)   
 [导入和导出包（SSIS 服务）](../../integration-services/service/import-and-export-packages-ssis-service.md)  
  
  
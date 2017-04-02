---
title: "在 SQL Server Data Tools 中运行包 | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Integration Services 包, 运行"
  - "SSIS 包, 运行"
  - "包 [Integration Services], 运行"
  - "SQL Server Integration Services 包, 运行"
ms.assetid: 318e6beb-5540-4101-82a5-18c9d47f0570
caps.latest.revision: 58
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 58
---
# 在 SQL Server Data Tools 中运行包
  在开发、调试和测试包的过程中，通常在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中运行包。 在从 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器运行包时，包始终可以立即运行。  
  
 包运行时， [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器在 **“进度”** 选项卡上显示包执行的进度。 除了有关包中失败的所有任务或容器的信息外，还可以查看包及其任务和容器的开始时间和完成时间。 在包完成运行后，运行时信息仍显示在“执行结果”选项卡上。 有关详细信息，请参阅 [Debugging Control Flow](../../integration-services/troubleshooting/debugging-control-flow.md)主题中的“进度报告”部分。  
  
 **设计时部署**。 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中运行包时，包被生成，然后部署到文件夹。 在运行包前，可以指定要包将部署到其中的文件夹。 如果未指定文件夹，默认将使用 **bin** 文件夹。 这种部署称为设计时部署。  
  
### 在 SQL Server Data Tools 中运行包  
  
1.  在“解决方案资源管理器”中，如果解决方案包含多个项目，则右键单击包含包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目，然后单击“设为启动对象”以便设置启动项目。  
  
2.  在“解决方案资源管理器”中，如果项目包含多个包，则右键单击某个包，然后单击“设为启动对象”以便设置启动包。  
  
3.  若要运行包，请执行以下操作：  
  
    -   打开要运行的包，然后单击菜单栏上的 **“启动调试”** ，或按 F5。 包运行完成后，按 Shift+F5 返回设计模式。  
  
    -   在“解决方案资源管理器”中，右键单击包，然后单击“执行包”。  
  
### 为设计时部署指定不同文件夹  
  
1.  在“解决方案资源管理器”中，右键单击包含要运行的包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目文件夹，然后单击“属性”。  
  
2.  在“\<项目名称>属性页”对话框中，单击“生成”。  
  
3.  更新 OutputPath 属性中的值以指定要用于设计时部署的文件夹，然后单击“确定”。  
  
## 另请参阅  
 [项目和包的执行](https://msdn.microsoft.com/library/hh213290.aspx)   
 [Integration Services (SSIS) 包](https://msdn.microsoft.com/library/ms141134.aspx)  
  
  
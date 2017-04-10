---
title: "使用保存的配置文件配置日志记录 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "容器 [Integration Services], 日志"
  - "日志 [Integration Services], 容器"
ms.assetid: e5fdbbcb-94ca-4912-aa7c-0d89cebbd308
caps.latest.revision: 42
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 42
---
# 使用保存的配置文件配置日志记录
  本过程介绍如何通过加载以前保存的日志记录配置文件来为包中的新容器配置日志记录。  
  
 默认情况下，包中的所有容器与其父容器使用相同的日志记录配置。 例如，Foreach 循环中的任务使用与 Foreach 循环相同的日志记录配置。  
  
### 为容器配置日志记录  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在 **SSIS** 菜单上，单击 **“日志记录”**。  
  
3.  展开包的树视图，并选择要配置的容器。  
  
4.  在 **“提供程序和日志”** 选项卡上，选择要用于该容器的日志。  
  
    > [!NOTE]  
    >  只能在包级创建日志。 有关详细信息，请参阅[在 SQL Server Data Tools 中启用包日志记录](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md)。  
  
5.  单击 **“详细信息”** 选项卡，单击 **“加载”**。  
  
6.  找到要使用的日志记录配置文件，并单击 **“打开”**。  
  
7.  （可选）通过在 **“事件”** 列中选中其复选框，选择要记录的其他日志项。 单击 **“高级”** 可以选择要为此项记录的信息类型。  
  
    > [!NOTE]  
    >  新容器可以包含最初用于创建日志记录配置的容器中所没有的其他日志项。 您必须手动选择这些其他日志项，才能对它们进行记录。  
  
8.  若要保存日志记录配置的更新后的版本，请单击 **“保存”**。  
  
9. 若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## 另请参阅  
 [Integration Services (SSIS) 日志记录](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
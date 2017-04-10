---
title: "Azure 存储连接管理器 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.afpstorageconn.f1"
  - "sql14.dts.designer.afpstorageconn.f1"
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
caps.latest.revision: 13
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 11
---
# Azure 存储连接管理器
  **Azure 存储连接管理器** 使一个 SSIS 包可使用你指定的属性值连接到 Azure 存储帐户：存储帐户名称和帐户密钥。  
  
>   [!NOTE] 若要确保 Azure 存储连接管理器和使用它的组件（即 Blob 源、Blob 目标、Blob 上传任务和 Blob 下载任务）可以连接到常规用途的存储帐户和 Blob 存储帐户，请确保[在此处](https://www.microsoft.com/download/details.aspx?id=49492)下载最新版本的 Azure 功能包。 有关这两种类型的存储帐户的详细信息，请参阅 [Microsoft Azure 存储空间简介](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts)。
  
 **Azure 存储连接管理器**是适用于 Azure for SQL Server 2016 的 SQL Server Integration Services (SSIS) 功能包的组件。 从 [此处](http://go.microsoft.com/fwlink/?LinkID=626967)下载功能包。  
  
1.  在“添加 SSIS 连接管理器”  对话框中，选择“AzureStorage” ，然后单击“添加” 。  
  
2.  在“Azure 存储连接管理器编辑器”对话框中，选择“使用 Azure 帐户”  以通过 Internet 连接到 Azure 存储服务，或选择“使用本地开发人员帐户”  以连接到 Azure 存储模拟器承载的本地服务。  
  
3.  如果选择了“使用 Azure 帐户”  选项，请执行以下操作：  
  
    1.  为“存储帐户名称”  和“帐户密钥”  字段指定值。 这些值将存储为 SSIS 包中的敏感数据。  
  
    2.  如果你想要使用 HTTPS 而不是 HTTP 来连接到 Azure 存储服务，请选择“使用 HTTPS”  。  
  
4.  单击 **“确定”** 关闭对话框。  
  
5.  你可以看到你在“属性”  窗口中创建的连接管理器的属性。  
  
  
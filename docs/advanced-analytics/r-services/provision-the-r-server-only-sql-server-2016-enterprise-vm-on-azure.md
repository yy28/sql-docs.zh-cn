---
title: "设置 Azure 上的 R Server Only SQL Server 2016 Enterprise VM | Microsoft Docs"
ms.custom: ""
ms.date: "12/22/2016"
ms.prod: "r-server"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c8826df7-aa67-4768-baa9-bdc875c4a766
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 5
---
# 设置 Azure 上的 R Server Only SQL Server 2016 Enterprise VM

Azure 上的 R Server Only SQL Server 2016 Enterprise 虚拟机是一个新选项，用于快速、方便地配置服务器环境以支持 R 解决方案。 此 Azure 虚拟机使用 Microsoft R Server（独立）进行了预配置。 

这一新的虚拟机替换了以前在 Azure 应用商店中提供的 Windows 虚拟机的 RRE。 

此虚拟机还包括用于部署在应用程序和后端系统中部署 R 分析的 DeployR Enterprise。 有关详细信息，请参阅[关于 Deploy R](https://msdn.microsoft.com/microsoft-r/deployr-about)。


## 设置 R Server 虚拟机

如果你刚接触 Azure VM 的使用，则我们建议查看本文以了解有关使用门户和配置虚拟机的详细信息。
[虚拟机 - 入门](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)

通过 Microsoft Azure 应用商店创建 R Server VM 
1. 单击“虚拟机”，然后在搜索框中输入 R Server。
2. 选择“R Server Only SQL Server 2016 Enterprise”
3. 按照以下文章中所述继续设置虚拟机：[https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-hero-tutorial/) 
7. 虚拟机已创建并运行之后，单击“连接”按钮以打开连接并登录到新计算机。
8. 进行连接时，“服务器管理器”会在默认情况下打开，但无需其他服务器配置。 关闭“服务器管理器”以访问桌面，并继续进行后续步骤：
    + 安装其他 R 工具或开发工具
    + 配置 DeployR  

在 Azure 经典门户中查找 R Server VM
1. 单击“虚拟机”，然后单击“新建”。
2. 在“新建”窗格中，“计算”和“虚拟机”应该已处于选择状态。 
3. 单击“从库中”以查找 VM 映像。 可以在搜索框中输入 R Server 或单击“Microsoft”，然后向下滚动，直到看到“R Server Only SQL Server 2016 Enterprise”。


## 安装 R 工具
默认情况下，Microsoft R Server 包含随 R 的基础安装而安装的所有 R 工具（包括 RTerm 和 RGui）。 如果要立即开始使用 R，则 RGui 的快捷方式已添加到桌面。

但是，你可能希望安装其他 R 工具，如 RStudio、R Tools for Visual Studio 或 Microsoft R Client。 请参阅以下链接以了解下载位置和说明：
+ [R Tools for Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx)
+ [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [RStudio for Windows](https://www.rstudio.com/products/rstudio/download/)

安装了这些工具之后，请确保使工具指向 R Server 库。

## 在虚拟机上使用 DeployR

使用在此 VM 上安装的 DeployR 实例需要一些附加步骤。 

配置 DeployR 实例：

1. 在 VM 上打开“DeployR 管理员实用工具”。
2. 按照如下所述设置 DeployR 管理员密码：[安装后步骤](https://msdn.microsoft.com/microsoft-r/deployr-install-on-windows)
3. 设置 DeployR Web 上下文。 有关详细信息，请参阅[云中的 DeployR 管理员安装](https://msdn.microsoft.com/microsoft-r/deployr-admin-install-in-cloud) 
4. 按照如下所述在 VM 上打开相应端口：[配置 Azure 终结点](https://msdn.microsoft.com/microsoft-r/deployr-admin-install-in-cloud#configuring-azure-endpoints) 
4. 按照如下所述更新 Windows 防火墙：[更新防火墙](https://msdn.microsoft.com/microsoft-r/deployr-admin-install-in-cloud#updating-the-firewall) 

## 访问 Azure 存储帐户中的数据 

需要使用 Azure 存储帐户中的数据时，有几个选项可用于访问或移动数据：


+ 使用实用工具（如 [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only)）将数据从存储帐户复制到本地文件系统。 

+ 将文件添加到存储帐户上的文件共享，然后在 VM 上以网络驱动器的形式装载文件共享。  有关详细信息，请参阅[装载 Azure 文件](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/)。 

## 使用 Azure Data Lake Storage (ADLS) 帐户中的数据

如果采用与用于 HDFS 文件系统（使用 webHDFS）的相同方式来引用存储帐户，则可以使用 ScaleR 从 ADLS 存储读取数据。  有关详细信息，请参阅此[设置指南](http://go.microsoft.com/fwlink/?LinkId=723452)。

## Resources

在 MSDSN 库中可以找到有关 Microsoft R 的其他文档：[R Server 和 Scale R](https://msdn.microsoft.com/microsoft-r)  


请参阅以下这些其他资源以对 R 进行总体了解： 
+ [DataCamp](http://www.datacamp.com) 提供 R 的免费初级和中级课程，以及有关使用 Revolution R 处理大数据的课程。
+ [堆栈溢出](http://www.stackoverflow.com) 适用于 R 编程和 ML 工具问题的良好资源。 
+ [交叉验证](https://stats.stackexchange.com/) 针对机器学习中统计问题的相关问题的站点。
+ [R 帮助邮件列表存档](https://www.r-project.org/mail.html) 历史记录信息的良好资源。 
+ [MRAN 网站](https://mran.microsoft.com/documents/getting-started/) 许多其他 R 资源。  

## 另请参阅
[SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx)

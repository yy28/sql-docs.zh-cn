---
title: "数据流目标 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 640e6a19-49ae-4ee8-ac07-008370158f0e
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# 数据流目标
  “数据流目标”是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) 目标组件，它能让 **OLE DB Provider for SSIS** 将 SSIS 包的输出作为表格结果集使用。 可以创建使用 OLE DB Provider for SSIS 的链接服务器，然后在链接服务器上运行 SQL 查询以显示由 SSIS 包返回的数据。  
  
 在下面的示例中，以下查询从 SSIS 目录的 Power BI 文件夹中的 SSISPackagePublishing 项目中的 Package.dtsx 包返回输出。 此查询使用名为 [Integration Services 的默认链接服务器] 的链接服务器，该服务器会反过来使用新的 OLE DB Provider for SSIS。 该查询包括 SSIS 目录中的文件夹名称、项目名称和包名称。 OLE DB Provider for SSIS 运行你在查询中指定的包，并返回表格结果集。  
  
```  
SELECT * FROM OPENQUERY([Default Linked Server for Integration Services], N'Folder=Power BI;Project=SSISPackagePublishing;Package=Package.dtsx')  
  
```  
  
## 数据馈送发布组件  
 数据馈送发布组件包含以下组件：OLE DB Provider for SSIS、数据流目标和 SSIS 包发布向导。 该向导让你将 SSIS 包作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库实例中的 SQL 视图发布。 该向导帮助你创建使用 OLE DB Provider for SSIS 的链接服务器和表示链接服务器上的查询的 SQL 视图。 你可以运行该视图，从作为表格数据集的 SSIS 包查询结果。  
  
 若要确认 SSISOLEDB 提供程序已安装，在 SQL Server Management Studio 中，展开 **服务器对象**、 **链接服务器**、 **提供程序**，并确认你看到了 **SSISOLEDB** 提供程序。 双击 **SSISOLEDB**，启用“允许进程内”（如果它未启用），然后单击“确定”。  
  
## 将 SSIS 包作为 SQL 视图发布  
 以下过程描述将 SSIS 包作为 SQL 视图发布的步骤。  
  
1.  使用 **数据流目标** 组件创建 SSIS 包，并将包部署到 SSIS 目录。  
  
2.  通过运行 C:\Program Files\Microsoft SQL Server\130\DTS\Binn 的 ISDataFeedPublishingWizard.exe 或通过从“开始”菜单运行“数据流发布向导”来运行“SSIS 包发布向导”。  
  
     该向导创建一个使用 OLE DB Provider for SSIS (SSISOLEDB) 的链接服务器，然后在链接服务器上创建一个包含查询的 SQL 视图。 该查询包括 SSIS 目录中的文件夹名称、项目名称和包名称。  
  
3.  在 SQL Server Management Studio 中执行 SQL 视图并从 SSIS 包查看结果。 该视图通过你创建的链接服务器将查询发送到 OLE DB Provider for SSIS。 OLE DB Provider for SSIS 执行你在查询中指定的包，然后返回表格结果集。  
  
> [!IMPORTANT]  
>  有关详细步骤，请参阅[演练：将 SSIS 包作为 SQL 视图发布](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)。  
  
## 通过使用 Power BI 管理中心从 SSIS 包将输出数据作为 OData 馈送公开。  
 通过使用 Power BI 管理中心，IT 管理人员可以从本地数据源将数据作为 OData 馈送向用户公开。 Power BI 管理中心默认情况下仅允许注册 SQL Server 数据源。 但是，你可以通过使用“数据流目标”和 **Microsoft OLE DB Provider for SQL Server Integration Services (SSISOLEDB)** 将 SSIS 包作为数据源注册到门户，并从 SSIS 包将结果数据作为 OData 馈送向用户公开。  
  
 管理中心让你能够在 SQL Server 数据库中发布视图。 因此，你可以使用 SSIS 包发布向导将 SSIS 包作为 SQL 视图发布。 然后可以在 Power BI 管理中心选择将包括在 OData 馈送源中的视图。 数据专员可以通过使用 Power Query Add-in for Excel 来使用 SSIS 包中的馈送。  
  
 有关详细演练，请参阅 [将 SSIS 包作为 OData 馈送源发布](http://go.microsoft.com/fwlink/?LinkID=317367)。  
  
## 本节内容  
  
-   [演练：将 SSIS 包作为 SQL 视图发布](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)  
  
-   [配置数据流目标](../../integration-services/data-flow/configure-data-streaming-destination.md)  
  
## 另请参阅  
 [将 SSIS 包作为 OData 馈送源发布](http://go.microsoft.com/fwlink/?LinkID=317367)  
  
  
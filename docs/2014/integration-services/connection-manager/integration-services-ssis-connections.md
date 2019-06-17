---
title: Integration Services (SSIS) 连接 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, connections
- SSIS packages, connections
- sources [Integration Services], connections
- packages [Integration Services], connections
- destinations [Integration Services], connections
- tasks [Integration Services], connections
- connections [Integration Services], about connections
- connections [Integration Services]
- SQL Server Integration Services packages, connections
ms.assetid: 72f5afa3-d636-410b-9e81-2ffa27772a8c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 78c3ba452d3ba681823e5c9f473d7a86f55809a1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833772"
---
# <a name="integration-services-ssis-connections"></a>Integration Services (SSIS) 连接
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包使用连接来执行不同的任务以及实现 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 功能：  
  
-   连接到源和目标数据存储区（如文本、XML、Excel 工作簿和关系数据库），以提取和加载数据。  
  
-   连接到包含引用数据的关系数据库，以执行完全查找或模糊查找。  
  
-   连接到关系数据库，以运行 SQL 语句（例如，SELECT、DELETE 和 INSERT 命令）以及存储过程。  
  
-   连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以执行维护和传输任务，例如，备份数据库和传输登录名。  
  
-   在文本和 XML 文件中以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中写入日志项，并将包配置写入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表。  
  
-   连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以创建某些转换在执行其工作时需要的临时工作表。  
  
-   连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目和数据库，以访问数据挖掘模型、处理多维数据集和维度，并运行 DDL 代码。  
  
-   指定现有的文件和文件夹，或创建新的文件和文件夹，以便用于 Foreach 循环枚举器和任务。  
  
-   连接到消息队列、Windows Management Instrumentation (WMI)、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对象 (SMO)、Web 和邮件服务器。  
  
 为了创建这些连接， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 使用了连接管理器，如下一部分所述。  
  
## <a name="connection-managers"></a>连接管理器  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 使用连接管理器作为连接的逻辑表示形式。 在设计时，可设置连接管理器的属性，以描述当包运行时 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 创建的物理连接。 例如，连接管理器包含在设计时设置的 `ConnectionString` 属性；在运行时，使用该连接字符串属性中的值创建物理连接。  
  
 包可以使用一种连接管理器类型的多个实例，您可以在每个实例上设置这些属性。 在运行时，一种连接管理器类型的每个实例创建具有不同属性的连接。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供了不同类型的连接管理器，从而使得包可以连接到多种数据源和服务器：  
  
-   提供了内置连接管理器，在您安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]时安装程序将安装这些连接管理器。  
  
-   提供了可从 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 网站下载的连接管理器。  
  
-   如果现有的连接管理器没有满足您的需求，可以创建自己的自定义连接管理器。  
  
### <a name="built-in-connection-managers"></a>内置连接管理器  
 下表列出了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的连接管理器类型。  
  
|类型|Description|主题|  
|----------|-----------------|-----------|  
|ADO|连接到 ActiveX 数据对象 (ADO) 对象。|[ADO 连接管理器](ado-connection-manager.md)|  
|ADO.NET|使用 .NET 提供程序连接到数据源。|[ADO.NET 连接管理器](ado-net-connection-manager.md)|  
|CACHE|从数据流或从缓存文件 (.caw) 中读取数据，并可将数据保存到缓存文件。|[缓存连接管理器](cache-connection-manager.md)|  
|DQS|连接到某一 Data Quality Services 服务器以及该服务器上的 Data Quality Services 数据库。|[DQS 清理连接管理器](dqs-cleansing-connection-manager.md)|  
|EXCEL|连接到 Excel 工作簿文件。|[Excel 连接管理器](excel-connection-manager.md)|  
|FILE|连接到文件或文件夹。|[文件连接管理器](file-connection-manager.md)|  
|FLATFILE|连接到单个平面文件中的数据。|[平面文件连接管理器](flat-file-connection-manager.md)|  
|FTP|连接到 FTP 服务器。|[FTP 连接管理器](ftp-connection-manager.md)|  
|HTTP|连接到 Web 服务器。|[HTTP 连接管理器](http-connection-manager.md)|  
|MSMQ|连接到消息队列。|[MSMQ 连接管理器](msmq-connection-manager.md)|  
|MSOLAP100|连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目。|[Analysis Services 连接管理器](analysis-services-connection-manager.md)|  
|MULTIFILE|连接到多个文件和文件夹。|[多文件连接管理器](multiple-files-connection-manager.md)|  
|MULTIFLATFILE|连接到多个数据文件和文件夹。|[多平面文件连接管理器](multiple-flat-files-connection-manager.md)|  
|OLEDB|使用 OLE DB 访问接口连接到数据源。|[OLE DB 连接管理器](ole-db-connection-manager.md)|  
|ODBC|使用 ODBC 连接到数据源。|[ODBC 连接管理器](odbc-connection-manager.md)|  
|SMOServer|连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对象 (SMO) 服务器。|[SMO 连接管理器](smo-connection-manager.md)|  
|SMTP|连接到 SMTP 邮件服务器。|[SMTP 连接管理器](smtp-connection-manager.md)|  
|SQLMOBILE|连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 数据库。|[SQL Server Compact Edition 连接管理器](sql-server-compact-edition-connection-manager.md)|  
|WMI|连接到服务器，并指定服务器上 Windows Management Instrumentation (WMI) 管理的范围。|[WMI 连接管理器](wmi-connection-manager.md)|  
  
### <a name="connection-managers-available-for-download"></a>可供下载的连接管理器  
 下表列出了可从 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 网站下载的其他连接管理器类型。  
  
> [!IMPORTANT]  
>  下表中列出的连接管理器只能用于 [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] 和 [!INCLUDE[ssDeveloperEd11](../../includes/ssdevelopered11-md.md)]。  
  
|类型|Description|主题|  
|----------|-----------------|-----------|  
|ORACLE|连接到 Oracle\<版本信息 > 服务器。|Oracle 连接管理器是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Oracle by Attunity 的连接管理器组件。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Oracle by Attunity 还包括源和目标。 有关详细信息，请访问下载页 [Microsoft Connectors for Oracle and Teradata by Attunity](https://go.microsoft.com/fwlink/?LinkId=251526)。|  
|SAPBI|连接到 SAP NetWeaver BI 7 版系统。|SAP BI 连接管理器是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for SAP BI 的连接管理器组件。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for SAP BI 还包括源和目标。 有关详细信息，请访问下载页 [Microsoft SQL Server 2008 功能包](https://go.microsoft.com/fwlink/?LinkId=262016)。|  
|TERADATA|连接到 Teradata\<版本信息 > 服务器。|Teradata 连接管理器是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Teradata by Attunity 的连接管理器组件。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Teradata by Attunity 还包括源和目标。 有关详细信息，请访问下载页 [Microsoft Connectors for Oracle and Teradata by Attunity](https://go.microsoft.com/fwlink/?LinkId=251526)。|  
  
### <a name="custom-connection-managers"></a>自定义连接管理器  
 您还可以编写自定义连接管理器。 有关详细信息，请参阅 [Developing a Custom Connection Manager](../extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
 有关如何在包中添加或删除连接管理器的详细信息，请参阅[在包中添加、删除或共享连接管理器](../add-delete-or-share-a-connection-manager-in-a-package.md)。  
  
 有关如何在包中设置连接管理器属性的详细信息，请参阅[设置连接管理器的属性](../set-the-properties-of-a-connection-manager.md)。  
  
## <a name="related-content"></a>相关内容  
  
-   technet.microsoft.com 上的视频 [利用 Microsoft Attunity Connector for Oracle 来增强包性能](https://technet.microsoft.com/sqlserver/gg598963.aspx)  
  
-   social.technet.microsoft.com 上的 Wiki 文章 [SSIS 连接](https://social.technet.microsoft.com/wiki/contents/articles/sql-server-integration-services-ssis.aspx#Connectivity)  
  
-   blogs.msdn.com 上的博客文章 [从 SSIS 连接到 MySQL](https://go.microsoft.com/fwlink/?LinkId=217669)。  
  
-   msdn.microsoft.com 上的技术文章 [在 SQL Server Integration Services 中提取和加载 SharePoint 数据](https://go.microsoft.com/fwlink/?LinkId=247826)。  
  
-   support.microsoft.com 上的技术文章[在 SSIS 中使用 Oracle 连接管理器时收到“DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER”错误消息](https://go.microsoft.com/fwlink/?LinkId=233696)。  
  
  

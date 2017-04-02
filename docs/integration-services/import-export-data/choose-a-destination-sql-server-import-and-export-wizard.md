---
title: "选择目标（SQL Server 导入和导出向导） | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.chooseadestination.f1"
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
caps.latest.revision: 104
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 95
---
# 选择目标（SQL Server 导入和导出向导）
 在提供有关数据源以及如何连接到它的信息后，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导会显示“选择目标”。 在此页上，需提供有关数据目标以及如何连接到它的信息。
  
若要了解可使用的数据目标，请参阅[可使用哪些数据源和目标？](Import%20and%20Export%20Data%20with%20the%20SQL%20Server%20Import%20and%20Export%20Wizard.md\#wizardSources)。 

## <a name="screen-shot-of-the-destination-page"></a>“目标”页面的屏幕截图
以下屏幕截图显示的是该向导的“选择目标”页的第一部分。

![选择目标](../../integration-services/import-export-data/media/choose-destination.png)

## <a name="choose-a-destination"></a>选择目标
 **目标**  
 通过选择可以将数据导入到目标中的数据提供程序来指定目标。 在大多数情况下，可以根据名称来判断所需的数据提供程序，因为提供程序的名称中包含目标的名称 — 例如，SQL Server、Oracle、平面文件、Excel 和 Access。
 
“目标”列表中可用数据访问接口的列表取决于计算机上安装的访问接口。 它还取决于你正在运行的是 64 位向导还是 32 位向导。

可用于目标的访问接口可能不止一个。 通常可以选择任何可用于目标的访问接口。 例如，若要连接到 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client、用于 SQL Server 的 .NET Framework 数据提供程序或用于 SQL Server 的 Microsoft OLE DB 提供程序。
 
在某些情况下，必须先选择一个泛型数据提供程序。 例如，如果有用于目标的 ODBC 驱动程序，则选择用于 ODBC 的 .NET Framework 数据访问接口。

对于某些目标，可能需要从 Microsoft 或第三方下载数据访问接口。 若要了解可使用的数据目标，请参阅[可使用哪些数据源和目标？](Import%20and%20Export%20Data%20with%20the%20SQL%20Server%20Import%20and%20Export%20Wizard.md\#wizardSources)。

## <a name="after-you-choose-a-destination"></a>选择目标之后
在选择目标之后，“选择目标”页属性的其余部分具有数量不定的选项，具体取决于所选的数据访问接口。

以下各节列出了某些常用目标的重要选项。 此处并未列出“目标”下拉列表中的所有可用目标。 有关其他选项和其他提供程序的信息，请参阅提供程序特定的文档。

> [!TIP] 如果目标需要连接字符串，可以在第三方站点 [The Connection Strings Reference](https://www.connectionstrings.com/)（连接字符串参考）上查找示例。  

## <a name="microsoft-sql-server"></a>Microsoft SQL Server 

如果要创建新 SQL Server 数据库作为目标，请选择 SQL Server Native Client 或 Microsoft OLE DB Provider for SQL Server。 如果选择用于 SQL Server 的 .NET Framework 数据访问接口，则创建新数据库的选项不可用。  

### <a name="connect-to-sql-server-with-sql-server-native-client-or-the-microsoft-ole-db-provider-for-sql-server"></a>使用 SQL Server Native Client 或用于 SQL Server 的 Microsoft OLE DB 提供程序连接到 SQL Server  

SQL Server Native Client 和用于 SQL Server 的 Microsoft OLE DB 提供程序将公开一组相同的选项。 下面的屏幕截图例举了 SQL Server Native Client 的选项。

![SQL Native 目标](../../integration-services/import-export-data/media/sql-native-destination.png)

 **服务器名称**  
 键入目标服务器的名称或 IP 地址，或者从列表中选择服务器。  
  
> [!NOTE] 如果所在的网络上有多个服务器，输入服务器名称可能会更方便。 如果单击下拉列表，可能需要很长时间来查询网络中所有可用的服务器，并且你的服务器名称可能不会列出在结果中。  
 
 若要指定非标准的 TCP 端口，请在服务器名称或 IP 地址之后键入逗号，然后键入端口号。
 
 **使用 Windows 身份验证**  
 指定向导是否应使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 身份验证登录数据库。 建议使用 Windows 身份验证。  
  
 **使用 SQL Server 身份验证**  
 指定向导是否应使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证登录数据库。 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则必须提供用户名和密码。  
  
 **用户名**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证时，提供数据库连接的用户名。  
  
 **密码**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证时，提供数据库连接的密码。  
  
 **数据库**  
 从指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上的数据库列表中选择。  
  
 **刷新**  
 通过单击“刷新”，还原可用数据库的列表。  
  
### <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>使用用于 SQL Server 的 .NET Framework 数据提供程序连接到 SQL Server 

此页显示用于 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据提供程序的选项分组列表。 此处列出了一些重要的选项。 选择此访问接口时所列出的其他选项并不是成功连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标数据库所必需。 

有关详细信息，请参阅 [.NET Framework Data Provider for SQL Server connection strings](https://www.connectionstrings.com/sqlconnection/)（用于 SQL Server 的 .NET Framework 数据提供程序的连接字符串）。

![SQL Server 目标](../../integration-services/import-export-data/media/sql-server-destination-net.png)
  
 **目标**  
 键入目标服务器的名称或 IP 地址，或者从列表中选择服务器。  
  
> [!NOTE] 如果所在的网络上有多个服务器，输入服务器名称可能会更方便。 如果单击下拉列表，可能需要很长时间来查询网络中所有可用的服务器，并且你的服务器名称可能不会列出在结果中。  
 
 若要指定非标准的 TCP 端口，请在服务器名称或 IP 地址之后键入逗号，然后键入端口号。
 
 **初始目录**  
 输入目标数据库的名称，或者从列表中选择数据库。  
  
 **集成安全性**  
 若要使用 Windows 集成身份验证进行连接（建议），请指定 **True**；若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证进行连接，请指定 **False**。 如果指定 **False**，则必须输入用户 ID 和密码。 默认值为 **False**。  
  
 **用户 ID**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证时，提供数据库连接的用户名。  
  
 **密码**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证时，提供数据库连接的密码。  

## <a name="oracle"></a>Oracle

使用用于 Oracle 的 .Net Framework 数据提供程序或用于 Oracle 的 Microsoft OLE DB 提供程序连接到 Oracle。 下面的屏幕截图显示了更易配置的用于 Oracle 的 .Net Framework 数据提供程序。

有关详细信息，请参阅 [.NET Framework Data Provider for Oracle connection strings](https://www.connectionstrings.com/net-framework-data-provider-for-oracle/)（用于 Oracle 的 .Net Framework 数据提供程序的连接字符串）或 [Microsoft OLE DB Provider for Oracle connection strings](https://www.connectionstrings.com/microsoft-ole-db-provider-for-oracle-msdaora/)（用于 Oracle 的 Microsoft OLE DB 提供程序的连接字符串）。

![Oracle 目标](../../integration-services/import-export-data/media/oracle-destination.png)

## <a name="odbc-destinations"></a>ODBC 目标

若要将数据保存到提供 ODBC 驱动程序的任何目标，请选择用于 ODBC 的 .NET Framework 数据访问接口。

若要为 ODBC 目标提供连接字符串，请参阅要使用的 ODBC 驱动程序的相关文档，或在 [The Connection Strings Reference](https://www.connectionstrings.com/)（连接字符串参考）中查找示例。 

下面的屏幕截图例举了到 SQL Server 的 ODBC 连接。 本例中使用的连接字符串如下：

    Driver={SQL Server};Server=(local);Database=TestData;Trusted_Connection=Yes;

在 **ConnectionString** 字段中输入连接字符串后，向导会分析该字符串，并在列表的“杂项”部分显示各个属性及其值。

![ODBC 连接 SQL 目标](../../integration-services/import-export-data/media/odbc-connection-sql-destination.png)

 ## <a name="text-files-flat-files"></a>文本文件（平面文件）
 
![平面文件目标](../../integration-services/import-export-data/media/flat-file-destination.png)  

**文件名**  
 指定要存储数据的文件的路径和文件名。 或者，单击 **“浏览”** 定位文件。  
  
 **浏览**  
 使用“打开”对话框定位文件。  
  
 **区域设置**  
 指定定义字符排序顺序以及日期和时间格式的区域设置 ID (LCID)。  
  
 **Unicode**  
 指示是否使用 Unicode。 如果使用 Unicode，则不必指定代码页。  
  
 **代码页**  
 指定所需使用的语言的代码页。  
  
 **格式**  
 指示是否使用带分隔符、固定宽度或右边未对齐的格式。  
  
|“值”|Description|  
|-----------|-----------------|  
|带分隔符|列由分隔符分隔。|  
|固定宽度|列的宽度固定。|  
|右边未对齐|在右边未对齐的文件中，除最后一列之外的每一列的宽度都固定，而最后一列由行分隔符进行分隔。|  
  
 **文本限定符**  
 键入要使用的文本限定符。 例如，您可以指定每个文本列均包含在引号中。  
  
 **第一个数据行中的列名称**  
 指示是否希望在第一个数据行中显示列名称。  
 
 ## <a name="microsoft-excel"></a>Microsoft Excel

>  **视频**：该向导的常见用途之一是将数据导出到 Excel。 以下是来自 YouTube 的一个四分钟视频，该视频通过清晰、简单的说明介绍了执行此操作的方法。 [Using the SQL Server Import and Export Wizard to Export to Excel](https://go.microsoft.com/fwlink/?linkid=829049)（使用 SQL Server 导入和导出向导导出到 Excel）。 （此视频使用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2012。）

下面的屏幕截图显示到 Microsoft Excel 工作簿的示例连接。

![Excel 目标](../../integration-services/import-export-data/media/excel-destination.png) 
 
 **Excel 文件路径**  
 指定要将数据导出到其中的电子表格的路径和文件名。 例如，针对本地计算机上的文件，请指定路径 **C:\\MyData.xlsx**，针对网络共享上的文件，请指定路径 **\\\\Sales\\Database\\Northwind.xlsx**。 或单击 **“浏览”**。   
  
 **浏览**  
 通过使用“打开”对话框定位电子表格。  

> [!NOTE] 该向导无法打开受密码保护的 Excel 文件。

 **Excel 版本**  
选择目标工作簿使用的 Excel 版本。  

可能需要下载并安装其他文件，才能连接到所选 Excel 版本。 有关详细信息，请参阅本页上的[获取 Excel 和 Access 所需的下载](Choose%20a%20Data%20Source%20\%28SQL%20Server%20Import%20and%20Export%20Wizard%29.md\#officeDownloads)。

如果指定版本时遇到问题（例如，如果由于具有 Microsoft Office 365 而导致无法安装 Access 2016 Runtime），请尝试指定其他版本，可以是早期版本（例如 2013，而非 2016）。

**首行包含列名称**  
此选项似乎对 Excel 目标没有作用。 如果目标不具有列名称，则即使启用此选项，驱动程序也不会输出列名称。 在内部，该向导使用 F1、F2 等作为临时列标题。
 
## <a name="microsoft-access"></a>Microsoft Access  

下面的屏幕截图显示到 Microsoft Access 数据库的示例连接。

![Access 目标](../../integration-services/import-export-data/media/access-destination.png)

 **文件名**  
 指定要将数据导出到其中的数据库文件的路径和文件名。 例如，**C:\MyData.mdb、\\\Sales\Database\Northwind.mdb**。 或单击 **“浏览”**。
 
 >   [!NOTE] 向导只能连接到 .MDB 文件格式的 Access 数据库。  
  
 **浏览**  
 通过使用“打开”对话框定位数据库文件。  
  
 **用户名**  
当工作组信息文件与数据库关联时，为数据库连接提供一个有效的用户名。  
  
 **密码**  
当工作组信息文件与数据库关联时，为数据库连接提供相应的用户密码。

如果对于所有用户都使用一个密码保护数据库，则在“数据链接属性”对话框中提供此值。 若要打开“数据链接属性”对话框，请单击“高级”。    
  
 **高级**  
通过使用“数据链接属性”对话框指定高级选项，例如数据库密码或非默认工作组信息文件。  
  
## <a name="a-nameofficedownloadsaget-the-downloads-you-need-for-excel-and-access"></a><a name="officeDownloads"></a>获取 Excel 和 Access 所需的下载  
如果尚未安装 Microsoft Excel 和 Access 数据源的连接组件，则可能需要下载它们。

更高版本的组件可以打开早期版本的程序所创建的文件。 在某些情况下，早期版本的组件也可以打开程序的更高版本所创建的文件。  
  
如果计算机安装有 32 位版本的 Office，则必须安装 32 位版本的组件。 还必须确保在 32 位模式中运行向导（或其创建的 Integration Services 包）。 
 |Microsoft Office 版本|下载|  
|------------------------------|--------------|  
|2007|[2007 Office system 驱动程序：数据连接组件](https://www.microsoft.com/download/details.aspx?id=23734)|  
|2010|[Microsoft Access 2010 Runtime](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2013|[Microsoft Access 2013 Runtime](http://www.microsoft.com/download/details.aspx?id=39358)|  
|2016|[Microsoft Access 2016 Runtime](https://www.microsoft.com/download/details.aspx?id=50040)|  
 
## <a name="azure-blob-storage"></a>Azure Blob 存储  
若要使用 Azure Blob 目标，必须安装用于 SSIS 的 Azure 功能包。 有关详细信息，请参阅[用于 Integration Services 的 Azure 功能包 (SSIS)](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。  

>   [!NOTE] 若要确保 Azure 存储空间连接管理器和使用它的组件（包括 Blob 目标）可以连接到通用存储帐户和 Blob 存储帐户，请确保[在此处](https://www.microsoft.com/download/details.aspx?id=49492)下载最新版本的 Azure 功能包。 有关这两种类型的存储帐户的详细信息，请参阅 [Microsoft Azure 存储空间简介](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts)。

![Azure blob 目标](../../integration-services/import-export-data/media/azure-blob-destination.png)

**使用 Azure 帐户**  
指定是否使用联机帐户。

 **存储帐户名称**  
 指定 Azure 存储帐户的名称。  
  
 **帐户密钥**  
 提供 Azure 存储帐户的密钥。  
  
 **使用 HTTPS**  
 指定是使用 HTTP 还是 HTTPS 连接到存储帐户。  
  
 **使用本地开发人员帐户**  
 指定是否在本地计算机上使用存储仿真程序。  
  
 **Blob 容器名称**  
 从指定的存储帐户中可用的存储容器列表中选择。  
  
 **Blob 文件格式**  
 选择文本或 Avro 文件格式。  
  
 **列分隔符字符**  
 如果选择文本格式，请指定列分隔符字符。  
  
 **使用第一行作为列名称**  
 指定第一行数据是否包含列名称。  

## <a name="whats-next"></a>下一步是什么？  
 提供有关数据目标以及有关如何连接到它的信息之后，下一页是“指定表复制或查询”。 在此页上，可指定要复制整个表还是仅复制特定行。 有关详细信息，请参阅[指定表复制或查询](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)。  

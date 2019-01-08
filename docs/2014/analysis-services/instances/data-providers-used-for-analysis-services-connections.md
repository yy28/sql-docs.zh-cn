---
title: 用于 Analysis Services 连接的数据提供程序 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 128f6dde-409d-4c12-9820-3305bab57b75
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 739723a42580c404d0529a6d84d907cf665f8270
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53368507"
---
# <a name="data-providers-used-for-analysis-services-connections"></a>用于 Analysis Services 连接的数据提供程序
  Analysis Services 为服务器和数据访问提供了三个数据访问接口。 连接到 Analysis Services 的所有应用程序均使用以下访问接口之一来进行数据访问操作。 ADOMD.NET 和 Analysis Services 管理对象 (AMO) 这两个访问接口为托管数据访问接口。 Analysis Services OLE DB 访问接口 (MSOLAP DLL) 为本地数据访问接口。  
  
 在运行多个 Analysis Services 版本的组织中，对于连接到 Analysis Services 数据的用户工作站，可能需要安装较新版本的数据访问接口。 连接到较新版本的 Analysis Services 需要具备同一主版本的数据访问接口。 例如，要连接到 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]，每个工作站必须具有 2014 版本提供的数据访问接口。 尽管 Excel 会安装其连接所需的数据访问接口，但是它提供的访问接口相对您正在使用的 Analysis Services 实例可能过时了。  
  
 本主题包含以下各节：  
  
 [如何确定服务器版本](#bkmk_ServVers)  
  
 [如何确定 Analysis Services 数据访问接口的版本](#bkmk_LibUpdate)  
  
 [在何处获取较新版本的数据访问接口](#bkmk_downloadsite)  
  
 [Analysis Services OLE DB 访问接口](#bkmk_OLE)  
  
 [ADOMD.NET](#bkmk_ADOMD)  
  
 [AMO](#blkmk_AMO)  
  
##  <a name="bkmk_ServVers"></a> 如何确定服务器版本  
 了解 Analysis Services 实例的版本将帮助您确定是否需要在您组织的工作站上安装较新版本的数据访问接口。  
  
-   在 SQL Server Management Studio 中，连接到 Analysis Services 实例。 右键单击你想要检查，指向的实例**报表**，然后单击**常规**。 报表中显示版本类别和版本构建信息。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 初始版本的主工作版本号为 12.0.2000.9。  
  
 有关如何获取版本和构建信息的详细信息，请参阅 [如何确定 SQL Server 及其组件的版本和版本类别](https://support.microsoft.com/kb/321185)。  
  
##  <a name="bkmk_LibUpdate"></a> 如何确定 Analysis Services 数据访问接口的版本  
 数据访问接口随 Analysis Services 安装，还可以由例行连接到 Analysis Services 数据库的客户端应用程序（如 Excel）安装。  
  
 Office 2007 安装 SQL Server 2005 数据提供程序。 Office 2010 安装 SQL Server 2008 数据提供程序。 Office 2013 安装 SQL Server 2012 数据访问接口。 如果使用 Office 或 SQL Server 的多个版本，且提供的连接或功能未达预期，则可能需要安装数据访问接口的较新版本。 您可以在同一计算机上并行运行每个数据访问接口的多个主版本。  
  
#### <a name="find-the-file-version-of-the-oledb-provider"></a>查找 OLEDB 访问接口的文件版本  
  
1.  转到 \Program Files\Microsoft Analysis Services\AS OLEDB\120。  
  
2.  右键单击 msolap120.dll，然后单击**属性**。  
  
 如果在此位置找不到文件，或文件夹路径包含 AS OLEDB\110 或 AS OLEDB\90，则表示您在使用较旧的版本，现在必须安装较新的版本 (AS OLEDB\11) 来连接到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
#### <a name="find-the-file-version-of-adomdnet-and-amo"></a>查找 ADOMD.NET 和 AMO 的文件版本  
  
1.  转到 C:\Windows\Assembly  
  
2.  右键单击 Microsoft.AnalysisServices.AdomdClient 并单击“属性”。 单击 **“版本”**。  
  
     对于 AMO，右键单击 Microsoft.AnalysisServices。  
  
 有关各发行版本号和工作版本号的详细信息，请参阅 [Blogspot 上的 SQL Server 工作版本](http://sqlserverbuilds.blogspot.com)。  
  
##  <a name="bkmk_downloadsite"></a> 在何处获取较新版本的数据访问接口  
 在客户端计算机上安装的版本应与提供数据的服务器的主版本相同。 如果服务器版本比在网络中工作站上安装的数据访问接口版本新，您可能需要安装较新的库。  
  
#### <a name="find-the-data-providers-on-the-download-site"></a>在下载站点上查找数据访问接口  
  
1.  转到 [Microsoft 下载中心](https://go.microsoft.com/fwlink/p/?LinkID=296473)。  
  
2.  展开 **“安装说明”**。  
  
3.  向下滚动到包含 Analysis Services 组件的部分。 ADOMD.NET、OLE DB 访问接口和 AMO 是列表中的第二、三和四项。 每个库提供 32 位或 64 位版本。 运行 64 位操作系统的服务器和较新工作站将需要 64 位版本。  
  
##  <a name="bkmk_OLE"></a> Analysis Services OLE DB 访问接口  
 Analysis Services OLE DB 访问接口是 Analysis Services 数据库连接的本机访问接口。 MSOLAP 由 ADOMD.NET 和 AMO 间接使用，将连接请求委托给数据访问接口。 您还可以直接从应用程序代码调用 OLE DB 访问接口，如果解决方案要求不使用托管 API，您可能要这样做。  
  
 Analysis Services OLE DB 访问接口由 SQL Server 安装程序、Excel 和其他常用于访问 Analysis Services 数据库的应用程序自动安装。 您还可以通过从下载中心下载来手动安装它。 默认情况下，访问接口可以在 \Program Files\Microsoft Analysis Services 文件夹中找到。 任何用于访问 Analysis Services 数据的工作站上都必须安装此访问接口。  
  
 MSOLAP130.dll 是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中附带的 Analysis Services OLE DB 提供程序版本。 其他最近早期版本有 MSOLAP10.dll（对于 SQL Server 2008 和 2008 R2）和 MSOLAP90.dll（对于 SQL Server 2005）。  
  
 OLE DB 访问接口经常在连接字符串上指定。 Analysis Services 连接字符串使用不同的命名法来指代 OLE DB 访问接口：MSOLAP。\<版本 >.dll  
  
 MSOLAP.5.dll 是随 Excel 2013 安装的当前 Analysis Services OLE DB 访问接口。 以前的版本（如 MSOLAP.4.dll 或 MSOLAP.3.dll）经常可在运行早期 Excel 版本的工作站上找到。 一些 Analysis Services 功能（如 PowerPivot 外接程序）需要特定版本的 OLE DB 访问接口。 有关详细信息，请参阅[连接字符串属性 (Analysis Services)](connection-string-properties-analysis-services.md)。  
  
##  <a name="bkmk_ADOMD"></a> ADOMD.NET  
 ADOMD.NET 是用于查询 Analysis Services 数据的托管数据访问接口。 Excel 在连接到特定 Analysis Services 多维数据集时使用 ADOMD.NET。 您在 Excel 中看到的连接字符串用于 ADOMD.NET 连接。  
  
 ADOMD.NET 由 SQL Server 安装程序进行安装，SQL Server 客户端应用程序使用它来连接 Analysis Services。 Office 会安装此库，为 Excel 中的数据连接提供支持。 和 SQL Server 中包含的其他数据访问接口一样，如果在自定义代码中使用 ADOMD.NET，您可以重新分发它。 还可以下载并手动安装它来获取更新的版本（请参阅本主题中的 [如何确定 Analysis Services 数据提供程序的版本](#bkmk_LibUpdate) ）。  
  
 若要查看文件版本信息，请在全局程序集高速缓存中查找 ADOMD.NET，其中列出的 `Microsoft.AnalysisServices.AdomdClient`即是该库。  
  
 连接到数据库时，用于所有三个库的连接字符串属性大半都是相同的。 几乎所有为 ADOMD.NET 定义的连接字符串 (<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>) 都也将对 AMO 和 Analysis Services OLE DB 提供程序有效。 有关详细信息，请参阅[连接字符串属性 (Analysis Services)](connection-string-properties-analysis-services.md)。  
  
 有关以编程方式连接的详细信息，请参阅 [Establishing Connections in ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-client/connections-in-adomd-net)。  
  
##  <a name="blkmk_AMO"></a> AMO  
 AMO 是用于服务器管理和数据定义的托管数据访问接口。 例如，SQL Server Management Studio 使用 AMO 连接 Analysis Services。  
  
 AMO 由 SQL Server 安装程序进行安装，SQL Server 客户端应用程序使用它来连接 Analysis Services。 在自定义代码中使用 AMO 时，还可以下载并手动安装它（请参阅本主题中的 [如何确定 Analysis Services 数据提供程序的版本](#bkmk_LibUpdate) ）。 AMO 可以在全局程序集高速缓存中找到，例如 `Microsoft.AnalysisServices`。  
  
 使用 AMO 的连接是通常最小，包含的"数据源 =\<服务器名 >"。 在建立连接后，您使用 API 来处理数据库收集和主要对象。 SSDT 和 SSMS 使用 AMO 连接到 Analysis Services 实例。  
  
 有关以编程方式连接的详细信息，请参阅 [Programming AMO Fundamental Objects](https://docs.microsoft.com/bi-reference/amo/programming-amo-fundamental-objects)。  
  
## <a name="see-also"></a>请参阅  
 [连接到 Analysis Services](connect-to-analysis-services.md)  
  
  

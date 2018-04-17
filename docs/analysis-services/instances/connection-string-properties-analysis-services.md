---
title: 连接字符串属性 (Analysis Services) |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 29a00a41-5b0d-44b2-8a86-1b16fe507768
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 9c2daf9234b44f7108339d9a743118373b9b42c1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="connection-string-properties-analysis-services"></a>连接字符串属性 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  本主题介绍的是连接字符串属性，您可能需要在某个设计器或管理工具中设置这些属性，也可能在连接到并查询 Analysis Services 数据的客户端应用程序所生成的连接字符串中看到这些属性。 因此，它仅涉及可用属性的一部分。 完整列表包含各种服务器和数据库属性，允许您为特定应用程序自定义连接，而不管实例或数据库在服务器上是如何配置的。  
  
 在应用程序代码中生成自定义连接字符串的开发人员应查看 ADOMD.NET 客户端的 API 文档，以查看更详细的列表： <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>  
  
 本主题中所述的属性由以下 Analysis Services 客户端库使用：ADOMD.NET、AMO 和 Analysis Services 的 OLE DB 访问接口。 大多数连接字符串属性可用于所有这三种客户端库。 例外将专门进行说明。
  
> [!NOTE]  
>  设置属性时，如果您无意中两次设置同一属性，则在连接字符串中使用后设置的那个属性。  
  
 有关如何在现有 Microsoft 应用程序中指定 Analysis Services 连接的详细信息，请参阅[从客户端应用程序 &#40;Analysis Services&#41; 连接](../../analysis-services/instances/connect-from-client-applications-analysis-services.md)。  
  
##  <a name="bkmk_common"></a>常用的连接参数  
 下表介绍在生成连接字符串时最常用的那些属性。  
  
|属性|Description|示例|  
|--------------|-----------------|-------------|  
|**Data Source** 或 **DataSource**|指定服务器实例。 此属性对于所有连接都是必需的。 有效值包括服务器的网络名称或 IP 地址、local 或 localhost（对本地连接）、URL（如果针对 HTTP 或 HTTPS 访问配置了服务器）或本地多维数据集 (.cub) 文件的名称。|对于默认实例和端口 (TCP 2383) 为`Data source=AW-SRV01` 。<br /><br /> 对于命名实例 ($Finance) 和固定端口为`Data source=AW-SRV01$Finance:8081` 。<br /><br /> 对于采用默认实例和端口的完全限定的域名为`Data source=AW-SRV01.corp.Adventure-Works.com` 。<br /><br /> 对于服务器的 IP 地址为`Data source=172.16.254.1` ，它绕过 DNS 服务器查找，对于解决连接问题很有用。|  
|**Initial Catalog** 或 **Catalog**|指定要连接到的 Analysis Services 数据库的名称。 该数据库必须部署在 Analysis Services 上，并且您必须有权连接到它。 此属性对于 AMO 连接是可选的，但是对于 ADOMD.NET 是必需的。|`Initial catalog=AdventureWorks2016`|  
|**提供程序**|有效值包括 MSOLAP。\<版本 >，其中\<版本 > 是 4、 5、 6 或 7。<br /><br /> -   MSOLAP.4 已在 SQL Server 2008 中发布并再次在 SQL Server 2008 R2 中发布（对于 SQL Server 2008 和 2008 R2，文件名为 msolap100.dll）<br />-   MSOLAP.5 已在 SQL Server 2012 中发布（文件名为 msolap110.dll）<br />-   MSOLAP.6 已在 SQL Server 2014 中发布（文件名为 msolap1200.dll）<br />-   MSOLAP.7 已在 SQL Server 2016 中发布（文件名为 msolap130.dll）<br /><br /> 此属性是可选的。 默认情况下，客户端库从注册表读取 OLE DB 访问接口的当前版本。 仅在需要特定版本的数据提供程序时才需要设置此属性，例如要连接到 SQL Server 2012 实例。<br /><br /> MSOLAP.4 已在 SQL Server 2008 和 SQL Server 2008 R2 中发布。 2008 R2 版本支持 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿，有时需要在 SharePoint 服务器上手动安装。 要区分这些版本，您必须检查访问接口的文件属性中的内部版本号：转到 Program files\Microsoft Analysis Services\AS OLEDB\10。 右键单击 msolap110.dll，然后选择“ **属性**”。 单击**“详细信息”**。 查看文件版本信息。 版本应包括 10.50。\<buildnumber > SQL Server 2008 r2。 有关详细信息，请参阅 [在 SharePoint 服务器上安装 Analysis Services OLE DB 提供程序](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859) 和 [用于 Analysis Services 连接的数据提供程序](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md)。|`Provider=MSOLAP.7` 用于需要 SQL Server 2016 版本的 Analysis Services OLE DB 提供程序的连接。|  
|**Cube**|多维数据集名称或透视名称。 一个数据库可以包含多个多维数据集和透视。 可以使用多个目标时，在连接字符串上包括多维数据集或透视名称。|`Cube=SalesPerspective` 显示你可以使用 Cube 连接字符串属性指定多维数据集名称或透视名称。|  
  
##  <a name="bkmk_auth"></a> 身份验证和安全  
 本节介绍与身份验证和加密有关的连接字符串属性。 Analysis Services 只使用 Windows 身份验证，但是您可以在连接字符串上设置属性以传递特定用户名和密码。  
  
 按字母顺序列出属性。  
  
|属性|Description|  
|--------------|-----------------|  
|**EffectiveUserName**|必须在服务器上模拟最终用户标识时使用。 按“域\用户”格式指定帐户。 要使用此属性，调用方在 Analysis Services 中必须具有管理权限。 有关在 SharePoint 的 Excel 工作簿中使用此属性的详细信息，请参阅 [在 SharePoint Server 2013 中使用 Analysis Services EffectiveUserName](http://go.microsoft.com/fwlink/?LinkId=311905)。 有关如何将此属性用于 Reporting Services 的说明，请参阅 [使用 EffectiveUserName 在 SSAS 中模拟](http://go.microsoft.com/fwlink/?LinkId=301385)。<br /><br /> 在**for SharePoint 安装中使用** EffectiveUserName [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 来捕获使用情况信息。 将用户标识提供给服务器以便可以在日志文件中记录包含用户标识的事件或错误。 在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]中，它不用于授权目的。|  
|**Encrypt Password**|指定是否使用本地密码来加密本地多维数据集。 有效值为 True 或 False。 默认值为 False。|  
|**Encryption Password**|用于对加密的本地多维数据集进行解密的密码。 默认值为空。 此值必须由用户显式设置。|  
|**Impersonation Level**|指示模拟客户端时服务器可以使用的模拟级别。 有效值包括：<br /><br /> -   匿名。 客户端对服务器而言是匿名的。 服务器进程无法获取有关客户端的信息，并且不能模拟客户端。<br />-   标识。 服务器进程可以获取客户端标识。 服务器可以模拟客户端标识进行授权，但不能作为客户端访问系统对象。<br />-   模拟。 这是默认值。 可以模拟客户端标识，但是仅在建立连接时，并非每次调用时都可以模拟。<br />-   委托。 代表客户端操作时，服务器进程可以模拟客户端安全上下文。 代表客户端操作时，服务器进程还可以进行针对其他服务器的传出调用。|  
|**Integrated Security**|调用方的 Windows 标识用于连接到 Analysis Services。 有效值为空、SSPI 和 BASIC。<br /><br /> **集成安全性**=**SSPI** 是 TCP 连接的默认值，支持 NTLM、Kerberos 或匿名身份验证。 HTTP 连接的默认值为空。<br /><br /> 使用 **SSPI**时， **ProtectionLevel** 必须设置为以下值之一： **Connect**、 **PktIntegrity**、 **PktPrivacy**。|  
|**Persist Encrypted**|当客户端应用程序需要数据源对象以加密形式保存敏感身份验证信息（如密码）时设置此属性。 默认情况下，不保存身份验证信息。|  
|**Persist Security Info**|有效值为 True 和 False。 设置为 True 时，在建立连接后可以从连接获取安全信息（如以前在连接字符串上指定的用户标识或密码）。 默认值为 False。|  
|**保护级别**|确定连接上使用的安全级别。 有效值包括：<br /><br /> -   **None**。 不进行身份验证的连接或匿名连接。 不对发送到服务器的数据进行身份验证。<br />-   **Connect**。 进行身份验证的连接。 仅当客户端与服务器建立关系时进行身份验证。<br />-   **Pkt 完整性**。 加密的连接。 验证从客户端接收了所有数据并且数据在途中未更改。<br />-   **Pkt 隐私**。 签名的加密，仅对于 XMLA 支持。 验证从客户端接收了所有数据并且数据在途中未更改，通过加密来保护数据的隐私。<br /><br /> 有关详细信息，请参阅 [Establishing Secure Connections in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-establishing-secure-connections.md)|  
|**Roles**|指定逗号分隔的预定义的角色列表，以使用该角色具有的权限连接到服务器或数据库。 如果忽略此属性，则使用所有角色且有效权限为所有角色的组合权限。 如果将此属性设置为空值（例如 Roles=’ ‘），则客户端连接没有角色成员身份。<br /><br /> 管理员使用此属性通过角色具有的权限进行连接。 如果角色的权限不足，一些命令可能失败。|  
|**SSPI**|显式指定将 **Integrated Security** 设置为 **SSPI**时要将哪个安全包用于客户端身份验证。 SSPI 支持多个包，但是您可以使用此属性指定特定的包。 有效值为“协商”、Kerberos、NTLM 和“匿名用户”。 如果未设置此属性，则所有包可用于连接。|  
|**Use Encryption for Data**|加密数据传输。 有效值为 True 和 False。|  
|**User ID**=…; **Password**=|将 **User ID** 和 **Password** 一起使用。 Analysis Services 模拟通过这些凭据指定的用户标识。 在 Analysis Services 连接上，仅当为 HTTP 访问配置了服务器并且您在 IIS 虚拟目录上指定了基本身份验证替代集成安全性时才在命令行上列出凭据。 直接连接到服务器时，将忽略 **UserID** 和 **Password** 连接字符串参数并使用已登录用户的上下文进行连接。 <br /><br />用户名和密码必须是 Windows 标识（本地用户帐户或域用户帐户）的凭据。 请注意 **User ID** 包含嵌入的空格。 此属性的其他别名包括 **UserName** （无空格）和 **UID**。 **Password** 的别名为 **PWD**。|  
  
##  <a name="bkmk_special"></a> 特殊用途的参数  
 本节介绍其余连接字符串参数。 这些参数用于确保应用程序所需的特定连接行为。  
  
 按字母顺序列出属性。  
  
|属性|Description|  
|--------------|-----------------|  
|**Application Name**|设置与连接关联的应用程序的名称。 当监视跟踪事件，特别是您具有访问同一数据库的几个应用程序时，此值很有用。 例如，将 Application Name=’test’ 添加到连接字符串将导致 ‘test’ 在 SQL Server Profiler 跟踪中显示，如以下屏幕快照中所示：<br /><br /> ![SSAS_AppNameExcample](../../analysis-services/instances/media/ssas-appnameexcample.gif "SSAS_AppNameExcample")<br /><br /> 此属性的别名包括 **sspropinitAppName**、 **AppName**。 有关详细信息，请参阅 [连接到 SQL Server 时使用 Application Name 参数](http://go.microsoft.com/fwlink/?LinkId=301699)。|  
|**AutoSyncPeriod**|设置客户端和服务器缓存同步的频率（毫秒）。 ADOMD.NET 为具有最小内存开销的常用对象提供客户端缓存。 这有助于减少到服务器的往返次数。 默认值为 10000 毫秒（或 10 秒钟）。 设置为 null 或 0 时，关闭自动同步功能。|  
|**Character Encoding**|定义如何在请求中对字符编码。 有效值为 Default 或 UTF-8（它们是等效的）和 UTF-16。| 
|**CommitTimeout**|XMLA 属性。 确定在进行回滚前，当前正在运行的命令的提交阶段需等待的时间（毫秒）。 如果大于 0，则覆盖服务器配置中对应 CommitTimeout 属性的值。 |   
|**CompareCaseSensitiveStringFlags**|为指定的区域设置调整区分大小写的字符串比较。 有关如何设置此属性的详细信息，请参阅 [CompareCaseSensitiveStringFlags 属性](http://msdn.microsoft.com/library/aa237459\(v=sql.80\).aspx)。|  
|**Compression Level**|如果 **TransportCompression** 为 XPRESS，您可以设置压缩级别以控制使用的压缩程度。 有效值为 0-9，其中 0 表示最小程度的压缩，9 表示最大程度的压缩。 增大压缩程度将降低性能。 默认值为 0。|  
|**Connect Timeout**|确定客户端在超时前尝试连接所用的最长时间（秒）。如果在此期间连接未成功，则客户端不再尝试连接并生成错误。|  
|**MDX Compatibility**|此属性的目的是确保发出 MDX 查询的应用程序具有一致的 MDX 行为集。 Excel 使用 MDX 查询填充和计算连接到 Analysis Services 的数据透视表，它将此属性设置为 1 以确保在数据透视表中显示不规则层次结构中的占位符成员。 有效值包括 0、1、2。<br /><br /> 0 和 1 表示公开占位符成员；2 表示不公开这些成员。 如果它为空，则假定为 0。|  
|**MDX Missing Member Mode=Error**|指示是否在 MDX 语句中忽略缺少的成员。 有效值为 Default、Error 和 Ignore。 Default 使用服务器定义的值。 Error 在成员不存在时生成错误。 Ignore 指定应忽略缺失值。|  
|**Optimize Response**|位掩码指示启用以下哪个查询响应优化。<br /><br /> -   0x01 使用 NormalTupleSet（这是默认值）<br />-   0x02 在切片器为空时使用|  
|**Packet Size**|网络数据包大小（字节）为 512-32,767。 默认网络数据包大小为 4096。|  
|**Protocol Format**|设置发送给服务器的 XML 格式。 有效值为 Default、XML 或 Binary。 协议为 XMLA。 您可以指定以压缩格式（默认值）发送 XML、作为原始 XML 发送或以二进制格式发送。 二进制格式对 XML 元素和属性编码，使得它们更小。 压缩是进一步减小请求和响应大小的专用格式。 压缩和二进制格式用于提高数据传输请求和响应的速度。<br /><br /> 如果要使用二进制或压缩格式，您必须使用连接上的客户端库。 OLE DB 访问接口可以将请求和响应格式设置为二进制或压缩格式。 AMO 和 ADOMD.NET 将请求格式设置为文本，但是接受二进制或压缩格式的响应。<br /><br /> 此连接字符串属性与 **EnableBinaryXML** 和 **EnableCompression** 服务器配置设置等效。|  
|**Real Time Olap**|设置此属性以绕过缓存，导致所有分区主动侦听查询通知。 默认情况下，不设置此属性。|  
|**Safety Options**|设置用户定义的函数和操作的安全级别。 有效值为 0、1、2。 在 Excel 连接中，此属性为 Safety Options=2。 有关此选项的详细信息可以在 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>。|  
|**SQLQueryMode**|指定 SQL 查询是否包含计算。 有效值为 Data、Calculated、IncludeEmpty。 Data 表示不允许计算。 Calculated 表示允许计算。 IncludeEmpty 表示允许计算并在查询结果中返回空行。|  
|**Timeout**|指定在生成错误前客户端库等待命令完成的最长时间（秒）。|  
|**Transport Compression**|定义在通过 **Protocol Format** 属性指定压缩时如何压缩客户端和服务器通信。 有效值为 Default、None、Compressed 和 **gzip**。 Default 表示不压缩 TCP，或对 HTTP 使用 **gzip** 。 None 指示不使用压缩。 Compressed 使用 XPRESS 压缩（SQL Server 2008 和更高版本）。 **gzip** 仅对于 HTTP 连接有效，其中 HTTP 请求包括 Accept-Encoding=gzip。|  
|**UseExistingFile**|连接到本地多维数据集时使用。 此属性指定是否覆盖本地多维数据集。 有效值为 True 或 False。 如果设置为 True，则多维数据集文件必须存在。 现有文件将是连接目标。 如果设置为 False，则覆盖多维数据集文件。|  
|**VisualMode**|设置此属性以控制在应用维度安全性时如何聚合成员。<br /><br /> 对于允许每个人查看的多维数据集数据，聚合所有成员有意义，因为组成总计的所有值是可见的。 但是，如果您基于用户标识筛选或限制了维度，基于所有成员显示总计（将受限制的值和允许的值合并为一个总计）可能令人困惑，或导致显示的信息比应揭示的信息多。<br /><br /> 要在应用维度安全性时指定如何聚合成员，您可以将此属性设置为 True 以仅在聚合中使用允许的值，或将其设置为 False 以将受限制的值从总计中排除。<br /><br /> 在连接字符串上设置时，此值适用于多维数据集或透视级别。 在模型内，您可以在更精细的级别上控制可视总计。<br /><br /> 有效值为 0、1 和 2。<br /><br /> -   0 是默认值。 当前，默认行为与 2 等效，其中聚合包含未显示给用户的值。<br />-   1 从总计中排除隐藏的值。 这对 Excel 为默认值。<br />-   2 将隐藏的值包含在总计中。 这是服务器上的默认值。<br /><br /> 此属性的别名包括 **Visual Total** 或 **Default MDX Visual Mode**。|  
  
##  <a name="bkmk_reserved"></a> 保留供将来使用  
 以下属性允许用于连接字符串，但是在当前版本的 Analysis Services 中无效。  
  
-   Authenticated User  
  
-   Cache Authentication  
  
-   Cache Mode（已在早期版本中调查此属性的使用情况。 尽管您可能找到推荐使用它的博客文章，但是应避免设置此属性，除非 Microsoft 支持人员要求您这样做）。  
  
-   Cache Policy  
  
-   Cache Ratio  
  
-   Cache Ratio2  
  
-   Dynamic Debug Limit  
  
-   Debug Mode  
  
-   模式  
  
-   SQLCompatibility  
  
-   Use Formula Cache  
  
##  <a name="bkmk_examples"></a> 连接字符串示例  
 本节介绍在常用应用程序中设置 Analysis Services 连接时您最有可能使用的连接字符串。  
  
 **通用连接字符串**  
  
 如果您正在从 Reporting Services 配置连接，可能使用类似这样的连接字符串。  
  
 `Data source=<servername>; initial catalog=<databasename>`  
  
 **Excel 中的连接字符串**  
  
 Excel 中的默认 ADOMD.NET 连接字符串指定数据访问接口、服务器、数据库名称、Windows 集成安全性。 MDX 兼容级别始终设置为 1。 尽管您可以针对当前会话更改该值，但 Excel 会在下次打开文件时将 MDX 兼容级别重置为 1。  
  
 `Provider=MSOLAP.5;Integrated Security=SSPI;Persist Security Info=True;Initial Catalog=Adventure Works DW 2008R2;Data Source=AW-SRV01;MDX Compatibility=1;Safety Options=2;MDX Missing Member Mode=Error`  
  
 有关详细信息，请参阅[数据连接、数据源和连接字符串&#40;报表生成器和 SSRS& #41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 和 [SharePoint Server 2013 中用于 Excel Services 的数据身份验证](http://go.microsoft.com/fwlink/?LinkId=296350)。  
  
##  <a name="bkmk_supportedstrings"></a>Analysis Services 中使用的连接字符串格式  
 本节列出了 Analysis Services 支持的所有连接字符串格式。 除了与 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据库的连接，你还可以在连接 Analysis Services 的应用程序中指定这些连接字符串。  
  
 **与服务器的本机（或直接）连接**  
  
 `Data Source=server[:port][\instance]` ，其中，“port”和“\instance”都是可选的。 例如，指定“Data Source=server1”将在名为“server1”的服务器上打开指向默认实例（和默认端口 2383）的连接。  
  
 “Data Source=server1:port1”将打开指向运行在“server1”的端口“port1”上的 Analysis Services 实例的连接。  
  
 “Data Source=server1\instance1”将打开指向 SQL Browser（在其默认端口 2382 上）的连接，为名为“instance1”的实例解析该端口，然后打开指向该 Analysis Services 端口的连接。  
  
 “Data Source=server1:port1\instance1”将打开指向“port1”上的 SQL Browser 的连接，为名为“instance1”的实例解析该端口，然后打开指向该 Analysis Services 端口的连接。  
  
 **本地多维数据集连接（.cub 文件）**  
  
 `Data Source=<path>`，例如“Data Source=c:\temp\a.cub”  
  
 **与 msmdpump.dll 的 Http(s) 连接**  
  
 `Data Source=<URL>`，其中，URL 是包含 msmdpump.dll 的虚拟 IIS 文件夹的 HTTP 或 HTTPS 地址。 有关详细信息，请参阅[在 Internet Information Services (IIS) 8.0 上配置对 Analysis Services 的 HTTP 访问](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)。  
  
 **与 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿（.xlsx、.xlsb 或 .xlsm 文件）的 Http(s) 连接**  
  
 `Data Source=<URL>`，其中，URL 是指向已发布到某一 SharePoint 库的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿的 SharePoint 路径。 例如， `Data Source=http://localhost/Shared Documents/Sales.xlsx`。  
  
 **与 BI 语义模型连接文件的 Http(s) 连接**  
  
 `Data Source=<URL>` ，其中，URL 是指向 .bism 文件的 SharePoint 路径。 例如， `Data Source=http://localhost/Shared Documents/Sales.bism`。  
  
 **嵌入的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 连接**  
  
 `Data Source=$Embedded$`，其中，$embedded$ 是一个引用工作薄内嵌入的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据模型的名字对象。 此连接字符串在内部创建并管理。 请不要修改它。 嵌入的连接字符串由客户端工作站上的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 外接程序解析，或由 SharePoint 场中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 实例解析。  
  
 **Analysis Services 存储过程中的本地服务器环境**  
  
 `Data Source=*`，其中，* 解析为本地实例。  
  
##  <a name="bkmk_encrypt"></a> 加密连接字符串  
 Analysis Services 使用自身的加密密钥来加加密连接字符串。 它不生成自签名证书。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对它所使用的连接字符串进行加密和存储以连接到它的每个数据源。 如果与数据源的连接需要用户名和密码，则可以让 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将名称和密码与连接字符串存储在一起，也可以在每次需要连接到数据源时再提示您输入名称和密码。 如果让 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提示您输入用户信息，则不必存储和加密此信息。 但是，如果将此信息存储在连接字符串中，则需要对此信息加密并加以保护。  
  
 若要对连接字符串信息进行加密和保护， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用数据保护 API。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用一个单独的加密密钥对每个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的连接字符串信息进行加密。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在你创建数据库时创建此密钥，并基于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 启动帐户对该连接字符串信息进行加密。 当 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 启动时，将读取、解密并存储每个数据库的加密密钥。 当[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 需要连接某个数据源时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会使用适当的解密密钥对该数据源的连接字符串信息解密。  
  
## <a name="see-also"></a>另请参阅  
 [在 Internet Information Services (IIS) 8.0 上配置对 Analysis Services 的 HTTP 访问](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)   
 [针对 Kerberos 约束委派对 Analysis Services 进行配置](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)   
 [用于 Analysis Services 连接的数据访问接口](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md)   
 [连接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  

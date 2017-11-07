---
title: "调用 ASCmd cmdlet |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 2896b74a-3911-4b3f-89ab-bb375bdb34d8
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 366263980ae7ad9d5a792e6525888080a38ebbf6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="invoke-ascmd-cmdlet"></a>Invoke-ASCmd cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  使数据库管理员能够执行 XMLA 脚本、多维表达式 (MDX) 或数据挖掘扩展 (DMX) 语句或表格模型脚本语言 (TMSL) 脚本。  
  
 只有在 SQL Server 2016 Analysis Services 实例上的表格服务器模式下才支持 TMSL。  
  
 如果想要创建数据库或其他对象，这是你将使用的带有脚本输入文件的 cmdlet。  
  
## <a name="syntax"></a>语法  
 `Invoke-ASCmd –Query <string> [-Server <string>] [-Database <string>] [-Credential <PSCredential>] [-ConnectionTimeout <int>] [-QueryTimeout <int>] [-Variable <string[]>] [-TraceFile <string>] [-TraceFileFormat <TraceFileFormatOption>] [-TraceFileDelimiter <string>] [-TraceTimeout <int>] [-TraceLevel <TraceLevelOption>] [<CommonParameters>]`  
  
 `Invoke-ASCmd –InputFile <string> [-Server <string>] [-Database <string>] [-Credential <PSCredential>] [-ConnectionTimeout <int>] [-QueryTimeout <int>] [-Variable <string[]>] [-TraceFile <string>] [-TraceFileFormat <TraceFileFormatOption>] [-TraceFileDelimiter <string>] [-TraceTimeout <int>] [-TraceLevel <TraceLevelOption>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Invoke-ASCmd cmdlet 可以执行在输入文件中包含的查询或脚本。  
  
 对于 XMLA，支持以下命令：Alter、Backup、Batch、BeginTransaction、Cancel、ClearCache、CommitTransaction、Create、Delete、DesignAggregations、Drop、Insert、Lock、MergePartitions、NotifyTableChange、Process、Restore、RollbackTransaction、Statement（用于执行 MDX 查询和 DMX 语句）、Subscribe、Synchronize、Unlock、Update、UpdateCells。  
  
 对于 TMSL：支持 Alter、Create、Delete、MergePartitions、Process、Update。  
  
 此 cmdlet 支持 –Credential 参数，该参数可在您配置 Analysis Services 实例以进行 HTTP 访问时使用。 –Credential 参数具有可提供 Windows 用户标识的 PSCredential 对象。 之后，IIS 将在连接到 Analysis Services 时模拟该用户。 此标识必须对 Analysis Services 实例具有系统管理员权限才能运行脚本。  
  
## <a name="parameters"></a>Parameters  
  
### <a name="-query-string"></a>-查询\<字符串 >  
 直接在命令行中（而不是文件中）指定实际脚本、查询或语句。 也可以将查询指定为管道输入。 在使用 **Invoke-AsCmd** 时，必须为 **–InputFile** 或 **–Query**参数指定值。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|True (ByValue)|  
|接受通配符？|false|  
  
### <a name="-inputfile-string"></a>-InputFile\<字符串 >  
 标识包含 XMLA 脚本、MDX 查询、DMX 语句或 TMSL 脚本（在 JSON 中）的文件。 在使用 **Invoke-AsCmd** 时，必须为 **–InputFile** 或 **–Query**参数指定值。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-server-string"></a>服务器\<字符串 >  
 指定 cmdlet 要连接和执行的 Analysis Services 实例。 如果未提供服务器名称，将连接到本地主机。 对于默认实例，仅指定服务器名称。 对于命名实例，请使用格式 servername\instancename。 对于 HTTP 连接，请使用格式 http[s]://server[:port]/virtualdirectory/msmdpump.dll。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|localhost|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-database-string"></a>-数据库\<字符串 >  
 指定要对其执行 MDX 查询或 DMX 语句的数据库。 当 cmdlet 执行 XMLA 脚本时，将忽略 database 参数，因为数据库名称嵌入在 XMLA 脚本之中。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-credential-pscredential"></a>-Credential \<PSCredential >  
 指定可提供 Windows 用户名和密码的 PSCredential 对象。 仅当配置 Analysis Services 实例以使用基本身份验证进行 HTTP 访问时指定此参数。 对于使用集成安全性的本机连接，将忽略此参数。  
  
 如果此参数存在，则将其提供的凭据追加到连接字符串。 IIS 将在连接到 Analysis Services 时模拟该用户标识。 如果未指定凭据，将使用正在运行该工具的用户的默认 Windows 帐户。  
  
 若要使用此参数，请首先使用 Get-Credential 创建一个 PSCredential 对象，以便指定用户名和密码（例如， `$Cred=Get-Credential “adventure-works\admin”`。 然后，可以将此对象传送到 –Credential 参数 `(-Credential:$Cred`)。  
  
   有关 HTTP 访问的详细信息，请参阅[在 Internet Information Services (IIS) 8.0 上配置对 Analysis Services 的 HTTP 访问](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|True (ByValue)|  
|接受通配符？|false|  
  
### <a name="-connectiontimeout-int"></a>-ConnectionTimeout \<int >  
 指定连接到 Analysis Services 实例超时之前等待的秒数。超时值必须是 0 和 65534 之间的整数。 如果指定 0，则连接尝试将没有超时限制。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|30|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-querytimeout-int"></a>-QueryTimeout \<int >  
 指定查询超时之前等待的秒数。如果未指定超时值，则查询将不会超时。超时值必须是 1 和 65535 之间的整数。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|30|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-variable-string"></a>-变量\<string [] >  
 指定其他脚本变量。 每个变量都是一个名称-值对。 如果值中包含嵌入的空格或控制字符，则必须使用双引号 (") 将其引起来。 使用 PowerShell 数组可指定多个变量及其值。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-tracefile-string"></a>-TraceFile\<字符串 >  
 标识在执行 XMLA 脚本、MDX 查询或 DMX 语句时将接收 Analysis Services 跟踪事件的文件。 如果该文件已存在，则自动将其覆盖（但使用 -TraceLevel:Duration 和 –TraceLevel:DurationResult 参数设置创建的跟踪文件除外）。 包含空格的文件名必须用引号(" ")引起来。 如果文件名无效，将生成一个错误消息。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-tracefileformat-string"></a>-TraceFileFormat\<字符串 >  
 指定 –TraceFile 参数的文件格式（如果指定了该参数）。 可用选项为文本或 csv。 默认值为“csv”。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|csv|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-tracefiledelimiter-string"></a>-TraceFileDelimiter\<字符串 >  
 指定在将 csv 指定为跟踪文件格式时要用作跟踪文件分隔符的字符。 默认值为 |（竖线）。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-tracetimeout-int"></a>-TraceTimeout \<int >  
 指定结束跟踪之前 Analysis Services 引擎等待的秒数（如果指定了 –TraceFile 参数）。 如果在指定时间段没有记录跟踪消息，则认为跟踪已完成。 默认跟踪超时值为 5 秒。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|5|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-tracelevel-traceleveloption"></a>-TraceLevel \<TraceLevelOption >  
 指定在跟踪文件中收集和记录哪些数据。 可能值为 High、Medium、Low、Duration、DurationResult。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|High|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 此 cmdlet 支持以下常用参数：-Verbose、-Debug、-ErrorAction、-ErrorVariable、-OutBuffer 和 -OutVariable。 有关详细信息，请参阅 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## <a name="inputs-and-outputs"></a>输入和输出  
 输入类型是可以传送到 cmdlet 的对象的类型。 返回类型是 cmdlet 所返回的对象的类型。  
  
|||  
|-|-|  
|输入|PSObject|  
|输出|字符串|  
  
## <a name="example-1-xmla-input-file"></a>示例 1（XMLA 输入文件）  
  
```  
Invoke-ASCmd –InputFile:"C:\MyFolder\DiscoverConnections.xmla"  
```  
  
 此命令运行一个 XMLA 脚本，该脚本返回服务器上活动连接的列表。 文件 DiscoverConnections.xmla 包含以下 XMLA 脚本：  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
<RequestType>DISCOVER_CONNECTIONS</RequestType>  
<Restrictions />  
   <Properties>  
      <PropertyList>  
         <Content>Data</Content>  
      </PropertyList>  
   </Properties>  
</Discover>  
```  
  
## <a name="example-2-tmsl-input-file"></a>示例 2（TMSL 输入文件）  
 此示例等同于第一个示例，只不过脚本是 TMSL (JSON) 且需要 SQL Server 2016 的表格实例。 然后，你可以在 SQL Server Management Studio 中生成 TMSL 脚本。  
  
 如果有多个实例且表格实例是命名实例，请记住设置服务器名称：  
  
```  
Invoke-ASCmd –InputFile "C:\folder-name\T1200-NewDB.json" -Server "server-name\instance-name"  
```  
  
## <a name="example-3-query"></a>示例 3（查询）  
  
```  
Invoke-ASCmd -Database:"Adventure Works DW" -Query:"<Discover xmlns='urn:schemas-microsoft-com:xml analysis'><RequestType>DISCOVER_DATASOURCES</RequestType><Restrictions></Restrictions><Properties></Properties></Discover>"  
```  
  
 发现 XMLA 查询将返回可用于分析服务器的数据源以及连接到这些数据源所需的信息。 结果采用 XML 格式。 为改进可读性，你可以将输出传送到一个 XML 文件（例如，将 `| Out-file C:\Results\XMLAQueryOutput.xml` 追加到该命令），然后在浏览器或支持结构化 XML 的其他应用程序中查看结果。  
  
  
  


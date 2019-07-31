---
title: Integration Services 错误和消息引用 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- error numbers [Integration Services]
- hresults [Integration Services]
- errors [Integration Services], listed
ms.assetid: 2c825c07-5074-42ad-90ea-0dc5a588dcf7
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c4d989bf1049faa41838de1f86f93b9ef2db228e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057652"
---
# <a name="integration-services-error-and-message-reference"></a>Integration Services 错误和消息引用

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  下表按编号的升序列出了每个类别中的预定义 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 错误、警告和信息性消息及其数值代码和符号名称。 其中每个错误都定义为 <xref:Microsoft.SqlServer.Dts.Runtime.Hresults> 命名空间的 <xref:Microsoft.SqlServer.Dts.Runtime> 类中的一个字段。  
  
 当遇到不带其说明的错误代码时此列表可能非常有用。 目前该列表中不包括故障排除信息。  
  
> [!IMPORTANT]  
>  很多在使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 时可能看到的错误消息都来自其他组件。 在本主题中，您将找到由 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 组件引发的所有错误。 如果在此列表中没有看到您的错误，则该错误可能是由 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]之外的组件引发的。 其中可能包括 OLE DB 访问接口、其他数据库组件（如 [!INCLUDE[ssDE](../includes/ssde-md.md)] 和 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ）或者其他服务或组件，如文件系统、SMTP 服务器和消息队列（也称为 MSMQ）。 若要查找有关这些外部错误消息的信息，请参阅特定于组件的文档。  
  
 此列表包含下列各组消息：  
  
-   [错误消息 (DTS_E_*)](#msgError)  
  
-   [警告消息 (DTS_W_*)](#msgWarning)  
  
-   [信息性消息 (DTS_I_*)](#msgInfo)  
  
-   [常规消息和事件消息 (DTS_MSG_*)](#msgGeneral)  
  
-   [成功消息 (DTS_S_*)](#msgSuccess)  
  
-   [数据流组件错误消息 (DTSBC_E_*)](#msgPipeline)  
  
##  <a name="msgError"></a> 错误消息  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 错误消息的符号名称以 **DTS_E_** 开头。  
  
|十六进制代码|十进制代码|符号名称|描述|  
|----------------------|------------------|-------------------|-----------------|  
|0x8002F347|-2147290297|DTS_E_STOREDPROCSTASK_OVERWRITINGSPATDESTINATION|正在覆盖目标中的存储过程“%1”。|  
|0x8020837E|-2145352834|DTS_E_ADOSRCUNKNOWNTYPEMAPPEDTONTEXT|对于 %3，不支持找到的列“%2”的数据类型“%1”。 此列将被转换为 DT_NTEXT。|  
|0x8020838C|-2145352820|DTS_E_XMLSRCSCHEMACOLUMNNOTINEXTERNALMETADATA|XML 架构中表 %2 内的列 %1 在外部元数据列中没有映射。|  
|0xC0000032|-1073741774|DTS_E_NOTINITIALIZED|某个内部对象或变量未初始化。 这是一个内部产品错误。  当应该具有有效值的变量没有有效值时，会返回此错误。|  
|0xC0000033|-1073741773|DTS_E_EXPIRED|Integration Services 评估期已过。|  
|0xC0000034|-1073741772|DTS_E_NEGATIVEVALUESNOTALLOWED|不能为此属性赋予负值。 如果为只能包含正值的属性(例如 COUNT 属性)赋予负值，将出现此错误。|  
|0xC0000035|-1073741771|DTS_E_NEGATIVEINDEXNOTALLOWED|索引不能为负。 如果集合的索引使用负值，将出现此错误。|  
|0xC00060AB|-1073717077|DTS_E_INVALIDSSISSERVERNAME|无效的服务器名称“%1”。 SSIS 服务不支持多实例，请仅使用服务器名称，而不是“服务器名称\实例”。|  
|0xC0008445|-1073707963|DTS_E_SCRIPTMIGRATIONFAILED64BIT|由于缺少 Visual Tools for Applications 设计器支持，无法在 64 位平台上完成 VSA 脚本的迁移。 请在 64 位平台上在 WOW64 下运行迁移。|  
|0xC000931A|-1073704166|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_ERRORSINCOMMAND|执行命令时生成了错误。|  
|0xC000F427|-1073679321|DTS_E_SSISSTANDALONENOTINSTALLED|若要在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 之外运行 SSIS 包，必须安装 Integration Services 的 %1 或更高版本。|  
|0xC0010001|-1073676287|DTS_E_VARIABLENOTFOUND|找不到该变量。 如果在包的执行期间试图从容器的 Variables 集合检索某个变量，但该变量不在此处时，将出现这种情况。 变量可能已更改名称，或者并未创建。|  
|0xC0010003|-1073676285|DTS_E_VARIABLEREADONLY|试图写入只读变量“%1”时出错。|  
|0xC0010004|-1073676284|DTS_E_MANAGEDCOMPONENTSTORENOTFOUND|找不到包含任务和数据流任务组件的目录。 请检查您的安装是否完整。|  
|0xC0010006|-1073676282|DTS_E_PACKAGENAMETOOLONG|包名称过长。 长度限制为 128 个字符。 请缩短包名称的长度。|  
|0xC0010007|-1073676281|DTS_E_PACKAGEDESCRIPTIONTOOLONG|包说明过长。 长度限制为 1024 个字符。 请缩短包说明的长度。|  
|0xC0010008|-1073676280|DTS_E_VERCOMMENTSTOOLONG|VersionComments 属性过长。 长度限制为 1024 个字符。 请缩短 VersionComments 的长度。|  
|0xC0010009|-1073676279|DTS_E_ELEMENTNOTFOUND|在集合中找不到元素。 如果在包的执行期间试图从容器的集合检索某个元素，但该元素不在此处，将发生此错误。|  
|0xC001000A|-1073676278|DTS_E_PACKAGENOTFOUND|无法从 SQL Server 数据库加载指定的包。|  
|0xC001000C|-1073676276|DTS_E_INVALIDVARIABLEVALUE|对变量的赋值无效。 如果客户端或任务将运行时对象赋给某个变量值，将发生此错误。|  
|0xC001000D|-1073676275|DTS_E_RESERVEDNAMESPACE|为变量分配命名空间时出错。 命名空间 "System" 预留给系统使用。 如果组件或任务试图创建命名空间为 "System" 的变量，将发生此错误。|  
|0xC001000E|-1073676274|DTS_E_CONNECTIONNOTFOUND|找不到连接“%1”。 如果找不到特定的连接元素，Connections 集合将发生此错误。|  
|0xC001000F|-1073676273|DTS_E_64BITVARIABLERECAST|变量“%1”是 64 位整数变量，而此操作系统不支持此类变量。 已将该变量转换为 32 位整数。|  
|0xC0010010|-1073676272|DTS_E_CANTCHANGEREADONLYATRUNTIME|试图更改变量“%1”的只读属性。 如果在运行时更改某个变量的只读属性，将发生此错误。 只读属性只能在设计时更改。|  
|0xC0010011|-1073676271|DTS_E_VARIABLEINVALIDCONTAINERREF|将变量设置为容器引用的尝试无效。  不允许变量引用容器。|  
|0xC0010013|-1073676269|DTS_E_INVALIDVARVALUE|为变量“%1”赋予的值或对象无效。 如果值不适合变量，会发生此错误。|  
|0xC0010014|-1073676268|DTS_E_GENERICERROR|发生了一个或多个错误。 在此消息之前应有更为具体的错误消息，对这些错误进行详细说明。 此消息用作遇到错误的函数的返回值。|  
|0xC0010016|-1073676266|DTS_E_INVALIDARRAYVALUE|获取或设置数组值时出错。 不允许使用类型“%1”。 将数组加载到变量时会出现这种情况。|  
|0xC0010017|-1073676265|DTS_E_UNSUPPORTEDARRAYTYPE|数组中有不支持的类型。 将包含不支持的类型的数组保存到变量时会出现这种情况。|  
|0xC0010018|-1073676264|DTS_E_PERSISTENCEERROR|从节点“%2”加载值“%1”时出错。|  
|0xC0010019|-1073676263|DTS_E_INVALIDNODE|节点“%1”不是有效的节点。 保存失败时会出现这种情况。|  
|0xC0010020|-1073676256|DTS_E_ERRORLOADINGTASK|无法加载任务“%1”、类型“%2”。 此任务的联系信息为“%3”。|  
|0xC0010021|-1073676255|DTS_E_ERRORELEMENTNOTINCOLL|集合“%2”中没有元素“%1”。|  
|0xC0010022|-1073676254|DTS_E_MISSINGOBJECTDATA|宿主对象的 XML 块中缺少 ObjectData 元素。 当 XML 分析器要定位某对象的该数据元素，却找不到它时，会出现这种情况。|  
|0xC0010023|-1073676253|DTS_E_VARIABLENOTFOUNDINCOLL|找不到变量“%1”。 如果在包的执行期间试图从容器的 Variables 集合检索某个变量，但该变量不在此处，将出现此错误。  变量名称可能已更改，或者并未创建该变量。|  
|0xC0010025|-1073676251|DTS_E_HASEMPTYTASKHOSTS|该包含有无法加载的任务，所以无法执行。|  
|0xC0010026|-1073676250|DTS_E_TASKISEMPTY|无法加载该任务。 该任务的联系信息为“%1”。|  
|0xC0010027|-1073676249|DTS_E_ERRORLOADINGTASKNOCONTACT|加载任务“%1”时出错。|  
|0xC0010028|-1073676248|DTS_E_ERRORATLOADTASK|加载任务时出错。 从 XML 加载任务失败时会出现这种情况。|  
|0xC0010200|-1073675776|DTS_E_MULTIPLECACHEWRITES|%1 无法写入缓存，因为 %2 已经写入缓存中。|  
|0xC0010201|-1073675775|DTS_E_SETCACHEFORINSERTFAILED|无法为新的数据准备缓存。|  
|0xC0010202|-1073675774|DTS_E_SETCACHEFORFILLFAILED|无法将缓存标记为已填满数据。|  
|0xC0010203|-1073675773|DTS_E_READUNINITIALIZEDCACHE|缓存未初始化，无法由 %1 读取。|  
|0xC0010204|-1073675772|DTS_E_SETCACHEFORREADFAILED|无法准备缓存以提供数据。|  
|0xC0010205|-1073675771|DTS_E_READNOTFILLEDCACHE|%1 正在向缓存执行写入操作，%2 无法读取缓存。|  
|0xC0010206|-1073675770|DTS_E_WRITEWHILECACHEINUSE|正在从 %1 中读取缓存，%2 无法写入缓存。|  
|0xC0011001|-1073672191|DTS_E_CANTLOADFROMNODE|无法从指定的 XML 节点加载运行时对象。  如果试图从类型不正确的 XML 节点(例如非 SSIS XML 节点)加载包或其他对象，会出现这种情况。|  
|0xC0011002|-1073672190|DTS_E_OPENPACKAGEFILE|由于错误 0x%2!8.8X!，无法打开包文件“%1” “%3”。  如果在加载包时文件无法打开或无法正确加载到 XML 文档，会出现这种情况。 这可能是由于调用 LoadPackage 时提供的文件名不正确，或者指定的 XML 文件的格式不正确。|  
|0xC0011003|-1073672189|DTS_E_LOADPACKAGEXML|由于错误 0x%1!8.8X!，无法加载 XML “%2”。 如果在加载包时文件无法打开或无法正确加载到 XML 文档，会出现这种情况。  这可能是由于为 LoadPackage 方法提供的文件名不正确，或者指定的 XML 文件的格式不正确。|  
|0xC0011004|-1073672188|DTS_E_LOADPACKAGEXMLFILE|由于错误 0x%2!8.8X!，无法从包文件“%1”加载 XML “%3”。  如果在加载包时文件无法打开或无法正确加载到 XML 文档，会出现这种情况。 这可能是由于为 LoadPackage 方法提供的文件名不正确，或者指定的 XML 文件的格式不正确。|  
|0xC0011005|-1073672187|DTS_E_OPENFILE|无法打开包文件。 如果在加载包时文件无法打开或无法正确加载到 XML 文档，会出现这种情况。 这可能是由于为 LoadPackage 方法提供的文件名不正确，或者指定的 XML 文件的格式不正确。|  
|0xC0011006|-1073672186|DTS_E_UNABLETODECODEBINARYFORMAT|无法解码包中的二进制格式。|  
|0xC0011007|-1073672185|DTS_E_FUNDAMENTALLOADINGERROR|无法将包作为 XML 加载，因为包不具有有效的 XML 格式。 将发布一个特定的 XML 分析器错误。|  
|0xC0011008|-1073672184|DTS_E_LOADFROMXML|从 XML 加载时出错。 没有关于此问题的更详细错误信息，因为没有传递可存储详细错误信息的 Events 对象。|  
|0xC0011009|-1073672183|DTS_E_XMLDOMERROR|无法创建 XML 文档对象模型的实例。 可能未注册 MSXML。|  
|0xC001100D|-1073672179|DTS_E_CANNOTLOADOLDPACKAGES|无法加载包。 当试图加载更低版本的包，或包文件引用了无效的结构化对象时，会出现这种情况。|  
|0xC001100E|-1073672178|DTS_E_SAVEFILE|无法保存包文件。|  
|0xC001100F|-1073672177|DTS_E_SAVEPACKAGEFILE|无法保存包文件“%1”，错误为 0x%2!8.8X! “%3”。|  
|0xC001200D|-1073668083|DTS_E_IDTSNAMENOTSUPPORTED|该对象必须从 IDTSName100 继承，但情况并非如此。|  
|0xC0012018|-1073668072|DTS_E_CONFIGFORMATINVALID_PACKAGEDELIMITER|配置条目“%1”的格式不正确，不是以包分隔符开头。 无 "\package" 分隔符。|  
|0xC0012019|-1073668071|DTS_E_CONFIGFORMATINVALID|配置条目“%1”的格式不正确， 可能是缺少分隔符或格式有误，如数组分隔符无效。|  
|0xC001201B|-1073668069|DTS_E_CONFIGFILEFAILEDEXPORT|导出配置文件时出错。|  
|0xC0012021|-1073668063|DTS_E_PROPERTIESCOLLECTIONREADONLY|无法修改 Properties 集合。|  
|0xC0012022|-1073668062|DTS_E_DTRXMLSAVEFAILURE|无法保存配置文件。 该文件可能是只读的。|  
|0xC0012023|-1073668061|DTS_E_FAILPACKAGEONFAILURENA|FailPackageOnFailure 属性不适用于包容器。|  
|0xC0012024|-1073668060|DTS_E_TASKPRODUCTLEVEL|任务“%1”不能在安装的 Integration Services 的 %2 版本上运行。 它要求 %3 或更高版本。|  
|0xC0012029|-1073668055|DTS_E_UNABLETOSAVETOFILE|无法将 xml 保存到“%1”。 该文件可能是只读的。|  
|0xC0012037|-1073668041|DTS_E_CONFIGTYPECONVERSIONFAILED|无法转换包路径“%2”的配置“%1”中的类型。  如果无法将配置值从字符串转换为相应的目标类型，会出现这种情况。 请检查该配置值，确保可以将它转换为目标属性或变量所属的类型。|  
|0xC0012049|-1073668023|DTS_E_CONFIGFAILED|配置失败。 本消息是所有配置类型的通用警告。 在此之前应有更为详细的其他警告。|  
|0xC0012050|-1073668016|DTS_E_REMOTEPACKAGEVALIDATION|包未能通过 ExecutePackage 任务的验证。 无法运行包。|  
|0xC0013001|-1073663999|DTS_E_FAILTOCREATEMUTEX|无法创建互斥体“%1”，错误为 0x%2!8.8X!。|  
|0xC0013002|-1073663998|DTS_E_MUTEXOWNBYDIFFUSER|互斥体“%1”已经存在，由另一个用户拥有。|  
|0xC0013003|-1073663997|DTS_E_WAITFORMUTEXFAILED|无法获取互斥体“%1”，错误为 0x%2!8.8X!。|  
|0xC0013004|-1073663996|DTS_E_FAILTORELEASEMUTEX|无法释放互斥体“%1”，错误为 0x%2!8.8X!。|  
|0xC0014003|-1073659901|DTS_E_INVALIDTASKPOINTER|包装任务指针无效。 包装具有无效的任务指针。|  
|0xC0014004|-1073659900|DTS_E_ALREADYADDED|该可执行文件已添加到其他容器的 Executables 集合。 如果客户端试图将可执行文件添加到多个 Executables 集合，会出现这种情况。 在尝试添加可执行文件前，需要将其从当前 Executables 集合中删除。|  
|0xC0014005|-1073659899|DTS_E_UNKNOWNCONNECTIONMANAGERTYPE|为连接管理器“%2”指定的连接类型“%1”未被识别为有效的连接管理器类型。 当试图创建未知连接类型的连接管理器时会返回此错误。 请检查连接类型名称的拼写是否正确。|  
|0xC0014006|-1073659898|DTS_E_COLLECTIONCOULDNTADD|创建了一个对象，但将其添加到集合的尝试失败。 内存不足可导致这种情况。|  
|0xC0014007|-1073659897|DTS_E_ODBCERRORENV|创建开放式数据库连接(ODBC)环境时出错。|  
|0xC0014008|-1073659896|DTS_E_ODBCERRORDBC|创建开放式数据库连接(ODBC)数据库连接时出错。|  
|0xC0014009|-1073659895|DTS_E_ODBCERRORCONNECT|试图与数据库服务器建立开放式数据库连接(ODBC)连接时出错。|  
|0xC001400A|-1073659894|DTS_E_CONNECTIONMANAGERQUALIFIERALREADYSET|已对此连接管理器实例设置了限定符。 每个实例只能设置一次限定符。|  
|0xC001400B|-1073659893|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSET|此连接管理器实例未设置限定符。 需要设置限定符才能完成初始化。|  
|0xC001400C|-1073659892|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSUPPORTED|此连接管理器不支持指定限定符。|  
|0xC001400D|-1073659891|DTS_E_CANNOTCLONECONNECTIONMANAGER|不能克隆连接管理器“0x%1”以用于进程外执行。|  
|0xC001400E|-1073659890|DTS_E_NOSQLPROFILERDLL|SQL Server Profiler 的日志提供程序无法加载 pfclnt.dll。 请检查是否安装了 SQL Server Profiler。|  
|0xC001400F|-1073659889|DTS_E_LOGFAILED|SSIS 日志记录基础结构出错，错误代码为 0x%1!8.8X!。 此错误指示该日志记录错误不是由特定的日志提供程序引起的。|  
|0xC0014010|-1073659888|DTS_E_LOGPROVIDERFAILED|SSIS 日志记录提供程序“%1”出错，错误代码为 0x%2!8.8X! (%3)。  这指示该日志记录错误是由特定的日志提供程序引起的。|  
|0xC0014011|-1073659887|DTS_E_SAVETOSQLSERVER_OLEDB|SaveToSQLServer 方法遇到了 OLE DB 错误代码 0x%1!8.8X! (%2)。  发出的 SQL 语句已失败。|  
|0xC0014012|-1073659886|DTS_E_LOADFROMSQLSERVER_OLEDB|LoadFromSQLServer 方法遇到了 OLE DB 错误代码 0x%1!8.8X! (%2)。  发出的 SQL 语句已失败。|  
|0xC0014013|-1073659885|DTS_E_REMOVEFROMSQLSERVER_OLEDB|RemoveFromSQLServer 方法遇到了 OLE DB 错误代码 0x%1!8.8X! (%2)。发出的 SQL 语句已失败。|  
|0xC0014014|-1073659884|DTS_E_EXISTSONSQLSERVER_OLEDB|ExistsOnSQLServer 方法遇到了 OLE DB 错误代码 0x%1!8.8X! (%2)。 发出的 SQL 语句已失败。|  
|0xC0014015|-1073659883|DTS_E_CONNECTIONSTRING|OLE DB 在使用提供的连接字符串连接数据库时失败。|  
|0xC0014016|-1073659882|DTS_E_FROMEXECISNOTCHILD|在添加优先约束时，指定的来源可执行文件不是此容器的子级。|  
|0xC0014017|-1073659881|DTS_E_TOEXECISNOTCHILD|在添加优先约束时，指定的目标可执行文件不是此容器的子级。|  
|0xC0014018|-1073659880|DTS_E_ODBCTRANSACTIONENLIST|试图在事务中登记 ODBC 连接时出错。 SQLSetConnectAttr 无法设置 SQL_ATTR_ENLIST_IN_DTC 属性。|  
|0xC0014019|-1073659879|DTS_E_CONNECTIONOFFLINE|由于包的 OfflineMode 属性为 TRUE，连接管理器“%1”将不获取连接。 当 OfflineMode 为 TRUE 时，无法获取连接。|  
|0xC001401A|-1073659878|DTS_E_BEGINTRANSACTION|SSIS 运行时无法启动分布式事务，由于错误 0x%1!8.8X! “%2”。 DTC 事务无法启动。 原因可能是 MSDTC 服务未运行。|  
|0xC001401B|-1073659877|DTS_E_SETQUALIFIERDESIGNTIMEONLY|包执行期间无法对连接管理器调用 SetQualifier 方法。 此方法仅在设计时使用。|  
|0xC001401C|-1073659876|DTS_E_SQLPERSISTENCEVERSION|在 SQL Server 中存储或修改包要求 SSIS 运行时和数据库为同一版本。 在早期版本中不支持包存储功能。|  
|0xC001401D|-1073659875|DTS_E_CONNECTIONVALIDATIONFAILED|连接“%1”验证失败。|  
|0xC001401E|-1073659874|DTS_E_INVALIDFILENAMEINCONNECTION|连接中指定的文件名“%1”无效。|  
|0xC001401F|-1073659873|DTS_E_MULTIPLEFILESONRETAINEDCONNECTION|当 Retain 属性为 TRUE 时，连接中不能指定多个文件名。 在连接字符串中发现了竖线，这表明指定了多个文件名，另外 Retain 属性为 TRUE。|  
|0xC0014020|-1073659872|DTS_E_ODBCERROR|发生了 ODBC 错误 %1!d! 。|  
|0xC0014021|-1073659871|DTS_E_PRECEDENCECONSTRAINT|“%1”和“%2”之间的优先约束中存在错误。|  
|0xC0014022|-1073659870|DTS_E_FAILEDPOPNATIVEFEE|无法用本机 ForEachEnumerators 填充 ForEachEnumeratorInfos 集合，错误代码为: %1。|  
|0xC0014023|-1073659869|DTS_E_GETENUMERATOR|ForEach 枚举器的 GetEnumerator 方法失败，错误为 0x%1!8.8X! “%2”。 当 ForEach 枚举器无法执行枚举操作时，会出现这种情况。|  
|0xC0014024|-1073659868|DTS_E_CANTGETCERTDATA|无法从提供的证书对象获取原始证书数据(错误: %1)。 当 CPackage::put_CertificateObject 无法实例化 ManagedHelper 对象时，或者当 ManagedHelper 对象失败时，或者当 ManagedHelper 对象返回格式不正确的数组时，会发生这种情况。|  
|0xC0014025|-1073659867|DTS_E_CANTCREATECERTCONTEXT|无法创建证书上下文(错误: %1)。 当相应的 CryptoAPI 函数失败时，CPackage::put_CertificateObject 或 CPackage::LoadFromXML 中会出现这种情况。|  
|0xC0014026|-1073659866|DTS_E_CANTOPENCERTSTORE|打开 MY 证书存储区失败，错误为“%1”。此错误出现在 CPackage::LoadUserCertificateByName 和 CPackage::LoadUserCertificateByHash 中。|  
|0xC0014027|-1073659865|DTS_E_CANTFINDCERTBYNAME|在 MY 存储区中找不到指定名称的证书(错误: %1)。 此错误出现在 CPackage::LoadUserCertificateByName 中。|  
|0xC0014028|-1073659864|DTS_E_CANTFINDCERTBYHASH|在“MY”存储区中找不到具有指定哈希的证书(错误: %1)。 此错误出现在 CPackage::LoadUserCertificateByHash 中。|  
|0xC0014029|-1073659863|DTS_E_INVALIDCERTHASHFORMAT|该哈希值不是一维字节数组(错误: %1)。 此错误出现在 CPackage::LoadUserCertificateByHash 中。|  
|0xC001402A|-1073659862|DTS_E_CANTACCESSARRAYDATA|无法访问数组中的数据(错误: %1)。 调用 GetDataFromSafeArray 时可能出现此错误。|  
|0xC001402B|-1073659861|DTS_E_CREATEMANAGEDHELPERFAILED|SSIS 托管帮助器对象在创建时失败，错误为 0x%1!8.8X! “%2”。 只要 CoCreateInstance CLSID_DTSManagedHelper 失败，就会出现这种情况。|  
|0xC001402C|-1073659860|DTS_E_OLEDBTRANSACTIONENLIST|SSIS 运行时未能在分布式事务中登记 OLE DB 连接，错误为 0x%1!8.8X! “%2”。|  
|0xC001402D|-1073659859|DTS_E_SIGNPACKAGEFAILED|包签名失败，错误为 0x%1!8.8X! “%2”。 当 ManagedHelper.SignDocument 方法失败时，会出现这种情况。|  
|0xC001402E|-1073659858|DTS_E_CHECKENVELOPEFAILED|无法检查包 XML 中的 XML 签名信封，错误为 0x%1!8.8X! “%2”。 此错误出现在 CPackage::LoadFromXML 中。|  
|0xC001402F|-1073659857|DTS_E_GETXMLSOURCEFAILED|无法从 XML DOM 对象获取 XML 源，错误为 0x%1!8.8X! “%2”。 当 IXMLDOMDocument::get_xml 失败时，会出现这种情况。|  
|0xC0014030|-1073659856|DTS_E_PACKAGEVERIFICATIONFAILED|包的加密签名未通过验证由于以下错误未通过验证：0x%1!8.8X “%2”。 当签名验证操作失败时，会出现这种情况。|  
|0xC0014031|-1073659855|DTS_E_GETKEYFROMCERTFAILED|无法获取与指定证书相关联的加密密钥对，错误为 0x%1!8.8X! “%2”。 请确保您具有与发布的证书相关联的密钥对。 如果用户试图使用证书对文档签名，但没有该证书的私钥，通常会出现此错误。|  
|0xC0014032|-1073659854|DTS_E_INVALIDSIGNATURE|数字签名无效。 包的内容已修改。|  
|0xC0014033|-1073659853|DTS_E_UNTRUSTEDSIGNATURE|数字签名有效，但签名人不可信，因此无法保证真实性。|  
|0xC0014034|-1073659852|DTS_E_TRANSACTIONENLISTNOTSUPPORTED|该连接不支持在分布式事务中登记。|  
|0xC0014035|-1073659851|DTS_E_PACKAGEPROTECT|无法应用包保护，错误为 0x%1!8.8X! “%2”。 保存到 Xml 时会出现此错误。|  
|0xC0014036|-1073659850|DTS_E_PACKAGEUNPROTECT|无法删除包保护，错误为 0x%1!8.8X! “%2”。 此错误出现在 CPackage::LoadFromXML 方法中。|  
|0xC0014037|-1073659849|DTS_E_PACKAGEPASSWORD|此包已用密码加密。 未指定密码，或密码不正确。|  
|0xC0014038|-1073659848|DTS_E_DUPLICATECONSTRAINT|在指定的可执行文件之间已存在优先约束。 不允许有多个优先约束。|  
|0xC0014039|-1073659847|DTS_E_PACKAGELOADFAILED|由于错误 0x%1!8.8X!，无法加载包 “%2”。 当 CPackage::LoadFromXML 失败时，会出现这种情况。|  
|0xC001403A|-1073659846|DTS_E_PACKAGEOBJECTNOTENVELOPED|在已签名的 XML 信封中找不到包对象，错误为 0x%1!8.8X! “%2”。 当已签名的 XML 应包含 SSIS 包却未包含时，会出现这种情况。|  
|0xC001403B|-1073659845|DTS_E_JAGGEDEVENTINFO|参数名称、类型和说明数组的长度不相等。 这些长度必须相等。 数组的长度不匹配时会出现这种情况。 在每个数组中，每个参数应有一项。|  
|0xC001403C|-1073659844|DTS_E_GETPACKAGEINFOS|枚举包时出现 OLE DB 错误 0x%1!8.8X! (%2)。 已发出一条 SQL 语句，但已失败。|  
|0xC001403D|-1073659843|DTS_E_UNKNOWNLOGPROVIDERTYPE|为日志提供程序“%2”指定的日志提供程序类型“%1”未被识别为有效的日志提供程序类型。 当试图创建未知类型的日志提供程序时会出现此错误。 请检查日志提供程序类型名称的拼写是否正确。|  
|0xC001403E|-1073659842|DTS_E_UNKNOWNLOGPROVIDERTYPENOSUBS|日志提供程序类型未被识别为有效的日志提供程序类型。 当试图创建未知类型的日志提供程序时会出现此错误。 请检查日志提供程序类型名称的拼写是否正确。|  
|0xC001403F|-1073659841|DTS_E_UNKNOWNCONNECTIONMANAGERTYPENOSUBS|为连接管理器指定的连接类型不是有效的连接管理器类型。 当试图创建未知连接类型的连接管理器时会出现此错误。 请检查连接类型名称的拼写是否正确。|  
|0xC0014040|-1073659840|DTS_E_PACKAGEREMOVEFAILED|试图从 SQL Server 删除包“%1”时出错。|  
|0xC0014042|-1073659838|DTS_E_FOLDERADDFAILED|试图在 SQL Server 的文件夹“%2”中创建名为“%1”的文件夹时出错。|  
|0xC0014043|-1073659837|DTS_E_CREATEFOLDERONSQLSERVER_OLEDB|CreateFolderOnSQLServer 方法遇到了 OLE DB 错误代码 0x%1!8.8X! (%2)。发出的 SQL 语句已失败。|  
|0xC0014044|-1073659836|DTS_E_FOLDERRENAMEFAILED|An error occurred when renaming folder " %1\\\\%2" to "%1\\\\%3" on SQL Server.|  
|0xC0014045|-1073659835|DTS_E_RENAMEFOLDERONSQLSERVER_OLEDB|The RenameFolderOnSQLServer method encountered OLE DB error code 0x%1!8.8X! (%2). The SQL statement issued has failed.|  
|0xC0014046|-1073659834|DTS_E_FOLDERDELETEFAILED|Error deleting SQL Server folder "%1".|  
|0xC0014047|-1073659833|DTS_E_REMOVEFOLDERFROMSQLSERVER_OLEDB|The RemoveFolderOnSQLServer method encountered OLE DB error code 0x%1!8.8X! (%2). The SQL statement issued has failed.|  
|0xC0014048|-1073659832|DTS_E_INVALIDPATHTOPACKAGE|The specified package path does not contain a package name. This occurs when the path does not contain at least one backslash or one forward slash.|  
|0xC0014049|-1073659831|DTS_E_FOLDERNOTFOUND|Cannot find folder "%1".|  
|0xC001404A|-1073659830|DTS_E_FINDFOLDERONSQLSERVER_OLEDB|While trying to find a folder on SQL an OLE DB error was encountered with error code 0x%1!8.8X! (%2).|  
|0xC001404B|-1073659829|DTS_E_OPENLOGFAILED|The SSIS logging provider has failed to open the log. Error code: 0x%1!8.8X!.|  
|0xC001404C|-1073659828|DTS_E_GETCONNECTIONINFOS|Failed to get ConnectionInfos collection with error 0x%1!8.8X! "%2". This error occurs when the call to IDTSApplication100::get_ConnectionInfos fails.|  
|0xC001404D|-1073659827|DTS_E_VARIABLEDEADLOCK|Deadlock detected while trying to lock variables. The locks cannot be acquired after 16 attempts. The locks timed out.|  
|0xC001404E|-1073659826|DTS_E_NOTDISPENSED|The Variables collection has not been returned from the VariableDispenser. An operation was attempted that is only allowed on dispensed collections.|  
|0xC001404F|-1073659825|DTS_E_VARIABLESALREADYUNLOCKED|This Variables collection has already been unlocked. The Unlock method is called only once on a dispensed Variables collection.|  
|0xC0014050|-1073659824|DTS_E_VARIABLEUNLOCKFAILED|One or more variables failed to unlock.|  
|0xC0014051|-1073659823|DTS_E_DISPENSEDREADONLY|The Variables collection was returned the from VariableDispenser and cannot be modified. Items cannot be added to or removed from dispensed collections.|  
|0xC0014052|-1073659822|DTS_E_VARIABLEALREADYONREADLIST|The variable "%1" is already on the read list. A variable may only be added once to either the read lock list or the write lock list.|  
|0xC0014053|-1073659821|DTS_E_VARIABLEALREADYONWRITELIST|The variable "%1" is already on the write list. A variable may only be added once to either the read lock list or the write lock list.|  
|0xC0014054|-1073659820|DTS_E_LOCKVARIABLEFORREAD|Failed to lock variable "%1" for read access with error 0x%2!8.8X! "%3".|  
|0xC0014055|-1073659819|DTS_E_LOCKVARIABLEFORWRITE|Failed to lock variable "%1" for read/write access with error 0x%2!8.8X! "%3".|  
|0xC0014056|-1073659818|DTS_E_CUSTOMEVENTCONFLICT|The custom event "%1" is already declared with a different parameter list. A task is trying to declare a custom event, which another task has already declared with a different parameter list.|  
|0xC0014057|-1073659817|DTS_E_EVENTHANDLERNOTALLOWED|The task providing the custom event "%1" does not allow this event to be handled in the package. The custom event was declared with AllowEventHandlers = FALSE.|  
|0xC0014059|-1073659815|DTS_E_UNSAFEVARIABLESALREADYSET|The VariableDispenser received an unsafe Variables collection. This operation cannot be repeated.|  
|0xC001405A|-1073659814|DTS_E_INVALIDPARENTPACKAGEPATH|GetPackagePath was called on the ForEachEnumerator but there was no ForEachLoop package path specified.|  
|0xC001405B|-1073659813|DTS_E_VARIABLEDEADLOCK_READ|A deadlock was detected while trying to lock variable "%1" for read access. A lock could not be acquired after 16 attempts and timed out.|  
|0xC001405C|-1073659812|DTS_E_VARIABLEDEADLOCK_READWRITE|A deadlock was detected while trying to lock variables "%1" for read/write access. A lock cannot be acquired after 16 attempts. The locks timed out.|  
|0xC001405D|-1073659811|DTS_E_VARIABLEDEADLOCK_BOTH|A deadlock was detected while trying to lock variables "%1" for read access and variables "%2" for read/write access. A lock cannot be acquired after 16 attempts. The locks timed out.|  
|0xC001405E|-1073659810|DTS_E_PACKAGEPASSWORDEMPTY|The protection level of the package requires a password, but PackagePassword property is empty.|  
|0xC001405F|-1073659809|DTS_E_DECRYPTXML_PASSWORD|Failed to decrypt an encrypted XML node because the password was not specified or not correct. Package load will attempt to continue without the encrypted information.|  
|0xC0014060|-1073659808|DTS_E_DECRYPTPACKAGE_USERKEY|Failed to decrypt a package that is encrypted with a user key. You may not be the user who encrypted this package, or you are not using the same machine that was used to save the package.|  
|0xC0014061|-1073659807|DTS_E_SERVERSTORAGEDISALLOWED|The protection level, ServerStorage, cannot be used when saving to this destination. The system could not verify that the destination supports secure storage capability.|  
|0xC0014062|-1073659806|DTS_E_LOADFROMSQLSERVER|LoadFromSQLServer method has failed.|  
|0xC0014063|-1073659805|DTS_E_SIGNATUREPOLICYVIOLATION|The package cannot be loaded because the state of the digital signature violates signature policy. Error 0x%1!8.8X! "%2"|  
|0xC0014064|-1073659804|DTS_E_SIGNATURENOTPRESENT|The package is not signed.|  
|0xC0014065|-1073659803|DTS_E_SQLPROFILERDLL_ONLY_X86|The log provider for SQL Server Profiler was unable to load pfclnt.dll because it is only supported on 32-bit systems.|  
|0xC0014100|-1073659648|DTS_E_NAMEALREADYADDED|The object cannot be added because another object with the same name already exists in the collection. Use a different name to resolve this error.|  
|0xC0014101|-1073659647|DTS_E_NAMEALREADYEXISTS|The object name cannot be changed from "%1" to "%2" because another object in the collection already uses that name. Use a different name to resolve this error.|  
|0xC0014103|-1073659645|DTS_E_FAILEDDEPENDENCIES|There was an error enumerating the package dependencies. Check other messages for more information.|  
|0xC0014104|-1073659644|DTS_E_INVALIDCHECKPOINT_TRANSACTION|The current package settings are not supported.  Please change the SaveCheckpoints property or the TransactionOption property.|  
|0xC001410E|-1073659634|DTS_E_CONNECTIONMANAGERJOINTRANSACTION|The connection manager failed to defect from the transaction.|  
|0xC0015001|-1073655807|DTS_E_BPDUPLICATE|The specified breakpoint ID already exists. This error occurs when a task calls CreateBreakpoint with the same ID multiple times. It is possible to create a breakpoint with the same ID multiple times if the task calls RemoveBreakpoint on the first creation before creating the second one.|  
|0xC0015002|-1073655806|DTS_E_BPUNKNOWNID|The specified breakpoint ID does not exist. This error occurs when a task references a breakpoint that does not exist.|  
|0xC0015004|-1073655804|DTS_E_CANTWRITETOFILE|The file, "%1", could not be opened for writing. The file could be read-only, or you do not have the correct permissions.|  
|0xC0015005|-1073655803|DTS_E_NOROWSETRETURNED|No result rowset is associated with the execution of this query. The result is not correctly specified.|  
|0xC0015105|-1073655547|DTS_E_DUMP_FAILED|Debug dump files were not generated correctly. The hresult is 0x%1!8.8X!.|  
|0xC0016001|-1073651711|DTS_E_INVALIDURL|The URL specified is not valid. This can happen when the server or proxy URL is null, or in an incorrect format. A valid URL format is in the form of https://ServerName:Port/ResourcePath or https://ServerName:Port/ResourcePath.|  
|0xC0016002|-1073651710|DTS_E_INVALIDSCHEME|The URL %1 is not valid. This can happen when a scheme other than http or https is specified, or the URL is in an incorrect format. A valid URL format is in the form of https://ServerName:Port/ResourcePath or https://ServerName:Port/ResourcePath.|  
|0xC0016003|-1073651709|DTS_E_WINHTTPCANNOTCONNECT|Connection to server %1 cannot be established. This error can occur when the server does not exist, or the proxy settings are incorrect.|  
|0xC0016004|-1073651708|DTS_E_CONNECTIONTERMINATED|The connection with the server has been reset or terminated. Try again later.|  
|0xC0016005|-1073651707|DTS_E_LOGINFAILURE|The login attempt failed for "%1". This error occurs when the login credentials provided are incorrect. Verify the login credentials.|  
|0xC0016006|-1073651706|DTS_E_INVALIDSERVERNAME|The server name specified in the URL %1 cannot be resolved.|  
|0xC0016007|-1073651705|DTS_E_PROXYAUTH|Proxy authentication failed. This error occurs when login credentials are not provided, or the credentials are incorrect.|  
|0xC0016008|-1073651704|DTS_E_SECUREFAILURE|SSL certificate response obtained from the server was not valid. Cannot process the request.|  
|0xC0016009|-1073651703|DTS_E_TIMEOUT|The request has timed out. This error can occur when the timeout specified was too short, or a connection to the server or proxy cannot be established. Ensure that the server and proxy URL are correct.|  
|0xC001600A|-1073651702|DTS_E_CLIENTAUTH|Client certificate is missing. This error occurs when the server is expecting an SSL client certificate and the user has provided an invalid certificate, or has not provided a certificate. A client certificate must be configured for this connection.|  
|0xC001600B|-1073651701|DTS_E_REDIRECTFAILURE|The specified server, URL %1, has a redirect and the redirect request failed.|  
|0xC001600C|-1073651700|DTS_E_SERVERAUTH|Server authentication failed. This error occurs when login credentials are not provided, or the credentials are incorrect.|  
|0xC001600D|-1073651699|DTS_E_WINHTTPUNKNOWNERROR|Request cannot be processed. Try again later.|  
|0xC001600E|-1073651698|DTS_E_UNKNOWNSTATUSCODE|Server returned status code - %1!u! : %2. This error occurs when the server is experiencing problems.|  
|0xC001600F|-1073651697|DTS_E_WINHTTPNOTSUPPORTED|This platform is not supported by WinHttp services.|  
|0xC0016010|-1073651696|DTS_E_INVALIDTIMEOUT|Timeout value is not valid. Timeout should be in the range of %1!d! to %2!d! (in seconds).|  
|0xC0016011|-1073651695|DTS_E_INVALIDCHUNKSIZE|The chunk size is not valid. The ChunkSize property should be in the range of %1!d! to %2!d! (in KB).|  
|0xC0016012|-1073651694|DTS_E_CERTERROR|Error processing client certificate. This error can occur when the client certificate provided was not found in the Personal Certificate Store. Verify that the client certificate is valid.|  
|0xC0016013|-1073651693|DTS_E_FORBIDDEN|Server returned error code "403 - Forbidden". This error can occur when the specified resource needs "https" access, but the certificate validity period has expired, the certificate is not valid for the use requested, or the certificate has been revoked or revocation can not be checked.|  
|0xC0016014|-1073651692|DTS_E_WINHTTPOPEN|Error initializing HTTP session with proxy "%1". This error can occur when an invalid proxy was specified. HTTP connection manager only supports CERN-type proxies.|  
|0xC0016015|-1073651691|DTS_E_OPENCERTSTORE|Error opening certificate store.|  
|0xC0016016|-1073651690|DTS_E_UNPROTECTXMLFAILED|Failed to decrypt protected XML node "%1" with error 0x%2!8.8X! "%3". You may not be authorized to access this information. This error occurs when there is a cryptographic error. Verify that the correct key is available.|  
|0xC0016017|-1073651689|DTS_E_UNPROTECTCONNECTIONSTRINGFAILED|Failed to decrypt protected connection string for server "%1" with error 0x%2!8.8X! "%3". You may not be authorized to access this information. This error occurs when there is a cryptographic error. Verify that the correct key is available.|  
|0xC0016018|-1073651688|DTS_E_NEGATIVEVERSION|The version number cannot be negative. This error occurs when the VersionMajor, VersionMinor, or VersionBuild property of the package is set to a negative value.|  
|0xC0016019|-1073651687|DTS_E_PACKAGEMIGRATED|The package has been migrated to a later version during loading. It must be reloaded to complete the process. This is an internal error code.|  
|0xC0016020|-1073651680|DTS_E_PACKAGEMIGRATIONFAILED|Package migration from version %1!d! to version %2!d! failed with error 0x%3!8.8X! "%4".|  
|0xC0016021|-1073651679|DTS_E_PACKAGEMIGRATIONMODULELOAD|Package migration module has failed to load.|  
|0xC0016022|-1073651678|DTS_E_PACKAGEMIGRATIONMODULE|Package migration module has failed.|  
|0xC0016023|-1073651677|DTS_E_CANTDETERMINEWHICHPROPTOPERSIST|Unable to persist object using default persistence. This error occurs when the default persistence is unable to determine which objects are on the hosted object.|  
|0xC0016024|-1073651676|DTS_E_CANTADDREMOVEWHENEXECUTING|Cannot add or remove an element from a package in runtime mode. This error occurs when an attempt is made to add or remove an object from a collection while the package is executing.|  
|0xC0016025|-1073651675|DTS_E_NODENOTFOUND|The "%1" node cannot be found in custom default persistence. This error occurs if the default saved XML of an extensible object was changed in a way that a saved object is no longer found, or if the extensible object itself changed.|  
|0xC0016026|-1073651674|DTS_E_COLLECTIONLOCKED|This collection cannot be modified during package validation or execution.|  
|0xC0016027|-1073651673|DTS_E_COLLOCKED|The "%1" collection cannot be modified during package validation or execution. "%2" cannot be added to the collection.|  
|0xC0016029|-1073651671|DTS_E_FTPNOTCONNECTED|Connection with the FTP server has not been established.|  
|0xC001602A|-1073651670|DTS_E_FTPERROR|An error occurred in the requested FTP operation. Detailed error description: %1.|  
|0xC001602B|-1073651669|DTS_E_FTPINVALIDRETRIES|The number of retries is not valid. The number of retries should be between %1!d! and %2!d!.|  
|0xC001602C|-1073651668|DTS_E_LOADWININET|The FTP connection manager needs the following DLL to function: %1.|  
|0xC001602D|-1073651667|DTS_E_FTPINVALIDCONNECTIONSTRING|The port specified in the connection string is not valid. The ConnectionString format is ServerName:Port. Port should be an integer value between %1!d! and %2!d!.|  
|0xC001602E|-1073651666|DTS_E_FTPCREATEFOLDER|Creating folder "%1" ... %2.|  
|0xC001602F|-1073651665|DTS_E_FTPDELETEFOLDER|Deleting folder "%1" ... %2.|  
|0xC0016030|-1073651664|DTS_E_FTPCHANGEFOLDER|Changing current directory to "%1". %2.|  
|0xC0016031|-1073651663|DTS_E_FTPFILESEMPTY|No files to transfer. This error can occur when performing a Send or Receive operation and no files are specified for the transfer.|  
|0xC0016032|-1073651662|DTS_E_FTPINVALIDLOCALPATH|Specified local path is not valid. Specify a valid local path. This can occur when the specified local path is null.|  
|0xC0016033|-1073651661|DTS_E_FTPNOFILESTODELETE|No files specified to delete.|  
|0xC0016034|-1073651660|DTS_E_WINHTTPCERTDECODE|Internal error occurred while loading the certificate. This error could occur when the certificate data is invalid.|  
|0xC0016035|-1073651659|DTS_E_WINHTTPCERTENCODE|Internal error occurred while saving the certificate data.|  
|0xC0016049|-1073651639|DTS_E_CHECKPOINTMISMATCH|Checkpoint file "%1" does not match this package. The ID of the package and the ID in the checkpoint file do not match.|  
|0xC001604A|-1073651638|DTS_E_CHECKPOINTFILEALREADYEXISTS|An existing checkpoint file is found with contents that do not appear to be for this package, so the file cannot be overwritten to start saving new checkpoints. Remove the existing checkpoint file and try again. This error occurs when a checkpoint file exists, the package is set to not use a checkpoint file, but to save checkpoints. The existing checkpoint file will not be overwritten.|  
|0xC001604B|-1073651637|DTS_E_CHECKPOINTFILELOCKED|The checkpoint file "%1" is locked by another process. This may occur if another instance of this package is currently executing.|  
|0xC001604C|-1073651636|DTS_E_OPENCHECKPOINTFILE|Checkpoint file "%1" failed to open due to error 0x%2!8.8X! "%3".|  
|0xC001604D|-1073651635|DTS_E_CREATECHECKPOINTFILE|Checkpoint file "%1" failed during creation due to error 0x%2!8.8X! "%3".|  
|0xC0016050|-1073651632|DTS_E_FTPINVALIDPORT|The FTP Port contains an invalid value. The FTP Port value should be an integer between %1!d! and %2!d!.|  
|0xC00160AA|-1073651542|DTS_E_CONNECTTOSERVERFAILED|Connect to SSIS Service on machine "%1" failed:<br /><br /> %2.|  
|0xC0017002|-1073647614|DTS_E_PROPERTYEXPRESSIONSDISABLEDONVARIABLES|The Expression property is not supported on Variable objects. Use the EvaluateAsExpression property instead.|  
|0xC0017003|-1073647613|DTS_E_PROPERTYEXPRESSIONEVAL|The expression "%1" on property "%2" cannot be evaluated. Modify the expression to be valid.|  
|0xC0017004|-1073647612|DTS_E_PROPERTYEXPRESSIONSET|The result of the expression "%1" on property "%2" cannot be written to the property. The expression was evaluated, but cannot be set on the property.|  
|0xC0017005|-1073647611|DTS_E_FORLOOPEVALEXPRESSIONINVALID|The evaluation expression for the loop is not valid. The expression needs to be modified. There should be additional error messages.|  
|0xC0017006|-1073647610|DTS_E_EXPRESSIONNOTBOOLEAN|The expression "%1" must evaluate to True or False. Change the expression to evaluate to a Boolean value.|  
|0xC0017007|-1073647609|DTS_E_FORLOOPHASNOEXPRESSION|There is no expression for the loop to evaluate. This error occurs when the expression on the For Loop is empty. Add an expression.|  
|0xC0017008|-1073647608|DTS_E_FORLOOPASSIGNEXPRESSIONINVALID|The assignment expression for the loop is not valid and needs to be modified. There should be additional error messages.|  
|0xC0017009|-1073647607|DTS_E_FORLOOPINITEXPRESSIONINVALID|The initialization expression for the loop is not valid and needs to be modified. There should be additional error messages.|  
|0xC001700A|-1073647606|DTS_E_INVALIDVERSIONNUMBER|The version number in the package is not valid. The version number cannot be greater than current version number.|  
|0xC001700C|-1073647604|DTS_E_INVALIDVERNUMCANTBENEGATIVE|The version number in the package is not valid. The version number is negative.|  
|0xC001700D|-1073647603|DTS_E_PACKAGEUPDATEDISABLED|The package has an older format version, but automatic package format upgrading is disabled.|  
|0xC001700E|-1073647602|DTS_E_EXPREVALTRUNCATIONASERROR|A truncation occurred during evaluation of the expression.|  
|0xC0019001|-1073639423|DTS_E_FAILEDSETEXECVALVARIABLE|The wrapper was unable to set the value of the variable specified in the ExecutionValueVariable property.|  
|0xC0019004|-1073639420|DTS_E_VARIABLEEXPRESSIONERROR|The expression for variable "%1" failed evaluation. There was an error in the expression.|  
|0xC0019305|-1073638651|DTS_E_UNSUPPORTEDSQLVERSION|The attempted operation is not supported with this database version.|  
|0xC001A003|-1073635325|DTS_E_TXNSPECINVALID|Transaction cannot be specified when a retained connection is used. This error occurs when Retain is set to TRUE on the connection manager, but AcquireConnection was called with a non-null transaction parameter.|  
|0xC001A004|-1073635324|DTS_E_INCOMPATIBLETRANSACTIONCONTEXT|Incompatible transaction context was specified for a retained connection. This connection has been established under a different transaction context. Retained connections can be used under exactly one transaction context.|  
|0xC001B001|-1073631231|DTS_E_NOTSUSPENDED|Resume call failed because the package is not suspended. This occurs when the client calls resume, but the package is not suspended.|  
|0xC001B002|-1073631230|DTS_E_ALREADYEXECUTING|Execute call failed because the executable is already executing. This error occurs when the client calls Execute on a container that is still executing from the last Execute call.|  
|0xC001B003|-1073631229|DTS_E_NOTEXECUTING|Suspend or Resume call failed because the executable is not executing, or is not the top-level executable. This occurs when the client calls Suspend or Resume on an executable that is not currently processing an Execute call.|  
|0xC001C002|-1073627134|DTS_E_INVALIDFILE|The file specified in the For Each File enumerator is not valid. Check that the file specified in the For Each File enumerator exists.|  
|0xC001C010|-1073627120|DTS_E_VALUEINDEXNOTINTEGER|The value index is not an integer . Mapping a For Each Variable number %1!d! to the variable "%2".|  
|0xC001C011|-1073627119|DTS_E_VALUEINDEXNEGATIVE|The value index is negative. The ForEach Variable Mapping number %1!d! to variable "%2".|  
|0xC001C012|-1073627118|DTS_E_FOREACHVARIABLEMAPPING|ForEach Variable Mapping number %1!d! to variable "%2" cannot be applied.|  
|0xC001C013|-1073627117|DTS_E_OBJECTNOTINFOREACHLOOP|Failure when adding an object to a ForEachPropertyMapping that is not a direct child of the ForEachLoop container.|  
|0xC001F001|-1073614847|DTS_E_FAILEDSYSTEMVARIABLEREMOVE|Failed to remove a system variable. This error occurs when removing a variable that is a required variable.  Required variables are variables that are created by the runtime for communicating between tasks and the runtime.|  
|0xC001F002|-1073614846|DTS_E_CHANGESYSTEMVARIABLEREADONLYFAILED|Changing the property of a variable failed because it is a system variable. System variables are read-only.|  
|0xC001F003|-1073614845|DTS_E_CHANGESYSTEMVARIABLENAMEFAILED|Changing the name of a variable failed because it is a system variable. System variables are read-only.|  
|0xC001F004|-1073614844|DTS_E_CHANGESYSTEMVARIABLENAMESPACEFAILED|Changing the namespace of a variable failed because it is a system variable. System variables are read-only.|  
|0xC001F006|-1073614842|DTS_E_EVENTHANDLERNAMEREADONLY|Changing the event handler name failed. Event handler names are read-only.|  
|0xC001F008|-1073614840|DTS_E_PATHUNKNOWN|Cannot retrieve path to object. This is a system error.|  
|0xC001F009|-1073614839|DTS_E_RUNTIMEVARIABLETYPECHANGE|The type of the value being assigned to variable "%1" differs from the current variable type. Variables may not change type during execution. Variable types are strict, except for variables of type Object.|  
|0xC001F010|-1073614832|DTS_E_INVALIDSTRING|Invalid characters in string: "%1". This occurs when a string supplied for a property value contains unprintable characters.|  
|0xC001F011|-1073614831|DTS_E_INVALIDOBJECTNAME|SSIS object name is invalid. More specific errors would have been raised explaining the exact naming problem.|  
|0xC001F021|-1073614815|DTS_E_PROPERTYREADONLY|The property "%1" is read only. This occurs when a change to a read-only property is attempted.|  
|0xC001F022|-1073614814|DTS_E_FAILEDGETTYPEINFO|The object does not support type information. This occurs when the runtime attempts to get the type information from an object to populate the Properties collection.  The object must support type information.|  
|0xC001F023|-1073614813|DTS_E_FAILEDPROPERTYGET|An error occurred while retrieving the value of property "%1". The error code is 0x%2!8.8X!.|  
|0xC001F024|-1073614812|DTS_E_FAILEDPROPERTYGET_ERRORINFO|An error occurred while retrieving the value of property "%1". The error code is 0x%2!8.8X! "%3".|  
|0xC001F025|-1073614811|DTS_E_FAILEDPROPERTYSET|An error occurred while setting the value of property "%1". The error returned is 0x%2!8.8X!.|  
|0xC001F026|-1073614810|DTS_E_FAILEDPROPERTYSET_ERRORINFO|An error occurred while setting the value of property "%1". The error returned is 0x%2!8.8X! "%3".|  
|0xC001F027|-1073614809|DTS_E_PROPERTYWRITEONLY|The property "%1" is write-only. This error occurs when trying to retrieve the value of a property through a property object, but the property is write-only.|  
|0xC001F028|-1073614808|DTS_E_NODISPATCH|The object does not implement IDispatch. This error occurs when a property object or properties collection attempts to access an IDispatch interface on an object.|  
|0xC001F029|-1073614807|DTS_E_NOCONTAININGTYPELIB|Unable to retrieve the type library of the object. This error occurs when the Properties collection attempts to retrieve the type library for an object through its IDispatch interface.|  
|0xC001F02A|-1073614806|DTS_E_INVALIDTASKMONIKER|Cannot create a task from XML for task "%1!s!", type "%2!s!" due to error 0x%3!8.8X! "%4!s!".|  
|0xC001F02C|-1073614804|DTS_E_FAILEDCREATEXMLDOCUMENT|Failed to create an XML document "%1".|  
|0xC001F02D|-1073614803|DTS_E_PMVARPROPTYPESDIFFERENT|An error occurred because there is a property mapping from a variable to a property with a different type. The property type must match the variable type.|  
|0xC001F02E|-1073614802|DTS_E_PMINVALIDPROPMAPTARGET|Attempted to set property mapping to target unsupported object type. This error occurs when passing an unsupported object type to a property mapping.|  
|0xC001F02F|-1073614801|DTS_E_COULDNOTRESOLVEPACKAGEPATH|Cannot resolve a package path to an object in the package "%1".  Verify that the package path is valid.|  
|0xC001F030|-1073614800|DTS_E_PMNODESTPROPERTY|The destination property for the property map is empty. Set the destination property name.|  
|0xC001F031|-1073614799|DTS_E_INVALIDPROPERTYMAPPINGSFOUND|The package failed to restore at least one property mapping.|  
|0xC001F032|-1073614798|DTS_E_AMBIGUOUSVARIABLENAME|The variable name is ambiguous because multiple variables with this name exist in different namespaces. Specify namespace-qualified name to prevent ambiguity.|  
|0xC001F033|-1073614797|DTS_E_DESTINATIONOBJECTPARENTLESS|The destination object in a property mapping has no parent. The destination object is not a child of any sequence container. It may have been removed from the package.|  
|0xC001F036|-1073614794|DTS_E_INVALIDPROPERTYMAPPING|The property mapping is not valid. The mapping is ignored.|  
|0xC001F038|-1073614792|DTS_E_PMFAILALERTREMOVE|Failure when alerting property mappings that a target is being removed.|  
|0xC001F03A|-1073614790|DTS_E_INVALIDFOREACHPROPERTYMAPPING|An invalid property mapping is found on the For Each Loop. This occurs when the ForEach property mapping fails to restore.|  
|0xC001F040|-1073614784|DTS_E_PMPROPERTYINVALID|A destination property was specified on a property mapping that is invalid. This occurs when a property is specified on a destination object that in not found on that object.|  
|0xC001F041|-1073614783|DTS_E_INVALIDTASKMONIKERNOPARAM|Cannot create a task from XML. This occurs when the runtime is unable to resolve the name to create a task. Verify that the name is correct.|  
|0xC001F080|-1073614720|DTS_E_COULDNOTREPLACECHECKPOINTFILE|Cannot replace the existing checkpoint file with the updated checkpoint file. The checkpoint was successfully created in a temporary file, but overwriting the existing file with the new file failed.|  
|0xC001F081|-1073614719|DTS_E_CHECKPOINTFILENOTSPECIFIED|The package is configured to always restart from a checkpoint, but checkpoint file is not specified.|  
|0xC001F082|-1073614718|DTS_E_CHECKPOINTLOADXML|The attempt to load the XML checkpoint file "%1" failed with error 0x%2!8.8X! "%3". Check that the file name specified is correct, and that the file exists.|  
|0xC001F083|-1073614717|DTS_E_LOADCHECKPOINT|The package failed during execution because the checkpoint file cannot be loaded. Further execution of the package requires a checkpoint file. This error usually occurs when the CheckpointUsage property is set to ALWAYS, which specifies that the package always restarts.|  
|0xC001F185|-1073614459|DTS_E_NOEVALEXPRESSION|The evaluation condition expression on the For Loop "%1" is empty. There must be a Boolean evaluation expression in the For Loop.|  
|0xC001F186|-1073614458|DTS_E_EXPREVALASSIGNMENTTYPEMISMATCH|The result of the assignment expression "%1" cannot be converted to a type that is compatible with the variable that it was assigned to.|  
|0xC001F187|-1073614457|DTS_E_EXPREVALASSIGNMENTTOREADONLYVARIABLE|Error using a read-only variable "%1" in an assignment expression. The expression result cannot be assigned to the variable because the variable is read only. Choose a variable that can be written to, or remove the expression from this variable.|  
|0xC001F188|-1073614456|DTS_E_EXPREVALASSIGNMENTVARIABLELOCKFORWRITEFAILED|Cannot evaluate expression "%1" because the variable "%2" does not exist or cannot be accessed for writing. The expression result cannot be assigned to the variable because the variable was not found, or could not be locked for write access.|  
|0xC001F189|-1073614455|DTS_E_EXPREVALRESULTTYPENOTSUPPORTED|The expression "%1" has a result type of "%2", which cannot be converted to a supported type.|  
|0xC001F18A|-1073614454|DTS_E_EXPREVALRESULTTYPECONVERSIONFAILED|The conversion of the result of the expression"%1" from type "%2" to a supported type failed with error code 0x%3!8.8X!. An unexpected error occurred when trying to convert the expression result to a type supported by the runtime engine, even though the type conversion is supported.|  
|0xC001F200|-1073614336|DTS_E_DTSNAME_NOTNULL|The object name is not valid. The name cannot be set to NULL.|  
|0xC001F201|-1073614335|DTS_E_DTSNAME_NOTEMPTY|The object name is not valid. The name cannot be empty.|  
|0xC001F202|-1073614334|DTS_E_DTSNAME_LEGAL|The object name "%1" is not valid. The name cannot contain any of the following characters: / \ : [ ] . =|  
|0xC001F203|-1073614333|DTS_E_DTSNAME_PRINTABLE|Object name "%1" is not valid. The name cannot contain control characters that render it unprintable.|  
|0xC001F204|-1073614332|DTS_E_DTSNAME_NOLEADWHITESP|Object name "%1" is not valid. Name cannot begin with a whitespace.|  
|0xC001F205|-1073614331|DTS_E_DTSNAME_NOTRAILWHITESP|Object name "%1" is not valid. Name cannot end with a whitespace.|  
|0xC001F206|-1073614330|DTS_E_DTSNAME_BEGINSWITHALPHA|Object name "%1" is not valid. Name must begin with an alphabetical character.|  
|0xC001F207|-1073614329|DTS_E_DTSNAME_BEGINSWITHALPHAUNDERBAR|Object name "%1" is not valid. Name must begin with an alphabetical character or underscore "_".|  
|0xC001F208|-1073614328|DTS_E_DTSNAME_ALPHADIGITUNDERBAR|Object name "%1" is not valid. Name must contain only alphanumeric characters or underscores "_".|  
|0xC001F209|-1073614327|DTS_E_DTSNAME_VALIDFILENAME|Object name "%1" is not valid. The name cannot contain any of the following characters: / \ : ? " < > &#124;|  
|0xC001F420|-1073613792|DTS_E_FAILLOADINGPROPERTY|Failed to load the value property "%1" using default persistence.|  
|0xC001F422|-1073613790|DTS_E_NODELISTENUM_INVALIDCONNMGRTYPE|Connection manager "%1" is not of type "%2"|  
|0xC001F423|-1073613789|DTS_E_NODELISTENUM_XPATHISEMPTY|"%1" is empty|  
|0xC001F424|-1073613788|DTS_E_NODELISTENUM_INVALIDDATANODE|Invalid data node in the nodelist enumerator section|  
|0xC001F425|-1073613787|DTS_E_NODELISTENUM_NOENUMERATORCREATED|No enumerator can be created|  
|0xC001F427|-1073613785|DTS_E_OPERATIONFAILCACHEINUSE|The operation failed because the cache is in use.|  
|0xC001F428|-1073613784|DTS_E_PROPERTYCANNOTBEMODIFIED|The property cannot be modified.|  
|0xC001F429|-1073613783|DTS_E_PACKAGEUPGRADEFAILED|The package upgrade has failed.|  
|0xC00220DE|-1073602338|DTS_E_TKEXECPACKAGE_UNABLETOLOADFILE|Error 0x%1!8.8X! while loading package file "%3". %2.|  
|0xC00220DF|-1073602337|DTS_E_TKEXECPACKAGE_UNSPECIFIEDPACKAGE|The package is not specified.|  
|0xC00220E0|-1073602336|DTS_E_TKEXECPACKAGE_UNSPECIFIEDCONNECTION|The connection is not specified.|  
|0xC00220E2|-1073602334|DTS_E_TKEXECPACKAGE_INCORRECTCONNECTIONMANAGERTYPE|The connection manager "%1" has an unsupported type "%2". Only "FILE" and "OLEDB" connection managers are supported.|  
|0xC00220E3|-1073602333|DTS_E_TKEXECPACKAGE_UNABLETOLOADXML|Error 0x%1!8.8X! while loading package file "%3" into an XML document. %2.|  
|0xC00220E4|-1073602332|DTS_E_TKEXECPACKAGE_UNABLETOLOAD|Error 0x%1!8.8X! while preparing to load the package. %2.|  
|0xC0024102|-1073594110|DTS_E_TASKVALIDATIONFAILED|The Validate method on the task failed, and returned error code 0x%1!8.8X! (%2). The Validate method must succeed and indicate the result using an "out" parameter.|  
|0xC0024104|-1073594108|DTS_E_TASKEXECUTEFAILED|The Execute method on the task returned error code 0x%1!8.8X! (%2). The Execute method must succeed, and indicate the result using an "out" parameter.|  
|0xC0024105|-1073594107|DTS_E_RETRIEVINGDEPENDENCIES|A failure occurred on task "%1": 0x%2!8.8X! while retrieving dependencies. The runtime was retrieving dependencies from the task's dependencies collection when the error occurred. The task may have incorrectly implemented one of the dependency interfaces.|  
|0xC0024107|-1073594105|DTS_E_TASKVALIDATIONERROR|There were errors during task validation.|  
|0xC0024108|-1073594104|DTS_E_CONNECTIONSTRINGFORMAT|The connection string format is not valid. It must consist of one or more components of the form X=Y, separated by semicolons. This error occurs when a connection string with zero components is set on database connection manager.|  
|0xC0024109|-1073594103|DTS_E_UNQUOTEDSEMICOLON|The connection string components cannot contain unquoted semicolons. If the value must contain a semicolon, enclose the entire value in quotes. This error occurs when values in the connection string contain unquoted semicolons, such as the InitialCatalog property.|  
|0xC002410A|-1073594102|DTS_E_LOGPROVIDERVALIDATIONFAILED|Validation of one or more log providers failed. The package cannot execute. The package does not execute when a log provider fails validation.|  
|0xC002410B|-1073594101|DTS_E_INVALIDVALUEINARRAY|Invalid value in array.|  
|0xC002410C|-1073594100|DTS_E_ENUMERATIONELEMENTNOTENUMERABLE|An element of the enumerator returned by the ForEach Enumerator does not implement IEnumerator, contradicting the CollectionEnumerator property of the ForEach Enumerator.|  
|0xC002410D|-1073594099|DTS_E_INVALIDENUMERATORINDEX|The enumerator failed to retrieve element at index "%1!d!".|  
|0xC0029100|-1073573632|DTS_E_AXTASK_MISSING_ENTRY_METHOD_NAME|Function not found.|  
|0xC0029101|-1073573631|DTS_E_AXTASK_EMPTY_SCRIPT|Function not found.|  
|0xC0029102|-1073573630|DTS_E_AXTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|ActiveX Script Task was initiated with a wrong XML element.|  
|0xC0029105|-1073573627|DTS_E_AXTASK_HANDLER_NOT_FOUND|Handler not found.|  
|0xC0029106|-1073573626|DTS_E_AXTASKUTIL_ENUMERATE_LANGUAGES_FAILED|An error occurred while attempting to retrieve the scripting languages installed on the system.|  
|0xC0029107|-1073573625|DTS_E_AXTASKUTIL_SCRIPTHOST_CREATE_FAILED|An error occurred while creating the ActiveX script host. Verify that you have the script host installed properly.|  
|0xC0029108|-1073573624|DTS_E_AXTASKUTIL_SCRIPTHOSTINIT_FAILED|An error occurred while trying to instantiate the script host for the chosen language. Verify that the script language you have chosen is installed on your system.|  
|0xC0029109|-1073573623|DTS_E_AXTASKUTIL_ADDVARIABLES_FAILED|An error occurred while adding the SSIS variables to the script host namespace. This might prevent the task from using SSIS variables in the script.|  
|0xC002910A|-1073573622|DTS_E_AXTASKUTIL_SCRIPT_PARSING_FAILED|A fatal error occurred while trying to parse the script text. Verify that the script engine for the chosen language is installed properly.|  
|0xC002910B|-1073573621|DTS_E_AXTASKUTIL_MSG_BAD_FUNCTION|The function name entered is not valid. Verify that a valid function name has been specified.|  
|0xC002910C|-1073573620|DTS_E_AXTASKUTIL_EXECUTION_FAILED|An error occurred while executing the script. Verify that the script engine for the selected language is installed properly.|  
|0xC002910D|-1073573619|DTS_E_AXTASKUTIL_ADDTYPELIB_FAILED|An error occurred while adding the managed type library to the script host. Verify that the DTS 2000 runtime is installed.|  
|0xC002910E|-1073573618|DTS_E_BITASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Bulk Insert Task was initiated with a wrong XML element.|  
|0xC002910F|-1073573617|DTS_E_BITASK_DATA_FILE_NOT_SPECIFIED|Data file name not specified.|  
|0xC0029110|-1073573616|DTS_E_BITASK_HANDLER_NOT_FOUND|Handler not found.|  
|0xC0029111|-1073573615|DTS_E_BITASK_CANNOT_ACQUIRE_CONNECTION|Failed to acquire the specified connection: "%1".|  
|0xC0029112|-1073573614|DTS_E_BITASK_NO_CONNECTION_MANAGER_SPECIFIED|Attempt to obtain the Connection Manager failed.|  
|0xC0029113|-1073573613|DTS_E_BITASK_INVALID_CONNECTION|The connection is not valid.|  
|0xC0029114|-1073573612|DTS_E_BITASK_NULL_CONNECTION|The connection is null.|  
|0xC0029115|-1073573611|DTS_E_BITASK_EXECUTE_FAILED|Execution failed.|  
|0xC0029116|-1073573610|DTS_E_BITASK_CANNOT_RETRIEVE_TABLES|An error occurred while retrieving the tables from the database.|  
|0xC0029117|-1073573609|DTS_E_BITASK_CANNOT_RETRIEVE_COLUMN_INFO|An error occurred while retrieving the columns of the table.|  
|0xC0029118|-1073573608|DTS_E_BITASK_ERROR_IN_DB_OPERATION|An error occurred in the database operation.|  
|0xC0029119|-1073573607|DTS_E_BITASK_INVALIDSOURCECONNECTIONNAME|The specified connection "%1" is either not valid, or points to an invalid object. To continue, specify a valid connection.|  
|0xC002911A|-1073573606|DTS_E_BITASK_INVALIDDESTCONNECTIONNAME|The destination connection specified is not valid. Supply a valid connection to continue.|  
|0xC002911B|-1073573605|DTS_E_BITASK_DESTINATION_TABLE_NOT_SPECIFIED|You must specify a table name to continue.|  
|0xC002911C|-1073573604|DTS_E_BITASK_ERROR_IN_LOAD_FROM_XML|Error occurred in LoadFromXML at the tag "%1".|  
|0xC002911D|-1073573603|DTS_E_BITASK_ERROR_IN_SAVE_TO_XML|Error occurred in SaveToXML at the tag "%1".|  
|0xC002911E|-1073573602|DTS_E_BITASKUNMANCONNECTION_INVALID_CONNECTION|The connection is not valid.|  
|0xC002911F|-1073573601|DTS_E_BITASKUNMANCONNECTION_EXECUTE_FAILED|Execution failed.|  
|0xC0029120|-1073573600|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_TABLES|Error occurred while retrieving the tables from the database.|  
|0xC0029121|-1073573599|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_COLUMN_INFO|Error occurred while retrieving the columns of the table.|  
|0xC0029122|-1073573598|DTS_E_BITASKUNMANCONNECTION_CANNOT_OPEN_FILE|Error occurred while trying to open the data file.|  
|0xC0029123|-1073573597|DTS_E_BITASKUNMANCONNECTION_OEM_CONVERSION_FAILED|Cannot convert the input OEM file to the specified format.|  
|0xC0029124|-1073573596|DTS_E_BITASKUNMANCONNECTION_ERROR_IN_DB_OPERATION|Error in database operation.|  
|0xC0029125|-1073573595|DTS_E_DTSPROCTASK_NOCONNECTIONSPECIFIED|No connection manager specified.|  
|0xC0029126|-1073573594|DTS_E_DTSPROCTASK_CONNECTIONMANAGERNOTOLAP|Connection "%1" is not an Analysis Services connection.|  
|0xC0029127|-1073573593|DTS_E_DTSPROCTASK_UNABLETOLOCATECONNECTIONMANAGER|Unable to locate connection "%1".|  
|0xC0029128|-1073573592|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEEXE|Analysis Services Execute DDL task received an invalid task data node.|  
|0xC0029129|-1073573591|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEPROC|Analysis Services Processing task received an invalid task data node.|  
|0xC002912A|-1073573590|DTS_E_DTSPROCTASK_INVALIDDDL|The DDL is not valid.|  
|0xC002912B|-1073573589|DTS_E_DTSPROCTASK_INVALIDDDLPROCESSINGCOMMANDS|The DDL found in ProcessingCommands is not valid.|  
|0xC002912C|-1073573588|DTS_E_DTSPROCTASK_CANNOTWRITEINAREADONLYVARIABLE|The Execution result cannot be saved in a read-only variable.|  
|0xC002912D|-1073573587|DTS_E_DTSPROCTASK_INVALIDVARIABLE|Variable "%1" it's not defined.|  
|0xC002912E|-1073573586|DTS_E_DTSPROCTASK_CONNECTIONNOTFOUND|Connection Manager "%1" it's not defined.|  
|0xC002912F|-1073573585|DTS_E_DTSPROCTASK_INVALIDCONNECTION|Connection Manager "%1" it's not a FILE Connection Manager.|  
|0xC0029130|-1073573584|DTS_E_DTSPROCTASK_NONEXISTENTATTRIBUTE|"%1" was not found during deserialization.|  
|0xC0029131|-1073573583|DTS_E_DTSPROCTASK_TRACEHASBEENSTOPPED|The trace has been stopped due to an exception.|  
|0xC0029132|-1073573582|DTS_E_DTSPROCTASK_DDLEXECUTIONFAILED|Execution of DDL failed.|  
|0xC0029133|-1073573581|DTS_E_DTSPROCTASK_FILEDOESNOTEXIST|There is no file associated with connection "%1".|  
|0xC0029134|-1073573580|DTS_E_DTSPROCTASK_VARIABLENOTDEFINED|Variable "%1" is not defined.|  
|0xC0029135|-1073573579|DTS_E_DTSPROCTASK_FILECONNECTIONNOTDEFINED|File connection "%1" is not defined.|  
|0xC0029136|-1073573578|DTS_E_EXEC2000PKGTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Execute DTS 2000 Package task is initiated with a wrong XML element.|  
|0xC0029137|-1073573577|DTS_E_EXEC2000PKGTASK_HANDLER_NOT_FOUND|Handler not found.|  
|0xC0029138|-1073573576|DTS_E_EXEC2000PKGTASK_PACKAGE_NAME_NOT_SPECIFIED|Package name is not specified.|  
|0xC0029139|-1073573575|DTS_E_EXEC2000PKGTASK_PACKAGE_ID_NOT_SPECIFIED|Package ID is not specified.|  
|0xC002913A|-1073573574|DTS_E_EXEC2000PKGTASK_PACKAGE_VERSIONGUID_NOT_SPECIFIED|Package version GUID is not specified.|  
|0xC002913B|-1073573573|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_SPECIFIED|SQL Server is not specified.|  
|0xC002913C|-1073573572|DTS_E_EXEC2000PKGTASK_SQL_USERNAME_NOT_SPECIFIED|SQL Server user name not specified.|  
|0xC002913D|-1073573571|DTS_E_EXEC2000PKGTASK_FILE_NAME_NOT_SPECIFIED|Storage file name not specified.|  
|0xC002913E|-1073573570|DTS_E_EXEC2000PKGTASK_DTS2000CANTBEEMPTY|The DTS 2000 package property is empty.|  
|0xC002913F|-1073573569|DTS_E_EXEC2000PKGTASK_ERROR_IN_PACKAGE_EXECUTE|An error occurred while executing the DTS 2000 package.|  
|0xC0029140|-1073573568|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_AVAILABLE_NETWORK|Cannot load the available SQL Servers from the network. Check the network connection.|  
|0xC0029141|-1073573567|DTS_E_EXEC2000PKGTASK_DATATYPE_NULL|The data type cannot be null. Please specify the correct data type to use for validating the value.|  
|0xC0029142|-1073573566|DTS_E_EXEC2000PKGTASK_NULL_VALUE|Cannot validate a null against any data type.|  
|0xC0029143|-1073573565|DTS_E_EXEC2000PKGTASK_NULL_VALUE_ARGUMENT|A required argument is null.|  
|0xC0029144|-1073573564|DTS_E_EXEC2000PKGTASK_CLS_NOT_REGISTRED_EXCEPTION|To execute the DTS 2000 Package task, start SQL Server Setup and use the Advanced button from the Components to Install page to select Legacy Components.|  
|0xC0029145|-1073573563|DTS_E_EXEC2000PKGTASK_NOT_PRIMITIVE_TYPE|"%1" is not a value type.|  
|0xC0029146|-1073573562|DTS_E_EXEC2000PKGTASK_CONVERT_FAILED|Could not convert "%1" to "%2".|  
|0xC0029147|-1073573561|DTS_E_EXEC2000PKGTASK_ERROR_IN_VALIDATE|Could not validate "%1" against "%2".|  
|0xC0029148|-1073573560|DTS_E_EXEC2000PKGTASK_ERROR_IN_LOAD_FROM_XML|Error occurred in LoadFromXML at the tag "%1".|  
|0xC0029149|-1073573559|DTS_E_EXEC2000PKGTASK_ERROR_IN_SAVE_TO_XML|Error occurred in SaveToXML at the tag "%1".|  
|0xC002914A|-1073573558|DTS_E_EXECPROCTASK_INVALIDTIMEOUT|The time-out value provided is not valid. Specify the number of seconds that the task allows the process to run. The minimum time-out is 0, which indicates that no time-out value is used and the process runs to completion or until an error occurs. The maximum time-out is 2147483 (((2^31) - 1)/1000).|  
|0xC002914B|-1073573557|DTS_E_EXECPROCTASK_CANTREDIRECTIO|Cannot redirect streams if the process can continue executing beyond the lifetime of the task.|  
|0xC002914C|-1073573556|DTS_E_EXECPROCTASK_PROCESSHASTIMEDOUT|The process timed out.|  
|0xC002914D|-1073573555|DTS_E_EXECPROCTASK_EXECUTABLENOTSPECIFIED|The executable is not specified.|  
|0xC002914E|-1073573554|DTS_E_EXECPROCTASK_STDOUTVARREADONLY|The standard out variable is read-only.|  
|0xC002914F|-1073573553|DTS_E_EXECPROCTASK_STDERRVARREADONLY|The standard error variable is read-only.|  
|0xC0029150|-1073573552|DTS_E_EXECPROCTASK_RECEIVEDINVALIDTASKDATANODE|The Execute Process task received a task data node that is not valid.|  
|0xC0029151|-1073573551|DTS_E_EXECPROCTASK_PROCESSEXITCODEEXCEEDS|In Executing "%2" "%3" at "%1", The process exit code was "%4" while the expected was "%5".|  
|0xC0029152|-1073573550|DTS_E_EXECPROCTASK_WORKINGDIRDOESNOTEXIST|The directory "%1" does not exist.|  
|0xC0029153|-1073573549|DTS_E_EXECPROCTASK_FILEDOESNOTEXIST|File/Process "%1" does not exist in directory "%2".|  
|0xC0029154|-1073573548|DTS_E_EXECPROCTASK_FILENOTINPATH|File/Process "%1" is not in path.|  
|0xC0029156|-1073573546|DTS_E_EXECPROCTASK_WORKINGDIRECTORYDOESNOTEXIST|Working Directory "%1" does not exist.|  
|0xC0029157|-1073573545|DTS_E_EXECPROCTASK_ERROREXECUTIONVALUE|The process exited with return code "%1". However, "%2" was expected.|  
|0xC0029158|-1073573544|DTS_E_FSTASK_SYNCFAILED|Synchronization object failed.|  
|0xC0029159|-1073573543|DTS_E_FSTASK_INVALIDDATA|The File System task received an invalid task data node.|  
|0xC002915A|-1073573542|DTS_E_FSTASK_DIRECTORYEXISTS|The Directory already exists.|  
|0xC002915B|-1073573541|DTS_E_FSTASK_PATHNOTVALID|"%1" is not valid on operation type "%2".|  
|0xC002915C|-1073573540|DTS_E_FSTASK_DESTINATIONNOTSET|Destination property of operation "%1" not set.|  
|0xC002915D|-1073573539|DTS_E_FSTASK_SOURCENOTSET|Source property of operation "%1" not set.|  
|0xC002915E|-1073573538|DTS_E_FSTASK_CONNECTIONTYPENOTFILE|Type of Connection "%1" is not a file.|  
|0xC002915F|-1073573537|DTS_E_FSTASK_VARIABLEDOESNTEXIST|Variable "%1" does not exist.|  
|0xC0029160|-1073573536|DTS_E_FSTASK_VARIABLENOTASTRING|Variable "%1" is not a string.|  
|0xC0029163|-1073573533|DTS_E_FSTASK_FILEDOESNOTEXIST|File or directory "%1" represented by connection "%2" does not exist.|  
|0xC0029165|-1073573531|DTS_E_FSTASK_DESTCONNUSAGETYPEINVALID|The destination file connection manager "%1" has an invalid usage type: "%2".|  
|0xC0029166|-1073573530|DTS_E_FSTASK_SRCCONNUSAGETYPEINVALID|The source file connection manager "%1" has an invalid usage type "%2".|  
|0xC0029167|-1073573529|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATION|FileSystemOperation|  
|0xC0029168|-1073573528|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATIONDESC|Provides information regarding File System operations.|  
|0xC0029169|-1073573527|DTS_E_FSTASK_TASKDISPLAYNAME|File System Task|  
|0xC002916A|-1073573526|DTS_E_FSTASK_TASKDESCRIPTION|Perform file system operations, such as copying and deleting files.|  
|0xC002916B|-1073573525|DTS_E_FTPTASK_SYNCOBJFAILED|Synchronization object failed.|  
|0xC002916C|-1073573524|DTS_E_FTPTASK_UNABLETOOBTAINFILELIST|Unable to obtain the file list.|  
|0xC002916D|-1073573523|DTS_E_FTPTASK_LOCALPATHEMPTY|The local path is empty.|  
|0xC002916E|-1073573522|DTS_E_FTPTASK_REMOTEPATHEMPTY|The remote path is empty.|  
|0xC002916F|-1073573521|DTS_E_FTPTASK_LOCALVARIBALEEMPTY|The local variable is empty.|  
|0xC0029170|-1073573520|DTS_E_FTPTASK_REMOTEVARIBALEEMPTY|The remote variable is empty.|  
|0xC0029171|-1073573519|DTS_E_FTPTASK_FTPRCVDINVLDDATANODE|The FTP task received an invalid task data node.|  
|0xC0029172|-1073573518|DTS_E_FTPTASK_CONNECTION_NAME_NULL|The connection is empty. Verify that a valid FTP connection is provided.|  
|0xC0029173|-1073573517|DTS_E_FTPTASK_CONNECTION_NOT_FTP|The connection specified is not an FTP connection. Verify that a valid FTP connection is provided.|  
|0xC0029175|-1073573515|DTS_E_FTPTASK__INITIALIZATION_WITH_NULL_XML_ELEMENT|Cannot initialize the task with a null XML element.|  
|0xC0029176|-1073573514|DTS_E_FTPTASK_SAVE_TO_NULL_XML_ELEMENT|Cannot save the task to a null XML document.|  
|0xC0029177|-1073573513|DTS_E_FTPTASK_ERROR_IN_LOAD_FROM_XML|Error occurred in LoadFromXML at the tag "%1".|  
|0xC0029178|-1073573512|DTS_E_FTPTASK_NOFILESATLOCATION|There are no files at "%1".|  
|0xC0029179|-1073573511|DTS_E_FTPTASK_LOCALVARIABLEISEMPTY|The variable "%1" is empty.|  
|0xC002917A|-1073573510|DTS_E_FTPTASK_REMOTEVARIABLEISEMPTY|The variable "%1" is empty.|  
|0xC002917B|-1073573509|DTS_E_FTPTASK_NOFILESINCONNMGR|The File "%1" doesn't contain file path(s).|  
|0xC002917C|-1073573508|DTS_E_FTPTASK_NOFILEPATHSINLOCALVAR|The variable "%1" doesn't contain file path(s).|  
|0xC002917D|-1073573507|DTS_E_FTPTASK_VARIABLENOTASTRING|Variable "%1" is not a string.|  
|0xC002917E|-1073573506|DTS_E_FTPTASK_VARIABLENOTFOUND|Variable "%1" does not exist.|  
|0xC002917F|-1073573505|DTS_E_FTPTASK_INVALIDPATHONOPERATION|Invalid path on operation "%1".|  
|0xC0029180|-1073573504|DTS_E_FTPTASK_DIRECTORYEXISTS|"%1" already exists.|  
|0xC0029182|-1073573502|DTS_E_FTPTASK_CONNECTIONTYPENOTFILE|Type of Connection "%1" is Not a file.|  
|0xC0029183|-1073573501|DTS_E_FTPTASK_FILEDOESNOTEXIST|File represented by "%1" does not exist.|  
|0xC0029184|-1073573500|DTS_E_FTPTASK_INVALIDDIRECTORY|Directory is not specified in the variable "%1".|  
|0xC0029185|-1073573499|DTS_E_FTPTASK_NOFILESFOUND|No files found in "%1".|  
|0xC0029186|-1073573498|DTS_E_FTPTASK_NODIRECTORYPATHINCONMGR|Directory is not specified in the file connection manager "%1".|  
|0xC0029187|-1073573497|DTS_E_FTPTASK_UNABLETODELETELOCALEFILE|Unable to delete local file "%1".|  
|0xC0029188|-1073573496|DTS_E_FTPTASK_UNABLETOREMOVELOCALDIRECTORY|Unable to remove local directory "%1".|  
|0xC0029189|-1073573495|DTS_E_FTPTASK_UNABLETOCREATELOCALDIRECTORY|Unable to create local directory "%1".|  
|0xC002918A|-1073573494|DTS_E_FTPTASK_UNABLETORECEIVEFILES|Unable to receive files using "%1".|  
|0xC002918B|-1073573493|DTS_E_FTPTASK_UNABLETOSENDFILES|Unable to send files using "%1".|  
|0xC002918C|-1073573492|DTS_E_FTPTASK_UNABLETOMAKEDIRREMOTE|Unable to create remote directory using "%1".|  
|0xC002918D|-1073573491|DTS_E_FTPTASK_UNABLETOREMOVEDIRREMOTE|Unable to remove remote directory using "%1".|  
|0xC002918E|-1073573490|DTS_E_FTPTASK_UNABLETODELETEREMOTEFILES|Unable to delete remote files using "%1".|  
|0xC002918F|-1073573489|DTS_E_FTPTASK_UNABLETOCONNECTTOSERVER|Unable to connect to FTP server using "%1".|  
|0xC0029190|-1073573488|DTS_E_FTPTASK_INVALIDVARIABLEVALUE|Variable "%1" doesn't start with "/".|  
|0xC0029191|-1073573487|DTS_E_FTPTASK_INVALIDREMOTEPATH|Remote path "%1" doesn't start with "/".|  
|0xC0029192|-1073573486|DTS_E_DTS_E_FTPTASK_CANNOT_ACQUIRE_CONNECTION|There was an error acquiring the FTP connection. Please check if you have specified a valid connection type "%1".|  
|0xC0029193|-1073573485|DTS_E_MSGQTASKUTIL_CERT_OPEN_STORE_FAILED|Opening the certificate store failed.|  
|0xC0029194|-1073573484|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_DISPLAY_NAME|An error occurred while retrieving the display name of the certificate.|  
|0xC0029195|-1073573483|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_ISSUER_NAME|An error occurred while retrieving the issuer name of the certificate.|  
|0xC0029196|-1073573482|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_FRIENDLY_NAME|An error occurred while retrieving the friendly name of the certificate.|  
|0xC0029197|-1073573481|DTS_E_MSMQTASK_NO_CONNECTION|The MSMQ connection name is not set.|  
|0xC0029198|-1073573480|DTS_E_MSMQTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Task was initialized with the wrong XML element.|  
|0xC0029199|-1073573479|DTS_E_MSMQTASK_DATA_FILE_NAME_EMPTY|Data file name is empty.|  
|0xC002919A|-1073573478|DTS_E_MSMQTASK_DATA_FILE_SAVE_NAME_EMPTY|The name specified for the data file to save is empty.|  
|0xC002919B|-1073573477|DTS_E_MSMQTASK_DATA_FILE_SIZE_ERROR|File size should be less than 4 MB.|  
|0xC002919C|-1073573476|DTS_E_MSMQTASK_DATA_FILE_SAVE_FAILED|Saving the data file failed.|  
|0xC002919D|-1073573475|DTS_E_MSMQTASK_STRING_COMPARE_VALUE_MISSING|String filter value is empty.|  
|0xC002919E|-1073573474|DTS_E_MSMQTASK_INVALID_QUEUE_PATH|Queue path is not valid.|  
|0xC002919F|-1073573473|DTS_E_MSMQTASK_NOT_TRANSACTIONAL|The message queue task does not support enlisting in distributed transactions.|  
|0xC00291A0|-1073573472|DTS_E_MSMQTASK_INVALID_MESSAGE_TYPE|The message type is not valid.|  
|0xC00291A1|-1073573471|DTS_E_MSMQTASK_TASK_TIMEOUT|The message queue timed out. No message has been received.|  
|0xC00291A2|-1073573470|DTS_E_MSMQTASK_INVALID_PROPERTY_VALUE|The property specified is not valid. Verify that the argument type is correct.|  
|0xC00291A3|-1073573469|DTS_E_MSMQTASK_MESSAGE_NON_AUTHENTICATED|Message is not authenticated.|  
|0xC00291A4|-1073573468|DTS_E_MSMQTASK_INVALID_ENCRYPTION_ALGO_WRAPPER|You are trying to set the value of Encryption Algorithm with an invalid object.|  
|0xC00291A5|-1073573467|DTS_E_MSMQTASK_VARIABLE_TO_RECEIVE_STRING_MSG_EMPTY|The variable to receive string message is empty.|  
|0xC00291A6|-1073573466|DTS_E_MSMQTASK_RECEIVE_VARIABLE_EMPTY|Variable to receive variable message is empty.|  
|0xC00291A7|-1073573465|DTS_E_MSMQTASK_CONNECTIONTYPENOTMSMQ|Connection "%1" is not of type MSMQ.|  
|0xC00291A8|-1073573464|DTS_E_MSMQTASK_DATAFILE_ALREADY_EXISTS|The data file "%1" already exists at the specified location. Cannot overwrite the file as the Overwrite option is set to false.|  
|0xC00291A9|-1073573463|DTS_E_MSMQTASK_STRING_MSG_TO_VARIABLE_NOT_FOUND|The specified variable "%1" to receive string message is not found in the package variable collection.|  
|0xC00291AA|-1073573462|DTS_E_MSMQTASK_CONNMNGRNULL|The connection manager "%1" is empty.|  
|0xC00291AB|-1073573461|DTS_E_MSMQTASK_CONNMNGRDOESNOTEXIST|The connection manager "%1" does not exist.|  
|0xC00291AC|-1073573460|DTS_E_SCRIPTTASK_COMPILEERRORMSG|Error "%1": "%2"\r\nLine "%3"   Column "%4" through "%5".|  
|0xC00291AD|-1073573459|DTS_E_SCRIPTTASK_COMPILEERRORMSG2|There was an error compiling the script: "%1".|  
|0xC00291AE|-1073573458|DTS_E_SCRIPTTASK_COMPILEERRORMSG3|Error "%1": "%2"\r\nLine "%3" Columns "%4"-"%5"\r\nLine Text: "%6".|  
|0xC00291AF|-1073573457|DTS_E_SCRIPTTASK_SCRIPTREPORTEDFAILURE|User script returned a failure result.|  
|0xC00291B0|-1073573456|DTS_E_SCRIPTTASK_SCRIPTFILESFAILEDTOLOAD|User script files failed to load.|  
|0xC00291B1|-1073573455|DTS_E_SCRIPTTASK_SCRIPTTHREWEXCEPTION|User script threw an exception: "%1".|  
|0xC00291B2|-1073573454|DTS_E_SCRIPTTASK_COULDNOTCREATEENTRYPOINTCLASS|Could not create an instance of entrypoint class "%1".|  
|0xC00291B3|-1073573453|DTS_E_SCRIPTTASK_LOADFROMXMLEXCEPTION|There was an exception while loading Script Task from XML: "%1".|  
|0xC00291B4|-1073573452|DTS_E_SCRIPTTASK_SOURCEITEMNOTFOUNDEXCEPTION|Source item "%1" was not found in the package.|  
|0xC00291B5|-1073573451|DTS_E_SCRIPTTASK_BINARYITEMNOTFOUNDEXCEPTION|Binary item "%1" was not found in the package.|  
|0xC00291B6|-1073573450|DTS_E_SCRIPTTASK_UNRECOGNIZEDSCRIPTLANGUAGEEXCEPTION|"%1" was not recognized as a valid script language.|  
|0xC00291B7|-1073573449|DTS_E_SCRIPTTASK_ILLEGALSCRIPTNAME|The script name is not valid. It cannot contain spaces, slashes, special characters, or begin with a number.|  
|0xC00291B8|-1073573448|DTS_E_SCRIPTTASK_INVALIDSCRIPTLANGUAGE|The script language specified is not valid.|  
|0xC00291B9|-1073573447|DTS_E_SCRIPTTASK_CANTINITNULLTASK|Cannot initialize to a null task.|  
|0xC00291BA|-1073573446|DTS_E_SCRIPTTASK_MUSTINITWITHRIGHTTASK|The Script Task user interface must initialize to an Script Task.|  
|0xC00291BB|-1073573445|DTS_E_SCRIPTTASK_WASNOTINITED|The Script Task user interface is not initialized.|  
|0xC00291BC|-1073573444|DTS_E_SCRIPTTASK_HOST_NAME_CANT_EMPTY|Name cannot be empty.|  
|0xC00291BD|-1073573443|DTS_E_SCRIPTTASK_INVALID_SCRIPT_NAME|The project name is not valid. It cannot contain spaces, slashes, special characters, or begin with a number.|  
|0xC00291BE|-1073573442|DTS_E_SCRIPTTASK_INVALID_SCRIPT_LANGUAGE|The script language specified is not valid.|  
|0xC00291BF|-1073573441|DTS_E_SCRIPTTASK_INVALID_ENTRY_POINT|Entry point not found.|  
|0xC00291C0|-1073573440|DTS_E_SCRIPTTASK_LANGUAGE_EMPTY|The script language is not specified. Verify that a valid script language is specified.|  
|0xC00291C1|-1073573439|DTS_E_SCRIPTTASK_INITIALIZATION_WITH_NULL_TASK|User interface initialization: The task is null.|  
|0xC00291C2|-1073573438|DTS_E_SCRIPTTASK_UI_INITIALIZATION_WITH_WRONG_TASK|The Script Task user interface is initialized with an incorrect task.|  
|0xC00291C3|-1073573437|DTS_E_SENDMAILTASK_RECIPIENT_EMPTY|No recipient is specified.|  
|0xC00291C4|-1073573436|DTS_E_SENDMAILTASK_SMTP_SERVER_NOT_SPECIFIED|The Simple Mail Transfer Protocol (SMTP) server is not specified. Provide a valid name or IP address of the SMTP server.|  
|0xC00291C5|-1073573435|DTS_E_SENDMAILTASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Send Mail task is initiated with an incorrect XML element.|  
|0xC00291CB|-1073573429|DTS_E_SENDMAILTASK_INVALIDATTACHMENT|Either the file "%1" does not exist or you do not have permissions to access the file.|  
|0xC00291CD|-1073573427|DTS_E_SENDMAILTASK_CHECK_VALID_SMTP_SERVER|Verify that the Simple Mail Transfer Protocol (SMTP) server specified is valid.|  
|0xC00291CE|-1073573426|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTFILE|Connection "%1" is not of type File.|  
|0xC00291CF|-1073573425|DTS_E_SENDMAILTASK_FILEDOESNOTEXIST|On operation "%1", file "%2" does not exist.|  
|0xC00291D0|-1073573424|DTS_E_SENDMAILTASK_VARIABLETYPEISNOTSTRING|Variable "%1" is not of type string.|  
|0xC00291D1|-1073573423|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTSMTP|Connection "%1" is not of type SMTP.|  
|0xC00291D2|-1073573422|DTS_E_SENDMAILTASK_CONNMNGRNULL|Connection "%1" is empty.|  
|0xC00291D3|-1073573421|DTS_E_SENDMAILTASK_NOCONNMNGR|The specified connection "%1" does not exist.|  
|0xC00291D4|-1073573420|DTS_E_SQLTASK_NOSTATEMENTSPECIFIED|No Transact-SQL statement specified.|  
|0xC00291D5|-1073573419|DTS_E_SQLTASK_NOXMLSUPPORT|The connection does not support XML result sets.|  
|0xC00291D6|-1073573418|DTS_E_SQLTASK_NOHANDLERFORCONNECTION|Cannot locate a handler for the specified connection type.|  
|0xC00291D7|-1073573417|DTS_E_SQLTASK_NOCONNECTIONMANAGER|No connection manager is specified.|  
|0xC00291D8|-1073573416|DTS_E_SQLTASK_CANNOTACQUIRECONNMANAGER|Cannot acquire a connection from the connection manager.|  
|0xC00291D9|-1073573415|DTS_E_SQLTASK_NULLPARAMETERNAME|Cannot have a null parameter name.|  
|0xC00291DA|-1073573414|DTS_E_SQLTASK_INVALIDPARAMETERNAME|The parameter name is not valid.|  
|0xC00291DB|-1073573413|DTS_E_SQLTASK_VALIDPARAMETERTYPES|Valid parameter names are of type Int or String.|  
|0xC00291DC|-1073573412|DTS_E_SQLTASK_READONLYVARIABLE|Variable "%1" cannot be used in a result binding because it is read-only.|  
|0xC00291DD|-1073573411|DTS_E_SQLTASK_INDESNOTINCOLLECTION|The index is not assigned in this collection.|  
|0xC00291DE|-1073573410|DTS_E_SQLTASK_ROVARINOUTPARAMETER|The variable "%1" cannot be used as an "out" parameter or return value in a parameter binding because it is read-only.|  
|0xC00291DF|-1073573409|DTS_E_SQLTASK_OBJECTNOTINCOLLECTION|The object does not exist in this collection.|  
|0xC00291E0|-1073573408|DTS_E_SQLTASK_UNABLETOACQUIREMANAGEDCONN|Cannot acquire a managed connection.|  
|0xC00291E1|-1073573407|DTS_E_UNABLETOPOPRESULT|Cannot populate the result columns for a single row result type. The query returned an empty result set.|  
|0xC00291E2|-1073573406|DTS_E_SQLTASK_INVALIDNUMOFRESULTBINDINGS|There is an invalid number of result bindings returned for the ResultSetType: "%1".|  
|0xC00291E3|-1073573405|DTS_E_SQLTASK_RESULTBINDTYPEFORROWSETXML|The result binding name must be set to zero for full result set and XML results.|  
|0xC00291E4|-1073573404|DTS_E_SQLTASK_INVALIDEPARAMDIRECTIONFALG|The parameter directions flag is not valid.|  
|0xC00291E5|-1073573403|DTS_E_SQLTASK_NOSQLTASKDATAINXMLFRAGMENT|The XML fragment does not contain SQL Task data.|  
|0xC00291E6|-1073573402|DTS_E_SQLTASK_MULTIPLERETURNVALUEPARAM|A parameter with type return value is not the first parameter, or there are more than one parameter of type return value.|  
|0xC00291E7|-1073573401|DTS_E_SQLTASK_CONNECTIONTYPENOTFILE|Connection "%1" is not a file connection manager.|  
|0xC00291E8|-1073573400|DTS_E_SQLTASK_FILEDOESNOTEXIST|File represented by "%1" does not exist.|  
|0xC00291E9|-1073573399|DTS_E_SQLTASK_VARIABLETYPEISNOTSTRING|Type of variable "%1" is not string.|  
|0xC00291EA|-1073573398|DTS_E_SQLTASK_VARIABLENOTFOUND|Variable "%1" does not exist or could not be locked.|  
|0xC00291EB|-1073573397|DTS_E_SQLTASK_CANNOTLOCATECONNMANAGER|Connection manager "%1" does not exist.|  
|0xC00291EC|-1073573396|DTS_E_SQLTASK_FAILEDTOACQUIRECONNECTION|Failed to acquire connection "%1". Connection may not be configured correctly or you may not have the right permissions on this connection.|  
|0xC00291ED|-1073573395|DTS_E_SQLTASK_RESULTBYNAMENOTSUPPORTED|Result binding by name "%1" is not supported for this connection type.|  
|0xC00291EE|-1073573394|DTS_E_SQLTASKCONN_ERR_NO_ROWS|A result set type of single row is specified, but no rows were returned.|  
|0xC00291EF|-1073573393|DTS_E_SQLTASKCONN_ERR_NO_DISCONNECTED_RS|No disconnected record set is available for the Transact-SQL statement.|  
|0xC00291F0|-1073573392|DTS_E_SQLTASKCONN_ERR_UNSUPPORTED_TYPE|Unsupported type.|  
|0xC00291F1|-1073573391|DTS_E_SQLTASKCONN_ERR_UNKNOWN_TYPE|Unknown type.|  
|0xC00291F2|-1073573390|DTS_E_SQLTASKCONN_ERR_PARAM_DATA_TYPE|Unsupported data type on parameter binding \\"%s\\".|  
|0xC00291F3|-1073573389|DTS_E_SQLTASKCONN_ERR_PARAM_NAME_MIX|Parameter names cannot be an mix of ordinal and named types.|  
|0xC00291F4|-1073573388|DTS_E_SQLTASKCONN_ERR_PARAM_DIR|The parameter direction on parameter binding \\"%s\\" is not valid.|  
|0xC00291F5|-1073573387|DTS_E_SQLTASKCONN_ERR_RESULT_DATA_TYPE|The data type on result set binding \\"%s\\" is not supported.|  
|0xC00291F6|-1073573386|DTS_E_SQLTASKCONN_ERR_RESULT_COL_INDEX|The result column index %d is not valid.|  
|0xC00291F7|-1073573385|DTS_E_SQLTASKCONN_ERR_UNKNOWN_RESULT_COL|Cannot find column \\"%s\\" in the result set.|  
|0xC00291F9|-1073573383|DTS_E_SQLTASKCONN_ERR_NOROWSET|No result rowset is associated with the execution of this query.|  
|0xC00291FA|-1073573382|DTS_E_SQLTASKCONN_ERR_ODBC_DISCONNECTED|Disconnected recordsets are not available from ODBC connections.|  
|0xC00291FB|-1073573381|DTS_E_SQLTASKCONN_ERR_RESULT_SET_DATA_TYPE|The data type in the result set, column %hd, is not supported.|  
|0xC00291FC|-1073573380|DTS_E_SQLTASKCONN_ERR_CANT_LOAD_XML|Cannot load XML with query result.|  
|0xC00291FD|-1073573379|DTS_E_TTGENTASK_NOCONNORVARIABLE|A connection name or variable name for the package must be specified.|  
|0xC00291FE|-1073573378|DTS_E_TTGENTASK_FAILEDCREATE|Failed to create the package.|  
|0xC00291FF|-1073573377|DTS_E_TTGENTASK_BADTABLEMETADATA|The TableMetaDataNode is not an XMLNode.|  
|0xC0029200|-1073573376|DTS_E_TTGENTASK_FAILEDCREATEPIPELINE|Failed to create the pipeline.|  
|0xC0029201|-1073573375|DTS_E_TTGENTASK_BADVARIABLETYPE|The variable is not the correct type.|  
|0xC0029202|-1073573374|DTS_E_TTGENTASK_NOTFILECONNECTION|The connection manager specified is not a FILE connection manager.|  
|0xC0029203|-1073573373|DTS_E_TTGENTASK_BADFILENAME|Invalid file name specified on the connection manager "%1".|  
|0xC0029204|-1073573372|DTS_E_WEBSERVICETASK_CONNECTION_NAME_NULL|The connection is empty. Verify that a valid HTTP connection is specified.|  
|0xC0029205|-1073573371|DTS_E_WEBSERVICETASK_CONNECTION_NOT_FOUND|The connection does not exist. Verify that a valid, existing HTTP connection is specified.|  
|0xC0029206|-1073573370|DTS_E_WEBSERVICETASK_CONNECTION_NOT_HTTP|The connection specified is not a HTTP connection. Verify that a valid HTTP connection is specified.|  
|0xC0029207|-1073573369|DTS_E_WEBSERVICETASK_SERVICE_NULL|The Web Service name is empty. Verify that a valid web service name is specified.|  
|0xC0029208|-1073573368|DTS_E_WEBSERVICETASK_METHODNAME_NULL|The web method name is empty. Verify that a valid web method is specified.|  
|0xC0029209|-1073573367|DTS_E_WEBSERVICETASK_WEBMETHODINFO_NULL|The web method is empty or may not exist. Verify that there is an existing web method to specify.|  
|0xC002920A|-1073573366|DTS_E_WEBSERVICETASK_OUTPUTLOC_NULL|The output location is empty. Verify that an existing file connection or variable is specified.|  
|0xC002920B|-1073573365|DTS_E_WEBSERVICETASK_VARIABLE_NOT_FOUND|The variable cannot be found. Verify that the variable exists in the package.|  
|0xC002920C|-1073573364|DTS_E_WEBSERVICETASK_VARIABLE_READONLY|Cannot save the result. Verify that the variable is not read-only.|  
|0xC002920D|-1073573363|DTS_E_WEBSERVICETASK_ERROR_IN_LOAD_FROM_XML|Error occurred in LoadFromXML at the tag "%1".|  
|0xC002920E|-1073573362|DTS_E_WEBSERVICETASK_ERROR_IN_SAVE_TO_XML|Error occurred in SaveToXML at the tag "%1".|  
|0xC002920F|-1073573361|DTS_E_WEBSERVICETASK_TASK_SAVE_TO_NULL_XML_ELEMENT|Cannot save the task to a null XML document.|  
|0xC0029210|-1073573360|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_NULL_XML_ELEMENT|Cannot initialize the task with a null XML element.|  
|0xC0029211|-1073573359|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|The Web Service Task is initiated with an incorrect XML element.|  
|0xC0029212|-1073573358|DTS_E_WEBSERVICETASK_UNEXPECTED_XML_ELEMENT|Unexpected XML element found.|  
|0xC0029213|-1073573357|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_CONNECTION|There was an error acquiring the HTTP connection. Verify that a valid connection type is specified.|  
|0xC0029214|-1073573356|DTS_E_WEBSERVICETASK_FILE_CONN_NOT_FOUND|Cannot save the result. Verify that there is an existing file connection.|  
|0xC0029215|-1073573355|DTS_E_WEBSERVICETASK_FILE_NOT_FOUND|Cannot save the result. Verify that the file exists.|  
|0xC0029216|-1073573354|DTS_E_WEBSERVICETASK_FILE_NULL|Cannot save the result. The file name is empty or the file is in use by another process.|  
|0xC0029217|-1073573353|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_FILE_CONNECTION|There was an error in acquiring the file connection. Verify that a valid file connection is specified.|  
|0xC0029218|-1073573352|DTS_E_WEBSERVICETASK_DATATYPE_NOT_SUPPORTED|Only Complex Types with Primitive values, Primitive Arrays, and Enumerations are supported.|  
|0xC0029219|-1073573351|DTS_E_WEBSERVICETASK_PARAMTYPE_NOT_SUPPORTED|Only Primitive, Enum, Complex, PrimitiveArray, and ComplexArray types are supported.|  
|0xC002921A|-1073573350|DTS_E_WEBSERVICETASK_WSDL_VERSION_NOT_SUPPORTED|This version of WSDL is not supported.|  
|0xC002921B|-1073573349|DTS_E_WEBSERVICETASK_WRONG_XML_ELEMENT|Initialized with an incorrect XML element.|  
|0xC002921C|-1073573348|DTS_E_WEBSERVICETASK_XML_ATTRIBUTE_NOT_FOUND|A mandatory attribute is not found.|  
|0xC002921D|-1073573347|DTS_E_WEBSERVICETASK_ENUM_NO_VALUES|The enum "%1" does not have any values. The WSDL is corrupted.|  
|0xC002921E|-1073573346|DTS_E_WEBSERVICETASK_CONNECTIONNOTFOUND|The connection cannot be found.|  
|0xC002921F|-1073573345|DTS_E_WEBSERVICETASK_CONNECTION_ALREADY_EXISTS|Connection by this name already exists.|  
|0xC0029220|-1073573344|DTS_E_WEBSERVICETASK_NULL_CONNECTION|Connection cannot be null or empty.|  
|0xC0029221|-1073573343|DTS_E_WEBSERVICETASK_NOT_HTTP_CONNECTION|The connection specified is not a HTTP connection. Verify that a valid HTTP connection is specified.|  
|0xC0029222|-1073573342|DTS_E_WEBSERVICETASK_WSDL_NOT_FOUND|The specified Uniform Resource Identifier (URI) does not contain a valid WSDL.|  
|0xC0029223|-1073573341|DTS_E_WEBSERVICETASK_ERROR_IN_DOWNLOAD|Could not read the WSDL file. The input WSDL file is not valid. The reader threw the following error: "%1".|  
|0xC0029224|-1073573340|DTS_E_WEBSERVICETASK_SERVICE_DESC_NULL|Service Description cannot be null.|  
|0xC0029225|-1073573339|DTS_E_WEBSERVICETASK_SERVICENULL|Service name cannot be null.|  
|0xC0029226|-1073573338|DTS_E_WEBSERVICETASK_WSDL_NULL|URL cannot be null.|  
|0xC0029227|-1073573337|DTS_E_WEBSERVICETASK_SERVICE_NOT_FOUND|The service is not currently available.|  
|0xC0029228|-1073573336|DTS_E_WEBSERVICETASK_SOAPPORT_NOT_FOUND|The service is not available on the SOAP port.|  
|0xC0029229|-1073573335|DTS_E_WEBSERVICETASK_SOAPBINDING_NOT_FOUND|Failed to parse the Web Services Description Language (WSDL). Cannot find the Binding that corresponds to the SOAP port.|  
|0xC002922A|-1073573334|DTS_E_WEBSERVICETASK_SOAPPORTTYPE_NOT_FOUND|Failed to parse the Web Services Description Language (WSDL). Cannot find a PortType that corresponds to the SOAP port.|  
|0xC002922B|-1073573333|DTS_E_WEBSERVICETASK_MSG_NOT_FOUND|Cannot find the message that corresponds to the method specified.|  
|0xC002922C|-1073573332|DTS_E_WEBSERVICETASK_CANNOT_GEN_PROXY|Could not generate the proxy for the given web service. The following errors were encountered while generating the proxy "%1".|  
|0xC002922D|-1073573331|DTS_E_WEBSERVICETASK_CANNOT_LOAD_PROXY|Could not load the proxy for the given web service. The exact error is as follows: "%1".|  
|0xC002922E|-1073573330|DTS_E_WEBSERVICETASK_INVALID_SERVICE|Could not find the specified service. The exact error is as follows: "%1".|  
|0xC002922F|-1073573329|DTS_E_WEBSERVICETASK_WEBMETHOD_INVOKE_FAILED|The Web Service threw the following error during method execution: "%1".|  
|0xC0029230|-1073573328|DTS_E_WEBSERVICETASK_INVOKE_ERR|Could not execute the web method. The exact error is as follows: "%1".|  
|0xC0029231|-1073573327|DTS_E_WEBSERVICETASK_METHODINFO_NULL|MethodInfo cannot be null.|  
|0xC0029232|-1073573326|DTS_E_WEBSERVICETASK_VALUE_NOT_PRIMITIVE|The specified WebMethodInfo is not correct. The ParamValue supplied does not match the ParamType. The DTSParamValue is not of type PrimitiveValue.|  
|0xC0029233|-1073573325|DTS_E_WEBSERVICETASK_VALUE_NOT_ENUM|The WebMethodInfo specified is not correct. The ParamValue supplied does not match the ParamType. The DTSParamValue found is not of type EnumValue.|  
|0xC0029234|-1073573324|DTS_E_VALUE_WEBSERVICETASK_NOT_COMPLEX|The WebMethodInfo specified is not correct. The ParamValue supplied does not match the ParamType. The DTSParamValue found is not of type ComplexValue.|  
|0xC0029235|-1073573323|DTS_E_WEBSERVICETASK_VALUE_NOT_ARRAY|The WebMethodInfo specified is not correct. The ParamValue supplied does not match the ParamType. The DTSParamValue found is not of type ArrayValue.|  
|0xC0029236|-1073573322|DTS_E_WEBSERVICETASK_TYPE_NOT_PRIMITIVE|The WebMethodInfo you have specified is wrong. "%1" is not Primitive Type.|  
|0xC0029237|-1073573321|DTS_E_WEBSERVICETASK_ARRAY_VALUE_INVALID|The format of the ArrayValue is not valid. There should be at least one element in the array.|  
|0xC0029238|-1073573320|DTS_E_WEBSERVICETASK_SELECTED_VALUE_NULL|The value of the enumeration cannot be null. Select a default value for the enumeration.|  
|0xC0029239|-1073573319|DTS_E_WEBSERVICETASK_NULL_VALUE|Cannot validate a null against any datatype.|  
|0xC002923A|-1073573318|DTS_E_WEBSERVICETASK_ENUM_VALUE_NOT_FOUND|The enumeration Value is not correct.|  
|0xC002923B|-1073573317|DTS_E_WEBSERVICETASK_PROP_NOT_EXISTS|The class specified does not contain a public property by the name "%1".|  
|0xC002923C|-1073573316|DTS_E_WEBSERVICETASK_CONVERT_FAILED|Could not convert "%1" to "%2".|  
|0xC002923D|-1073573315|DTS_E_WEBSERVICETASK_CLEANUP_FAILED|Cleanup failed. The proxy that was created for the web service may not have been deleted.|  
|0xC002923E|-1073573314|DTS_E_WEBSERVICETASK_CREATE_INSTANCE_FAILED|Could not create an object of type "%1". Please check whether the default constructor exists.|  
|0xC002923F|-1073573313|DTS_E_WEBSERVICETASK_NOT_PRIMITIVE_TYPE|"%1" is not a value type.|  
|0xC0029240|-1073573312|DTS_E_WEBSERVICETASK_ERROR_IN_VALIDATE|Could not validate "%1" against "%1".|  
|0xC0029241|-1073573311|DTS_E_WEBSERVICETASK_DATATYPE_NULL|The data type cannot be null. Specify the value of the data type to validate.|  
|0xC0029242|-1073573310|DTS_E_WEBSERVICETASK_INDEX_OUT_OF_BOUNDS|The ParamValue cannot be inserted at this position. The index specified might be lesser than zero or greater than the length.|  
|0xC0029243|-1073573309|DTS_E_WEBSERVICETASK_WRONG_WSDL|The input WSDL file is not valid.|  
|0xC0029244|-1073573308|DTS_E_WMIDRTASK_SYNCOBJECTFAILED|Synchronization object failed.|  
|0xC0029245|-1073573307|DTS_E_WMIDRTASK_MISSINGWQLQUERY|The WQL query is missing.|  
|0xC0029246|-1073573306|DTS_E_WMIDRTASK_DESTINATIONMUSTBESET|The destination must be set.|  
|0xC0029247|-1073573305|DTS_E_WMIDRTASK_MISSINGCONNECTION|No WMI connection is set.|  
|0xC0029248|-1073573304|DTS_E_WMIDRTASK_INVALIDDATANODE|WMI Data Reader Task received an invalid task data node.|  
|0xC0029249|-1073573303|DTS_E_WMIDRTASK_FAILEDVALIDATION|The task failed validation.|  
|0xC002924A|-1073573302|DTS_E_WMIDRTASK_FILEDOESNOTEXIST|File "%1" does not exist.|  
|0xC002924B|-1073573301|DTS_E_WMIDRTASK_CONNECTIONMNGRDOESNTEXIST|Connection manager "%1" does not exist.|  
|0xC002924C|-1073573300|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRINGOROBJECT|Variable "%1" is not of type string or object.|  
|0xC002924D|-1073573299|DTS_E_WMIDRTASK_CONNECTIONTYPENOTFILE|Connection "%1" is not of type "FILE".|  
|0xC002924E|-1073573298|DTS_E_WMIDRTASK_CONNECTIONTYPENOTWMI|Connection "%1" is not of type "WMI".|  
|0xC002924F|-1073573297|DTS_E_WMIDRTASK_FILEALREADYEXISTS|File "%1" already exists.|  
|0xC0029250|-1073573296|DTS_E_WMIDRTASK_CONNECTIONMANAGEREMPTY|Connection manager "%1" is empty.|  
|0xC0029251|-1073573295|DTS_E_WMIDRTASK_VARNOTOBJECT|Variable "%1" should be of type object to be assigned a data table.|  
|0xC0029252|-1073573294|DTS_E_WMIDRTASK_TASKFAILURE|Task failed due to invalid WMI query: "%1".|  
|0xC0029253|-1073573293|DTS_E_WMIDRTASK_CANTWRITETOVAR|Unable to write to variable "%1" since it set to keep its original value.|  
|0xC0029254|-1073573292|DTS_E_WMIEWTASK_SYNCOBJECTFAILED|Synchronization object failed.|  
|0xC0029255|-1073573291|DTS_E_WMIEWTASK_MISSINGWQLQUERY|The WQL query is missing.|  
|0xC0029256|-1073573290|DTS_E_WMIEWTASK_MISSINGCONNECTION|The WMI connection is missing.|  
|0xC0029257|-1073573289|DTS_E_WMIEWTASK_QUERYFAILURE|The task failed to execute the WMI query.|  
|0xC0029258|-1073573288|DTS_E_WMIEWTASK_INVALIDDATANODE|The WMI Event Watcher Task received a task data node that is not valid.|  
|0xC0029259|-1073573287|DTS_E_WMIEWTASK_CONNECTIONMNGRDOESNTEXIST|Connection manager "%1" does not exist.|  
|0xC002925A|-1073573286|DTS_E_WMIEWTASK_FILEDOESNOTEXIST|File "%1" does not exist.|  
|0xC002925B|-1073573285|DTS_E_WMIEWTASK_VARIABLETYPEISNOTSTRING|Variable "%1" is not of type string.|  
|0xC002925C|-1073573284|DTS_E_WMIEWTASK_CONNECTIONTYPENOTFILE|Connection "%1" is not of type "FILE".|  
|0xC002925D|-1073573283|DTS_E_WMIEWTASK_CONNECTIONTYPENOTWMI|Connection "%1" is not of type "WMI".|  
|0xC002925E|-1073573282|DTS_E_WMIEWTASK_FILEALREADYEXISTS|File "%1" already exists.|  
|0xC002925F|-1073573281|DTS_E_WMIEWTASK_CONNECTIONMANAGEREMPTY|Connection manager "%1" is empty.|  
|0xC0029260|-1073573280|DTS_E_WMIEWTASK_TIMEOUTOCCURRED|Timeout of "%1" second(s) occurred before event represented by "%2".|  
|0xC0029261|-1073573279|DTS_E_WMIEWTASK_ERRMESSAGE|Watching for the Wql query caused the following system exception: "%1". Check the query for errors or WMI connection for access rights/permissions.|  
|0xC0029262|-1073573278|DTS_E_XMLTASK_NODEFAULTOPERTION|The Operations specified is not defined.|  
|0xC0029263|-1073573277|DTS_E_XMLTASK_CONNECTIONTYPENOTFILE|The connection type is not File.|  
|0xC0029264|-1073573276|DTS_E_XMLTASK_CANTGETREADERFROMSOURCE|Cannot get an XmlReader from the source XML document.|  
|0xC0029265|-1073573275|DTS_E_XMLTASK_CANTGETREADERFROMDEST|Cannot get an XmlReader from the changed XML document.|  
|0xC0029266|-1073573274|DTS_E_XMLTASK_CANTGETREADERFROMDIFFGRAM|Cannot get the XDL diffgram reader from the XDL diffgram XML.|  
|0xC0029268|-1073573272|DTS_E_XMLTASK_EMPTYNODELIST|The node list is empty.|  
|0xC0029269|-1073573271|DTS_E_XMLTASK_NOELEMENTFOUND|The element was not found.|  
|0xC002926A|-1073573270|DTS_E_XMLTASK_UNDEFINEDOPERATION|The Operations specified is not defined.|  
|0xC002926B|-1073573269|DTS_E_XMLTASK_XPATHNAVERROR|Unexpected content item in XPathNavigator.|  
|0xC002926C|-1073573268|DTS_E_XMLTASK_NOSCHEMAFOUND|No schema found to enforce validation.|  
|0xC002926D|-1073573267|DTS_E_XMLTASK_VALIDATIONERROR|A validation error occurred when validating the instance document.|  
|0xC002926E|-1073573266|DTS_E_XMLTASK_SYNCOBJECTFAILED|Synchronization object failed.|  
|0xC002926F|-1073573265|DTS_E_XMLTASK_ROOTNOODESNOTMATCHED|The root nodes do not match.|  
|0xC0029270|-1073573264|DTS_E_XMLTASK_INVALIDEDITSCRIPT|The Edit Script Operation type in the final Edit Script is not valid.|  
|0xC0029271|-1073573263|DTS_E_XMLTASK_CDATANODESISSUE|CDATA nodes should be added with DiffgramAddSubtrees class.|  
|0xC0029272|-1073573262|DTS_E_XMLTASK_COMMENTSNODEISSUE|Comment nodes should be added with DiffgramAddSubtrees class.|  
|0xC0029273|-1073573261|DTS_E_XMLTASK_TEXTNODEISSUES|Text nodes should be added with DiffgramAddSubtrees class.|  
|0xC0029274|-1073573260|DTS_E_XMLTASK_WHITESPACEISSUE|Significant white space nodes should be added with DiffgramAddSubtrees class.|  
|0xC0029275|-1073573259|DTS_E_XMLTASK_DIFFENUMISSUE|Correct the OperationCost array so that it reflects the XmlDiffOperation enumeration.|  
|0xC0029276|-1073573258|DTS_E_XMLTASK_TASKISEMPTY|There are no operations in the task.|  
|0xC0029277|-1073573257|DTS_E_XMLTASK_DOCUMENTHASDATA|The document already contains data and should not be used again.|  
|0xC0029278|-1073573256|DTS_E_XMLTASK_INVALIDENODETYPE|The node type is not valid.|  
|0xC0029279|-1073573255|DTS_E_XMLTASK_INVALIDDATANODE|The XML Task received a task data node that is not valid.|  
|0xC002927B|-1073573253|DTS_E_XMLTASK_VARIABLETYPEISNOTSTRING|Variable data type is not a String.|  
|0xC002927C|-1073573252|DTS_E_XMLTASK_COULDNOTGETENCODINGFROMDOCUMENT|Cannot get encoding from XML.|  
|0xC002927D|-1073573251|DTS_E_XMLTASK_MISSINGSOURCE|Source is not specified.|  
|0xC002927E|-1073573250|DTS_E_XMLTASK_MISSINGSECONDOPERAND|Second operand is not specified.|  
|0xC002927F|-1073573249|DTS_E_XMLTASK_INVALIDPATHDESCRIPTOR|Invalid XDL diffgram. "%1" is an invalid path descriptor.|  
|0xC0029280|-1073573248|DTS_E_XMLTASK_NOMATCHINGNODE|Invalid XDL diffgram. No node matches the path descriptor "%1".|  
|0xC0029281|-1073573247|DTS_E_XMLTASK_EXPECTINGDIFFGRAMELEMENT|Invalid XDL diffgram. Expecting xd:xmldiff as a root element with namespace URI "%1".|  
|0xC0029282|-1073573246|DTS_E_XMLTASK_MISSINGSRCDOCATTRIBUTE|The XDL diffgram is not valid. The srcDocHash attribute on the xd:xmldiff element is missing.|  
|0xC0029283|-1073573245|DTS_E_XMLTASK_MISSINGOPTIONSATTRIBUTE|The XDL diffgram is not valid. The options attribute on the xd:xmldiff element is missing.|  
|0xC0029284|-1073573244|DTS_E_XMLTASK_INVALIDSRCDOCATTRIBUTE|The XDL diffgram is not valid. The srcDocHash attribute has an invalid value.|  
|0xC0029285|-1073573243|DTS_E_XMLTASK_INVALIDOPTIONSATTRIBUTE|The XDL diffgram is not valid. The options attribute has an invalid value.|  
|0xC0029286|-1073573242|DTS_E_XMLTASK_SRCDOCMISMATCH|The XDL diffgram is not applicable to this XML document. The rcDocHash value does not match.|  
|0xC0029287|-1073573241|DTS_E_XMLTASK_MORETHANONENODEMATCHED|Invalid XDL diffgram; more than one node matches the "%1" path descriptor on the xd:node or xd:change element.|  
|0xC0029288|-1073573240|DTS_E_XMLTASK_XMLDECLMISMATCH|The XDL diffgram is not applicable to this XML document. A new XML declaration cannot be added.|  
|0xC0029289|-1073573239|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODEINLIST|Internal Error. XmlDiffPathSingleNodeList can contain only one node.|  
|0xC002928A|-1073573238|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODELEFT|Internal Error. "%1" nodes left after patch, expecting 1.|  
|0xC002928B|-1073573237|DTS_E_XMLTASK_XSLTRESULTFILEISNOTXML|The File/Text Produced by the XSLT is not a valid XmlDocument, thus can not be set as result of operation: "%1".|  
|0xC002928E|-1073573234|DTS_E_XMLTASK_FILEDOESNOTEXIST|There is no file associated with connection "%1".|  
|0xC002928F|-1073573233|DTS_E_XMLTASK_XMLTEXTEMPTY|Property "%1" has no source Xml text; Xml Text is either invalid, null or empty string.|  
|0xC0029290|-1073573232|DTS_E_XMLTASK_FILEALREADYEXISTS|File "%1" already exists.|  
|0xC0029293|-1073573229|DTS_E_TRANSFERTASKS_SRCCONNECTIONREQUIRED|A source connection must be specified.|  
|0xC0029294|-1073573228|DTS_E_TRANSFERTASKS_DESTCONNECTIONREQUIRED|A destination connection must be specified.|  
|0xC0029295|-1073573227|DTS_E_TRANSFERTASKS_CONNECTIONNOTFOUND|The connection "%1" could not be found in the package.|  
|0xC0029296|-1073573226|DTS_E_TRANSFERTASKS_SERVERVERSIONNOTALLOWED|The connection "%1" specifies a SQL Server instance with a version that is not supported for transfer.  Only versions 7, 2000, and 2005 are supported.|  
|0xC0029297|-1073573225|DTS_E_TRANSFERTASKS_SRCSERVERLESSEQUALDESTSERVER|The source connection "%1" must specify a SQL Server instance with a version earlier than or the same as the destination connection "%2".|  
|0xC0029298|-1073573224|DTS_E_TRANSFERTASKS_SRCDBREQUIRED|A source database must be specified.|  
|0xC0029299|-1073573223|DTS_E_TRANSFERTASKS_SRCDBMUSTEXIST|The source database "%1" must exist on the source server.|  
|0xC002929A|-1073573222|DTS_E_TRANSFERTASKS_DESTDBREQUIRED|A destination database must be specified.|  
|0xC002929B|-1073573221|DTS_E_TRANSFERTASKS_SRCDBANDDESTDBTHESAME|The source database and the destination database can not be the same.|  
|0xC002929C|-1073573220|DTS_E_TRANSFERDBTASK_FILENAMEREQUIRED|The transfer file information %1 is missing the filename.|  
|0xC002929D|-1073573219|DTS_E_TRANSFERDBTASK_FOLDERREQUIRED|The transfer file information %1 is missing the folder part.|  
|0xC002929E|-1073573218|DTS_E_TRANSFERTASKS_NETSHAREREQUIRED|The transfer file information %1 is missing the network share part.|  
|0xC002929F|-1073573217|DTS_E_TRANSFERTASKS_FILELISTSCOUNTMISMATCH|The number of source transfer files and the number of destination transfer files must be the same.|  
|0xC00292A0|-1073573216|DTS_E_DOESNOTSUPPORTTRANSACTIONS|Enlisting in transactions is not supported.|  
|0xC00292A1|-1073573215|DTS_E_TRANSFERDBTASK_OFFLINEERROR|The following exception occurred during an offline database transfer: %1.|  
|0xC00292A2|-1073573214|DTS_E_TRANSFERDBTASK_NETSHAREDOESNOTEXIST|The network share "%1" could not be found.|  
|0xC00292A3|-1073573213|DTS_E_TRANSFERDBTASK_NETSHARENOACCESS|The network share "%1 could not be accessed.  The error is: %2.|  
|0xC00292A4|-1073573212|DTS_E_TRANSFERDBTASK_USERMUSTBEDBOORSYSADMIN|The user "%1" must be a DBO or a sysadmin for "%2" in order to perform an online database transfer.|  
|0xC00292A5|-1073573211|DTS_E_TRANSFERDBTASK_USERMUSTBESYSADMIN|The user "%1" must be a sysadmin on "%2" to perform an offline database transfer.|  
|0xC00292A6|-1073573210|DTS_E_TRANSFERDBTASK_FTCATALOGSOFFLINEYUKONONLY|Full text catalogs can only be included when performing an offline database transfer between 2 SQL Server 2005 servers.|  
|0xC00292A7|-1073573209|DTS_E_TRANSFERDBTASK_NOOVERWRITEDB|The database "%1" already exists on the destination server "%2".|  
|0xC00292A8|-1073573208|DTS_E_TRANSFERDBTASK_MUSTHAVESOURCEFILES|At least one source file must be specified.|  
|0xC00292A9|-1073573207|DTS_E_TRANSFERDBTASKS_SRCFILENOTFOUND|Could not find the file "%1" in the source database "%2".|  
|0xC00292B3|-1073573197|DTS_E_MSMQTASK_FIPS1402COMPLIANCE|The operation requested is not allowed in systems compliant with U.S. FIPS 140-2.|  
|0xC002F210|-1073548784|DTS_E_SQLTASK_ERROREXECUTINGTHEQUERY|Executing the query "%1" failed with the following error: "%2". Possible failure reasons: Problems with the query, "ResultSet" property not set correctly, parameters not set correctly, or connection not established correctly.|  
|0xC002F300|-1073548544|DTS_E_TRANSFERSPTASK_ERRORREADINGSPNAMES|Error reading stored procedure names from the xml file.|  
|0xC002F301|-1073548543|DTS_E_TRANSFERSPTASK_INVALIDDATANODE|Invalid data node for the Transfer Stored Procedure task.|  
|0xC002F302|-1073548542|DTS_E_TRANSFERTASKS_CONNECTIONTYPEISNOTSMOSERVER|Connection "%1" is not of type "SMOServer".|  
|0xC002F303|-1073548541|DTS_E_TRANSFERSPTASK_EXECUTIONFAILED|Execution failed with the following error "%1".|  
|0xC002F304|-1073548540|DTS_E_ERROROCCURREDWITHFOLLOWINGMESSAGE|An error occurred with the following error message: "%1".|  
|0xC002F305|-1073548539|DTS_E_BITASK_EXECUTION_FAILED|Bulk insert execution failed.|  
|0xC002F306|-1073548538|DTS_E_FSTASK_INVALIDDESTPATH|Invalid destination path.|  
|0xC002F307|-1073548537|DTS_E_FSTASK_CANTCREATEDIR|Can not create directory. User chose to fail the task if directory exists.|  
|0xC002F308|-1073548536|DTS_E_SQLTASK_ODBCNOSUPPORTTRANSACTION|The task has a transaction option of "Required" and connection "%1" is of type "ODBC". ODBC connections don't support transactions.|  
|0xC002F309|-1073548535|DTS_E_SQLTASK_ERRORASSIGINGVALUETOVAR|An error occurred while assigning a value to variable "%1": "%2".|  
|0xC002F30A|-1073548534|DTS_E_FSTASK_SOURCEISEMPTY|The source is empty.|  
|0xC002F30B|-1073548533|DTS_E_FSTASK_DESTINATIONISEMPTY|The destination is empty.|  
|0xC002F30C|-1073548532|DTS_E_FSTASK_FILEDIRNOTFOUND|File or directory "%1" does not exist.|  
|0xC002F30D|-1073548531|DTS_E_FSTASK_VARSRCORDESTISEMPTY|Variable "%1" is used as a source or destination and is empty.|  
|0xC002F30E|-1073548530|DTS_E_FSTASK_FILEDELETED|File or directory "%1" was deleted.|  
|0xC002F30F|-1073548529|DTS_E_FSTASK_DIRECTORYDELETED|Directory "%1" was deleted.|  
|0xC002F310|-1073548528|DTS_E_WMIDRTASK_VARIABLETYPEISNOTOBJECT|The variable "%1" should be of type object to be assigned a data table.|  
|0xC002F311|-1073548527|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRING|The variable "%1" does not have a string data type.|  
|0xC002F312|-1073548526|DTS_E_FTPTASK_CANNOTACQUIRECONNECTION|There was an error acquiring the FTP connection. Verify that a valid connection type is specified in "%1".|  
|0xC002F313|-1073548525|DTS_E_FTPTASK_CONNECTIONNOTFOUND|The FTP connection manager "%1" can not be found.|  
|0xC002F314|-1073548524|DTS_E_FTPTASK_FILEUSAGETYPEERROR|File usage type of connection "%1" should be "%2" for operation "%3".|  
|0xC002F315|-1073548523|DTS_E_TRANSFERTASKS_SOURCECANTBESAMEASDESTINATION|The source server can not be the same as the destination server.|  
|0xC002F316|-1073548522|DTS_E_ERRMSGTASK_EMPTYSOURCELIST|There are no Error Messages to transfer.|  
|0xC002F317|-1073548521|DTS_E_ERRMSGTASK_DIFFERENTMESSAGEANDLANGUAGESIZES|The lists of error messages and their corresponding languages are of different sizes.|  
|0xC002F318|-1073548520|DTS_E_ERRMSGTASK_ERRORMESSAGEOUTOFRANGE|The error message id "%1" is out of the allowed range of user defined error messages. User defined error message ids are between 50000 and 2147483647.|  
|0xC002F319|-1073548519|DTS_E_TRANSFERTASKS_NOTRANSACTIONSUPPORT|This task can not participate in a transaction.|  
|0xC002F320|-1073548512|DTS_E_ERRMSGTASK_FAILEDTOTRANSFERERRORMESSAGES|Failed to transfer some or all of the Error Messages.|  
|0xC002F321|-1073548511|DTS_E_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|The error message "%1" already exists at destination server.|  
|0xC002F324|-1073548508|DTS_E_ERRMSGTASK_ERRORMESSAGECANTBEFOUND|The error message "%1" can not be found at source server.|  
|0xC002F325|-1073548507|DTS_E_TRANSFERTASKS_EXECUTIONFAILED|Execution failed with the following error: "%1".|  
|0xC002F327|-1073548505|DTS_E_JOBSTASK_FAILEDTOTRANSFERJOBS|Failed to transfer the Job(s).|  
|0xC002F330|-1073548496|DTS_E_JOBSTASK_EMPTYSOURCELIST|There are no Jobs to transfer.|  
|0xC002F331|-1073548495|DTS_E_JOBSTASK_JOBEXISTSATDEST|The job "%1" already exists at destination server.|  
|0xC002F334|-1073548492|DTS_E_JOBSTASK_JOBCANTBEFOUND|The job "%1" can not be found at source server.|  
|0xC002F337|-1073548489|DTS_E_LOGINSTASK_EMPTYLIST|The list of "Logins" to transfer is empty.|  
|0xC002F338|-1073548488|DTS_E_LOGINSTASK_CANTGETLOGINSNAMELIST|Can not get the list of "Logins" from source server.|  
|0xC002F340|-1073548480|DTS_E_LOGINSTASK_ERRORLOGINEXISTS|Login "%1" already exists at destination server.|  
|0xC002F342|-1073548478|DTS_E_LOGINSTASK_LOGINNOTFOUND|Login "%1" does not exist at source.|  
|0xC002F344|-1073548476|DTS_E_LOGINSTASK_FAILEDTOTRANSFERLOGINS|Failed to transfer some or all of the logins.|  
|0xC002F345|-1073548475|DTS_E_STOREDPROCSTASK_FAILEDTOTRANSFERSPS|Failed to transfer the stored procedure(s). More informative error should have been raised.|  
|0xC002F346|-1073548474|DTS_E_STOREDPROCSTASK_STOREDPROCNOTFOUND|Stored Procedure "%1" is not found at the source.|  
|0xC002F349|-1073548471|DTS_E_STOREDPROCSTASK_ERRORSTOREDPROCEDUREEXISTS|Stored procedure "%1" already exists at destination server.|  
|0xC002F350|-1073548464|DTS_E_STOREDPROCSTASK_EMPTYSOURCELIST|There are no stored procedures to transfer.|  
|0xC002F353|-1073548461|DTS_E_TRANSOBJECTSTASK_FAILEDTOTRANSFEROBJECTS|Failed to transfer the object(s).|  
|0xC002F354|-1073548460|DTS_E_TRANSOBJECTSTASK_EMPTYLIST|The list of "Objects" to transfer is empty.|  
|0xC002F355|-1073548459|DTS_E_TRANSOBJECTSTASK_NOSPATSOURCE|Stored procedure "%1" does not exist at the source.|  
|0xC002F356|-1073548458|DTS_E_TRANSOBJECTSTASK_SPALREADYATDEST|Stored procedure "%1" already exists at destination.|  
|0xC002F357|-1073548457|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSPS|An error occurred while trying to get set the Stored Procedures list to transfer: "%1".|  
|0xC002F359|-1073548455|DTS_E_TRANSOBJECTSTASK_NORULEATSOURCE|Rule "%1" does not exist at the source.|  
|0xC002F360|-1073548448|DTS_E_TRANSOBJECTSTASK_RULEALREADYATDEST|Rule "%1" already exists at destination.|  
|0xC002F361|-1073548447|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGRULES|An error occurred while trying to get set the Rules list to transfer: "%1".|  
|0xC002F363|-1073548445|DTS_E_TRANSOBJECTSTASK_NOTABLEATSOURCE|Table "%1" does not exist at the source.|  
|0xC002F364|-1073548444|DTS_E_TRANSOBJECTSTASK_TABLEALREADYATDEST|Table "%1" already exists at destination.|  
|0xC002F365|-1073548443|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTABLES|An error occurred while trying to get set the Tables list to transfer: "%1".|  
|0xC002F367|-1073548441|DTS_E_TRANSOBJECTSTASK_NOVIEWATSOURCE|View "%1" does not exist at the source.|  
|0xC002F368|-1073548440|DTS_E_TRANSOBJECTSTASK_VIEWALREADYATDEST|View "%1" already exists at destination.|  
|0xC002F369|-1073548439|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGVIEWS|An error occurred while trying to get set the Views list to transfer: "%1".|  
|0xC002F371|-1073548431|DTS_E_TRANSOBJECTSTASK_NOUDFATSOURCE|User Defined Function "%1" does not exist at the source.|  
|0xC002F372|-1073548430|DTS_E_TRANSOBJECTSTASK_UDFALREADYATDEST|User Defined Function "%1" already exists at destination.|  
|0xC002F373|-1073548429|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDFS|An error occurred while trying to get set the User Defined Functions list to transfer: "%1".|  
|0xC002F375|-1073548427|DTS_E_TRANSOBJECTSTASK_NODEFAULTATSOURCE|Default "%1" does not exist at the source.|  
|0xC002F376|-1073548426|DTS_E_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|Default "%1" already exists at destination.|  
|0xC002F377|-1073548425|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGDEFAULTS|An error occurred while trying to get set the Defaults list to transfer: "%1".|  
|0xC002F379|-1073548423|DTS_E_TRANSOBJECTSTASK_NOUDDTATSOURCE|User Defined Data Type "%1" does not exist at the source.|  
|0xC002F380|-1073548416|DTS_E_TRANSOBJECTSTASK_UDDTALREADYATDEST|User Defined Data Type "%1" already exists at destination.|  
|0xC002F381|-1073548415|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDDTS|An error occurred while trying to get set the User Defined Data Types list to transfer: "%1".|  
|0xC002F383|-1073548413|DTS_E_TRANSOBJECTSTASK_NOPFATSOURCE|Partition Function "%1" does not exist at the source.|  
|0xC002F384|-1073548412|DTS_E_TRANSOBJECTSTASK_PFALREADYATDEST|Partition Function "%1" already exists at destination.|  
|0xC002F385|-1073548411|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPFS|An error occurred while trying to get set the Partition Functions list to transfer: "%1".|  
|0xC002F387|-1073548409|DTS_E_TRANSOBJECTSTASK_NOPSATSOURCE|Partition Scheme "%1" does not exist at the source.|  
|0xC002F388|-1073548408|DTS_E_TRANSOBJECTSTASK_PSALREADYATDEST|Partition Scheme "%1" already exists at destination.|  
|0xC002F389|-1073548407|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPSS|An error occurred while trying to get set the Partition Schemes list to transfer: "%1".|  
|0xC002F391|-1073548399|DTS_E_TRANSOBJECTSTASK_NOSCHEMAATSOURCE|Schema "%1" does not exist at the source.|  
|0xC002F392|-1073548398|DTS_E_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|Schema "%1" already exists at destination.|  
|0xC002F393|-1073548397|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSCHEMAS|An error occurred while trying to get set the Schemas list to transfer: "%1".|  
|0xC002F395|-1073548395|DTS_E_TRANSOBJECTSTASK_NOSQLASSEMBLYATSOURCE|SqlAssembly "%1" does not exist at the source.|  
|0xC002F396|-1073548394|DTS_E_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|SqlAssembly "%1" already exists at destination.|  
|0xC002F397|-1073548393|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSQLASSEMBLIES|An error occurred while trying to get set the SqlAssemblies list to transfer: "%1".|  
|0xC002F399|-1073548391|DTS_E_TRANSOBJECTSTASK_NOAGGREGATEATSOURCE|User Defined Aggregate "%1" does not exist at the source.|  
|0xC002F400|-1073548288|DTS_E_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|User Defined Aggregate "%1" already exists at destination.|  
|0xC002F401|-1073548287|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGAGGREGATES|An error occurred while trying to get set the User Defined Aggregates list to transfer: "%1".|  
|0xC002F403|-1073548285|DTS_E_TRANSOBJECTSTASK_NOTYPEATSOURCE|User Defined Type "%1" does not exist at the source.|  
|0xC002F404|-1073548284|DTS_E_TRANSOBJECTSTASK_TYPEALREADYATDEST|User Defined Type "%1" already exists at destination.|  
|0xC002F405|-1073548283|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTYPES|An error occurred while trying to get set the User Defined Types list to transfer: "%1".|  
|0xC002F407|-1073548281|DTS_E_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONATSOURCE|XmlSchemaCollection "%1" does not exist at the source.|  
|0xC002F408|-1073548280|DTS_E_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|XmlSchemaCollection "%1" already exists at destination.|  
|0xC002F409|-1073548279|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGXMLSCHEMACOLLECTIONS|An error occurred while trying to get set the XmlSchemaCollections list to transfer: "%1".|  
|0xC002F411|-1073548271|DTS_E_TRANSOBJECTSTASK_SUPPORTEDONYUKONONLY|Objects of type "%1" are only supported between SQL Server 2005 or newer servers.|  
|0xC002F413|-1073548269|DTS_E_LOGINSTASK_EMPTYDATABASELIST|The databases list is empty.|  
|0xC002F414|-1073548268|DTS_E_TRANSOBJECTSTASK_NOLOGINATSOURCE|Login "%1" does not exist at the source.|  
|0xC002F416|-1073548266|DTS_E_TRANSOBJECTSTASK_LOGINALREADYATDEST|Login "%1" already exists at destination.|  
|0xC002F417|-1073548265|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGLOGINS|An error occurred while trying to get set the Logins list to transfer: "%1".|  
|0xC002F419|-1073548263|DTS_E_TRANSOBJECTSTASK_NOUSERATSOURCE|User "%1" does not exist at the source.|  
|0xC002F41B|-1073548261|DTS_E_TRANSOBJECTSTASK_USERALREADYATDEST|User "%1" already exists at destination.|  
|0xC002F41C|-1073548260|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUSERS|An error occurred while trying to get set the Users list to transfer: "%1".|  
|0xC002F41F|-1073548257|DTS_E_BITASK_CANNOTRETAINCONNINTRANSACTION|The task can not have a retained connection manager in a transaction.|  
|0xC002F421|-1073548255|DTS_E_SQLTASKOUTPUTENCODINGNOTSUPPORTED|Unable to obtain XML data from SQL Server as Unicode because the provider does not support the OUTPUTENCODING property.|  
|0xC002F426|-1073548250|DTS_E_FTPTASK_FILECONNECTIONNOTFOUND|For the FTP operation "%1", the FILE connection manager "%2" can not be found.|  
|0xC002F428|-1073548248|DTS_E_TRANSOBJECTSTASK_CANNOTDROPOBJECTS|"Logins" are server level objects and can not be dropped first since the source and destination are the same server. Dropping objects first will remove the logins from the source as well.|  
|0xC002F429|-1073548247|DTS_E_SQLTASK_PARAMSIZEERROR|Parameter "%1" cannot be negative. (-1) is used for the default value.|  
|0xC0040019|-1073479655|DTS_E_UNREGISTEREDPIPELINEXML_LOAD|Data Flow objects cannot be loaded. Check if Microsoft.SqlServer.PipelineXml.dll is properly registered.|  
|0xC0040020|-1073479648|DTS_E_UNREGISTEREDPIPELINEXML_SAVE|Data Flow objects cannot be saved. Check if Microsoft.SqlServer.PipelineXml.dll is properly registered.|  
|0xC0040040|-1073479616|DTS_E_PIPELINE_SAVE|Failed to save Data Flow objects.|  
|0xC0040041|-1073479615|DTS_E_PIPELINE_LOAD|Failed to load Data Flow objects|  
|0xC0040042|-1073479614|DTS_E_SAVE_PERSTFORMAT|Failed to save Data Flow objects. The specified format is not supported.|  
|0xC0040043|-1073479613|DTS_E_LOAD_PERSTFORMAT|Failed to load Data Flow objects. The specified format is not supported.|  
|0xC0040044|-1073479612|DTS_E_SETPERSIST_PROPEVENTS|Failed to set the XML persistence events property for the Data Flow objects.|  
|0xC0040045|-1073479611|DTS_E_SETPERSIST_XMLDOM|Failed to set the persistence XML DOM property for the Data Flow objects.|  
|0xC0040046|-1073479610|DTS_E_SETPERSIST_XMLNODE|Failed to set the persistence XML ELEMENT property for the Data Flow objects.|  
|0xC0040047|-1073479609|DTS_E_SETPERSISTPROP_FAILED|Failed to set xml persistence properties for the Data Flow objects.|  
|0xC0040048|-1073479608|DTS_E_NOCUSTOMPROPCOL|Failed to get custom property collection for Data Flow components.|  
|0xC0047000|-1073451008|DTS_E_CYCLEINEXECUTIONTREE|An execution tree contains a cycle.|  
|0xC0047001|-1073451007|DTS_E_DISCONNECTEDOBJECT|The %1 object "%2" (%3!d!) is disconnected from the layout.|  
|0xC0047002|-1073451006|DTS_E_INVALIDOBJECTID|The ID for the layout object is not valid.|  
|0xC0047003|-1073451005|DTS_E_INPUTWITHOUTPATHS|A required input object is not connected to a path object.|  
|0xC0047005|-1073451003|DTS_E_INVALIDSYNCHRONOUSINPUT|%1 has an invalid synchronous input ID %2!d!.|  
|0xC0047006|-1073451002|DTS_E_INVALIDOUTPUTLINEAGEID|%1 has lineage ID %2!d!, but should have had %3!d!.|  
|0xC0047008|-1073451000|DTS_E_DUPLICATENAMESINCOLLECTION|The package contains two objects with the duplicate name of "%1" and "%2".|  
|0xC0047009|-1073450999|DTS_E_INVALIDEXCLUSIONGROUP|The "%1" and the "%2" are in the same exclusion group, but they do not have the same synchronous input.|  
|0xC004700A|-1073450998|DTS_E_DUPLICATELINEAGEIDSINCOLLECTION|Two objects in the same collection have a duplicate lineage ID of %1!d!. The objects are %2 and %3.|  
|0xC004700B|-1073450997|DTS_E_VALIDATIONFAILEDONLAYOUT|The layout failed validation.|  
|0xC004700C|-1073450996|DTS_E_VALIDATIONFAILEDONCOMPONENTS|One or more component failed validation.|  
|0xC004700D|-1073450995|DTS_E_VALIDATIONFAILED|The layout and one or more components failed validation.|  
|0xC004700E|-1073450994|DTS_E_THREADSTARTUPFAILED|The Data Flow task engine failed at startup because it cannot create one or more required threads.|  
|0xC004700F|-1073450993|DTS_E_CANTGETMUTEX|A thread failed to create a mutex at initialization.|  
|0xC0047010|-1073450992|DTS_E_CANTGETSEMAPHORE|A thread failed to create a semaphore at initialization.|  
|0xC0047011|-1073450991|DTS_E_BUFFERFAILUREDETAILS|The system reports %1!d! percent memory load. There are %2 bytes of physical memory with %3 bytes free. There are %4 bytes of virtual memory with %5 bytes free. The paging file has %6 bytes with %7 bytes free.|  
|0xC0047012|-1073450990|DTS_E_BUFFERALLOCFAILED|A buffer failed while allocating %1!d! bytes.|  
|0xC0047013|-1073450989|DTS_E_CANTCREATEBUFFERMANAGER|The Buffer Manager could not be created.|  
|0xC0047015|-1073450987|DTS_E_BUFFERBADSIZE|Buffer Type %1!d! had a size of %2!I64d! bytes.|  
|0xC0047016|-1073450986|DTS_E_DANGLINGWITHPATH|%1 is marked as dangling, but has a path attached to it.|  
|0xC0047017|-1073450985|DTS_E_INDIVIDUALVALIDATIONFAILED|%1 failed validation and returned error code 0x%2!8.8X!.|  
|0xC0047018|-1073450984|DTS_E_INDIVIDUALPOSTEXECUTEFAILED|%1 failed the post-execute phase and returned error code 0x%2!8.8X!.|  
|0xC0047019|-1073450983|DTS_E_INDIVIDUALPREPAREFAILED|%1 failed the prepare phase and returned error code 0x%2!8.8X!.|  
|0xC004701A|-1073450982|DTS_E_INDIVIDUALPREEXECUTEFAILED|%1 failed the pre-execute phase and returned error code 0x%2!8.8X!.|  
|0xC004701B|-1073450981|DTS_E_INDIVIDUALCLEANUPFAILED|%1 failed the cleanup phase and returned error code 0x%2!8.8X!.|  
|0xC004701C|-1073450980|DTS_E_INVALIDINPUTLINEAGEID|%1 has lineage ID %2!d! that was not previously used in the Data Flow task.|  
|0xC004701E|-1073450978|DTS_E_EXECUTIONTREECYCLE|Cannot connect %1 to %2 because a cycle would be created.|  
|0xC004701F|-1073450977|DTS_E_CANTCOMPARE|The data type "%1" cannot be compared. Comparison of that data type is not supported, so it cannot be sorted or used as a key.|  
|0xC0047020|-1073450976|DTS_E_REFUSEDFORSHUTDOWN|This thread has shut down and is not accepting buffers for input.|  
|0xC0047021|-1073450975|DTS_E_THREADFAILED|SSIS Error Code DTS_E_THREADFAILED.  Thread "%1" has exited with error code 0x%2!8.8X!.  There may be error messages posted before this with more information on why the thread has exited.|  
|0xC0047022|-1073450974|DTS_E_PROCESSINPUTFAILED|SSIS Error Code DTS_E_PROCESSINPUTFAILED.  The ProcessInput method on component "%1" (%2!d!) failed with error code 0x%3!8.8X! while processing input "%4" (%5!d!). The identified component returned an error from the ProcessInput method. The error is specific to the component, but the error is fatal and will cause the Data Flow task to stop running.  There may be error messages posted before this with more information about the failure.|  
|0xC0047023|-1073450973|DTS_E_CANTREALIZEVIRTUALBUFFERS|A set of virtual buffers cannot be realized.|  
|0xC0047024|-1073450972|DTS_E_PIPELINETOOCOMPLEX|The number of threads required for this pipeline is %1!d!, which is more than the system limit of %2!d!. The pipeline requires too many threads as configured. There are either too many asynchronous outputs, or EngineThreads property is set too high. Split the pipeline into multiple packages, or reduce the value of the EngineThreads property.|  
|0xC0047028|-1073450968|DTS_E_SCHEDULERCOULDNOTCOUNTSOURCES|The Data Flow engine scheduler cannot obtain a count of the sources in the layout.|  
|0xC0047029|-1073450967|DTS_E_SCHEDULERCOULDNOTCOUNTDESTINATIONS|The Data Flow engine scheduler cannot obtain a count of the destinations in the layout.|  
|0xC004702A|-1073450966|DTS_E_COMPONENTVIEWISUNAVAILABLE|The component view is unavailable. Make sure the component view has been created.|  
|0xC004702B|-1073450965|DTS_E_INCORRECTCOMPONENTVIEWID|The component view ID is incorrect. The component view may be out of synchronization. Try releasing the component view and recreating it.|  
|0xC004702C|-1073450964|DTS_E_BUFFERNOTLOCKED|This buffer is not locked and cannot be manipulated.|  
|0xC004702D|-1073450963|DTS_E_CANTBUILDBUFFERTYPE|The Data Flow task cannot allocate memory to build a buffer definition. The buffer definition had %1!d! columns.|  
|0xC004702E|-1073450962|DTS_E_CANTREGISTERBUFFERTYPE|The Data Flow task cannot register a buffer type. The type had %1!d! columns and was for execution tree %2!d!.|  
|0xC004702F|-1073450961|DTS_E_INVALIDUSESDISPOSITIONSVALUE|The UsesDispositions property cannot be changed from its initial value. This occurs when the XML is edited and the UsesDispositions value is modified. This value is set by the component when it is added to the package and is not allowed to change.|  
|0xC0047030|-1073450960|DTS_E_THREADFAILEDINITIALIZE|The Data Flow task failed to initialize a required thread and cannot begin execution. The thread previously reported a specific error.|  
|0xC0047031|-1073450959|DTS_E_THREADFAILEDCREATE|The Data Flow task failed to create a required thread and cannot begin running. The usually occurs when there is an out-of-memory state.|  
|0xC0047032|-1073450958|DTS_E_EXECUTIONTREECYCLEADDINGSYNCHRONOUSINPUT|The synchronous input of "%1" cannot be set to "%2" because a cycle would be created.|  
|0xC0047033|-1073450957|DTS_E_INVALIDCUSTOMPROPERTYNAME|A custom property named "%1" is invalid because there is a stock property with that name. A custom property cannot have the same name as a stock property on the same object.|  
|0xC0047035|-1073450955|DTS_E_BUFFERLOCKUNDERFLOW|The buffer was already unlocked.|  
|0xC0047036|-1073450954|DTS_E_INDIVIDUALCACHEINTERFACESFAILED|%1 failed initialization and returned error code 0x%2!8.8X!.|  
|0xC0047037|-1073450953|DTS_E_INDIVIDUALRELEASEINTERFACESFAILED|%1 failed during shut down and returned error code 0x%2!8.8X!. A component failed to release its interfaces.|  
|0xC0047038|-1073450952|DTS_E_PRIMEOUTPUTFAILED|SSIS Error Code DTS_E_PRIMEOUTPUTFAILED.  The PrimeOutput method on %1 returned error code 0x%2!8.8X!.  The component returned a failure code when the pipeline engine called PrimeOutput(). The meaning of the failure code is defined by the component, but the error is fatal and the pipeline stopped executing.  There may be error messages posted before this with more information about the failure.|  
|0xC0047039|-1073450951|DTS_E_THREADCANCELLED|SSIS Error Code DTS_E_THREADCANCELLED.  Thread "%1" received a shutdown signal and is terminating. The user requested a shutdown, or an error in another thread is causing the pipeline to shutdown.  There may be error messages posted before this with more information on why the thread was cancelled.|  
|0xC004703A|-1073450950|DTS_E_DISTRIBUTORCANTSETPROPERTY|Distributor for thread "%1" failed to initialize property "%2" on component "%3" because of error 0x%8.8X. The distributor could not initialize the component's property and cannot continue running.|  
|0xC004703B|-1073450949|DTS_E_CANTREGISTERVIEWBUFFERTYPE|The Data Flow task cannot register a view buffer type. The type had %1!d! columns and was for input ID %2!d!.|  
|0xC004703F|-1073450945|DTS_E_CANTCREATEEXECUTIONTREE|There is not enough memory to create an execution tree.|  
|0xC0047040|-1073450944|DTS_E_CANTINSERTINTOHASHTABLE|There is not enough memory to insert an object into the hash table.|  
|0xC0047041|-1073450943|DTS_E_OBJECTNOTINHASHTABLE|The object is not in the hash table.|  
|0xC0047043|-1073450941|DTS_E_CANTCREATECOMPONENTVIEW|Cannot create a component view because another one already exists. Only one component view can exist at a time.|  
|0xC0047046|-1073450938|DTS_E_LAYOUTCANTSETUSAGETYPE|At input "%1" (%2!d!), the virtual input column collection does not contain a virtual input column with lineage ID %3!d!.|  
|0xC0047047|-1073450937|DTS_E_WRONGOBJECTTYPE|The requested object has the incorrect object type.|  
|0xC0047048|-1073450936|DTS_E_CANTCREATESPOOLFILE|The buffer manager cannot create a temporary storage file on any path in the BufferTempStoragePath property. There is an incorrect file name or no permission or the paths have been full.|  
|0xC0047049|-1073450935|DTS_E_SEEKFAILED|The buffer manager could not seek to offset %1!d! in file "%2". The file is damaged.|  
|0xC004704A|-1073450934|DTS_E_EXTENDFAILED|The buffer manager cannot extend the file "%1" to length %2!lu! bytes.  There was insufficient disk space.|  
|0xC004704B|-1073450933|DTS_E_FILEWRITEFAILED|The buffer manager cannot write %1!d! bytes to file "%2". There was insufficient disk space or quota.|  
|0xC004704C|-1073450932|DTS_E_FILEREADFAILED|The buffer manager cannot read %1!d! bytes from file "%2". The file is damaged.|  
|0xC004704D|-1073450931|DTS_E_VIRTUALNOTSEQUENTIAL|Buffer ID %1!d! supports other virtual buffers and cannot be placed into sequential mode. IDTSBuffer100.SetSequentialMode was called on a buffer that supports virtual buffers.|  
|0xC004704E|-1073450930|DTS_E_BUFFERISREADONLY|This operation could not be performed because buffer is in read-only mode. A read-only buffer cannot be modified.|  
|0xC004704F|-1073450929|DTS_E_EXECUTIONTREECYCLESETTINGID|ID %1 cannot be set to %2!d! because a cycle would be created.|  
|0xC0047050|-1073450928|DTS_E_NOMOREBUFFERTYPES|The buffer manager ran out of memory while trying to extend the table of buffer types. This is caused by an out-of-memory condition.|  
|0xC0047051|-1073450927|DTS_E_CANTCREATENEWTYPE|The buffer manager failed to create a new buffer type.|  
|0xC0047053|-1073450925|DTS_E_SCHEDULERBADTREE|The Data Flow engine scheduler failed to retrieve the execution tree with index %1!d! from the layout. The scheduler received a count containing more execution trees than actually exist.|  
|0xC0047056|-1073450922|DTS_E_CANTCREATEPRIMEOUTPUTBUFFER|The Data Flow task failed to create a buffer to call PrimeOutput for output "%3" (%4!d!) on component "%1" (%2!d!). This error usually occurs due to an out-of-memory condition.|  
|0xC0047057|-1073450921|DTS_E_SCHEDULERTHREADMEMORY|The Data Flow engine scheduler failed to create a thread object because not enough memory is available. This is caused by an out-of-memory condition.|  
|0xC004705A|-1073450918|DTS_E_SCHEDULEROBJECT|The Data Flow engine scheduler cannot retrieve object with ID %1!d! from the layout. The Data Flow engine scheduler previously located an object that is now no longer available.|  
|0xC004705B|-1073450917|DTS_E_PREPARETREENODEFAILED|The Data Flow task failed to prepare buffers for the execution tree node beginning at output "%1" (%2!d!).|  
|0xC004705C|-1073450916|DTS_E_CANTCREATEVIRTUALBUFFER|The Data Flow task cannot create a virtual buffer to prepare for execution.|  
|0xC004705E|-1073450914|DTS_E_NOMOREIDS|The maximum ID has been reached. There are no more IDs available to assign to objects.|  
|0xC004705F|-1073450913|DTS_E_ALREADYATTACHED|The %1 is already attached and cannot be attached again.  Detach it and try again.|  
|0xC0047060|-1073450912|DTS_E_OUTPUTCOLUMNNAMECONFLICT|Column name "%1" on output "%2" cannot be used because it conflicts with a column of the same name on synchronous input "%3".|  
|0xC0047061|-1073450911|DTS_E_EOFANNOUNCEMENTFAILED|The Data Flow task cannot to create a buffer to mark the end of the rowset.|  
|0xC0047062|-1073450910|DTS_E_USERCOMPONENTEXCEPTION|A managed user component has thrown exception "%1".|  
|0xC0047063|-1073450909|DTS_E_SCHEDULERMEMORY|The Data Flow engine scheduler cannot allocate enough memory for the execution structures. The system was low on memory before execution started.|  
|0xC0047064|-1073450908|DTS_E_BUFFERNOOBJECTMEMORY|An out-of-memory condition prevented the creation of the buffer object.|  
|0xC0047065|-1073450907|DTS_E_BUFFERNOMAPMEMORY|An out-of-memory condition prevents the mapping of a buffer's lineage IDs to DTP_HCOL indexes.|  
|0xC0047066|-1073450906|DTS_E_INDIVIDUALPUTVARIABLESFAILED|The "%1!s!" cannot cache the Variables collection and returned error code 0x%2!8.8X.|  
|0xC0047067|-1073450905|DTS_E_INDIVIDUALPUTCOMPONENTMETADATAFAILED|The "%1" failed to cache the component metadata object and returned error code 0x%2!8.8X!.|  
|0xC0047068|-1073450904|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITION|"%1" has a non-zero SortKeyPosition, but its value (%2!ld!) is too large. It must be less than or equal to the number of columns.|  
|0xC004706A|-1073450902|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITIONS|The IsSorted property of %1 is set to TRUE, but the absolute values of the non-zero output column SortKeyPositions do not form a monotonically increasing sequence, starting at one.|  
|0xC004706B|-1073450901|DTS_E_INDIVIDUALVALIDATIONSTATUSFAILED|"%1" failed validation and returned validation status "%2".|  
|0xC004706C|-1073450900|DTS_E_CANTCREATECOMPONENT|Component "%1!s!" could not be created and returned error code 0x%2!8.8X! "%3!s!". Make sure that the component is registered correctly.|  
|0xC004706D|-1073450899|DTS_E_COMPONENTNOTREGISTERED|The module containing "%1" is not registered or installed correctly.|  
|0xC004706E|-1073450898|DTS_E_COMPONENTNOTFOUND|The module containing "%1" cannot be located, even though it is registered.|  
|0xC004706F|-1073450897|DTS_E_BINARYCODENOTFOUND|The script component is configured to pre-compile the script, but binary code is not found. Please visit the IDE in Script Component Editor by clicking Design Script button to cause binary code to be generated.|  
|0xC0047070|-1073450896|DTS_E_CANTCREATEBLOBFILE|The buffer manager cannot create a file to spool a long object on the directories named in the BLOBTempStoragePath property.  Either an incorrect file name was provided, or there are no permissions, or the paths have been full.|  
|0xC0047071|-1073450895|DTS_E_SYNCHRONOUSIDMISMATCH|The SynchronousInputID property on "%1" was %2!d!, and %3!d! was expected.|  
|0xC0047072|-1073450894|DTS_E_OBJECTIDNOTFOUND|No object exists with the ID %1!d!.|  
|0xC0047073|-1073450893|DTS_E_OBJECTIDLOOKUPFAILED|Unable to locate an object with ID %1!d! because of the error code 0x%2!8.8X!.|  
|0xC0047074|-1073450892|DTS_E_INVALIDCODEPAGE|The code page %1!d! specified on output column "%2" (%3!d!) is not valid. Select a different code page for output column "%2".|  
|0xC0047075|-1073450891|DTS_E_INDIVIDUALPUTEVENTINFOSFAILED|The EventInfos collection could not be cached by "%1" and returned error code 0x%2!8.8X!.|  
|0xC0047077|-1073450889|DTS_E_DUPLICATEOUTPUTCOLUMNNAMES|The name for "%1" is a duplicate.  All names must be unique.|  
|0xC0047078|-1073450888|DTS_E_NOOUTPUTCOLUMNFORINPUTCOLUMN|There is no output column associated with input column "%1" (%2!d!).|  
|0xC0047079|-1073450887|DTS_E_EXCLGRPNOSYNCINP|"%1" has a virtual buffer extending from a root source. There is an exclusion group that is not zero with a synchronous input that is zero.|  
|0xC004707A|-1073450886|DTS_E_ERROROUTCANTBEONSYNCNONEXCLUSIVEOUTPUT|"%1" cannot be an error output because error outputs cannot be placed on synchronous, non-exclusive outputs.|  
|0xC004707B|-1073450885|DTS_E_EXPREVALDIVBYZERO|A divide-by-zero error occurred. The right side operand evaluates to zero in the expression "%1".|  
|0xC004707C|-1073450884|DTS_E_EXPREVALLITERALOVERFLOW|The literal "%1" is too large to fit into type %2. The magnitude of the literal overflows the type.|  
|0xC004707D|-1073450883|DTS_E_EXPREVALBINARYOPNUMERICOVERFLOW|The result of the binary operation "%1" on data types %2 and %3 exceeds the maximum size for numeric types. The operand types could not be implicitly cast into a numeric (DT_NUMERIC) result without loss of precision or scale. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC004707E|-1073450882|DTS_E_EXPREVALBINARYOPOVERFLOW|The result of the binary operation "%1" exceeds the maximum size for result data type "%2". The magnitude of the result of the operation overflows the type of the result.|  
|0xC004707F|-1073450881|DTS_E_EXPREVALFUNCTIONOVERFLOW|The result of the function call "%1" is too large to fit in type "%2". The magnitude of the result of the function call overflows the type of the operand. An explicit cast to a larger type may be required.|  
|0xC0047080|-1073450880|DTS_E_EXPREVALBINARYTYPEMISMATCH|The data types "%1" and "%2" are incompatible for binary operator "%3". The operand types could not be implicitly cast into compatible types for the operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0047081|-1073450879|DTS_E_EXPREVALUNSUPPORTEDBINARYTYPE|The data type "%1" cannot be used with binary operator "%2". The type of one or both of the operands is not supported for the operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0047082|-1073450878|DTS_E_EXPREVALBINARYSIGNMISMATCH|There is a sign mismatch for the bitwise binary operator "%1" in operation "%2". Both operands for this operator must be positive or negative.|  
|0xC0047083|-1073450877|DTS_E_EXPREVALBINARYOPERATIONFAILED|The binary operation "%1" failed with error code 0x%2!8.8X!. An internal error occurred, or an out-of-memory condition exists.|  
|0xC0047084|-1073450876|DTS_E_EXPREVALBINARYOPERATIONSETTYPEFAILED|Attempt to set the result type of binary operation "%1" failed with error code 0x%2!8.8X!.|  
|0xC0047085|-1073450875|DTS_E_EXPREVALSTRINGCOMPARISONFAILED|Comparing "%1" to string "%2" failed.|  
|0xC0047086|-1073450874|DTS_E_EXPREVALUNSUPPORTEDUNNARYTYPE|The data type "%1" cannot be used with unary operator "%2". This operand type is not supported for the operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC0047087|-1073450873|DTS_E_EXPREVALUNARYOPERATIONFAILED|The unary operation "%1" failed with error code 0x%2!8.8X!. An internal error occurred, or there is an out-of-memory condition.|  
|0xC0047088|-1073450872|DTS_E_EXPREVALUNARYOPERATIONSETTYPEFAILED|Attempt to set the result type of unary operation "%1" failed with error code 0x%2!8.8X!.|  
|0xC0047089|-1073450871|DTS_E_EXPREVALPARAMTYPEMISMATCH|The function "%1" does not support the data type "%2" for parameter number %3!d!. The type of the parameter could not be implicitly cast into a compatible type for the function. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC004708A|-1073450870|DTS_E_EXPREVALINVALIDFUNCTION|The function "%1" was not recognized. Either the function name is incorrect or does not exist.|  
|0xC004708B|-1073450869|DTS_E_EXPREVALFNSUBSTRINGINVALIDLENGTH|The length %1!d! is not valid for function "%2". The length parameter cannot be negative. Change the length parameter to zero or a positive value.|  
|0xC004708C|-1073450868|DTS_E_EXPREVALFNSUBSTRINGINVALIDSTARTINDEX|The start index %1!d! is not valid for function "%2". The start index value must be an integer greater than 0. Start index is one-based, not zero-based.|  
|0xC004708E|-1073450866|DTS_E_EXPREVALCHARMAPPINGFAILED|The function "%1" cannot perform the character mapping on string "%2".|  
|0xC004708F|-1073450865|DTS_E_EXPREVALINVALIDDATEPART|"%1" is not a valid date part for function "%2".|  
|0xC0047090|-1073450864|DTS_E_EXPREVALINVALIDNULLPARAM|Parameter number %1!d! of the function NULL with data type "%2" is not valid. The parameters of NULL() must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0047091|-1073450863|DTS_E_EXPREVALINVALIDNULLPARAMTYPE|Parameter number %1!d! of the function NULL with data type "%2" is not an integer. A parameter of NULL() must be an integer or a type that can be converted to an integer.|  
|0xC0047092|-1073450862|DTS_E_EXPREVALFUNCTIONPARAMNOTSTATIC|Parameter number %1!d! of the function "%2" is not static. This parameter must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0047093|-1073450861|DTS_E_EXPREVALINVALIDCASTPARAM|Parameter number %1!d! of the cast to data type "%2" is not valid. The parameters of cast operators must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0047094|-1073450860|DTS_E_EXPREVALINVALIDCASTPARAMTYPE|Parameter number %1!d! of the cast to data type "%2" is not an integer. A parameter of a cast operator must be an integer or a type that can be converted to an integer.|  
|0xC0047095|-1073450859|DTS_E_EXPREVALINVALIDCAST|Cannot cast expression "%1" from data type "%2" to data type "%3". The requested cast is not supported.|  
|0xC0047096|-1073450858|DTS_E_EXPREVALINVALIDTOKEN|Attempt to parse the expression "%1" failed.  The token "%2" at line number "%3", character number "%4" was not recognized. The expression cannot be parsed because it contains invalid elements at the location specified.|  
|0xC0047097|-1073450857|DTS_E_EXPREVALUNEXPECTEDPARSEERROR|An error occurred when parsing the expression "%1". The expression failed to parse for an unknown reason.|  
|0xC0047098|-1073450856|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONWITHHR|Attempt to parse the expression "%1" failed and returned error code 0x%2!8.8X!. The expression cannot be parsed. It might contain invalid elements or it might not be well-formed. There may also be an out-of-memory error.|  
|0xC0047099|-1073450855|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSION|The expression "%1" is not valid and cannot be parsed. The expression may contain invalid elements or it may not be well-formed.|  
|0xC004709A|-1073450854|DTS_E_EXPREVALEXPRESSIONEMPTY|There was no expression to compute. An attempt was made to compute or get the string of an empty expression.|  
|0xC004709B|-1073450853|DTS_E_EXPREVALCOMPUTEFAILED|Attempt to compute the expression "%1" failed with error code 0x%2!8.8X!.|  
|0xC004709C|-1073450852|DTS_E_EXPREVALBUILDSTRINGFAILED|Attempt to generate a string representation of the expression failed with error code 0x%1!8.8X!. Failed when attempting to generate a displayable string that represents the expression.|  
|0xC004709D|-1073450851|DTS_E_EXPREVALCANNOTCONVERTRESULT|Cannot convert the expression result data type "%1" to the column data type "%2". The result of the expression should be written to an input/output column, but the data type of the expression cannot be converted to the data type of the column.|  
|0xC004709E|-1073450850|DTS_E_EXPREVALCONDITIONALOPINVALIDCONDITIONTYPE|The conditional expression "%1" of the conditional operator has an invalid data type of "%2". The conditional expression of the conditional operator must return a Boolean, which is type DT_BOOL.|  
|0xC004709F|-1073450849|DTS_E_EXPREVALCONDITIONALOPTYPEMISMATCH|The data types "%1" and "%2" are incompatible for the conditional operator. The operand types cannot be implicitly cast into compatible types for the conditional operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC00470A0|-1073450848|DTS_E_EXPREVALCONDITIONALOPSETTYPEFAILED|Attempt to set the result type of conditional operation "%1" failed with error code 0x%2!8.8X!.|  
|0xC00470A1|-1073450847|DTS_E_BUFFERORPHANED|This buffer has been orphaned. The buffer manager has shut down, leaving an outstanding buffer and no cleanup will occur for the buffer. There is a potential for memory leaks and other problems.|  
|0xC00470A2|-1073450846|DTS_E_EXPREVALINPUTCOLUMNNAMENOTFOUND|Attempt to find the input column named "%1" failed with error code 0x%2!8.8X!. The input column specified was not found in the input column collection.|  
|0xC00470A3|-1073450845|DTS_E_EXPREVALINPUTCOLUMNIDNOTFOUND|Attempt to find the input column with lineage ID %1!d! failed with error code 0x%2!8.8X!. The input column was not found in the input column collection.|  
|0xC00470A4|-1073450844|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNNAME|The expression contains unrecognized token "%1". If "%1" is a variable, it should be expressed as "\@%1". The specified token is not valid. If the token is intended to be a variable name, it should be prefixed with the \@ symbol.|  
|0xC00470A5|-1073450843|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNID|The expression contains unrecognized token "#%1!d!".|  
|0xC00470A6|-1073450842|DTS_E_EXPREVALVARIABLENOTFOUND|The variable "%1" was not found in the Variables collection. The variable might not exist in the correct scope.|  
|0xC00470A7|-1073450841|DTS_E_EXPREVALINVALIDTOKENSTATE|Attempt to parse the expression "%1" failed. The expression might contain an invalid token, an incomplete token, or an invalid element. It might not be well-formed, or might be missing part of a required element such as a parenthesis.|  
|0xC00470A8|-1073450840|DTS_E_BLANKOUTPUTCOLUMNNAME|The name for "%1" is blank, and names cannot be blank.|  
|0xC00470A9|-1073450839|DTS_E_HASSIDEEFFECTSWITHSYNCINP|The "%1" has the HasSideEffects property set to TRUE, but "%1" is synchronous and cannot have side effects. Set the HasSideEffects property to FALSE.|  
|0xC00470AA|-1073450838|DTS_E_EXPREVALINVALIDCASTCODEPAGE|The value, %1!d!, specified for the code page parameter of the cast to data type "%2", is not valid. The code page is not installed on the machine.|  
|0xC00470AB|-1073450837|DTS_E_EXPREVALINVALIDCASTPRECISION|The value %1!d! specified for the precision parameter of the cast to data type "%2" is not valid. Precision must be in the range %3!d! to %4!d! and the precision value is out of range for the type cast.|  
|0xC00470AC|-1073450836|DTS_E_EXPREVALINVALIDCASTSCALE|The value %1!d! specified for the scale parameter of the cast to data type "%2" is not valid. The scale must be in the range %3!d! to %4!d! and the scale value is out of range for the type cast. Scale must not exceed precision and must be positive.|  
|0xC00470AD|-1073450835|DTS_E_NONSORTEDOUTPUTHASSORTKEYPOSITIONS|The IsSorted property for "%1" is false, but %2!lu! of its output columns' SortKeyPositions are non-zero.|  
|0xC00470AF|-1073450833|DTS_E_EXPREVALCONDITIONALOPCODEPAGEMISMATCH|The code pages must match for operands of conditional operation "%1" for type %2. The code page of the left operand does not match the code page of the right operand. For the conditional operator on the specified type, the code pages must be the same.|  
|0xC00470B1|-1073450831|DTS_E_REFERENCEDMETADATABADCOUNT|Input "%1" (%2!d!) references input "%3" (%4!d!), but they do not have the same number of columns. Input %5!d! has %6!d! columns, while input %7!d! has %8!d! columns.|  
|0xC00470B2|-1073450830|DTS_E_OBJECTLINEAGEIDNOTFOUND|No object exists with a lineage ID of %1!d!.|  
|0xC00470B3|-1073450829|DTS_E_FILENAMEOUTPUTCOLUMNOTFOUND|The output column for the file name cannot be found.|  
|0xC00470B4|-1073450828|DTS_E_FILENAMEOUTPUTCOLUMNINVALIDDATATYPE|The output column for the file name is not a null-terminated Unicode character string, which is data type DT_WSTR.|  
|0xC00470B5|-1073450827|DTS_E_DISTRIBUTORADDFAILED|A distributor failed to give a buffer to thread "%1" because of error 0x%2!8.8X!. The target thread is probably shutting down.|  
|0xC00470B6|-1073450826|DTS_E_LOCALENOTINSTALLED|The LocaleID %1!ld! is not installed on this system.|  
|0xC00470B7|-1073450825|DTS_E_EXPREVALILLEGALHEXESCAPEINSTRINGLITERAL|The string literal "%1" contains an illegal hexadecimal escape sequence of  "\x%2". The escape sequence is not supported in string literals in the expression evaluator. The hexadecimal escape sequences must be of the form \xhhhh where h is a valid hexadecimal digit.|  
|0xC00470B8|-1073450824|DTS_E_EXPREVALILLEGALESCAPEINSTRINGLITERAL|The string literal "%1" contains an illegal escape sequence of "\\%2!c!". The escape sequence is not supported in string literals in the expression evaluator. If a backslash is needed in the string, use a double backslash, "\\\\".|  
|0xC00470B9|-1073450823|DTS_E_NOOUTPUTCOLUMNS|"%1" contains no output columns. An asynchronous output must contain output columns.|  
|0xC00470BA|-1073450822|DTS_E_LOBDATATYPENOTSUPPORTED|The "%1" has a long object data type of DT_TEXT, DT_NTEXT, or DT_IMAGE, which is not supported.|  
|0xC00470BB|-1073450821|DTS_E_OUTPUTWITHMULTIPLEERRORS|Output ID %1!d! was given multiple error output configurations. First %2!d! and %3!d!, then %4!d! and %5!d!.|  
|0xC00470BC|-1073450820|DTS_E_FAILEDDURINGOLEDBDATATYPECONVERSIONCHECK|The OLE DB provider failed during the data type conversion verification for "%1".|  
|0xC00470BD|-1073450819|DTS_E_BUFFERISEOR|This buffer represents the end of the rowset and its row count cannot be altered.  An attempt was made to call AddRow or RemoveRow on a buffer that has the end of rowset flag.|  
|0xC00470BE|-1073450818|DTS_E_EXPREVALUNSUPPORTEDTYPE|The data type "%1" is not supported in an expression. The specified type is not supported or is not valid.|  
|0xC00470BF|-1073450817|DTS_E_PRIMEOUTPUTNOEOR|The PrimeOutput method on "%1" returned success, but did not report an end of the rowset. There is an error in the component. It should have reported an end-of-row. The pipeline will shut down execution to avoid unpredictable results.|  
|0xC00470C0|-1073450816|DTS_E_EXPREVALDATACONVERSIONOVERFLOW|An overflow occurred while converting from data type "%1" to data type "%2". The source type is too large for the destination type.|  
|0xC00470C1|-1073450815|DTS_E_EXPREVALDATACONVERSIONNOTSUPPORTED|Conversion from data type "%1" to data type "%2" is unsupported. The source type cannot be converted to the destination type.|  
|0xC00470C2|-1073450814|DTS_E_EXPREVALDATACONVERSIONFAILED|Error code 0x%1!8.8X! occurred attempting to convert from data type %2 to data type %3.|  
|0xC00470C3|-1073450813|DTS_E_EXPREVALCONDITIONALOPERATIONFAILED|The conditional operation "%1" failed with error code 0x%2!8.8X!. There was an internal error or an out-of-memory error.|  
|0xC00470C4|-1073450812|DTS_E_EXPREVALCASTFAILED|Casting expression "%1" from data type "%2" to data type "%3" failed with error code 0x%4!8.8X!.|  
|0xC00470C5|-1073450811|DTS_E_EXPREVALFUNCTIONCOMPUTEFAILED|Evaluating function "%1" failed with error code 0x%2!8.8X!.|  
|0xC00470C6|-1073450810|DTS_E_EXPREVALFUNCTIONCONVERTPARAMTOMEMBERFAILED|Parameter number %1!d! of the function "%2" cannot be converted to a static value.|  
|0xC00470C7|-1073450809|DTS_E_REDIRECTROWUNAVAILABLEWITHFASTLOADANDZEROMAXINSERTCOMMITSIZE|The error row disposition on "%1" cannot be set to redirect the row when the fast load option is turned on, and the maximum insert commit size is set to zero.|  
|0xC00470CE|-1073450802|DTS_E_EXPREVALBINARYOPERATORCODEPAGEMISMATCH|The code pages for operands of binary operator "%1" for type "%2" must match. Currently, the code page of the left operand does not match the code page of the right operand. For the specified binary operator on the specified type, the code pages must be the same.|  
|0xC00470CF|-1073450801|DTS_E_EXPREVALVARIABLECOMPUTEFAILED|Retrieving the value of Variable "%1" failed with error code 0x%2!8.8X!.|  
|0xC00470D0|-1073450800|DTS_E_EXPREVALVARIABLETYPENOTSUPPORTED|The data type of variable "%1" is not supported in an expression.|  
|0xC00470D1|-1073450799|DTS_E_EXPREVALCASTCODEPAGEMISMATCH|Unable to cast expression "%1" from data type "%2" to data type "%3" because the code page of the value being cast (%4!d!) does not match the requested result code page (%5!d!). The code page of the source must match the code page requested for the destination.|  
|0xC00470D2|-1073450798|DTS_E_BUFFERSIZEOUTOFRANGE|The default buffer size must be between %1!d! and %2!d! bytes. An attempt was made to set the DefaultBufferSize property to a value that is too small or too large.|  
|0xC00470D3|-1073450797|DTS_E_BUFFERMAXROWSIZEOUTOFRANGE|The default buffer maximum rows must be larger than %1!d! rows. An attempt was made to set the DefaultBufferMaxRows property to a value that is too small.|  
|0xC00470D4|-1073450796|DTS_E_EXTERNALCOLUMNMETADATACODEPAGEMISMATCH|The code page on %1 is %2!d! and is required to be %3!d!.|  
|0xC00470D5|-1073450795|DTS_E_THREADCOUNTOUTOFRANGE|Failed to assign %3!d! to the EngineThreads property of the Data Flow task. The value must be between %1!d! and %2!d!.|  
|0xC00470D6|-1073450794|DTS_E_EXPREVALINVALIDTOKENSINGLEQUOTE|Parsing the expression "%1" failed. The single quotation mark at line number "%2", character number "%3", was not expected.|  
|0xC00470D7|-1073450793|DTS_E_EXPREVALINVALIDTOKENSINGLEEQUAL|Parsing the expression "%1" failed. The equal sign (=) at line number "%2", character number "%3", was not expected. A double equals sign (==) may be required at the location specified.|  
|0xC00470DA|-1073450790|DTS_E_INDIVIDUALPUTREFTRACKERFAILED|Component "%1" failed to cache the runtime object reference tracker collection and returned error code 0x%2!8.8X!.|  
|0xC00470DB|-1073450789|DTS_E_EXPREVALAMBIGUOUSINPUTCOLUMNNAME|There are multiple input columns with the name "%1". The desired input column must be specified uniquely as [Component Name].[%2] or referenced by lineage ID. Currently, the input column specified exists on more than one component.|  
|0xC00470DC|-1073450788|DTS_E_EXPREVALDOTTEDINPUTCOLUMNNAMENOTFOUND|Locating the input column named "[%1].[%2]" failed with error code 0x%3!8.8X!. The input column was not found in the input column collection.|  
|0xC00470DD|-1073450787|DTS_E_EXPREVALAMBIGUOUSVARIABLENNAME|There are multiple variables with the name "%1". The desired variable must be specified uniquely as \@[Namespace::%2]. The variable exists in more than one namespace.|  
|0xC00470DE|-1073450786|DTS_E_REDUCTIONFAILED|The Data Flow engine scheduler failed to reduce the execution plan for the pipeline. Set the OptimizedMode property to false.|  
|0xC00470DF|-1073450785|DTS_E_EXPREVALSQRTINVALIDPARAM|The function SQRT cannot operate on negative values, and a negative value was passed to the SQRT function.|  
|0xC00470E0|-1073450784|DTS_E_EXPREVALLNINVALIDPARAM|The function LN cannot operate on zero or negative values, and a zero or negative value was passed to the LN function.|  
|0xC00470E1|-1073450783|DTS_E_EXPREVALLOGINVALIDPARAM|The function LOG cannot operate on zero or negative values, and a zero or negative value was passed to the LOG function.|  
|0xC00470E2|-1073450782|DTS_E_EXPREVALPOWERINVALIDPARAM|The parameters passed to the function POWER cannot be evaluated and yield an indeterminate result.|  
|0xC00470E3|-1073450781|DTS_E_NOCANCELEVENT|The runtime cannot provide a cancel event because of error 0x%1!8.8X!.|  
|0xC00470E4|-1073450780|DTS_E_CANCELRECEIVED|The pipeline received a request to cancel and is shutting down.|  
|0xC00470E5|-1073450779|DTS_E_EXPREVALUNARYOPOVERFLOW|The result of the unary minus (negation) operation "%1" exceeds the maximum size for result data type "%2". The magnitude of the result of the operation overflows the type of the result.|  
|0xC00470E6|-1073450778|DTS_E_EXPREVALPLACEHOLDERINEXPRESSION|The placeholder "%1" was found in an expression. This must be replaced with an actual parameter or operand.|  
|0xC00470E7|-1073450777|DTS_E_EXPREVALFNRIGHTINVALIDLENGTH|The length %1!d! specified for function "%2" is negative, and is not valid. The length parameter must be positive.|  
|0xC00470E8|-1073450776|DTS_E_EXPREVALFNREPLICATEINVALIDREPEATCOUNT|The repeat count %1!d! is negative and is not valid for function "%2". The repeat count parameter cannot be negative.|  
|0xC00470EA|-1073450774|DTS_E_EXPREVALVARIABLECOULDNOTBEREAD|Reading the variable "%1" failed with error code 0x%2!8.8X!.|  
|0xC00470EC|-1073450772|DTS_E_EXPREVALBINARYOPDTSTRNOTSUPPORTED|For operands of a binary operation, the data type DT_STR is supported only for input columns and cast operations. The expression "%1" has a DT_STR operand that is not an input column or the result of a cast, and cannot be used in a binary operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC00470ED|-1073450771|DTS_E_EXPREVALCONDITIONALOPDTSTRNOTSUPPORTED|For operands of the conditional operator, the data type DT_STR is supported only for input columns and cast operations. The expression "%1" has a DT_STR operand that is not an input column or the result of a cast, and cannot be used with the conditional operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC00470EE|-1073450770|DTS_E_EXPREVALFNFINDSTRINGINVALIDOCCURRENCECOUNT|The occurrence count %1!d! is not valid for function "%2". This parameter must be greater than zero.|  
|0xC00470EF|-1073450769|DTS_E_INDIVIDUALPUTLOGENTRYINFOS|"%1" failed to cache the LogEntryInfos collection and returned error code 0x%2!8.8X!.|  
|0xC00470F0|-1073450768|DTS_E_EXPREVALINVALIDDATEPARTNODE|The date part parameter specified for function "%1" is not valid. It must be a static string.  The date part parameter cannot contain dynamic elements, such as input columns, and must be of type DT_WSTR.|  
|0xC00470F1|-1073450767|DTS_E_EXPREVALINVALIDCASTLENGTH|The value %1!d! specified for the length parameter of the cast to data type %2 is negative and not valid. The length must be positive.|  
|0xC00470F2|-1073450766|DTS_E_EXPREVALINVALIDNULLCODEPAGE|The value %1!d! specified for the code page parameter of the NULL function with data type "%2" is not valid. The code page is not installed on the computer.|  
|0xC00470F3|-1073450765|DTS_E_EXPREVALINVALIDNULLPRECISION|The value %1!d! specified for the precision parameter of the NULL function with data type "%2" is out of range. Precision must be in the range %3!d! to %4!d!.|  
|0xC00470F4|-1073450764|DTS_E_EXPREVALINVALIDNULLSCALE|The value %1!d! specified for the scale parameter of the NULL function with data type %2 is out of range. Scale must be in the range %3!d! to %4!d!. Scale must not exceed precision and must not be negative.|  
|0xC00470F5|-1073450763|DTS_E_EXPREVALINVALIDNULLLENGTH|The value %1!d! specified for the length parameter of the "NULL" function with data type %2 is negative and not valid. The length must be positive.|  
|0xC00470F6|-1073450762|DTS_E_NEGATIVESNOTALLOWED|The %1 can't be assigned a negative value.|  
|0xC00470F7|-1073450761|DTS_E_FASTPARSENOTALLOWED|The "%1" custom property for "%2" cannot be set to true.  The column data type must be one of the following:  DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4, DT_UI8, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAMPOFFSET, DT_DATE, DT_DBDATE, DT_DBTIME, DT_DBTIME2, or DT_FILETIME.|  
|0xC00470F8|-1073450760|DTS_E_CANNOTREATTACHPATH|The "%1" cannot be reattached. Delete the path, add a new one, and attach it.|  
|0xC00470F9|-1073450759|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALSINGULAR|The function "%1" requires %2!d! parameters, not %3!d! parameter. The function name was recognized, but the number of parameters is not valid.|  
|0xC00470FA|-1073450758|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSSINGULARPLURAL|The function "%1" requires %2!d! parameter, not %3!d! parameters. The function name was recognized, but the number of parameters is not valid.|  
|0xC00470FB|-1073450757|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALPLURAL|The function "%1" requires %2!d! parameters, not %3!d! parameters. The function name was recognized, but the number of parameters is not valid.|  
|0xC00470FC|-1073450756|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONOUTOFMEMORY|Attempt to parse the expression "%1" failed because there was an out-of-memory error.|  
|0xC00470FD|-1073450755|DTS_E_INDIVIDUALCHECKPRODUCTLEVELFAILED|The %1 failed to be able to perform its required product level check and returned error code 0x%2!8.8X!.|  
|0xC00470FE|-1073450754|DTS_E_PRODUCTLEVELTOLOW|SSIS Error Code DTS_E_PRODUCTLEVELTOLOW.  The %1 cannot run on installed %2 of Integration Services. It requires %3 or higher.|  
|0xC00470FF|-1073450753|DTS_E_EXPREVALSTRINGLITERALTOOLONG|A string literal in the expression exceeds the maximum allowed length of %1!d! characters.|  
|0xC0047100|-1073450752|DTS_E_EXPREVALSTRINGVARIABLETOOLONG|The variable %1 contains a string that exceeds the maximum allowed length of %2!d! characters.|  
|0xC0047101|-1073450751|DTS_E_COMPONENT_NOINTERFACE|The %1 was found, but it does not support a required Integration Services interface (IDTSRuntimeComponent100).  Obtain an updated version of this component from the component provider.|  
|0xC0048000|-1073446912|DTS_E_CANNOTOPENREGISTRYKEY|The registry key "%1" cannot be opened.|  
|0xC0048001|-1073446911|DTS_E_INVALIDCOMPONENTFILENAME|Cannot get the file name for the component with a CLSID of "%1". Verify that the component is registered properly or that the CLSID provided is correct.|  
|0xC0048002|-1073446910|DTS_E_UNKNOWNCOMPONENTHASINVALIDCLSID|The CLSID for one of the components is not valid. Verify that all the components in the pipeline have valid CLSIDs.|  
|0xC0048003|-1073446909|DTS_E_COMPONENTHASINVALIDCLSID|The CLSID for one of the components with ID %1!d! is not valid.|  
|0xC0048004|-1073446908|DTS_E_INVALIDINDEX|The index is not valid.|  
|0xC0048005|-1073446907|DTS_E_CANNOTACCESSDTSAPPLICATIONOBJECT|The Application object cannot be accessed. Verify that SSIS is correctly installed.|  
|0xC0048006|-1073446906|DTS_E_ERROROCCURREDWHILERETRIEVINGFILENAME|Retrieving the file name for a component failed with error code 0x%1!8.8X!.|  
|0xC0048007|-1073446905|DTS_E_CANNOTRETRIEVEPROPERTYFORCOMPONENT|Cannot retrieve property "%1" from component with ID %2!d!.|  
|0xC0048008|-1073446904|DTS_E_DUPLICATEIDFOUND|Attempting to use ID %1!d! more than once in the Data Flow Task.|  
|0xC0048009|-1073446903|DTS_E_CANNOTRETRIEVEBYLINEAGE|Cannot retrieve an item by lineage ID from a collection that does not contain columns.|  
|0xC004800B|-1073446901|DTS_E_CANNOTMAPRUNTIMECONNECTIONMANAGER|Cannot find the connection manager with ID "%1" in the connection manager collection due to error code 0x%2!8.8X!. That connection manager is needed by "%3" in the connection manager collection of "%4". Verify that a connection manager in the connection manager collection, Connections, has been created with that ID.|  
|0xC004800E|-1073446898|DTS_E_INPUTNOTKNOWN|Thread "%1" received a buffer for input %2!d!, but this thread is not responsible for that input. An error occurred, causing the Data Flow engine scheduler to build a bad execution plan.|  
|0xC004800F|-1073446897|DTS_E_GETRTINTERFACEFAILED|The component "%1" (%2!d!) cannot provide an IDTSRuntimeComponent100 interface.|  
|0xC0048011|-1073446895|DTS_E_CANTGIVEAWAYBUFFER|The Data Flow task engine attempted to copy a buffer to assign another thread, but failed.|  
|0xC0048012|-1073446894|DTS_E_CANTCREATEVIEWBUFFER|The Data Flow task engine failed to create a view buffer of type %1!d! over type %2!d! for buffer %3!d.|  
|0xC0048013|-1073446893|DTS_E_UNUSABLETEMPORARYPATH|The buffer manager could not create a temporary file on the path "%1". The path will not be considered for temporary storage again.|  
|0xC0048014|-1073446892|DTS_E_DIRECTTONONERROROUTPUT|The buffer manager attempted to push an error row to an output that was not registered as an error output. There was a call to DirectErrorRow on an output that does not have the IsErrorOut property set to TRUE.|  
|0xC0048015|-1073446891|DTS_E_BUFFERISPRIVATE|A call was made to a buffer method on a private buffer and private buffers do not support this operation.|  
|0xC0048016|-1073446890|DTS_E_BUFFERISFLAT|Private mode buffers do not support this operation.|  
|0xC0048017|-1073446889|DTS_E_BUFFERISPRIMEOUTPUT|This operation cannot be called on a buffer passed to PrimeOutput. A call was made to a buffer method during PrimeOutput, but that call is not allowed during PrimeOutput.|  
|0xC0048018|-1073446888|DTS_E_BUFFERISPROCESSINPUT|This operation cannot be called on a buffer passed to ProcessInput. A call was made to a buffer method during ProcessInput, but that call is not allowed during ProcessInput.|  
|0xC0048019|-1073446887|DTS_E_BUFFERGETTEMPFILENAME|The buffer manager could not get a temporary file name.|  
|0xC004801A|-1073446886|DTS_E_REFERENCECOLUMNTOOWIDE|The code encountered a column that was too wide.|  
|0xC004801B|-1073446885|DTS_E_CANNOTGETRUNTIMECONNECTIONMANAGERID|Cannot get the ID of the runtime connection manager specified by "%1" in the connection manager collection, Connections, of "%2" due to error code 0x%3!8.8X!. Verify that the ConnectionManager.ID property of the runtime connection object has been set for the component.|  
|0xC004801C|-1073446884|DTS_E_EMPTYRUNTIMECONNECTIONMANAGERID|The "%1" in the connection manager collection, Connections, of "%2" does not have a value for the ID property. Verify that the ConnectionManagerID property of the runtime connection object has been set for the component.|  
|0xC004801D|-1073446883|DTS_E_METADATAREADONLY|Metadata cannot be changed during execution.|  
|0xC004801F|-1073446881|DTS_E_UPGRADEFAILED|The component metadata for "%1" could not be upgraded to the newer version of the component. The PerformUpgrade method failed.|  
|0xC0048020|-1073446880|DTS_E_COMPONENTVERSIONMISMATCH|The version of %1 is not compatible with this version of the DataFlow.|  
|0xC0048021|-1073446879|DTS_E_ERRORCOMPONENT|The component is missing, not registered, not upgradeable, or missing required interfaces. The contact information for this component is "%1".|  
|0xC0048022|-1073446878|DTS_E_BUFFERISNOTPRIMEOUTPUT|The method was called on the wrong buffer. Buffers that are not used for component output do not support this operation.|  
|0xC0049014|-1073442796|DTS_E_EXPREVALSTATIC_COMPUTATIONFAILED|An error occurred during computation of the expression.|  
|0xC0049030|-1073442768|DTS_E_EXPREVALSTATIC_DIVBYZERO|Division by zero occurred in the expression.|  
|0xC0049031|-1073442767|DTS_E_EXPREVALSTATIC_LITERALOVERFLOW|The magnitude of the literal value was too big to fit in the type requested.|  
|0xC0049032|-1073442766|DTS_E_EXPREVALSTATIC_BINARYOPNUMERICOVERFLOW|The result of a binary operation was too big for the maximum size for numeric types. The operand types could not be implicitly cast into a numeric (DT_NUMERIC) result without loss of precision or scale. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0049033|-1073442765|DTS_E_EXPREVALSTATIC_BINARYOPOVERFLOW|The magnitude of the result of a binary operation overflows the maximum size for result data type.|  
|0xC0049034|-1073442764|DTS_E_EXPREVALSTATIC_FUNCTIONOVERFLOW|The magnitude of the result of a function call was too big to fit in the result type, and overflowed the type of the operand. An explicit cast to a larger type may be required.|  
|0xC0049035|-1073442763|DTS_E_EXPREVALSTATIC_BINARYTYPEMISMATCH|Incompatible data types were used with a binary operator. The operand types could not be implicitly cast into compatible types for the operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0049036|-1073442762|DTS_E_EXPREVALSTATIC_UNSUPPORTEDBINARYTYPE|An unsupported data type was used with a binary operator. The type of one, or both, of the operands is not supported for the operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0049037|-1073442761|DTS_E_EXPREVALSTATIC_BINARYSIGNMISMATCH|There is a sign mismatch for the bitwise binary operator. The operands for this operator must be both positive or both negative.|  
|0xC0049038|-1073442760|DTS_E_EXPREVALSTATIC_BINARYOPERATIONFAILED|A binary operation failed. There was an out-of-memory condition, or an internal error occurred.|  
|0xC0049039|-1073442759|DTS_E_EXPREVALSTATIC_BINARYOPERATIONSETTYPEFAILED|Setting the result type of a binary operation failed.|  
|0xC004903A|-1073442758|DTS_E_EXPREVALSTATIC_STRINGCOMPARISONFAILED|Cannot compare two strings.|  
|0xC004903B|-1073442757|DTS_E_EXPREVALSTATIC_UNSUPPORTEDUNNARYTYPE|An unsupported data type is used with a unary operator. The operand type is not supported for the operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC004903C|-1073442756|DTS_E_EXPREVALSTATIC_UNARYOPERATIONFAILED|A unary operation failed. An out-of-memory condition occurred, or there was an internal error.|  
|0xC004903D|-1073442755|DTS_E_EXPREVALSTATIC_UNARYOPERATIONSETTYPEFAILED|Setting the result type of a unary operation failed.|  
|0xC004903E|-1073442754|DTS_E_EXPREVALSTATIC_PARAMTYPEMISMATCH|A function has a parameter with an unsupported data type. The type of the parameter cannot be implicitly cast into a compatible type for the function. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC004903F|-1073442753|DTS_E_EXPREVALSTATIC_INVALIDFUNCTION|An invalid function name appeared in the expression. Verify that the function name is correct and does exist.|  
|0xC0049040|-1073442752|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDLENGTH|The length parameter was not valid for function SUBSTRING. The length parameter cannot be negative.|  
|0xC0049041|-1073442751|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDSTARTINDEX|The start index was not valid for function SUBSTRING. The start index value must be an integer greater than zero. The start index is 1-based, not 0-based.|  
|0xC0049042|-1073442750|DTS_E_EXPREVALSTATIC_INVALIDNUMBEROFPARAMS|An incorrect number of parameters was given to a function. The function name was recognized, but the number of parameters was not correct.|  
|0xC0049043|-1073442749|DTS_E_EXPREVALSTATIC_CHARMAPPINGFAILED|A character mapping function failed.|  
|0xC0049044|-1073442748|DTS_E_EXPREVALSTATIC_INVALIDDATEPART|An unrecognized date part parameter was specified for a date function.|  
|0xC0049045|-1073442747|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAM|An invalid parameter was given for function NULL. The parameters of NULL must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0049046|-1073442746|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAMTYPE|An invalid parameter was given for function NULL. A parameter of NULL must be an integer, or a type that can be converted to an integer.|  
|0xC0049047|-1073442745|DTS_E_EXPREVALSTATIC_FUNCTIONPARAMNOTSTATIC|An invalid parameter was given for a function. This parameter must be static and cannot contain dynamic elements such as input columns.|  
|0xC0049048|-1073442744|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAM|An invalid parameter was given for a cast operation. Parameters of cast operators must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0049049|-1073442743|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAMTYPE|An invalid parameter was given for a cast operation. A parameter of a cast operator must be an integer, or a type that can be converted to an integer.|  
|0xC004904A|-1073442742|DTS_E_EXPREVALSTATIC_INVALIDCAST|The expression contained an unsupported type cast.|  
|0xC004904B|-1073442741|DTS_E_EXPREVALSTATIC_INVALIDTOKEN|The expression contained a token that was not recognized. The expression could not be parsed because it contains invalid elements.|  
|0xC004904C|-1073442740|DTS_E_EXPREVALSTATIC_FAILEDTOPARSEEXPRESSION|The expression is not valid and could not be parsed. It might contain invalid elements, or it might not be well-formed.|  
|0xC004904D|-1073442739|DTS_E_EXPREVALSTATIC_UNARYOPOVERFLOW|The result of a unary minus (negation) operation overflowed the maximum size for result data type. The magnitude of the result of the operation overflows the type of the result.|  
|0xC004904E|-1073442738|DTS_E_EXPREVALSTATIC_COMPUTEFAILED|Attempt to compute the expression failed.|  
|0xC004904F|-1073442737|DTS_E_EXPREVALSTATIC_BUILDSTRINGFAILED|Attempt to generate a string representation of the expression failed.|  
|0xC0049050|-1073442736|DTS_E_EXPREVALSTATIC_CANNOTCONVERTRESULT|Cannot convert the expression result data type to the column data type. The result of the expression should be written to an input/output column, but the data type of the expression cannot be converted to the data type of the column.|  
|0xC0049051|-1073442735|DTS_E_EXPREVALSTATIC_CONDITIONALOPINVALIDCONDITIONTYPE|The conditional expression of the conditional operator has invalid data type. The conditional expression must be of type DT_BOOL.|  
|0xC0049052|-1073442734|DTS_E_EXPREVALSTATIC_CONDITIONALOPTYPEMISMATCH|The data types of the operands of the conditional operator were incompatible. The operand types could not be implicitly cast into compatible types for the conditional operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0049053|-1073442733|DTS_E_EXPREVALSTATIC_CONDITIONALOPSETTYPEFAILED|Setting the result type of a conditional operation failed.|  
|0xC0049054|-1073442732|DTS_E_EXPREVALSTATIC_INPUTCOLUMNNAMENOTFOUND|The input column specified was not found in the input column collection.|  
|0xC0049055|-1073442731|DTS_E_EXPREVALSTATIC_INPUTCOLUMNIDNOTFOUND|Attempt to find an input column by lineage ID failed. The input column was not found in the input column collection.|  
|0xC0049056|-1073442730|DTS_E_EXPREVALSTATIC_NOINPUTCOLUMNCOLLECTION|The expression contains an unrecognized token that appears to be an input column reference, but the input column collection is not available to process input columns. The input column collection has not been provided to the expression evaluator, but an input column was included in the expression.|  
|0xC0049057|-1073442729|DTS_E_EXPREVALSTATIC_VARIABLENOTFOUND|A variable specified was not found in the collection. It might not exist in the correct scope. Verify that the variable exists and that the scope is correct.|  
|0xC0049058|-1073442728|DTS_E_EXPREVALSTATIC_INVALIDTOKENSTATE|Attempt to parse the expression failed. The expression contains an invalid or incomplete token. It may contain invalid elements, be missing part of a required element such as closing parentheses, or may not be well formed.|  
|0xC0049059|-1073442727|DTS_E_EXPREVALSTATIC_INVALIDCASTCODEPAGE|The value specified for the code page parameter of the cast to data type DT_STR or DT_TEXT is not valid. The specified code page is not installed on the computer.|  
|0xC004905A|-1073442726|DTS_E_EXPREVALSTATIC_INVALIDCASTPRECISION|The value specified for the precision parameter of a cast operation is out of range for the type cast.|  
|0xC004905B|-1073442725|DTS_E_EXPREVALSTATIC_INVALIDCASTSCALE|The value specified for the scale parameter of a cast operation is out of range for the type cast. Scale must not exceed precision and must not be negative.|  
|0xC004905C|-1073442724|DTS_E_EXPREVALSTATIC_CONDITIONALOPCODEPAGEMISMATCH|The code pages do not match in a conditional operation. The code page of the left operand does not match the code page of the right operand. For the conditional operator of that type, the code pages must be the same.|  
|0xC004905D|-1073442723|DTS_E_EXPREVALSTATIC_ILLEGALHEXESCAPEINSTRINGLITERAL|A string literal contains an illegal hexadecimal escape sequence. The escape sequence is not supported in string literals in the expression evaluator. Hexadecimal escape sequences must be of the form \xhhhh where h is a valid hexadecimal digit.|  
|0xC004905E|-1073442722|DTS_E_EXPREVALSTATIC_ILLEGALESCAPEINSTRINGLITERAL|The string literal contains an illegal escape sequence. The escape sequence is not supported in string literals in the expression evaluator. If a backslash is needed in the string, format it as a double backslash, "\\\\".|  
|0xC004905F|-1073442721|DTS_E_EXPREVALSTATIC_UNSUPPORTEDTYPE|An unsupported or unrecognized data type was used in the expression.|  
|0xC0049060|-1073442720|DTS_E_EXPREVALSTATIC_DATACONVERSIONOVERFLOW|An overflow occurred while converting between data types. The source type is too large to fit in the destination type.|  
|0xC0049061|-1073442719|DTS_E_EXPREVALSTATIC_DATACONVERSIONNOTSUPPORTED|The expression contains an unsupported data type conversion. The source type cannot be converted to the destination type.|  
|0xC0049062|-1073442718|DTS_E_EXPREVALSTATIC_DATACONVERSIONFAILED|An error occurred while attempting to perform data conversion. The source type could not be converted to the destination type.|  
|0xC0049063|-1073442717|DTS_E_EXPREVALSTATIC_CONDITIONALOPERATIONFAILED|The conditional operation failed.|  
|0xC0049064|-1073442716|DTS_E_EXPREVALSTATIC_CASTFAILED|An error occurred while attempting to perform a type cast.|  
|0xC0049065|-1073442715|DTS_E_EXPREVALFAILEDTOCONVERTSTRCOLUMNTOWSTR|Converting "%1" from type DT_STR to type DT_WSTR failed with error code 0x%2!8.8X!. An error occurred while performing the implicit conversion on the input column.|  
|0xC0049066|-1073442714|DTS_E_EXPREVALSTATIC_FAILEDTOCONVERTSTRCOLUMNTOWSTR|Converting an input column from type DT_STR to type DT_WSTR failed. An error occurred while performing the  implicit conversion on the input column.|  
|0xC0049067|-1073442713|DTS_E_EXPREVALSTATIC_FUNCTIONCOMPUTEFAILED|An error occurred while evaluating the function.|  
|0xC0049068|-1073442712|DTS_E_EXPREVALSTATIC_FUNCTIONCONVERTPARAMTOMEMBERFAILED|A function parameter cannot be converted to a static value. The parameter must be static and cannot contain dynamic elements such as input columns.|  
|0xC0049088|-1073442680|DTS_E_EXPREVALSTATIC_FNRIGHTINVALIDLENGTH|The length parameter is not valid for function RIGHT. The length parameter cannot be negative.|  
|0xC0049089|-1073442679|DTS_E_EXPREVALSTATIC_FNREPLICATEINVALIDREPEATCOUNT|The repeat count parameter is not valid for function REPLICATE. This parameter cannot be negative.|  
|0xC0049096|-1073442666|DTS_E_EXPREVALSTATIC_BINARYOPERATORCODEPAGEMISMATCH|The code pages do not match in a binary operation. The code page of the left operand does not match the code page of the right operand. For this binary operation, the code pages must be the same.|  
|0xC0049097|-1073442665|DTS_E_EXPREVALSTATIC_VARIABLECOMPUTEFAILED|Retrieving the value for a variable failed.|  
|0xC0049098|-1073442664|DTS_E_EXPREVALSTATIC_VARIABLETYPENOTSUPPORTED|The expression contains a variable with an unsupported data type.|  
|0xC004909B|-1073442661|DTS_E_EXPREVALSTATIC_CASTCODEPAGEMISMATCH|Unable to cast the expression because the code page of the value being cast does not match the requested result code page. The code page of the source must match the code page requested for the destination.|  
|0xC004909C|-1073442660|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEQUOTE|The expression contains an unexpected single quotation mark. A double quotation mark may be required.|  
|0xC004909D|-1073442659|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEEQUAL|The expression contains an unexpected equal sign (=). This error usually occurs when a double equals sign (==) is needed.|  
|0xC00490AA|-1073442646|DTS_E_EXPREVALSTATIC_AMBIGUOUSINPUTCOLUMNNAME|An ambiguous input column name was specified.  The column must be qualified as [Component Name].[Column Name] or referenced by lineage ID. This error occurs when the input column exists on more than one component, and must be differentiated by the addition of component name or by using the lineage ID.|  
|0xC00490AB|-1073442645|DTS_E_EXPREVALSTATIC_PLACEHOLDERINEXPRESSION|A placeholder function parameter or operand was found in an expression. This should be replaced with an actual parameter or operand.|  
|0xC00490AC|-1073442644|DTS_E_EXPREVALSTATIC_AMBIGUOUSVARIABLENNAME|An ambiguous variable name was specified. The desired variable must be qualifed as \@[Namespace::Variable]. This error occurs when the variable exists in more than one namespace.|  
|0xC00490D3|-1073442605|DTS_E_EXPREVALSTATIC_BINARYOPDTSTRNOTSUPPORTED|For operands of binary operation, the data type DT_STR is only supported for input columns and cast operations. A DT_STR operand that is not an input column or the result of a cast cannot be used with a binary operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC00490D4|-1073442604|DTS_E_EXPREVALSTATIC_CONDITIONALOPDTSTRNOTSUPPORTED|For operands of the conditional operator, the data type DT_STR is only supported for input columns and cast operations. A DT_STR operand that is not an input column or the result of a cast cannot be used with the conditional operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC00490D5|-1073442603|DTS_E_EXPREVALSTATIC_FNFINDSTRINGINVALIDOCCURRENCECOUNT|The occurrence count parameter is not valid for function FINDSTRING. This parameter must be greater than zero.|  
|0xC00490DD|-1073442595|DTS_E_EXPREVALSTATIC_INVALIDDATEPARTNODE|The "date part" parameter specified for a date function is not valid. "Date part" parameters must be static strings, and cannot contain dynamic elements such as input columns. They must be of type DT_WSTR.|  
|0xC00490DE|-1073442594|DTS_E_EXPREVALSTATIC_INVALIDCASTLENGTH|The value specified for the length parameter of a cast operation is not valid. The length must be positive. The length specified for the type cast is negative. Change to a positive value.|  
|0xC00490DF|-1073442593|DTS_E_EXPREVALSTATIC_INVALIDNULLLENGTH|The value specified for the length parameter of a NULL function is not valid. The length must be positive. The length specified for the NULL function is negative. Change to a positive value.|  
|0xC00490E0|-1073442592|DTS_E_EXPREVALSTATIC_INVALIDNULLCODEPAGE|The value specified for the code page parameter of the NULL function with data type DT_STR or DT_TEXT is not valid. The code page specified is not installed on the computer. Either change the code page that is specified, or install the code page on the computer.|  
|0xC00490E1|-1073442591|DTS_E_EXPREVALSTATIC_INVALIDNULLPRECISION|The value specified for the precision parameter of a NULL function is not valid. The precision that was specified is out of range for the NULL function.|  
|0xC00490E2|-1073442590|DTS_E_EXPREVALSTATIC_INVALIDNULLSCALE|The value specified for the scale parameter of a NULL function is not valid. The scale that was specified is out of range for the NULL function. Scale must not exceed precision and must be positive.|  
|0xC00490E8|-1073442584|DTS_E_XMLSRCERRORSETTINGERROROUTPUTCOLUMNDATA|The %1 failed attempting to write data to %2 on %3. %4|  
|0xC00490F5|-1073442571|DTS_E_TXLOOKUP_CANCEL_REQUESTED|Lookup transform has received a cancel request from the user.|  
|0xC00490F6|-1073442570|DTS_E_LOBLENGTHLIMITEXCEEDED|Processing of character or binary large object (LOB) data has stopped because the 4-GB limit was reached.|  
|0xC00490F7|-1073442569|DTS_E_CANNOTLOADCOMPONENT|The managed pipeline component "%1" could not be loaded.  The exception was: %2.|  
|0xC00F9304|-1072721148|DTS_E_OLEDB_EXCEL_NOT_SUPPORTED|SSIS Error Code DTS_E_OLEDB_EXCEL_NOT_SUPPORTED: The Excel Connection Manager is not supported in the 64-bit version of SSIS, as no OLE DB provider is available.|  
|0xC00F9310|-1072721136|DTS_E_CACHEBADHEADER|The cache file is damaged, or the file was not created by using the Cache connection manager.  Provide a valid cache file.|  
|0xC0202001|-1071636479|DTS_E_MISSINGSQLCOMMAND|The SQL command has not been set correctly. Check SQLCommand property.|  
|0xC0202002|-1071636478|DTS_E_COMERROR|COM error object information is available.  Source: "%1"  error code: 0x%2!8.8X!  Description: "%3".|  
|0xC0202003|-1071636477|DTS_E_ACQUIREDCONNECTIONUNAVAILABLE|Unable to access the acquired connections.|  
|0xC0202004|-1071636476|DTS_E_INCORRECTCOLUMNCOUNT|The number of columns is incorrect.|  
|0xC0202005|-1071636475|DTS_E_COLUMNNOTFOUND|Column "%1" cannot be found at the datasource.|  
|0xC0202007|-1071636473|DTS_E_OLEDBRECORD|An OLE DB record is available.  Source: "%1"  Hresult: 0x%2!8.8X!  Description: "%3".|  
|0xC0202009|-1071636471|DTS_E_OLEDBERROR|SSIS Error Code DTS_E_OLEDBERROR.  An OLE DB error has occurred. Error code: 0x%1!8.8X!.|  
|0xC020200A|-1071636470|DTS_E_ALREADYCONNECTED|Component is already connected. The component needs to be disconnected before attempting to connect it.|  
|0xC020200B|-1071636469|DTS_E_INCORRECTSTOCKPROPERTYVALUE|The value of the property "%1" is incorrect.|  
|0xC020200E|-1071636466|DTS_E_CANNOTOPENDATAFILE|Cannot open the datafile "%1".|  
|0xC0202010|-1071636464|DTS_E_DESTINATIONFLATFILEREQUIRED|No destination flat file name was provided. Make sure the flat file connection manager is configured with a connection string. If the flat file connection manager is used by multiple components, ensure that the connection string contains enough file names.|  
|0xC0202011|-1071636463|DTS_E_TEXTQUALIFIERNOTFOUND|The text qualifier for column "%1" cannot be found.|  
|0xC0202014|-1071636460|DTS_E_CANNOTCONVERTTYPES|Conversion from "%1" to "%2" is not supported.|  
|0xC0202015|-1071636459|DTS_E_PROBLEMDETECTINGTYPECOMPATIBILITY|The error code 0x%1!8.8X! was returned when validating type conversion from %2 to %3.|  
|0xC0202016|-1071636458|DTS_E_CANNOTMAPINPUTCOLUMNTOOUTPUTCOLUMN|Cannot find input column with lineage ID "%1!d!" which is needed by "%2". Check SourceInputColumnLineageID custom property of the output column.|  
|0xC0202017|-1071636457|DTS_E_INCORRECTMINIMUMNUMBEROFOUTPUTS|The number of outputs is incorrect. There must be at least %1!d! outputs.|  
|0xC0202018|-1071636456|DTS_E_INCORRECTEXACTNUMBEROFOUTPUTS|The number of outputs is incorrect. There must be exactly %1!d! output(s).|  
|0xC0202019|-1071636455|DTS_E_STRINGCONVERSIONTOOLONG|A string was too long to be converted.|  
|0xC020201A|-1071636454|DTS_E_INCORRECTEXACTNUMBEROFINPUTS|The number of inputs is incorrect. There must be exactly %1!d! inputs.|  
|0xC020201B|-1071636453|DTS_E_CANNOTHAVEZEROINPUTCOLUMNS|The number of input columns for %1 cannot be zero.|  
|0xC020201C|-1071636452|DTS_E_CANNOTHAVEINPUTS|This component has %1!d! inputs.  No input is allowed on this component.|  
|0xC020201D|-1071636451|DTS_E_PROCESSINPUTCALLEDWITHINVALIDINPUTID|ProcessInput was called with an invalid input ID of %1!d!.|  
|0xC020201F|-1071636449|DTS_E_INCORRECTCUSTOMPROPERTYTYPE|The custom property "%1" needs to be of type %2.|  
|0xC0202020|-1071636448|DTS_E_INVALIDBUFFERTYPE|The buffer type is not valid. Make sure the Pipeline layout and all components pass validation.|  
|0xC0202021|-1071636447|DTS_E_INCORRECTCUSTOMPROPERTYVALUE|The value for custom property "%1" is incorrect.|  
|0xC0202022|-1071636446|DTS_E_CONNECTIONREQUIREDFORMETADATA|An error occurred due to no connection. A connection is required when requesting metadata. If you are working offline, uncheck Work Offline on the SSIS menu to enable the connection.|  
|0xC0202023|-1071636445|DTS_E_CANTCREATECUSTOMPROPERTY|The custom property "%1" cannot be created.|  
|0xC0202024|-1071636444|DTS_E_CANTGETCUSTOMPROPERTYCOLLECTION|The custom property collection cannot be retrieved for initialization.|  
|0xC0202025|-1071636443|DTS_E_CANNOTCREATEACCESSOR|Cannot create an OLE DB accessor. Verify that the column metadata is valid.|  
|0xC0202026|-1071636442|DTS_E_PRIMEOUTPUTCALLEDWITHINVALIDOUTPUTID|PrimeOutput was called with an invalid output ID of %1!d!.|  
|0xC0202027|-1071636441|DTS_E_INCORRECTSTOCKPROPERTY|The value for property "%1" on "%2" is not valid.|  
|0xC0202028|-1071636440|DTS_E_CONNECTIONREQUIREDFORREAD|A connection is required to read data.|  
|0xC020202C|-1071636436|DTS_E_ERRORWHILEREADINGHEADERROWS|An error occurred while reading header rows.|  
|0xC020202D|-1071636435|DTS_E_DUPLICATECOLUMNNAME|Duplicate column name "%1".|  
|0xC0202030|-1071636432|DTS_E_CANNOTGETCOLUMNNAME|Cannot get the name of the column with ID %1!d!.|  
|0xC0202031|-1071636431|DTS_E_CANTDIRECTROW|Direct row to output "%1" (%2!d!) failed.|  
|0xC020203A|-1071636422|DTS_E_CANNOTCREATEBULKINSERTHREAD|Cannot create the bulk insert thread due to error "%1".|  
|0xC020203B|-1071636421|DTS_E_BULKINSERTHREADINITIALIZATIONFAILED|The thread for the SSIS Bulk Insert task failed initialization.|  
|0xC020203E|-1071636418|DTS_E_BULKINSERTTHREADALREADYRUNNING|The thread for the SSIS Bulk Insert task is already running.|  
|0xC020203F|-1071636417|DTS_E_BULKINSERTTHREADABNORMALCOMPLETION|The thread for the SSIS Bulk Insert task terminated with errors or warnings.|  
|0xC0202040|-1071636416|DTS_E_CANNOTGETIROWSETFASTLOAD|Failed to open a fastload rowset for "%1". Check that the object exists in the database.|  
|0xC0202041|-1071636415|DTS_E_CONNECTREQUIREDFORMETADATAVALIDATION|Error due to no connection. A connection is required before metadata validation can proceed.|  
|0xC0202042|-1071636414|DTS_E_DESTINATIONTABLENAMENOTPROVIDED|A destination table name has not been provided.|  
|0xC0202043|-1071636413|DTS_E_ICONVERTTYPEUNAVAILABLE|The OLE DB provider used by the OLE DB adapter does not support IConvertType. Set the adapter's ValidateColumnMetaData property to FALSE.|  
|0xC0202044|-1071636412|DTS_E_OLEDBPROVIDERDATATYPECONVERSIONUNSUPPORTED|The OLE DB provider used by the OLE DB adapter cannot convert between types "%1" and "%2" for "%3".|  
|0xC0202045|-1071636411|DTS_E_VALIDATECOLUMNMETADATAFAILED|Column metadata validation failed.|  
|0xC0202047|-1071636409|DTS_E_ATTEMPTINGTOINSERTINTOAROWIDCOLUMN|"%1" is a row ID column and cannot be included in a data insertion operation.|  
|0xC0202048|-1071636408|DTS_E_ATTEMPTINGTOINSERTINTOAROWVERCOLUMN|Attempting insertion into the row version column "%1". Cannot insert into a row version column.|  
|0xC0202049|-1071636407|DTS_E_ATTEMPTINGTOINSERTINTOAREADONLYCOLUMN|Failure inserting into the read-only column "%1".|  
|0xC020204A|-1071636406|DTS_E_UNABLETORETRIEVECOLUMNINFO|Unable to retrieve column information from the data source. Make sure your target table in the database is available.|  
|0xC020204B|-1071636405|DTS_E_CANTLOCKBUFFER|A buffer could not be locked. The system is out of memory or the buffer manager has reached its quota.|  
|0xC020204C|-1071636404|DTS_E_INVALIDCOMPARISONFLAGS|The %1 has a ComparisonFlags property that includes extra flags with the value %2!d!.|  
|0xC020204D|-1071636403|DTS_E_COLUMNMETADATAUNAVAILABLEFORVALIDATION|The column metadata was unavailable for validation.|  
|0xC0202053|-1071636397|DTS_E_CANNOTWRITETODATAFILE|Cannot write to the data file.|  
|0xC0202055|-1071636395|DTS_E_COLUMNDELIMITERNOTFOUND|The column delimiter for column "%1" was not found.|  
|0xC0202058|-1071636392|DTS_E_COLUMNPARSEFAILED|Failed to parse the column "%1" in the data file.|  
|0xC020205A|-1071636390|DTS_E_RAWFILENAMEREQUIRED|The file name is not properly specified.  Supply the path and name to the raw file either directly in the FileName property or by specifying a variable in the FileNameVariable property.|  
|0xC020205B|-1071636389|DTS_E_RAWFILECANTOPEN|File "%1" cannot be opened for writing. Error may occur when there are no file privileges or the disk is full.|  
|0xC020205C|-1071636388|DTS_E_RAWFILECANTBUFFER|An I/O buffer cannot be created for the output file. Error may occur when there are no file privileges or the disk is full.|  
|0xC020205D|-1071636387|DTS_E_RAWCANTWRITE|Cannot write %1!d! bytes to file "%2". See previous error messages for details.|  
|0xC020205E|-1071636386|DTS_E_RAWBADHEADER|Encountered bad metadata in file header. The file is damaged or not a SSIS-produced raw data file.|  
|0xC020205F|-1071636385|DTS_E_RAWEXISTSCREATEONCE|Error occurred because the output file already exists and the WriteOption is set to Create Once. Set the WriteOption property to Create Always, or delete the file.|  
|0xC0202060|-1071636384|DTS_E_RAWCANTAPPENDTRUNCATE|Error caused by conflicting property settings. Both the AllowAppend property and the ForceTruncate property are set to TRUE. Both properties cannot be set to TRUE. Set one of the two properties to FALSE.|  
|0xC0202061|-1071636383|DTS_E_RAWBADVERSION|The file had bad version and flags information. The file is damaged or not a SSIS-produced raw data file.|  
|0xC0202062|-1071636382|DTS_E_RAWVERSIONINCOMPATIBLEAPPEND|The output file was written by an incompatible version and cannot be appended. The file may be an older file format that is no longer useable.|  
|0xC0202064|-1071636380|DTS_E_RAWMETADATAMISMATCH|Cannot append output file because no column in the existing file matches column "%1" from the input. Old file does not match in metadata.|  
|0xC0202065|-1071636379|DTS_E_RAWMETADATACOUNTMISMATCH|Cannot append output file because the number of columns in the output file does not match the number of columns in this destination. The old file does not match in metadata.|  
|0xC0202067|-1071636377|DTS_E_ERRORRETRIEVINGCOLUMNCODEPAGE|There was an error retrieving column code page information.|  
|0xC0202068|-1071636376|DTS_E_RAWCANTREAD|Cannot read %1!d! bytes from file "%2". The cause of the failure should have been previously reported.|  
|0xC0202069|-1071636375|DTS_E_RAWUNEXPECTEDEOF|Unexpected end-of-file encountered while reading %1!d! bytes from file "%2". The file ended prematurely because of an invalid file format.|  
|0xC020206A|-1071636374|DTS_E_RAWNOLONGTYPES|The column %1 cannot be used. The raw adapters do not support image, text, or ntext data.|  
|0xC020206B|-1071636373|DTS_E_RAWUNEXPECTEDTYPE|The adapter encountered an unrecognized data type of %1!d!. This could be caused by a damaged input file (source) or by an invalid buffer type (destination).|  
|0xC020206C|-1071636372|DTS_E_RAWSTRINGTOOLONG|String too long. The adapter read a string that was %1!d! bytes long, and expected a string no longer than %2!d! bytes, at offset %3!d!. This could indicate a damaged input file. The file shows a string length that is too large for the buffer column.|  
|0xC020206E|-1071636370|DTS_E_RAWSKIPFAILED|The raw adapter attempted to skip %1!d! bytes in the input file for unreferenced column "%2" with lineage ID %3!d!, but there was an error. The error returned from the operating system should have been previously reported.|  
|0xC020206F|-1071636369|DTS_E_RAWREADFAILED|The raw adapter attempted to read %1!d! bytes in the input file for column "%2" with lineage ID %3!d!, but there was an error. The error returned from the operating system should have been previously reported.|  
|0xC0202070|-1071636368|DTS_E_RAWFILENAMEINVALID|The file name property is not valid. The file name is a device or contains invalid characters.|  
|0xC0202071|-1071636367|DTS_E_BULKINSERTAPIPREPARATIONFAILED|Unable to prepare the SSIS bulk insert for data insertion.|  
|0xC0202072|-1071636366|DTS_E_INVALIDDATABASEOBJECTNAME|Database object name "%1" is not valid.|  
|0xC0202073|-1071636365|DTS_E_INVALIDORDERCLAUSE|Order clause is not valid.|  
|0xC0202074|-1071636364|DTS_E_RAWFILECANTOPENREAD|File "%1" cannot be opened for reading. Error may occur when there are no privileges or the file is not found. Exact cause is reported in previous error message.|  
|0xC0202075|-1071636363|DTS_E_TIMEGENCANTCREATE|Unable to create the Microsoft.AnalysisServices.TimeDimGenerator.TimeDimGenerator.|  
|0xC0202076|-1071636362|DTS_E_TIMEGENCANTCONFIGURE|Unable to configure the Microsoft.AnalysisServices.TimeDimGenerator.|  
|0xC0202077|-1071636361|DTS_E_TIMEGENCANTCONVERT|Unsupported datatype for column %1!d!.|  
|0xC0202079|-1071636359|DTS_E_TIMEGENCANTREAD|The attempt to read from the Microsoft.AnalysisServices.TimeDimGenerator failed with error code 0x%1!8.8X!.|  
|0xC020207A|-1071636358|DTS_E_TIMEGENCANTREADCOLUMN|The attempt to read column "%2!d!" data from the Microsoft.AnalysisServices.TimeDimGenerator failed with error code 0x%2!8.8X!.|  
|0xC020207B|-1071636357|DTS_E_RSTDESTBADVARIABLENAME|The VariableName property is not set to the name of a valid variable. Need a runtime variable name to write to.|  
|0xC020207C|-1071636356|DTS_E_RSTDESTRSTCONFIGPROBLEM|Unable to create or configure the ADODB.Recordset object.|  
|0xC020207D|-1071636355|DTS_E_RSTDESTRSTWRITEPROBLEM|Error writing to the ADODB.Recordset object.|  
|0xC020207E|-1071636354|DTS_E_FILENAMEINVALID|The file name is not valid. The file name is a device or contains invalid characters.|  
|0xC020207F|-1071636353|DTS_E_FILENAMEINVALIDWITHPARAM|The file name "%1" is not valid. The file name is a device or contains invalid characters.|  
|0xC0202080|-1071636352|DTS_E_CMDDESTNOPARAMS|Unable to retrieve destination column descriptions from the parameters of the SQL command.|  
|0xC0202081|-1071636351|DTS_E_CMDDESTNOTBOUND|Parameters are not bound. All parameters in the SQL command must be bound to input columns.|  
|0xC0202082|-1071636350|DTS_E_TXPIVOTBADUSAGE|The PivotUsage value for the input column "%1" (%2!d!) is not valid.|  
|0xC0202083|-1071636349|DTS_E_TXPIVOTTOOMANYPIVOTKEYS|Too many Pivot Keys found. Only one input column can be used as the Pivot Key.|  
|0xC0202084|-1071636348|DTS_E_TXPIVOTNOPIVOTKEY|No Pivot Key found. One input column must be used as the Pivot Key.|  
|0xC0202085|-1071636347|DTS_E_TXPIVOTINPUTALREADYMAPPED|More than one output column (such as "%1" (%2!d!)) is mapped to input column "%3" (%4!d!).|  
|0xC0202086|-1071636346|DTS_E_TXPIVOTCANTMAPPIVOTKEY|Output column "%1" (%2!d!) cannot be mapped to PivotKey input column.|  
|0xC0202087|-1071636345|DTS_E_TXPIVOTCANTMAPPINGNOTFOUND|Output column "%1" (%2!d!) has a SourceColumn %3!d! that is not a valid input column lineage ID.|  
|0xC0202088|-1071636344|DTS_E_TXPIVOTEMPTYPIVOTKEYVALUE|Output column "%1" (%2!d!) is mapped to a Pivoted Value input column, but its PivotKeyValue property value is missing.|  
|0xC0202089|-1071636343|DTS_E_TXPIVOTDUPLICATEPIVOTKEYVALUE|Output column "%1" (%2!d!) is mapped to a Pivoted Value input column with a non-unique PivotKeyValue property value.|  
|0xC020208A|-1071636342|DTS_E_TXPIVOTOUTPUTNOTMAPPED|Input column "%1" (%2!d!) is not mapped to any output column.|  
|0xC020208B|-1071636341|DTS_E_TXPIVOTCANTCOMPARESETKEYS|Failure occurred while comparing values for the set keys.|  
|0xC020208D|-1071636339|DTS_E_TXPIVOTNOBLOB|The Input column "%1" (%2!d!) cannot be used as a Set Key, Pivot Key, or Pivot Value because it contains long data.|  
|0xC020208E|-1071636338|DTS_E_TXPIVOTBADOUTPUTTYPE|Incorrect output type. The output column "%1" (%2!d!) must have the same data type and metadata as the input column to which it is mapped.|  
|0xC020208F|-1071636337|DTS_E_TXPIVOTPROCESSERROR|Failure when trying to pivot the source records.|  
|0xC0202090|-1071636336|DTS_E_TXPIVOTBADPIVOTKEYVALUE|The pivot key value "%1" is not valid.|  
|0xC0202091|-1071636335|DTS_E_ERRORWHILESKIPPINGDATAROWS|An error occurred while skipping data rows.|  
|0xC0202092|-1071636334|DTS_E_ERRORWHILEREADINGDATAROWS|An error occurred while processing file "%1" on data row %2!I64d!.|  
|0xC0202093|-1071636333|DTS_E_FAILEDTOINITIALIZEFLATFILEPARSER|An error occurred while initializing the flat file parser.|  
|0xC0202094|-1071636332|DTS_E_UNABLETORETRIEVECOLUMNINFOFROMFLATFILECONNECTIONMANAGER|Unable to retrieve column information from the flat file connection manager.|  
|0xC0202095|-1071636331|DTS_E_FAILEDTOWRITEOUTCOLUMNNAME|Failed to write out column name for column "%1".|  
|0xC0202096|-1071636330|DTS_E_INVALIDFLATFILECOLUMNTYPE|The column type for column "%1" is incorrect. It is type "%2". It can only be either "%3" or "%4".|  
|0xC0202097|-1071636329|DTS_E_DISKIOBUFFEROVERFLOW|The attempt to write data of %1!d! bytes into the disk I/O failed. The disk I/O buffer has %2!d! free bytes.|  
|0xC0202098|-1071636328|DTS_E_FAILEDTOWRITEOUTHEADER|An error occurred while writing out the file header.|  
|0xC0202099|-1071636327|DTS_E_FAILEDTOGETFILESIZE|An error occurred while getting the file size for file "%1".|  
|0xC020209A|-1071636326|DTS_E_FAILEDTOSETFILEPOINTER|An error occurred while setting the file pointer for file "%1".|  
|0xC020209B|-1071636325|DTS_E_UNABLETOSETUPDISKIOBUFFER|An error occurred while setting up the disk I/O buffer.|  
|0xC020209C|-1071636324|DTS_E_COLUMNDATAOVERFLOWDISKIOBUFFER|The column data for column "%1" overflowed the disk I/O buffer.|  
|0xC020209D|-1071636323|DTS_E_DISKIOFAILED|An unexpected disk I/O error occurred while reading the file.|  
|0xC020209E|-1071636322|DTS_E_DISKIOTIMEDOUT|An disk I/O time out occurred while reading the file.|  
|0xC020209F|-1071636321|DTS_E_INPUTSNOTREADONLY|The Usage Type specified for the input columns to this transform cannot be read/write. Change the Usage Type to be read-only.|  
|0xC02020A0|-1071636320|DTS_E_CANNOTCOPYORCONVERTFLATFILEDATA|Cannot copy or convert flat file data for column "%1".|  
|0xC02020A1|-1071636319|DTS_E_FAILEDCOLUMNDATACONVERSIONSTATUS|Data conversion failed. The data conversion for column "%1" returned status value %2!d! and status text "%3".|  
|0xC02020A2|-1071636318|DTS_E_VARIABLESCOLLECTIONUNAVAILABLE|The Variables collection is not available.|  
|0xC02020A3|-1071636317|DTS_E_TXUNPIVOTDUPLICATEPIVOTKEYVALUE|Duplicate PivotKeyValue. Input column "%1" (%2!d!) is mapped to a Pivoted Value output column and has a non-unique PivotKeyValue.|  
|0xC02020A4|-1071636316|DTS_E_TXUNPIVOTNOUNPIVOTDESTINATION|No unpivot destination found. At least one input column must be mapped with a PivotKeyValue to an DestinationColumn in the output.|  
|0xC02020A5|-1071636315|DTS_E_TXUNPIVOTBADKEYLIST|PivotKeyValue is not valid. In an UnPivot transform with more than one unpivoted DestinationColumn, the set of PivotKeyValues per destination must match exactly.|  
|0xC02020A6|-1071636314|DTS_E_TXUNPIVOTBADUNPIVOTMETADATA|Incorrect UnPivot metadata. In an UnPivot transform, all input columns with a PivotKeyValue that is set, and are pointing to the same DestinationColumn, must have metadata that exactly matches the DestinationColumn.|  
|0xC02020A7|-1071636313|DTS_E_TXPIVOTBADPIVOTKEYCONVERT|Cannot convert the pivot key value "%1" to the data type of the pivot key column.|  
|0xC02020A8|-1071636312|DTS_E_TXUNPIVOTTOOMANYPIVOTKEYS|Too many Pivot Keys specified. Only one output column can be used as the Pivot Key.|  
|0xC02020A9|-1071636311|DTS_E_TXUNPIVOTUNMAPPEDOUTPUT|Output column "%1" (%2!d!) is not mapped by any input column's DestinationColumn property.|  
|0xC02020AA|-1071636310|DTS_E_TXUNPIVOTNOPIVOT|No output column is marked as the PivotKey.|  
|0xC02020AB|-1071636309|DTS_E_TXUNPIVOTNOTINPUTMAP|Input column "%1" (%2!d!) has a DestinationColumn property value that does not refer to a valid output column LineageID.|  
|0xC02020AC|-1071636308|DTS_E_TXUNPIVOTDUPLICATEDESTINATION|Duplicate destination error. More than one non-pivoted input column is mapped to the same destination output column.|  
|0xC02020AD|-1071636307|DTS_E_TOTALINPUTCOLSCANNOTBEZERO|No input columns found. At least one input column must be mapped to an output column.|  
|0xC02020AE|-1071636306|DTS_E_TXMERGEJOINMUSTHAVESAMENUMBEROFINPUTANDOUTPUTCOLS|The number of input and output columns are not equal. The total number of input columns on all inputs must be the same as the total number of output columns.|  
|0xC02020AF|-1071636305|DTS_E_INPUTMUSTBESORTED|The input is not sorted. The "%1" must be sorted.|  
|0xC02020B0|-1071636304|DTS_E_TXMERGEJOININVALIDJOINTYPE|The JoinType custom property for the %1 contains a value of %2!ld!, which is not valid. Valid values are 0 (full), 1 (left), or 2 (inner).|  
|0xC02020B1|-1071636303|DTS_E_TXMERGEJOININVALIDNUMKEYCOLS|The NumKeyColumns value is not valid. In the %1, the value for the NumKeyColumns custom property must be between 1 and %2!lu!.|  
|0xC02020B2|-1071636302|DTS_E_NOKEYCOLS|No key columns are found. The %1 must have at least one column with a SortKeyPosition that is non-zero.|  
|0xC02020B3|-1071636301|DTS_E_TXMERGEJOINNOTENOUGHKEYCOLS|Not enough key columns. The %1 must have at least %2!ld! columns with non-zero SortKeyPosition values.|  
|0xC02020B4|-1071636300|DTS_E_TXMERGEJOINDATATYPEMISMATCH|Datatype mismatch occurred. The datatypes for the columns with SortKeyPosition value %1!ld! do not match.|  
|0xC02020B5|-1071636299|DTS_E_TXMERGEJOININVALIDSORTKEYPOS|The column with the SortKeyPosition value of %1!ld! is not valid. It should be %2!ld!.|  
|0xC02020B6|-1071636298|DTS_E_TXMERGEJOINSORTDIRECTIONMISMATCH|Sort direction mismatch. The sort directions for the columns with SortKeyPosition value %1!ld! do not match.|  
|0xC02020B7|-1071636297|DTS_E_TXMERGEJOINOUTPUTCOLMUSTHAVEASSOCIATEDINPUTCOL|Missing column. The %1 must have an associated input column.|  
|0xC02020B8|-1071636296|DTS_E_TXMERGEJOINREADONLYINPUTCOLSWITHNOOUTPUTCOL|Input columns must have output columns. There are input columns with a usage type of read-only that do not have associated output columns.|  
|0xC02020B9|-1071636295|DTS_E_TXMERGEJOINNONSTRINGCOMPARISONFLAGSNOTZERO|The comparison flags are not zero. The comparison flags for non-string columns must be zero.|  
|0xC02020BA|-1071636294|DTS_E_TXMERGEJOINCOMPARISONFLAGSMISMATCH|The comparison flags for the columns with SortKeyPosition value %1!ld! do not match.|  
|0xC02020BB|-1071636293|DTS_E_TXPIVOTBADPIVOTKEYVALUENOSTRING|Unrecognized pivot key value.|  
|0xC02020BC|-1071636292|DTS_E_TXLINEAGEINVALIDLINEAGEITEM|Lineage item value %1!ld! is not valid. The valid range is between %2!ld! and %3!ld!.|  
|0xC02020BD|-1071636291|DTS_E_CANNOTHAVEANYINPUTCOLUMNS|Input columns not allowed. The number of input columns must be zero.|  
|0xC02020BE|-1071636290|DTS_E_TXLINEAGEDATATYPEMISMATCH|The datatype for "%1" is not valid for the specified lineage item.|  
|0xC02020BF|-1071636289|DTS_E_TXLINEAGEINVALIDLENGTH|The length for "%1" is not valid for the specified lineage item.|  
|0xC02020C1|-1071636287|DTS_E_METADATAMISMATCHWITHOUTPUTCOLUMN|The metadata for "%1" does not match the metadata for the associated output column.|  
|0xC02020C3|-1071636285|DTS_E_TXMERGESORTKEYPOSMISMATCH|There are output columns that have SortKeyPosition values that don't match the associated input columns' SortKeyPosition.|  
|0xC02020C4|-1071636284|DTS_E_ADDROWTOBUFFERFAILED|The attempt to add a row to the Data Flow task buffer failed with error code 0x%1!8.8X!.|  
|0xC02020C5|-1071636283|DTS_E_DATACONVERSIONFAILED|Data conversion failed while converting column "%1" (%2!d!) to column "%3" (%4!d!).  The conversion returned status value %5!d! and status text "%6".|  
|0xC02020C6|-1071636282|DTS_E_FAILEDTOALLOCATEROWHANDLEBUFFER|The attempt to allocate a row handle buffer failed with error code 0x%1!8.8X!.|  
|0xC02020C7|-1071636281|DTS_E_FAILEDTOSENDROWTOSQLSERVER|The attempt to send a row to SQL Server failed with error code 0x%1!8.8X!.|  
|0xC02020C8|-1071636280|DTS_E_FAILEDTOPREPAREBUFFERSTATUS|The attempt to prepare the buffer status failed with error code 0x%1!8.8X!.|  
|0xC02020C9|-1071636279|DTS_E_FAILEDTOBUFFERROWSTARTS|The attempt to retrieve the start of the buffer row failed with error code 0x%1!8.8X!.|  
|0xC02020CA|-1071636278|DTS_E_BULKINSERTTHREADTERMINATED|The thread for the SSIS Bulk Insert is no longer running.  No more rows can be inserted. Try increasing the bulk insert thread timeout.|  
|0xC02020CB|-1071636277|DTS_E_RAWTOOMANYCOLUMNS|The source file is not valid. The source file is returning a count of more than 131,072 columns. This usually occurs when the source file is not produced by the raw file destination.|  
|0xC02020CC|-1071636276|DTS_E_TXUNIONALL_EXTRADANGLINGINPUT|The %1 is an extra unattached input and will be removed.|  
|0xC02020CD|-1071636275|DTS_E_TXUNIONALL_NONDANGLINGUNATTACHEDINPUT|The %1 is not attached but is not marked as dangling.  It will be marked as dangling.|  
|0xC02020CF|-1071636273|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUE|Duplicate pivot key value "%1".|  
|0xC02020D0|-1071636272|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUENOSTRING|Duplicate pivot key value.|  
|0xC02020D1|-1071636271|DTS_E_FAILEDTOGETCOMPONENTLOCALEID|Failure retrieving component locale ID. Error code 0x%1!8.8X!.|  
|0xC02020D2|-1071636270|DTS_E_MISMATCHCOMPONENTCONNECTIONMANAGERLOCALEID|Mismatched locale IDs. The component locale ID (%1!d!) does not match the connection manager locale ID (%2!d!).|  
|0xC02020D3|-1071636269|DTS_E_LOCALEIDNOTSET|The component locale ID has not been set. Flat file adapters need to have the locale ID on the flat file connection manager set.|  
|0xC02020D4|-1071636268|DTS_E_RAWBYTESTOOLONG|The binary field is too large. The adapter attempted to read a binary field that was %1!d! bytes long, but expected a field no longer than %2!d! bytes at offset %3!d!. This usually occurs when the input file is not valid. The file contains a string length that is too large for the buffer column.|  
|0xC02020D5|-1071636267|DTS_E_TXSAMPLINGINVALIDPCT|The percentage, %2!ld!, is not valid for the "%1" property. It must be between 0 and 100.|  
|0xC02020D6|-1071636266|DTS_E_TXSAMPLINGINVALIDROWS|The number of rows, %2!ld!, is not valid for the "%1" property. It must be greater than 0.|  
|0xC02020D7|-1071636265|DTS_E_RAWSTRINGINPUTTOOLONG|The adapter was asked to write a string that was %1!I64d! bytes long, but all data must be less than 4294967295 bytes in length.|  
|0xC02020D9|-1071636263|DTS_E_ATLEASTONEINPUTMUSTBEMAPPEDTOOUTPUT|No inputs were mapped to an output. The "%1" must have at least one input column mapped to an output column.|  
|0xC02020DB|-1071636261|DTS_E_CANNOTCONVERTDATATYPESWITHDIFFERENTCODEPAGES|Conversion from "%1" with code page %2!d! to "%3" with code page %4!d! is not supported.|  
|0xC02020DC|-1071636260|DTS_E_COLUMNNOTMAPPEDTOEXTERNALMETADATACOLUMN|The external metadata column mapping for %1 is not valid.  The external metadata column ID cannot be zero.|  
|0xC02020DD|-1071636259|DTS_E_COLUMNMAPPEDTONONEXISTENTEXTERNALMETADATACOLUMN|The %1 is mapped to an external metadata column that does not exist.|  
|0xC02020E5|-1071636251|DTS_E_UNABLETOWRITELOBDATATOBUFFER|Writing long object data of type DT_TEXT, DT_NTEXT, or DT_IMAGE to Data Flow task buffer failed for column "%1".|  
|0xC02020E8|-1071636248|DTS_E_CANNOTGETIROWSET|Opening a rowset for "%1" failed. Check that the object exists in the database.|  
|0xC02020E9|-1071636247|DTS_E_VARIABLEACCESSFAILED|Accessing variable "%1" failed with error code 0x%2!8.8X!.|  
|0xC02020EA|-1071636246|DTS_E_CONNECTIONMANAGERNOTFOUND|The connection manager "%1" is not found. A component failed to find the connection manager in the Connections collection.|  
|0xC02020EB|-1071636245|DTS_E_VERSIONUPGRADEFAILED|The upgrade from version "%1" to version %2!d! failed.|  
|0xC02020EC|-1071636244|DTS_E_RSTDESTBIGBLOB|A value in an input column is too large to be stored in the ADODB.Recordset object.|  
|0xC02020ED|-1071636243|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|Columns "%1" and "%2" cannot convert between unicode and non-unicode string data types.|  
|0xC02020EE|-1071636242|DTS_E_ROWCOUNTBADVARIABLENAME|The variable "%1" specified by VariableName property is not a valid variable. Need a valid variable name to write to.|  
|0xC02020EF|-1071636241|DTS_E_ROWCOUNTBADVARIABLETYPE|The variable "%1" specified by VariableName property is not an integer. Change the variable to be of type VT_I4, VT_UI4, VT_I8, or VT_UI8.|  
|0xC02020F0|-1071636240|DTS_E_NOCOLUMNADVANCETHROUGHFILE|No column was specified to allow the component to advance through the file.|  
|0xC02020F1|-1071636239|DTS_E_MERGEJOINSORTEDOUTPUTHASNOSORTKEYPOSITIONS|The "%1" has IsSorted set to TRUE, but the SortKeyPosition on all output columns are zero. Either change the IsSorted to FALSE, or select at least one output column to contain a non-zero SortKeyPosition.|  
|0xC02020F2|-1071636238|DTS_E_METADATAMISMATCHWITHINPUTCOLUMN|The "%1" metadata does not match the metadata of the input column.|  
|0xC02020F3|-1071636237|DTS_E_RSTDESTBADVARIABLE|The value of the specified variable cannot be located, locked, or set.|  
|0xC02020F4|-1071636236|DTS_E_CANTPROCESSCOLUMNTYPECODEPAGE|The column "%1" cannot be processed because more than one code page (%2!d! and %3!d!) are specified for it.|  
|0xC02020F5|-1071636235|DTS_E_CANTINSERTCOLUMNTYPE|The column "%1" can't be inserted because the conversion between types %2 and %3 is not supported.|  
|0xC02020F6|-1071636234|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|Column "%1" cannot convert between unicode and non-unicode string data types.|  
|0xC02020F8|-1071636232|DTS_E_COULDNOTFINDINPUTBUFFERCOLUMNBYLINEAGE|The %1 cannot find the column with LineageID %2!ld! in its input buffer.|  
|0xC02020F9|-1071636231|DTS_E_COULDNOTGETCOLUMNINFOFORINPUTBUFFER|The %1 cannot get the column information for column %2!lu! from its input buffer.|  
|0xC02020FA|-1071636230|DTS_E_COULDNOTGETCOLUMNINFOFORCOPYBUFFER|The %1 cannot get the column information for column "%2!lu!" from its copy buffer.|  
|0xC02020FB|-1071636229|DTS_E_COULDNOTREGISTERCOPYBUFFER|The %1 cannot register a buffer type for its copy buffer.|  
|0xC02020FC|-1071636228|DTS_E_COULDNOTCREATECOPYBUFFER|The %1 cannot create a buffer to copy its data into for sorting.|  
|0xC02020FD|-1071636227|DTS_E_DATAREADERDESTREADFAILED|DataReader client has failed to call Read or has closed the DataReader.|  
|0xC02020FE|-1071636226|DTS_E_NOSCHEMAINFOFOUND|No column information was returned by the SQL command.|  
|0xC02020FF|-1071636225|DTS_E_GETSCHEMATABLEFAILED|The %1 was unable to retrieve column information for the SQL command. The following error occurred: %2|  
|0xC0202100|-1071636224|DTS_E_SOURCETABLENAMENOTPROVIDED|A source table name has not been provided.|  
|0xC0203110|-1071632112|DTS_E_CACHE_INVALID_INDEXPOS|The cache index position, %1!d!, is not valid. For non-index columns, the index position should be 0. For index columns, the index position should be a sequential, positive number.|  
|0xC0203111|-1071632111|DTS_E_CACHE_DUPLICATE_INDEXPOS|The index position, %1!d!, is a duplicate. For non-index columns, the index position should be 0. For index columns, the index position should be a sequential, positive number.|  
|0xC0203112|-1071632110|DTS_E_CACHE_TOO_FEW_INDEX_COLUMNS|At least one index column should be specified for the Cache connection manager. To specify an index column, set the Index Position property of the cache column.|  
|0xC0203113|-1071632109|DTS_E_CACHE_INDEXPOS_NOT_CONTINUOUS|Cache index positions must be contiguous. For non-index columns, the index position should be 0. For index columns, the index position should be a sequential, positive number.|  
|0xC0204000|-1071628288|DTS_E_PROPERTYNOTSUPPORTED|The property "%1" cannot be set on "%2". The property being set is not supported on the specified object. Check the property name, case, and spelling.|  
|0xC0204002|-1071628286|DTS_E_CANTCHANGEPROPERTYTYPE|The property type cannot be changed from the type that was set by the component.|  
|0xC0204003|-1071628285|DTS_E_CANTADDOUTPUTID|Output ID %1!d! failed during insert. The new output was not created.|  
|0xC0204004|-1071628284|DTS_E_CANTDELETEOUTPUTID|Cannot delete output ID %1!d! from the output collection.  The ID may not be valid, or the ID may have been the default or error output.|  
|0xC0204006|-1071628282|DTS_E_FAILEDTOSETPROPERTY|Failed to set property "%1" on "%2".|  
|0xC0204007|-1071628281|DTS_E_FAILEDTOSETOUTPUTCOLUMNTYPE|Failed to set the type of %1 to type: "%2", length: %3!d!, precision: %4!d!, scale: %5!d!, codepage: %6!d!.|  
|0xC0204008|-1071628280|DTS_E_MORETHANONEERROROUTPUTFOUND|More than one error output was found on the component, and there can be only one.|  
|0xC020400A|-1071628278|DTS_E_CANTSETOUTPUTCOLUMNPROPERTY|The property on an output column cannot be set.|  
|0xC020400B|-1071628277|DTS_E_CANTMODIFYERROROUTPUTCOLUMNDATATYPE|The data type for "%1" cannot be modified in the error "%2".|  
|0xC020400E|-1071628274|DTS_E_CANONLYSETISSORTEDONSOURCE|The "%1" cannot have its IsSorted property set to TRUE because it is not a source output. A source output has a SynchronousInputID value of zero.|  
|0xC020400F|-1071628273|DTS_E_CANONLYSETSORTKEYONSOURCE|The "%1" cannot have a SortKeyPosition property set to non-zero because "%2" is not a source output. The output column "colname" (ID) cannot have its SortKeyPosition property set to non-zero because its output "outputname" (ID) is not a source output.|  
|0xC0204010|-1071628272|DTS_E_CANONLYSETCOMPFLAGSONSOURCE|The ComparisonFlags property cannot be set to a non-zero value for "%1" because the "%2" is not a source output. The output column "colname" (ID) cannot have a ComparisonFlags property set to non-zero because its output "outputname" (ID) is not a source output.|  
|0xC0204011|-1071628271|DTS_E_NONSTRINGCOMPARISONFLAGSNOTZERO|The comparison flags for "%1" must be zero because its type is not a string type. ComparisonFlags can only be non-zero for string type columns.|  
|0xC0204012|-1071628270|DTS_E_COMPFLAGSONLYONSORTCOL|The "%1" cannot have a ComparisonFlags property set to non-zero because its SortKeyPosition is set to zero. An output column's ComparisonFlags can only be non-zero if its SortKeyPosition is also non-zero.|  
|0xC0204013|-1071628269|DTS_E_READONLYSTOCKPROPERTY|The property is read-only.|  
|0xC0204014|-1071628268|DTS_E_INVALIDDATATYPE|The %1 had an invalid datatype value (%2!ld!) set.|  
|0xC0204015|-1071628267|DTS_E_CODEPAGEREQUIRED|The "%1" requires a code page to be set but the value passed was zero.|  
|0xC0204016|-1071628266|DTS_E_INVALIDSTRINGLENGTH|The "%1" has a length that is not valid. The length must be between %2!ld! and %3!ld!.|  
|0xC0204017|-1071628265|DTS_E_INVALIDSCALE|The "%1" has a scale that is not valid. The scale must be between %2!ld! and %3!ld!.|  
|0xC0204018|-1071628264|DTS_E_INVALIDPRECISION|The "%1" has a precision that is not valid. The precision must be between %2!ld! and %3!ld!.|  
|0xC0204019|-1071628263|DTS_E_PROPVALUEIGNORED|The "%1" has a value set for length, precision, scale, or code page that is a value other than zero, but the data type requires the value to be zero.|  
|0xC020401A|-1071628262|DTS_E_CANTSETOUTPUTCOLUMNDATATYPEPROPERTIES|The %1 does not allow setting output column datatype properties.|  
|0xC020401B|-1071628261|DTS_E_INVALIDDATATYPEFORERRORCOLUMNS|The "%1" contains an invalid data type. "%1 " is a special error column,  and the only valid data type is DT_I4.|  
|0xC020401C|-1071628260|DTS_E_NOERRORDESCFORCOMPONENT|The component does not supply error code descriptions.|  
|0xC020401D|-1071628259|DTS_E_UNRECOGNIZEDERRORCODE|The specified error code is not associated with this component.|  
|0xC020401F|-1071628257|DTS_E_TRUNCATIONTRIGGEREDREDIRECTION|A truncation caused a row to be redirected, based on the truncation disposition settings.|  
|0xC0204020|-1071628256|DTS_E_CANTSETUSAGETYPETOREADWRITE|The "%1" is unable to make the column with lineage ID %2!d! read/write because that usage type is not allowed on this column. An attempt was made to change the usage type of an input column to a type, UT_READWRITE, that is not supported on this component.|  
|0xC0204023|-1071628253|DTS_E_CANTSETUSAGETYPE|The %1 has forbidden the requested use of the input column with lineage ID %2!d!.|  
|0xC0204024|-1071628252|DTS_E_FAILEDTOSETUSAGETYPE|The "%1" was unable to make the requested change to the input column with lineage ID %2!d!. The request failed with error code 0x%3!8.8X!. The specified error occurred while attempting to set the usage type of an input column.|  
|0xC0204025|-1071628251|DTS_E_FAILEDTOSETOUTPUTCOLUMNDATATYPEPROPERTIES|Attempt to set the data type properties on "%1" failed with error code 0x%2!8.8X!. The error occurred while attempting to set one or more of the data type properties of the output column.|  
|0xC0204026|-1071628250|DTS_E_UNABLETORETRIEVEMETADATA|The metadata for "%1" cannot be retrieved. Make sure the object name is correct and the object exists.|  
|0xC0204027|-1071628249|DTS_E_CANNOTMAPOUTPUTCOLUMN|The output column cannot be mapped to an external metadata column.|  
|0xC0204028|-1071628248|DTS_E_UNSUPPORTEDVARIABLETYPE|The variable %1 is required to be of type "%2".|  
|0xC020402A|-1071628246|DTS_E_CANTSETEXTERNALMETADATACOLUMNDATATYPEPROPERTIES|The %1 does not allow setting external metadata column datatype properties.|  
|0xC020402B|-1071628245|DTS_E_IDNOTINPUTNOROUTPUT|The ID, %1!lu!, is neither an input ID nor an output ID. The specified ID must be the input ID or the output ID that the external metadata collection is associated with.|  
|0xC020402C|-1071628244|DTS_E_METADATACOLLECTIONNOTUSED|The external metadata collection on "%1" is marked as not used, so no operations can be performed on it.|  
|0xC020402D|-1071628243|DTS_E_NOBUFFERTYPEONSYNCOUTPUT|The %1 is a synchronous output and the buffer type cannot be retrieved for a synchronous output.|  
|0xC0207000|-1071616000|DTS_E_INPUTCOLUMNUSAGETYPENOTREADONLY|The input column "%1" must be read-only. The input column has a usage type other than read-only, which is not allowed.|  
|0xC0207001|-1071615999|DTS_E_MISSINGCUSTOMPROPERTY|The "%1" is missing the required property "%2". The object is required to have the specified custom property.|  
|0xC0207002|-1071615998|DTS_E_ILLEGALCUSTOMOUTPUTPROPERTY|The output %1 cannot not have property "%2", but currently has that property assigned.|  
|0xC0207003|-1071615997|DTS_E_INVALIDOUTPUTEXCLUSIONGROUP|The %1 must be in exclusion group %2!d!. All outputs must be in the specified exclusion group.|  
|0xC0207004|-1071615996|DTS_E_PROPERTYISEMPTY|The property "%1" is empty. The property cannot be empty.|  
|0xC0207005|-1071615995|DTS_E_CREATEEXPRESSIONOBJECTFAILED|Memory cannot be allocated for the expression "%1". There was an out-of-memory error while creating an internal object to hold the expression.|  
|0xC0207006|-1071615994|DTS_E_EXPRESSIONPARSEFAILED|Cannot parse the expression "%1". The expression was not valid, or there is an out-of-memory error.|  
|0xC0207007|-1071615993|DTS_E_EXPRESSIONCOMPUTEFAILED|Computing the expression "%1" failed with error code 0x%2!8.8X!. The expression may have errors, such as divide by zero, that cannot be detected at parse time, or there may be an out-of-memory error.|  
|0xC0207008|-1071615992|DTS_E_FAILEDTOCREATEEXPRESSIONARRAY|Memory cannot be allocated for the Expression objects. An out-of-memory error occurred while creating the array of Expression object pointers.|  
|0xC020700A|-1071615990|DTS_E_FAILEDTOCREATEEXPRESSIONMANANGER|The %1 failed with error code 0x%2!8.8X! while creating the Expression Manager.|  
|0xC020700B|-1071615989|DTS_E_SPLITEXPRESSIONNOTBOOLEAN|The expression "%1" is not Boolean. The result type of the expression must be Boolean.|  
|0xC020700C|-1071615988|DTS_E_EXPRESSIONVALIDATIONFAILED|The expression "%1" on "%2" is not valid.|  
|0xC020700E|-1071615986|DTS_E_COLUMNNOTMATCHED|The column "%1" (%2!d!) cannot be matched to any input file column. The output column name or input column name cannot be found in the file.|  
|0xC020700F|-1071615985|DTS_E_SETRESULTCOLUMNFAILED|Attempting to set the result column for the expression "%1" on %2 failed with error code 0x%3!8.8X!. The input or output column that was to receive the result of the expression cannot be determined, or the expression result cannot be cast to the column type.|  
|0xC0207011|-1071615983|DTS_E_FAILEDTOGETLOCALEIDFROMPACKAGE|The %1 failed to get the locale ID from the package.|  
|0xC0207012|-1071615982|DTS_E_INCORRECTPARAMETERMAPPINGFORMAT|The parameter mapping string is not in the correct format.|  
|0xC0207013|-1071615981|DTS_E_NOTENOUGHPARAMETERSPROVIDED|The SQL command requires %1!d! parameters, but the parameter mapping only has %2!d! parameters.|  
|0xC0207014|-1071615980|DTS_E_PARAMETERNOTFOUNDINMAPPING|The SQL command requires a parameter named "%1", which is not found in the parameter mapping.|  
|0xC0207015|-1071615979|DTS_E_DUPLICATEDATASOURCECOLUMNNAME|There is more than one data source column with the name "%1".  The data source column names must be unique.|  
|0xC0207016|-1071615978|DTS_E_DATASOURCECOLUMNWITHNONAMEFOUND|There is a data source column with no name.  Each data source column must have a name.|  
|0xC0208001|-1071611903|DTS_E_DISCONNECTEDCOMPONENT|A component is disconnected from the layout.|  
|0xC0208002|-1071611902|DTS_E_INVALIDCOMPONENTID|The ID for a layout component is not valid.|  
|0xC0208003|-1071611901|DTS_E_INVALIDINPUTCOUNT|A component has an invalid number of inputs.|  
|0xC0208004|-1071611900|DTS_E_INVALIDOUTPUTCOUNT|A component has an invalid number of outputs.|  
|0xC0208005|-1071611899|DTS_E_NOINPUTSOROUTPUTS|A component does not have any inputs or outputs.|  
|0xC0208007|-1071611897|DTS_E_CANTALLOCATECOLUMNINFO|Not enough memory was available to allocate a list of the columns that are being manipulated by this component.|  
|0xC0208008|-1071611896|DTS_E_OUTPUTCOLUMNNOTININPUT|Output column "%1" (%2!d!) references input column with lineage ID %3!d!, but no input could be found with that lineage ID.|  
|0xC0208009|-1071611895|DTS_E_SORTNEEDSONEKEY|At least one input column must be marked as a sort key, but no keys were found.|  
|0xC020800A|-1071611894|DTS_E_SORTDUPLICATEKEYWEIGHT|Both column "%1" (%2!d!) and column "%3" (%4!d!) were marked with sort key weight %5!d!.|  
|0xC020800D|-1071611891|DTS_E_CANTMODIFYINVALID|The component cannot perform the requested metadata change until the validation problem is fixed.|  
|0xC020800E|-1071611890|DTS_E_CANTADDINPUT|An input cannot be added to the inputs collection.|  
|0xC020800F|-1071611889|DTS_E_CANTADDOUTPUT|An output cannot be added to the outputs collection.|  
|0xC0208010|-1071611888|DTS_E_CANTDELETEINPUT|An input cannot be deleted from the inputs collection.|  
|0xC0208011|-1071611887|DTS_E_CANTDELETEOUTPUT|An output cannot be removed from the outputs collection.|  
|0xC0208014|-1071611884|DTS_E_CANTCHANGEUSAGETYPE|The usage type of the column cannot be changed.|  
|0xC0208016|-1071611882|DTS_E_INVALIDUSAGETYPEFORCUSTOMPROPERTY|The %1 must be read/write to have custom property "%2". The input or output column has the specified custom property, but is not read/write. Remove the property, or make the column read/write.|  
|0xC0208017|-1071611881|DTS_E_READWRITECOLUMNMISSINGREQUIREDCUSTOMPROPERTY|The %1 is read/write and is required to have custom property "%2". Add the property, or make remove the read/write attribute from the column.|  
|0xC0208018|-1071611880|DTS_E_CANTDELETECOLUMN|The column cannot be deleted. The component does not allow columns to be deleted from this input or output.|  
|0xC0208019|-1071611879|DTS_E_CANTADDCOLUMN|The component does not allow adding columns to this input or output.|  
|0xC020801A|-1071611878|DTS_E_CANNOTTFINDRUNTIMECONNECTIONOBJECT|The connection "%1" cannot be found. Verify that the connection manager has a connection with that name.|  
|0xC020801B|-1071611877|DTS_E_CANNOTFINDRUNTIMECONNECTIONMANAGER|The runtime connection manager with the ID "%1" cannot be found. Verify that the connection manager collection has a connection manager with that ID.|  
|0xC020801C|-1071611876|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|SSIS Error Code DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER.  The AcquireConnection method call to the connection manager "%1" failed with error code 0x%2!8.8X!.  There may be error messages posted before this with more information on why the AcquireConnection method call failed.|  
|0xC020801D|-1071611875|DTS_E_ACQUIREDCONNECTIONISINVALID|The connection acquired from the connection manager "%1" is not valid.|  
|0xC020801E|-1071611874|DTS_E_INCORRECTCONNECTIONMANAGERTYPE|The connection manager "%1" is an incorrect type.  The type required is "%2". The type available to the component is "%3".|  
|0xC020801F|-1071611873|DTS_E_CANNOTACQUIREMANAGEDCONNECTIONFROMCONNECTIONMANAGER|Cannot acquire a managed connection from the run-time connection manager.|  
|0xC0208020|-1071611872|DTS_E_CANTINITINPUT|An input cannot be created to initialize the inputs collection.|  
|0xC0208021|-1071611871|DTS_E_CANTINITOUTPUT|An output cannot be created to initialize the outputs collection.|  
|0xC0208023|-1071611869|DTS_E_EXTRACTORCANTWRITE|Writing to the file "%1" failed with error code 0x%2!8.8X!.|  
|0xC0208024|-1071611868|DTS_E_INCORRECTCONNECTIONOBJECTTYPE|The connection manager "%1" returned an object of an  incorrect type from the AcquireConnection method.|  
|0xC0208025|-1071611867|DTS_E_INPUTCOLPROPERTYNOTFOUND|The "%3" property is required on input column "%1" (%2!d!), but is not found. The missing property should be added.|  
|0xC0208026|-1071611866|DTS_E_EXTRACTORUNREFERENCED|The "%1" is marked read-only, but is not referenced by any other column. Unreferenced columns are not allowed.|  
|0xC0208027|-1071611865|DTS_E_EXTRACTORREFERENCEDCOLUMNNOTFOUND|The "%1" references column ID %2!d!, and that column is not found on the input. A reference points to a nonexistent column.|  
|0xC0208028|-1071611864|DTS_E_EXTRACTORDATACOLUMNNOTBLOB|The "%1" references "%2", and that column is not of a BLOB type.|  
|0xC0208029|-1071611863|DTS_E_INSERTERREFERENCEDCOLUMNNOTFOUND|The "%1" references output column ID %2!d!, and that column is not found on the output.|  
|0xC020802A|-1071611862|DTS_E_INSERTERCANTREAD|Reading from the file "%1" failed with error code 0x%2!8.8X!.|  
|0xC020802B|-1071611861|DTS_E_TXSCD_NOTYPEDCOLUMNSATINPUT|There must be at least one column of Fixed, Changing, or Historical type on the input of a Slowly Changing Dimension transform. Verify that at least one column is a FixedAttribute, ChangingAttribute, or HistoricalAttribute.|  
|0xC020802C|-1071611860|DTS_E_TXSCD_INVALIDINPUTCOLUMNTYPE|The ColumnType property of "%1" is not valid. The current value is outside the range of acceptable values.|  
|0xC020802D|-1071611859|DTS_E_TXSCD_CANNOTMAPDIFFERENTTYPES|The input column "%1" cannot be mapped to external column "%2" because they have different data types. The Slowly Changing Dimension transform does not allow mapping between column of different types except for DT_STR and DT_WSTR.|  
|0xC020802E|-1071611858|DTS_E_NTEXTDATATYPENOTSUPPORTEDWITHANSIFILES|The data type for "%1" is DT_NTEXT, which is not supported with ANSI files. Use DT_TEXT instead and convert the data to DT_NTEXT using the data conversion component.|  
|0xC020802F|-1071611857|DTS_E_TEXTDATATYPENOTSUPPORTEDWITHUNICODEFILES|The data type for "%1" is DT_TEXT, which is not supported with Unicode files. Use DT_NTEXT instead and convert the data to DT_TEXT using the data conversion component.|  
|0xC0208030|-1071611856|DTS_E_IMAGEDATATYPENOTSUPPORTED|The data type for "%1" is DT_IMAGE, which is not supported. Use DT_TEXT or DT_NTEXT instead and convert the data from, or to, DT_IMAGE using the data conversion component.|  
|0xC0208031|-1071611855|DTS_E_FLATFILEFORMATNOTSUPPORTED|Format "%1" is not supported by Flat File Connection Manager. Supported formats are Delimited, FixedWidth, RaggedRight, and Mixed.|  
|0xC0208032|-1071611854|DTS_E_EXTRACTORFILENAMECOLUMNNOTSTRING|The "%1" should contain a file name, but it is not of a String type.|  
|0xC0208033|-1071611853|DTS_E_EXTRACTORCANTAPPENDTRUNCATE|Error caused by conflicting property settings. The "%1" has both the AllowAppend property and the ForceTruncate property set to TRUE. Both properties cannot be set to TRUE. Set one of the two properties to FALSE.|  
|0xC0208034|-1071611852|DTS_E_EXTRACTORCOLUMNALREADYREFERENCED|The %1 references column ID %2!d!, but that column is already referenced by %3. Remove one of the two reference to the column.|  
|0xC0208035|-1071611851|DTS_E_CONNECTIONMANANGERNOTASSIGNED|A connection manager has not been assigned to the %1.|  
|0xC0208036|-1071611850|DTS_E_INSERTERCOLUMNALREADYREFERENCED|The %1 references the output column with ID %2!d!, but that column is already referenced by %3.|  
|0xC0208037|-1071611849|DTS_E_INSERTERCOLUMNNOTREFERENCED|The "%1" is not referenced by any input column. Each output column must be referenced by exactly one input column.|  
|0xC0208038|-1071611848|DTS_E_INSERTERDATACOLUMNNOTBLOB|The "%1" references "%2", and that column is not the correct type. It must be DT_TEXT, DT_NTEXT, or DT_IMAGE. A reference points to a column that must be a BLOB.|  
|0xC0208039|-1071611847|DTS_E_INSERTERFILENAMECOLUMNNOTSTRING|The "%1" should contain a file name, but it is not a String type.|  
|0xC020803A|-1071611846|DTS_E_INSERTEREXPECTBOMINVALIDTYPE|The "%1" has the ExpectBOM property set to TRUE for %2, but the column is not NT_NTEXT. The ExpectBOM specifies that the Import Column transformation expects a byte-order mark (BOM). Either set the ExpectBOM property to false or change the output column data type to DT_NTEXT.|  
|0xC020803B|-1071611845|DTS_E_INSERTERINVALIDDATACOLUMNSETTYPE|Data output columns must be DT_TEXT, DT_NTEXT, or DT_IMAGE. The data output column may only be set to a BLOB type.|  
|0xC020803C|-1071611844|DTS_E_TXSCD_FIXEDATTRIBUTECHANGE|If the FailOnFixedAttributeChange property is set to TRUE, the transformation will fail when a fixed attribute change is detected. To send rows to the Fixed Attribute output, set the FailOnFixedAttributeChange property to FALSE.|  
|0xC020803D|-1071611843|DTS_E_TXSCD_LOOKUPFAILURE|The Lookup transformation failed to retrieve any rows. The transform fails when the FailOnLookupFailure is set to TRUE and no rows are retrieved.|  
|0xC020803E|-1071611842|DTS_E_TXSCD_INVALIDNUMBERSOFPARAMETERS|There must be at least one column type of Key on the input of a Slowly Changing Dimension transformation. Set at least one column type to Key.|  
|0xC020803F|-1071611841|DTS_E_TXSCD_CANNOTFINDEXTERNALCOLUMN|Cannot find external column with name "%1".|  
|0xC0208040|-1071611840|DTS_E_TXSCD_INFFEREDINDICATORNOTBOOL|Inferred indicator column "%1" must be of type DT_BOOL.|  
|0xC0208107|-1071611641|DTS_E_ERRORROWDISPMUSTBENOTUSED|The %1 must have its error row disposition value set to RD_NotUsed.|  
|0xC0208108|-1071611640|DTS_E_TRUNCROWDISPMUSTBENOTUSED|The %1 must have its truncation row disposition value set to RD_NotUsed.|  
|0xC0208201|-1071611391|DTS_E_TXAGG_INPUTNOTFOUNDFOROUTPUT|Cannot find input column with lineage ID %1!d! needed by output column with ID %2!d!.|  
|0xC0208202|-1071611390|DTS_E_TXAGG_INVALIDOUTPUTDATATYPEFORAGGREGATE|Invalid output data type for aggregate type specified at output column ID %1!d!.|  
|0xC0208203|-1071611389|DTS_E_TXAGG_INVALIDINPUTDATATYPEFORAGGREGATE|Invalid input data type for %1 used for the specified aggregate at %2.|  
|0xC0208204|-1071611388|DTS_E_TXAGG_INPUTOUTPUTDATATYPEMISMATCH|Data types of input column lineage ID %1!d! and output column ID %2!d! do not match.|  
|0xC0208205|-1071611387|DTS_E_UNABLETOGETINPUTBUFFERHANDLE|Cannot get input buffer handle for input ID %1!d!.|  
|0xC0208206|-1071611386|DTS_E_UNABLETOGETOUTPUTBUFFERHANDLE|Cannot get output buffer handle for output ID %1!d!.|  
|0xC0208207|-1071611385|DTS_E_UNABLETOFINDCOLUMNHANDLEINOUTPUTBUFFER|Cannot find column with lineage ID %1!d! in output buffer.|  
|0xC0208208|-1071611384|DTS_E_UNABLETOFINDCOLUMNHANDLEININPUTBUFFER|Cannot find column with lineage ID %1!d! in input buffer.|  
|0xC0208209|-1071611383|DTS_E_CANNOTHAVEZEROOUTPUTCOLUMNS|The number of output columns for %1 cannot be zero.|  
|0xC020820A|-1071611382|DTS_E_CONNECTIONMANAGERCOLUMNCOUNTMISMATCH|The number of columns in the flat file connection manager must be the same as the number of columns in the flat file adapter. The number of columns for the flat file connection manager is %1!d!, while the number of columns for the flat file adapter is %2!d!.|  
|0xC020820B|-1071611381|DTS_E_MISMATCHCONNECTIONMANAGERCOLUMN|The column "%1" at index %2!d! in the flat file connection manager was not found at index %3!d! in the column collection of the flat file adapter.|  
|0xC020820D|-1071611379|DTS_E_EXTERNALMETADATACOLUMNISALREADYMAPPED|The external metadata column with ID %1!d! has already been mapped to %2.|  
|0xC020820E|-1071611378|DTS_E_TXAGG_STRING_TOO_LONG|The transform encountered a key column that was larger than %1!u! characters.|  
|0xC020820F|-1071611377|DTS_E_DERIVEDRESULT_TOO_LONG|The transform encountered a result value that was longer than %1!u! bytes.|  
|0xC0208210|-1071611376|DTS_E_TXAGG_MEMALLOCERROUTPUTDESCRIPTORS|Unable to allocate memory.|  
|0xC0208211|-1071611375|DTS_E_TXAGG_MEMALLOCERRWORKSPACEDESCRIPTORS|Unable to allocate memory.|  
|0xC0208212|-1071611374|DTS_E_TXAGG_MEMALLOCERRSORTORDERDESCRIPTORS|Unable to allocate memory.|  
|0xC0208213|-1071611373|DTS_E_TXAGG_MEMALLOCERRNUMERICDESCRIPTORS|Unable to allocate memory.|  
|0xC0208214|-1071611372|DTS_E_TXAGG_MEMALLOCERRCOUNTDISTINCTDESCRIPTOR|Unable to allocate memory.|  
|0xC0208215|-1071611371|DTS_E_TXAGG_MEMALLOCERRWORKSPACESORTORDERDESCRIPTORS|Unable to allocate memory.|  
|0xC0208216|-1071611370|DTS_E_TXAGG_MEMALLOCERRWORKSPACENUMERICDESCRIPTORS|Unable to allocate memory.|  
|0xC0208217|-1071611369|DTS_E_TXAGG_MEMALLOCERRWORKSPACEBUFFCOLS|Unable to allocate memory.|  
|0xC0208218|-1071611368|DTS_E_UNREFERENCEDINPUTCOLUMN|The input column "%1" is not referenced.|  
|0xC0208219|-1071611367|DTS_E_CANTBUILDTHREADPOOL|The Sort transformation could not create a thread pool with %1!d! threads. Not enough memory is available.|  
|0xC020821A|-1071611366|DTS_E_QUEUEWORKITEMFAILED|The Sort transformation cannot queue a work item to its thread pool. There is not enough memory available.|  
|0xC020821B|-1071611365|DTS_E_SORTTHREADSTOPPED|A worker thread in the Sort transformation stopped with error code 0x%1!8.8X!. A catastrophic error was encountered while sorting a buffer.|  
|0xC020821E|-1071611362|DTS_E_SORTBADTHREADCOUNT|MaxThreads was %1!ld!, and should be between 1 and %2!ld!, inclusive or -1 to default to the number of CPUs.|  
|0xC020821F|-1071611361|DTS_E_DTPXMLLOADFAILURE|Unable to load from XML.|  
|0xC0208220|-1071611360|DTS_E_DTPXMLSAVEFAILURE|Unable to save to XML.|  
|0xC0208221|-1071611359|DTS_E_DTPXMLINT32CONVERTERR|Unable to convert the value "%1" to an integer.|  
|0xC0208222|-1071611358|DTS_E_DTPXMLBOOLCONVERTERR|Unable to convert the value "%1" to a Boolean.|  
|0xC0208223|-1071611357|DTS_E_DTPXMLPARSEERRORNEARID|Load error encountered near object with ID %1!d!.|  
|0xC0208226|-1071611354|DTS_E_DTPXMLPROPERTYTYPEERR|The value "%1" is not valid for the attribute "%2".|  
|0xC0208228|-1071611352|DTS_E_DTPXMLSETUSAGETYPEERR|The value "%1" is not valid for the attribute "%2".|  
|0xC0208229|-1071611351|DTS_E_DTPXMLDATATYPEERR|The value "%1" is not valid for the attribute "%2".|  
|0xC020822A|-1071611350|DTS_E_UNMAPPEDINPUTCOLUMN|The %1 is not mapped to an output column.|  
|0xC020822B|-1071611349|DTS_E_INPUTCOLUMNBADMAP|The %1 has a mapping that is not valid.  An output column with an ID of %2!ld! does not exist on this component.|  
|0xC020822D|-1071611347|DTS_E_MULTIPLYMAPPEDOUTCOL|The %1 is mapped to an output column that already has a mapping on this input.|  
|0xC020822E|-1071611346|DTS_E_TXAGG_STRINGPROMOTIONFAILED|Could not convert input column with Lineage ID %1!ld! to DT_WSTR due to error 0x%2!8.8X!.|  
|0xC0208230|-1071611344|DTS_E_DTPXMLIDLOOKUPERR|Referenced object with ID %1!d! not found in package.|  
|0xC0208231|-1071611343|DTS_E_DTPXMLINVALIDXMLPERSISTPROPERTY|Cannot read a persistence property required for the pipelinexml module. The property was not provided by the pipeline.|  
|0xC0208232|-1071611342|DTS_E_DTPXMLPROPERTYSTATEERR|The value "%1" is not valid for the attribute "%2".|  
|0xC0208233|-1071611341|DTS_E_CANTGETCUSTOMPROPERTY|Cannot retrieve custom property "%1".|  
|0xC0208234|-1071611340|DTS_E_UNABLETOLOCATEINPUTCOLUMNID|An input column with the lineage ID %1!d!, referenced in the ParameterMap custom property with the parameter on position number %2!d!, cannot be found in the input columns collection.|  
|0xC0208235|-1071611339|DTS_E_TXLOOKUP_UNABLETOLOCATEREFCOLUMN|Unable to locate reference column "%1".|  
|0xC0208236|-1071611338|DTS_E_TXLOOKUP_INCOMPATIBLEDATATYPES|%1 and reference column named "%2" have incompatible data types.|  
|0xC0208237|-1071611337|DTS_E_TXLOOKUP_PARAMMETADATAMISMATCH|The parameterized SQL statement yields metadata which does not match the main SQL statement.|  
|0xC0208238|-1071611336|DTS_E_TXLOOKUP_INCORRECTNUMOFPARAMETERS|The parameterized SQL statement contains an incorrect number of parameters. Expected %1!d!, but found %2!d!.|  
|0xC0208239|-1071611335|DTS_E_TXLOOKUP_INVALIDJOINTYPE|%1 has a datatype which cannot be joined on.|  
|0xC020823A|-1071611334|DTS_E_TXLOOKUP_INVALIDCOPYTYPE|%1 has a datatype which cannot be copied.|  
|0xC020823B|-1071611333|DTS_E_INSERTERINVALIDCOLUMNDATATYPE|The %1 has an unsupported datatype. It must be DT_STR or DT_WSTR.|  
|0xC020823C|-1071611332|DTS_E_EXTRACTORINVALIDCOLUMNDATATYPE|The %1 has an unsupported datatype. It must be DT_STR, DT_WSTR, DT_TEXT, DT_NTEXT, or DT_IMAGE.|  
|0xC020823D|-1071611331|DTS_E_TXCHARMAPINVALIDCOLUMNDATATYPE|The %1 has an unsupported datatype. It must be DT_STR, DT_WSTR, DT_TEXT, or DT_NTEXT.|  
|0xC020823E|-1071611330|DTS_E_SORTCANTCREATEEVENT|The Sort transformation cannot create an event to communicate with its worker threads. Not enough system handles are available to the Sort transformation.|  
|0xC020823F|-1071611329|DTS_E_SORTCANTCREATETHREAD|The Sort transformation cannot create a worker thread. Not enough memory is available to Sort transformation.|  
|0xC0208240|-1071611328|DTS_E_SORTCANTCOMPARE|The Sort transformation failed to compare row %1!d! in buffer ID %2!d! to row %3!d! in buffer ID %4!d!.|  
|0xC0208242|-1071611326|DTS_E_TXLOOKUP_TOOFEWREFERENCECOLUMNS|The Lookup transformation reference metadata contains too few columns. Check the SQLCommand property. The SELECT statement must return at least one column.|  
|0xC0208243|-1071611325|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNINFO|Unable to allocate memory for an array of ColumnInfo structures.|  
|0xC0208244|-1071611324|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNPAIR|Could not allocate memory for an array of ColumnPair structures.|  
|0xC0208245|-1071611323|DTS_E_TXLOOKUP_MALLOCERR_BUFFCOL|Unable to allocate memory for an array of BUFFCOL structures for the creation of a main workspace.|  
|0xC0208246|-1071611322|DTS_E_TXLOOKUP_MAINWORKSPACE_CREATEERR|Unable to create a main workspace buffer.|  
|0xC0208247|-1071611321|DTS_E_TXLOOKUP_HASHTABLE_MALLOCERR|Unable to allocate memory for hash table.|  
|0xC0208248|-1071611320|DTS_E_TXLOOKUP_HASHNODEHEAP_CREATEERR|Unable to allocate memory to create a heap for hash nodes.|  
|0xC0208249|-1071611319|DTS_E_TXLOOKUP_HASHNODEHEAP_MALLOCERR|Unable to allocate memory for a hash node heap.|  
|0xC020824A|-1071611318|DTS_E_TXLOOKUP_LRUNODEHEAP_CREATEERR|Unable to create a heap for LRU nodes. An out-of-memory condition occurred.|  
|0xC020824B|-1071611317|DTS_E_TXLOOKUP_LRUNODEHEAP_MALLOCERR|Unable to allocate memory for the LRU node heap. An out-of-memory condition occurred.|  
|0xC020824C|-1071611316|DTS_E_TXLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|OLE DB error occurred while loading column metadata. Check SQLCommand and SqlCommandParam properties.|  
|0xC020824D|-1071611315|DTS_E_TXLOOKUP_OLEDBERR_GETIROWSET|OLE DB error occurred while fetching rowset. Check SQLCommand and SqlCommandParam properties.|  
|0xC020824E|-1071611314|DTS_E_TXLOOKUP_OLEDBERR_FILLBUFFER|OLE DB error occurred while populating internal cache. Check SQLCommand and SqlCommandParam properties.|  
|0xC020824F|-1071611313|DTS_E_TXLOOKUP_OLEDBERR_BINDPARAMETERS|OLE DB error occurred while binding parameters. Check SQLCommand and SqlCommandParam properties.|  
|0xC0208250|-1071611312|DTS_E_TXLOOKUP_OLEDBERR_CREATEBINDING|OLE DB error occurred while creating bindings. Check SQLCommand and SqlCommandParam properties.|  
|0xC0208251|-1071611311|DTS_E_TXLOOKUP_INVALID_CASE|An invalid case was encountered in a switch statement during runtime.|  
|0xC0208252|-1071611310|DTS_E_TXLOOKUP_MAINWORKSPACE_MALLOCERR|Unable to allocate memory for a new row for the main workspace buffer. An out-of-memory condition occurred.|  
|0xC0208253|-1071611309|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMIROWSET|OLE DB error occurred while fetching parameterized rowset. Check SQLCommand and SqlCommandParam properties.|  
|0xC0208254|-1071611308|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMSINGLEROW|OLE DB error occurred while fetching parameterized row. Check SQLCommand and SqlCommandParam properties.|  
|0xC0208255|-1071611307|DTS_E_TXAGG_MAINWORKSPACE_MALLOCERR|Unable to allocate memory for a new row for the main workspace buffer. An out-of-memory condition occurred.|  
|0xC0208256|-1071611306|DTS_E_TXAGG_MAINWORKSPACE_CREATEERR|Unable to create a main workspace buffer.|  
|0xC0208257|-1071611305|DTS_E_TXAGG_HASHTABLE_MALLOCERR|Unable to allocate memory for the hash table.|  
|0xC0208258|-1071611304|DTS_E_TXAGG_HASHNODEHEAP_CREATEERR|Unable to allocate memory to create a heap for the hash nodes.|  
|0xC0208259|-1071611303|DTS_E_TXAGG_HASHNODEHEAP_MALLOCERR|Unable to allocate memory for the hash node heap.|  
|0xC020825A|-1071611302|DTS_E_TXAGG_CDNODEHEAP_CREATEERR|Unable to allocate memory to create a heap for CountDistinct nodes.|  
|0xC020825B|-1071611301|DTS_E_TXAGG_CDNODEHEAP_MALLOCERR|Unable to allocate memory for CountDistinct node heap.|  
|0xC020825C|-1071611300|DTS_E_TXAGG_CDCHAINHEAP_CREATEERR|Unable to allocate memory to create a heap for CountDistinct chains.|  
|0xC020825D|-1071611299|DTS_E_TXAGG_CDHASHTABLE_CREATEERR|Unable to allocate memory for CountDistinct hash table.|  
|0xC020825E|-1071611298|DTS_E_TXAGG_CDWORKSPACE_MALLOCERR|Unable to allocate memory for a new row for the CountDistinct workspace buffer.|  
|0xC020825F|-1071611297|DTS_E_TXAGG_CDWORKSPACE_CREATEERR|Unable to create a CountDistinct workspace buffer.|  
|0xC0208260|-1071611296|DTS_E_TXAGG_CDCOLLASSEARRAY_MALLOCERR|Unable to allocate memory for CountDistinct Collapse array.|  
|0xC0208261|-1071611295|DTS_E_TXAGG_CDCHAINHEAP_MALLOCERR|Unable to allocate memory for CountDistinct chains.|  
|0xC0208262|-1071611294|DTS_E_TXCOPYMAP_MISMATCHED_COLUMN_METADATA|Columns with lineage IDs %1!d! and %2!d! have mismatched metadata. The input column that is mapped to an output column for copymap does not have the same metadata (datatype, precision, scale, length, or codepage).|  
|0xC0208263|-1071611293|DTS_E_TXCOPYMAP_INCORRECT_OUTPUT_COLUMN_MAPPING|The output column with lineage ID "%1!d!" is incorrectly mapped to an input column. The CopyColumnId property of the output column is not correct.|  
|0xC0208265|-1071611291|DTS_E_CANTGETBLOBDATA|Failed to retrieve long data for column "%1".|  
|0xC0208266|-1071611290|DTS_E_CANTADDBLOBDATA|Long data was retrieved for a column but cannot be added to the Data Flow task buffer.|  
|0xC0208267|-1071611289|DTS_E_MCASTOUTPUTCOLUMNS|Output "%1" (%2!d!) has output columns, but multicast outputs do not declare columns. The package is damaged.|  
|0xC0208273|-1071611277|DTS_E_UNABLETOGETLOCALIZEDRESOURCE|Unable to load a localized resource ID %1!d!. Verify that the RLL file is present.|  
|0xC0208274|-1071611276|DTS_E_DTPXMLEVENTSCACHEERR|Cannot acquire Events Interface. An invalid Events interface was passed to the data flow module for persisting to XML.|  
|0xC0208275|-1071611275|DTS_E_DTPXMLPATHLOADERR|An error occurred while setting a path object during XML load.|  
|0xC0208276|-1071611274|DTS_E_DTPXMLINPUTLOADERR|Error setting input object during XML load.|  
|0xC0208277|-1071611273|DTS_E_DTPXMLOUTPUTLOADERR|Error setting output object during XML load.|  
|0xC0208278|-1071611272|DTS_E_DTPXMLINPUTCOLUMNLOADERR|Error setting input column object during XML load.|  
|0xC0208279|-1071611271|DTS_E_DTPXMLOUTPUTCOLUMNLOADERR|Error setting output column object during XML load.|  
|0xC0208280|-1071611264|DTS_E_DTPXMLPROPERTYLOADERR|Error setting property object during XML load.|  
|0xC0208281|-1071611263|DTS_E_DTPXMLCONNECTIONLOADERR|Error setting connection object during XML load.|  
|0xC0208282|-1071611262|DTS_E_FG_MISSING_OUTPUT_COLUMNS|Special transformation-specific columns are either missing or have incorrect types.|  
|0xC0208283|-1071611261|DTS_E_FG_PREPARE_TABLES_AND_ACCESSORS|Fuzzy Grouping transformation failed to create required tables and accessors.|  
|0xC0208284|-1071611260|DTS_E_FG_COPY_INPUT|Fuzzy Grouping transformation failed to copy input.|  
|0xC0208285|-1071611259|DTS_E_FG_GENERATE_GROUPS|Fuzzy Grouping transformation failed to generate groups.|  
|0xC0208286|-1071611258|DTS_E_FG_LEADING_TRAILING|An unexpected error occurred in Fuzzy Grouping when applying the settings of property '%1'.|  
|0xC0208287|-1071611257|DTS_E_FG_PICK_CANONICAL|The Fuzzy Grouping transformation failed to pick a canonical row of data to use in standardizing the data.|  
|0xC0208288|-1071611256|DTS_E_FG_NOBLOBS|Fuzzy Grouping does not support input columns of type IMAGE, TEXT, or NTEXT.|  
|0xC0208289|-1071611255|DTS_E_FG_FUZZY_MATCH_ON_NONSTRING|A fuzzy match is specified on column "%1" (%2!d!) that is not a data type of DT_STR or DT_WSTR.|  
|0xC020828A|-1071611254|DTS_E_FUZZYGROUPINGINTERNALPIPELINEERROR|A Fuzzy Grouping transformation pipeline error occurred and returned error code 0x%1!8.8X!: "%2".|  
|0xC020828B|-1071611253|DTS_E_CODE_PAGE_NOT_SUPPORTED|The code page %1!d! specified on column "%2" (%3!d!) is not supported.  You must first convert this column to DT_WSTR which can be done by inserting a Data Conversion Transform before this one.|  
|0xC0208294|-1071611244|DTS_E_SETEODFAILED|Failure encountered while setting end of data flag for the buffer driving output "%1" (%2!d!).|  
|0xC0208296|-1071611242|DTS_E_CANTCLONE|The input buffer could not be cloned. An out-of-memory condition occurred or there was an internal error.|  
|0xC02082F9|-1071611143|DTS_E_TXCHARMAP_CANTKATAKANAHIRAGANA|Column "%1" requests that Katakana and Hiragana characters be produced at the same time.|  
|0xC02082FA|-1071611142|DTS_E_TXCHARMAP_CANTSIMPLECOMPLEX|Column "%1" requests that Simple Chinese and Traditional Chinese characters be produced at the same time.|  
|0xC02082FB|-1071611141|DTS_E_TXCHARMAP_CANTFULLHALF|Column "%1" requests operations to generate both full width and half width characters.|  
|0xC02082FC|-1071611140|DTS_E_TXCHARMAP_CANTCHINAJAPAN|Column "%1" combines operations on Japanese characters with operations for Chinese characters.|  
|0xC02082FD|-1071611139|DTS_E_TXCHARMAP_CANTCASECHINESE|Column "%1" combines operations on Chinese characters with uppercase and lowercase operations.|  
|0xC02082FE|-1071611138|DTS_E_TXCHARMAP_CANTCASEJAPANESE|Column "%1" combines operations on Japanese characters with uppercase and lowercase operations.|  
|0xC02082FF|-1071611137|DTS_E_TXCHARMAP_CANTBOTHCASE|Column "%1" maps the column to both uppercase and lowercase.|  
|0xC0208300|-1071611136|DTS_E_TXCHARMAP_CANTLINGUISTIC|Column "%1" combines flags other than uppercase and lowercase with the linguistic casing operation.|  
|0xC0208301|-1071611135|DTS_E_TXCHARMAP_INVALIDMAPFLAGANDDATATYPE|The data type of column "%1" cannot be mapped as specified.|  
|0xC0208302|-1071611134|DTS_E_TXFUZZYLOOKUP_UNSUPPORTED_MATCH_INDEX_VERSION|The version (%1) of the pre-existing match index "%2" is not supported. The version expected is "%3". This error occurs if the version persisted in the index metadata does not match the version which the current code was built for. Fix the error by rebuilding the index with the current version of the code.|  
|0xC0208303|-1071611133|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX|The table "%1" does not appear to be a valid pre-built match index. This error occurs if the metadata record cannot be loaded from the specified pre-built index.|  
|0xC0208304|-1071611132|DTS_E_TXFUZZYLOOKUP_UNABLE_TO_READ_MATCH_INDEX|Unable to read specified pre-built match index "%1".  OLEDB Error code: 0x%2!8.8X!.|  
|0xC0208305|-1071611131|DTS_E_TXFUZZYLOOKUP_NO_JOIN_COLUMNS|There were no input columns with a valid join to a reference table column.  Make sure that there is at least one join defined using the input column properties JoinToReferenceColumn and JoinType.|  
|0xC0208306|-1071611130|DTS_E_TXFUZZYLOOKUP_INDEX_DOES_NOT_CONTAIN_COLUMN|The specified pre-existing match index "%1" was not originally built with fuzzy match information for column "%2".  It must be rebuilt to include this information. This error occurs when the index was built with the column not being a fuzzy join column.|  
|0xC0208307|-1071611129|DTS_E_TXFUZZYLOOKUP_IDENTIFIER_PROPERTY|The name "%1" given for property "%2" is not a valid SQL identifier name. This error occurs if the name for the property does not conform to the specifications for a valid SQL identifier name.|  
|0xC0208309|-1071611127|DTS_E_TXFUZZYLOOKUP_MINSIMILARITY_INVALID|The MinSimilarity threshold property on the Fuzzy Lookup transformation must be a value greater than or equal to 0.0 but less than 1.0.|  
|0xC020830A|-1071611126|DTS_E_TXFUZZYLOOKUP_INVALID_PROPERTY_VALUE|The value "%1" for property "%2" is not valid.|  
|0xC020830B|-1071611125|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_FUZZY_JOIN_DATATYPES|The fuzzy lookup specified between input column "%1" and reference column "%2" is not valid because fuzzy joins are only supported between string columns, types DT_STR and DT_WSTR.|  
|0xC020830C|-1071611124|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_EXACT_JOIN_DATATYPES|The exact lookup columns, "%1" and "%2", do not have equal data types or are not comparable string types. Exact joins are supported between columns with equal data types or a DT_STR and DT_WSTR combination.|  
|0xC020830D|-1071611123|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_COPYCOLUMN_DATATYPES|The copy columns, "%1" and "%2", do not have equal data types or are not trivially convertible string types. This occurs because copying from reference to output between columns with equal data types, or a DT_STR and DT_WSTR combination, is supported, but other types are not.|  
|0xC020830E|-1071611122|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_PASSTHRUCOLUMN_DATATYPES|The passthrough columns, "%1" and "%2", do not have equal data types. Only columns with equal data types are supported as passthrough columns from input to output.|  
|0xC020830F|-1071611121|DTS_E_TXFUZZYLOOKUP_UNABLETOLOCATEREFCOLUMN|Cannot locate reference column "%1".|  
|0xC0208311|-1071611119|DTS_E_TXFUZZYLOOKUP_OUTPUT_COLUMN_MUST_BE_PASSTHRU_COLUMN_OR_A_COPY_COLUMN|An output column must have exactly one CopyColumn or PassThruColumn property specified. This error occurs when neither the CopyColumn or the PassThruColumn properties, or both the CopyColumn and PassThruColumn properties, are set to non-empty values.|  
|0xC0208312|-1071611118|DTS_E_TXFUZZYLOOKUP_PASSTHRU_COLUMN_NOT_FOUND|The source lineage id '%1!d!' specified for property '%2' on output column '%3' was not found in the input column collection. This occurs when the input column id specified on an output column as a passthrough column is not found in the set of inputs.|  
|0xC0208313|-1071611117|DTS_E_TXFUZZYLOOKUP_INDEXED_COLUMN_NOT_FOUND_IN_REF_TABLE|The column "%1" in the pre-built index "%2" was not found in the reference table/query. This happens if the schema/query of the reference table has changed since the pre-existing match index was built.|  
|0xC0208314|-1071611116|DTS_E_TXFUZZYLOOKUP_TOKEN_TOO_LONG|The component encountered a token that was larger than 2147483647 characters.|  
|0xC0208315|-1071611115|DTS_E_RAWMETADATAMISMATCHTYPE|The output file cannot be appended. Column "%1" matches by name, but the column in the file has type %2 and the input column has type %3. The metadata for the column does not match on data type.|  
|0xC0208316|-1071611114|DTS_E_RAWMETADATAMISMATCHSIZE|The output file cannot be appended. Column "%1" matches by name, but the column in the file has maximum length %2!d! and the input column has maximum length %3!d!. The metadata for the column does not match in length.|  
|0xC0208317|-1071611113|DTS_E_RAWMETADATAMISMATCHCODEPAGE|The output file cannot be appended. Column "%1" matches by name, but the column in the file has code page %2!d! and the input column has code page %3!d!. The metadata for the named column does not match on code page.|  
|0xC0208318|-1071611112|DTS_E_RAWMETADATAMISMATCHPRECISION|The output file cannot be appended. Column "%1" matches by name, but the column in the file has precision %2!d! and the input column has precision %3!d!. The metadata for the named column does not match on precision.|  
|0xC0208319|-1071611111|DTS_E_RAWMETADATAMISMATCHSCALE|The output file cannot be appended. Column "%1" matches by name, but the column in the file has scale %2!d! and the input column has scale %3!d!.  The metadata for the named column does not match on scale.|  
|0xC020831A|-1071611110|DTS_E_COULD_NOT_DETERMINE_DATASOURCE_DBMSNAME|Unable to determine the DBMS name and version on "%1". This occurs if the IDBProperties on the connection did not return information needed to verify the DBMS name and version.|  
|0xC020831B|-1071611109|DTS_E_INCORRECT_SQL_SERVER_VERSION|The DBMS type or version of "%1" is not supported.  A connection to Microsoft SQL Server version 8.0 or later is required. This occurs if IDBProperties on the connection did not return a the correct version.|  
|0xC020831D|-1071611107|DTS_E_CANTDELETEERRORCOLUMNS|The %1 is a special error output column and cannot be deleted.|  
|0xC020831E|-1071611106|DTS_E_UNEXPECTEDCOLUMNDATATYPE|The data type specified for column "%1" is not the expected type "%2".|  
|0xC020831F|-1071611105|DTS_E_INPUTCOLUMNNOTFOUND|The input column lineage ID "%1" referenced by property "%2" on output column "%3" could not be located in the input column collection.|  
|0xC0208320|-1071611104|DTS_E_TXGROUPDUPS_INPUTCOLUMNNOTJOINED|The input column "%1" referenced by the "%2" property on output column "%3" must have property ToBeCleaned=True and have a valid ExactFuzzy property value.|  
|0xC0208322|-1071611102|DTS_E_TXFUZZYLOOKUP_REF_TABLE_MISSING_IDENTITY_INDEX|The reference table '%1' does not have a clustered index on an integer identity column, which is required if the property 'CopyRefTable' is set to FALSE. If CopyRefTable is false, the reference table must have a clustered index on an integer identity column.|  
|0xC0208323|-1071611101|DTS_E_TXFUZZYLOOKUP_REF_CONTAINS_NON_INTEGER_IDENT_COLUMN|The reference table '%1' contains a non-integer type identity column which is not supported. Use a view of the table without the column '%2'.  This error occurs  because when a copy is made of the reference table, an integer identity column is added, and only one identity column is allowed per table.|  
|0xC0208324|-1071611100|DTS_E_TXFUZZY_MATCHCONTRIBUTION_AND_HIERARCHY_SPECIFIED|Both MatchContribution and hierarchy information cannot be specified at the same time. This is not allowed because these properties are both weighing factors for scoring.|  
|0xC0208325|-1071611099|DTS_E_TXFUZZY_HIERARCHY_INCORRECT|Levels in hierarchy should be unique numbers . Valid  level in hierarchy values are integers greater than or equal to 1. The smaller the number is, the lower the column is in the hierarchy. The default value is 0, indicating that the column is not part of a hierarchy. Overlaps and gaps are not allowed.|  
|0xC0208326|-1071611098|DTS_E_TXFUZZYGROUPING_INSUFFICIENT_FUZZY_JOIN_COLUMNS|No columns to fuzzy group on were defined.  There must be at least one input column with column properties ToBeCleaned=true and ExactFuzzy=2.|  
|0xC0208329|-1071611095|DTS_E_TXFUZZYLOOKUP_COLUMNINVALID|The column with ID '%1!d!' was not valid for an undetermined reason.|  
|0xC020832A|-1071611094|DTS_E_TXFUZZYLOOKUP_UNSUPPORTEDDATATYPE|The data type of column '%1' is not supported.|  
|0xC020832C|-1071611092|DTS_E_TXFUZZYLOOKUP_OUTPUTLENGTHMISMATCH|The length of output column '%1' is less than that of its source column '%2'.|  
|0xC020832F|-1071611089|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFINPUTCOLUMNS|There should be only one input column.|  
|0xC0208330|-1071611088|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFOUTPUTCOLUMNS|There should be exactly two output columns.|  
|0xC0208331|-1071611087|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFINPUTCOLUMN|The input column can only have DT_WSTR or DT_NTEXT as its data type.|  
|0xC0208332|-1071611086|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFOUTPUTCOLUMN|The output column [%1!d!] can only have '%2' as its data type.|  
|0xC0208333|-1071611085|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFREFERENCECOLUMN|The reference column can only have DT_STR or DT_WSTR as its data type.|  
|0xC0208334|-1071611084|DTS_E_TERMEXTRACTION_UNABLETOLOCATEREFCOLUMN|An error occurred while locating the reference column '%1'.|  
|0xC0208335|-1071611083|DTS_E_TERMEXTRACTION_INCORRECTTERMTYPE|The Term Type of the transformation can only be WordOnly, PhraseOnly or WordPhrase.|  
|0xC0208336|-1071611082|DTS_E_TERMEXTRACTION_INCORRECTFREQUENCYTHRESHOLD|The value of Frequency Threshold should not be lower than '%1!d!'.|  
|0xC0208337|-1071611081|DTS_E_TERMEXTRACTION_INCORRECTMAXLENOFTERM|The value of Max Length of Term should not be lower than '%1!d!'.|  
|0xC0208338|-1071611080|DTS_E_TERMEXTRACTION_TOOFEWREFERENCECOLUMNS|Term Extraction reference metadata contains too few columns.|  
|0xC0208339|-1071611079|DTS_E_TERMEXTRACTION_MALLOCERR_REFERENCECOLUMNINFO|An error occurred while allocating memory.|  
|0xC020833A|-1071611078|DTS_E_TERMEXTRACTION_MAINWORKSPACE_CREATEERR|An error occurred while creating a workspace buffer.|  
|0xC020833B|-1071611077|DTS_E_TERMEXTRACTION_OLEDBERR_CREATEBINDING|An OLEDB error occurred while creating bindings.|  
|0xC020833C|-1071611076|DTS_E_TERMEXTRACTION_OLEDBERR_GETIROWSET|An OLEDB error occurred while fetching rowsets.|  
|0xC020833D|-1071611075|DTS_E_TERMEXTRACTION_OLEDBERR_FILLBUFFER|An OLEDB error occurred while populating internal cache.|  
|0xC020833E|-1071611074|DTS_E_TERMEXTRACTION_PROCESSERR|An error occurred while extracting terms on row %1!ld!, column %2!ld!. The error code returned was 0x%3!8.8X!. Please remove it from the input as a work-around.|  
|0xC020833F|-1071611073|DTS_E_TERMEXTRACTIONORLOOKUP_PROCESSERR_DEPOSITFULL|The number of the term candidates exceeds its limit, 4G.|  
|0xC0208340|-1071611072|DTS_E_TERMEXTRACTION_INVALIDOUTTERMTABLEORCOLUMN|The reference table, view, or column that is used for Exclusion Terms is not valid.|  
|0xC0208341|-1071611071|DTS_E_TXFUZZYLOOKUP_STRINGCOLUMNTOOLONG|The length of string column '%1' exceeds 4000 characters.  A conversion from DT_STR to DT_WSTR is necessary, so a truncation would occur.  Either reduce the column width or use only DT_WSTR column types.|  
|0xC0208342|-1071611070|DTS_E_TERMEXTRACTION_OUTTERMTABLEANDCOLUMNNOTSET|The reference table, view, or column to be used for an Exclusion Terms has not been set.|  
|0xC0208343|-1071611069|DTS_E_TERMLOOKUP_TOOFEWOUTPUTCOLUMNS|Term Lookup contains too few output columns.|  
|0xC0208344|-1071611068|DTS_E_TERMLOOKUP_INCORRECTDATATYPEOFREFERENCECOLUMN|The reference column can only have DT_STR or DT_WSTR as its data type.|  
|0xC0208345|-1071611067|DTS_E_TERMLOOKUP_UNABLETOLOCATEREFCOLUMN|An error occurred while locating the reference column '%1'.|  
|0xC0208346|-1071611066|DTS_E_TERMLOOKUP_TOOFEWREFERENCECOLUMNS|Term Lookup reference metadata contains too few columns.|  
|0xC0208347|-1071611065|DTS_E_TERMEXTRACTIONORLOOKUP_TESTOFFSETERROR|An error occurred while normalizing words.|  
|0xC0208348|-1071611064|DTS_E_TERMLOOKUP_MAINWORKSPACE_CREATEERR|An error occurred while creating a workspace buffer.|  
|0xC0208349|-1071611063|DTS_E_TERMLOOKUP_OLEDBERR_CREATEBINDING|An OLEDB error occurred while creating bindings.|  
|0xC020834A|-1071611062|DTS_E_TERMLOOKUP_OLEDBERR_GETIROWSET|An OLEDB error occurred while fetching rowsets.|  
|0xC020834B|-1071611061|DTS_E_TERMLOOKUP_OLEDBERR_FILLBUFFER|An OLEDB error occurred while populating internal cache.|  
|0xC020834C|-1071611060|DTS_E_TERMLOOKUP_PROCESSERR|An error occurred while looking up terms on row %1!ld!, column %2!ld!. The error code returned was 0x%3!8.8X!. Please remove it from the input as a work-around.|  
|0xC020834D|-1071611059|DTS_E_TERMLOOKUP_TEXTIDINPUTCOLUMNNOTMAPPEDWITHOUTPUTCOLUMN|At least one Passthrough column is not mapped to an output column.|  
|0xC020834E|-1071611058|DTS_E_TERMLOOKUP_INCORRECTEXACTNUMBEROFTEXTCOLUMNS|There should be exactly one input column mapped to one reference column.|  
|0xC020834F|-1071611057|DTS_E_TERMLOOKUP_TEXTINPUTCOLUMNHAVEINCORRECTDATATYPE|The input column mapped to a reference column can only have DT_NTXT or DT_WSTR as its data type.|  
|0xC0208354|-1071611052|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX_NAME|The reference table name "%1" is not a valid SQL identifier. This error occurs if the table name cannot be parsed from the input string. There may be unquoted spaces in the name. Verify that the name is correctly quoted.|  
|0xC0208355|-1071611051|DTS_E_TERMEXTRACTION_TERMFILTERSTARTITERATIONERROR|An error occurred while the Term Filter was starting its iteration.|  
|0xC0208356|-1071611050|DTS_E_TERMEXTRACTION_EMPTYTERMRESULTERROR|An error occurred while reclaiming the buffer used for caching terms. The error code returned was 0x%1!8.8X!.|  
|0xC0208357|-1071611049|DTS_E_TERMEXTRACTION_STDLENGTHERROR|An std::length_error occurred from the STL containers.|  
|0xC0208358|-1071611048|DTS_E_TERMLOOKUP_SAVEWORDWITHPUNCTERROR|An error occurred while saving words with punctuation characters. The error code returned was 0x%1!8.8X!.|  
|0xC0208359|-1071611047|DTS_E_TERMLOOKUP_ADDREFERENCETERM|An error occurred while processing the %1!ld!th reference term. The error code returned was 0x%2!8.8X!. Please remove the reference term from your reference table as a work-around.|  
|0xC020835A|-1071611046|DTS_E_TERMLOOKUP_SORREFERENCETERM|An error occurred while sorting reference terms. The error code returned was 0x%1!8.8X!.|  
|0xC020835B|-1071611045|DTS_E_TERMLOOKUP_COUNTTERM|An error occurred while counting term candidates. The error code returned was 0x%1!8.8X!.|  
|0xC020835C|-1071611044|DTS_E_FUZZYLOOKUP_REFERENCECACHEFULL|Fuzzy Lookup was unable to load the entire reference table into main memory as is required when the Exhaustive property is enabled.  Either we ran out of system memory or a limit was specified for MaxMemoryUsage which was not sufficient to load the reference table.  Either set MaxMemoryUsage to 0 or increase it significantly.  Alternatively, disable Exhaustive.|  
|0xC020835D|-1071611043|DTS_E_TERMLOOKUP_INITIALIZE|An error occurred while initializing the engine of Term Lookup. The error code returned was 0x%1!8.8X!.|  
|0xC020835E|-1071611042|DTS_E_TERMLOOKUP_PROCESSSENTENCE|An error occurred while processing sentences. The error code returned was 0x%1!8.8X!.|  
|0xC020835F|-1071611041|DTS_E_TEXTMININGBASE_APPENDTOTEMPBUFFER|An error occurred while adding strings to an internal buffer. The error code returned was 0x%1!8.8X!.|  
|0xC0208360|-1071611040|DTS_E_TERMEXTRACTION_SAVEPOSTAG|An error occurred while saving part-of-speech tags from an internal buffer. The error code returned was 0x%1!8.8X!.|  
|0xC0208361|-1071611039|DTS_E_TERMEXTRACTION_COUNTTERM|An error occurred while counting term candidates. The error code returned was 0x%1!8.8X!.|  
|0xC0208362|-1071611038|DTS_E_TERMEXTRACTION_INITPOSPROCESSOR|An error occurred while initializing the part-of-speech processor. The error code returned was 0x%1!8.8X!.|  
|0xC0208363|-1071611037|DTS_E_TERMEXTRACTION_INITFSA|An error occurred while loading the finite state automata. The error code returned was 0x%1!8.8X!.|  
|0xC0208364|-1071611036|DTS_E_TERMEXTRACTION_INITIALIZE|An error occurred while initializing the engine of Term Extraction. The error code returned was 0x%1!8.8X!.|  
|0xC0208365|-1071611035|DTS_E_TERMEXTRACTION_PROCESSSENTENCE|An error occurred while processing within a sentence. The error code returned was 0x%1!8.8X!.|  
|0xC0208366|-1071611034|DTS_E_TERMEXTRACTION_INITPOSTAGVECTOR|An error occurred while initializing the part-of-speech processor. The error code returned was 0x%1!8.8X!.|  
|0xC0208367|-1071611033|DTS_E_TERMEXTRACTION_SAVEPTRSTRING|An error occurred while adding strings to an internal buffer. The error code returned was 0x%1!8.8X!.|  
|0xC0208368|-1071611032|DTS_E_TERMEXTRACTION_ADDWORDTODECODER|An error occurred while adding words to a statistical decoder. The error code returned was 0x%1!8.8X!.|  
|0xC0208369|-1071611031|DTS_E_TERMEXTRACTION_DECODE|An error occurred while decoding for a sentence. The error code returned was 0x%1!8.8X!.|  
|0xC020836A|-1071611030|DTS_E_TERMEXTRACTION_SETEXCLUDEDTERM|An error occurred while setting exclusion terms. The error code returned was 0x%1!8.8X!.|  
|0xC020836B|-1071611029|DTS_E_TERMEXTRACTION_PROCESSDOCUMENT|An error occurred while processing a document in the input. The error code returned was 0x%1!8.8X!.|  
|0xC020836C|-1071611028|DTS_E_TEXTMININGBASE_TESTPERIOD|An error occurred while testing whether a dot is a part of an acronym. The error code returned was 0x%1!8.8X!.|  
|0xC020836D|-1071611027|DTS_E_TERMLOOKUP_ENGINEADDREFERENCETERM|An error occurred while setting reference terms. The error code returned was 0x%1!8.8X!.|  
|0xC020836E|-1071611026|DTS_E_TERMLOOKUP_PROCESSDOCUMENT|An error occurred while processing a document in the input. The error code returned was 0x%1!8.8X!.|  
|0xC020836F|-1071611025|DTS_E_INVALIDBULKINSERTPROPERTYVALUE|The value for the property %1 is %2!d!, which is not allowed.  The value must be greater than or equal to %3!d!.|  
|0xC0208370|-1071611024|DTS_E_INVALIDBULKINSERTFIRSTROWLASTROWVALUES|The value for the property %1 is %2!d!, which must be less than or equal to the value of %3!d! for property %4.|  
|0xC0208371|-1071611023|DTS_E_FUZZYLOOKUPUNABLETODELETEEXISTINGMATCHINDEX|An error was encountered when trying to delete the existing fuzzy match index named "%1". It is possible that this table was not created by Fuzzy Lookup (or this version of Fuzzy Lookup), it has been damaged, or there is another problem. Try manually deleting the table named "%2" or specify a different name for the MatchIndexName property.|  
|0xC0208372|-1071611022|DTS_E_TERMEXTRACTION_INCORRECTSCORETYPE|The Score Type of the transformation can only be Frequency or TFIDF.|  
|0xC0208373|-1071611021|DTS_E_FUZZYLOOKUPREFTABLETOOBIG|The reference table specified has too many rows. Fuzzy Lookup only works with reference tables having less than 1 billion rows. Consider using a smaller view of your reference table.|  
|0xC0208374|-1071611020|DTS_E_FUZZYLOOKUPUNABLETODETERMINEREFERENCETABLESIZE|Unable to determine the size of the reference table '%1'.  It is possible that this object is a view and not a table.  Fuzzy Lookup does not support views when CopyReferentaceTable=false.  Make sure that the table exists and that CopyReferenceTable=true.|  
|0xC0208377|-1071611017|DTS_E_XMLSRCOUTPUTCOLUMNDATATYPENOTSUPPORTED|The SSIS Data Flow Task data type "%1" on the %2 is not supported for the %3.|  
|0xC0208378|-1071611016|DTS_E_XMLSRCCANNOTFINDCOLUMNTOSETDATATYPE|Unable to set data type properties for the output column with ID %1!d! on the output with ID %2!d!. The output or column could not be found.|  
|0xC0208379|-1071611015|DTS_E_CUSTOMPROPERTYISREADONLY|The value of custom property "%1" on the %2 cannot be changed.|  
|0xC020837A|-1071611014|DTS_E_OUTPUTCOLUMNHASNOERRORCOLUMN|The %1 on the non-error output has no corresponding output column on the error output.|  
|0xC020837B|-1071611013|DTS_E_ERRORCOLUMNHASNOOUTPUTCOLUMN|The %1 on the error output has no corresponding output column on the non-error output.|  
|0xC020837C|-1071611012|DTS_E_ERRORCOLUMNHASINCORRECTPROPERTIES|The %1 on the error output has properties that do not match the properties of its corresponding data source column.|  
|0xC020837D|-1071611011|DTS_E_ADOSRCOUTPUTCOLUMNDATATYPECANNOTBECHANGED|The data type of output columns on the %1 cannot be changed, except for DT_WSTR and DT_NTEXT columns.|  
|0xC020837F|-1071611009|DTS_E_ADOSRCDATATYPEMISMATCH|The data type of "%1" does not match the data type "%2" of the source column "%3".|  
|0xC0208380|-1071611008|DTS_E_ADOSRCCOLUMNNOTINSCHEMAROWSET|The %1 does not have a matching source column in the schema.|  
|0xC0208381|-1071611007|DTS_E_TERMLOOKUP_INVALIDREFERENCETERMTABLEORCOLUMN|The reference table/view or column used for the reference terms is invalid.|  
|0xC0208382|-1071611006|DTS_E_TERMLOOKUP_REFERENCETERMTABLEANDCOLUMNNOTSET|The reference table/view or column used for the reference terms has not been set.|  
|0xC0208383|-1071611005|DTS_E_COLUMNMAPPEDTOALREADYMAPPEDEXTERNALMETADATACOLUMN|The %1 is mapped to the external metadata column with ID %2!ld!, which is already mapped to another column.|  
|0xC0208384|-1071611004|DTS_E_TXFUZZYLOOKUP_TOOMANYPREFIXES|The SQL object name '%1' specified for property '%2' contains more than the maximum number of prefixes.  The maximum is 2.|  
|0xC0208385|-1071611003|DTS_E_MGDSRCSTATIC_OVERFLOW|The value was too large to fit in the column.|  
|0xC0208386|-1071611002|DTS_E_DATAREADERDESTREADERISCLOSED|The SSIS IDataReader is closed.|  
|0xC0208387|-1071611001|DTS_E_DATAREADERDESTREADERISATEND|The SSIS IDataReader is past the end of the result set.|  
|0xC0208388|-1071611000|DTS_E_DATAREADERDESTINVALIDCOLUMNORDINAL|The ordinal position of the column is not valid.|  
|0xC0208389|-1071610999|DTS_E_DATAREADERDESTCANNOTCONVERT|Cannot convert the %1 from data type "%2" to data type "%3".|  
|0xC020838A|-1071610998|DTS_E_DATAREADERDESTINVALIDCODEPAGE|The %1 has unsupported code page %2!d!.|  
|0xC020838B|-1071610997|DTS_E_XMLSRCEXTERNALMETADATACOLUMNNOTINSCHEMA|The %1 has no mapping to the XML schema.|  
|0xC020838D|-1071610995|DTS_E_TXTERMLOOKUP_MISMATCHED_COLUMN_METADATA|Columns with lineage IDs %1!d! and %2!d! have mismatched metadata. The input column that is mapped to an output column does not have the same metadata (datatype, precision, scale, length, or codepage).|  
|0xC020838E|-1071610994|DTS_E_DATAREADERDESTREADERTIMEOUT|The SSIS IDataReader is closed. The read timeout has expired.|  
|0xC020838F|-1071610993|DTS_E_ADOSRCINVALIDSQLCOMMAND|An error occurred executing the provided SQL command: "%1". %2|  
|0xC0208390|-1071610992|DTS_E_JOINTYPEDOESNTMATCHETI|The JoinType property specified for input column '%1' differs from the JoinType specified for the corresponding reference table column when the Match Index was initially created.  Either rebuild the Match Index with the given JoinType or change the JoinType to match the type used when the Match Index was created.|  
|0xC0208392|-1071610990|DTS_E_SQLCEDESTDATATYPENOTSUPPORTED|The data type "%1" found on column "%2" is not supported for the %3.|  
|0xC0208393|-1071610989|DTS_E_DATAREADERDESTDATATYPENOTSUPPORTED|The data type "%1" found on %2 is not supported for the %3.|  
|0xC0208394|-1071610988|DTS_E_RECORDSETDESTDATATYPENOTSUPPORTED|The data type of the %1 is not supported for the %2.|  
|0xC0208446|-1071610810|DTS_E_TXSCRIPTMIGRATIONCOULDNOTADDREFERENCE|Failed to add project reference "%1" while migrating %2. Migration might need to be completed manually.|  
|0xC0208447|-1071610809|DTS_E_TXSCRIPTMIGRATIONMULTIPLEENTRYPOINTSFOUND|Multiple entry points with the name "%1" were found during the migration of %2. Migration might need to be completed manually.|  
|0xC0208448|-1071610808|DTS_E_TXSCRIPTMIGRATIONNOENTRYPOINTFOUND|No entry point was found during the migration of %1. Migration might need to be completed manually.|  
|0xC020844B|-1071610805|DTS_E_ADODESTINSERTIONFAILURE|An exception has occurred during data insertion, the message returned from the provider is: %1|  
|0xC020844C|-1071610804|DTS_E_ADODESTCONNECTIONTYPENOTSUPPORTED|Failed to retrieve the provider invariant name from %1, it is currently not supported by ADO NET Destination component|  
|0xC020844D|-1071610803|DTS_E_ADODESTARGUMENTEXCEPTION|An argument exception has occurred while data provider tried to insert data to destination. The returned message is : %1|  
|0xC020844E|-1071610802|DTS_E_ADODESTWRONGBATCHSIZE|The BatchSize property must be a non-negative integer|  
|0xC020844F|-1071610801|DTS_E_ADODESTERRORUPDATEROW|An error has occurred while sending this row to destination data source.|  
|0xC0208450|-1071610800|DTS_E_ADODESTEXECUTEREADEREXCEPTION|Executing tSQL command throws an exception, the message is :  %1|  
|0xC0208451|-1071610799|DTS_E_ADODESTDATATYPENOTSUPPORTED|The data type "%1" found on column "%2" is not supported for the %3.|  
|0xC0208452|-1071610798|DTS_E_ADODESTFAILEDTOACQUIRECONNECTION|ADO NET Destination has failed to acquire the connection %1. The connection may have been corrupted.|  
|0xC0208453|-1071610797|DTS_E_ADODESTNOTMANAGEDCONNECTION|The specified connection %1 is not managed, please use managed connection for ADO NET destination.|  
|0xC0208454|-1071610796|DTS_E_ADODESTNOERROROUTPUT|The destination component does not have an error output. It may have been corrupted.|  
|0xC0208455|-1071610795|DTS_E_ADODESTNOLINEAGEID|The lineageID %1 associated with external column %2 does not exist at run time.|  
|0xC0208456|-1071610794|DTS_E_ADODESTEXTERNALCOLNOTEXIST|The %1 does not exist in the database. It may have been removed or renamed.|  
|0xC0208457|-1071610793|DTS_E_ADODESTGETSCHEMATABLEFAILED|Failed to get properties of external columns. The table name you entered may not exist, or you do not have SELECT permission on the table object and an alternative attempt to get column properties through connection has failed. Detailed error messages are: %1|  
|0xC0208458|-1071610792|DTS_E_ADODESTCOLUMNERRORDISPNOTSUPPORTED|Input column error disposition is not supported by ADO NET Destination component.|  
|0xC0208459|-1071610791|DTS_E_ADODESTCOLUMNTRUNDISPNOTSUPPORTED|Input column truncation disposition is not supported by ADO NET Destination component.|  
|0xC020845A|-1071610790|DTS_E_ADODESTINPUTTRUNDISPNOTSUPPORTED|Input  truncation row disposition is not supported by ADO NET Destination component.|  
|0xC020845B|-1071610789|DTS_E_ADODESTTABLENAMEERROR|The Table or View name is not expected. \n\t If you are quoting the table name, please use the prefix %1 and the suffix %2 of your selected data provider for quotation. \n\t If you are using multipart name, please use at most three parts for the table name.|  
|0xC0209001|-1071607807|DTS_E_FAILEDTOFINDCOLUMNINBUFFER|Failed to find column "%1" with lineage ID %2!d! in the buffer. The buffer manager returned error code 0x%3!8.8X!.|  
|0xC0209002|-1071607806|DTS_E_FAILEDTOGETCOLUMNINFOFROMBUFFER|Failed to get information for column "%1" (%2!d!) from the buffer. The error code returned was 0x%3!8.8X!.|  
|0xC0209011|-1071607791|DTS_E_TXAGG_ARITHMETICOVERFLOW|Arithmetic overflow encountered while aggregating "%1".|  
|0xC0209012|-1071607790|DTS_E_FAILEDTOGETCOLINFO|Failed to get information for row %1!ld!, column %2!ld! from the buffer. The error code returned was 0x%3!8.8X!.|  
|0xC0209013|-1071607789|DTS_E_FAILEDTOSETCOLINFO|Failed to set information for row %1!ld!, column %2!ld! into the buffer. The error code returned was 0x%3!8.8X!.|  
|0xC0209015|-1071607787|DTS_E_REQUIREDBUFFERISNOTAVAILBLE|A required buffer is not available.|  
|0xC0209016|-1071607786|DTS_E_FAILEDTOGETBUFFERBOUNDARYINFO|The attempt to get buffer boundary information failed with error code 0x%1!8.8X!.|  
|0xC0209017|-1071607785|DTS_E_FAILEDTOSETBUFFERENDOFROWSET|Setting the end of rowset for the buffer failed with error code 0x%1!8.8X!.|  
|0xC0209018|-1071607784|DTS_E_FAILEDTOGETDATAFORERROROUTPUTBUFFER|Failed to get data for the error output buffer.|  
|0xC0209019|-1071607783|DTS_E_FAILEDTOREMOVEROWFROMBUFFER|Removing a row from the buffer failed with error code 0x%1!8.8X!.|  
|0xC020901B|-1071607781|DTS_E_FAILEDTOSETBUFFERERRORINFO|The attempt to set buffer error information failed with error code 0x%1!8.8X!.|  
|0xC020901C|-1071607780|DTS_E_COLUMNSTATUSERROR|There was an error with %1 on %2. The column status returned was: "%3".|  
|0xC020901D|-1071607779|DTS_E_TXLOOKUP_METADATAXMLCACHEERR|Unable to cache reference metadata.|  
|0xC020901E|-1071607778|DTS_E_TXLOOKUP_ROWLOOKUPERROR|Row yielded no match during lookup.|  
|0xC020901F|-1071607777|DTS_E_INVALIDERRORDISPOSITION|The %1 has an invalid error or truncation row disposition.|  
|0xC0209022|-1071607774|DTS_E_FAILEDTODIRECTERRORROW|Directing the row to the error output failed with error code 0x%1!8.8X!.|  
|0xC0209023|-1071607773|DTS_E_FAILEDTOPREPARECOLUMNSTATUSESFORINSERT|Preparing column statuses for insert failed with error code 0x%1!8.8X!.|  
|0xC0209024|-1071607772|DTS_E_FAILEDTOFINDCOLUMNBYLINEAGEID|An attempt to find %1 with lineage ID %2!d! in the Data Flow Task buffer failed with error code 0x%3!8.8X!.|  
|0xC0209025|-1071607771|DTS_E_FAILEDTOFINDNONSPECIALERRORCOLUMN|Failed to find any non-special error column in %1.|  
|0xC0209029|-1071607767|DTS_E_INDUCEDTRANSFORMFAILUREONERROR|SSIS Error Code DTS_E_INDUCEDTRANSFORMFAILUREONERROR.  The "%1" failed because error code 0x%2!8.8X! occurred, and the error row disposition on "%3" specifies failure on error. An error occurred on the specified object of the specified component.  There may be error messages posted before this with more information about the failure.|  
|0xC020902A|-1071607766|DTS_E_INDUCEDTRANSFORMFAILUREONTRUNCATION|The "%1" failed because truncation occurred, and the truncation row disposition on "%2" specifies failure on truncation. A truncation error occurred on the specified object of the specified component.|  
|0xC020902B|-1071607765|DTS_E_TXSPLITEXPRESSIONEVALUATEDTONULL|The expression "%1" on "%2" evaluated to NULL, but the "%3" requires a Boolean results. Modify the error row disposition on the output to treat this result as False (Ignore Failure) or to redirect this row to the error output (Redirect Row).  The expression results must be Boolean for a Conditional Split.  A NULL expression result is an error.|  
|0xC020902C|-1071607764|DTS_E_TXSPLITSTATIC_EXPRESSIONEVALUATEDTONULL|The expression evaluated to NULL, but a Boolean result is required. Modify the error row disposition on the output to treat this result as False (Ignore Failure) or to redirect this row to the error output (Redirect Row). The expression results must be Boolean for a Conditional Split.  A NULL expression result is an error.|  
|0xC020902D|-1071607763|DTS_E_UTF16BIGENDIANFORMATNOTSUPPORTED|The file format of UTF-16 big endian is not supported.  Only UTF-16 little endian format is supported.|  
|0xC020902E|-1071607762|DTS_E_UTF8FORMATNOTSUPPORTEDASUNICODE|The file format of UTF-8 is not supported as Unicode.|  
|0xC020902F|-1071607761|DTS_E_DTPXMLCANTREADIDATTR|Cannot read ID attribute.|  
|0xC020903E|-1071607746|DTS_E_TXLOOKUP_INDEXCOLUMNREUSED|The cache index column %1 is referenced by more than one lookup input column.|  
|0xC020903F|-1071607745|DTS_E_TXLOOKUP_INDEXCOLUMNSMISMATCH|Lookup does not reference all cache connection manager index columns. Number of joined columns in lookup: %1!d!. Number of index columns: %2!d!.|  
|0xC0209069|-1071607703|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC020906A|-1071607702|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|The data value violated the schema constraint.|  
|0xC020906B|-1071607701|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_TRUNCATED|The data was truncated.|  
|0xC020906C|-1071607700|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the provider was unsigned.|  
|0xC020906D|-1071607699|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the provider.|  
|0xC020906E|-1071607698|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_UNAVAILABLE|No status is available.|  
|0xC020906F|-1071607697|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|The user did not have the correct permissions to write to the column.|  
|0xC0209070|-1071607696|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|The data value violated the integrity constraints for the column.|  
|0xC0209071|-1071607695|DTS_E_OLEDBSOURCEADAPTERSTATIC_UNAVAILABLE|No status is available.|  
|0xC0209072|-1071607694|DTS_E_OLEDBSOURCEADAPTERSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC0209073|-1071607693|DTS_E_OLEDBSOURCEADAPTERSTATIC_TRUNCATED|The data was truncated.|  
|0xC0209074|-1071607692|DTS_E_OLEDBSOURCEADAPTERSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the provider was unsigned.|  
|0xC0209075|-1071607691|DTS_E_OLEDBSOURCEADAPTERSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the provider.|  
|0xC0209076|-1071607690|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|The data value violated the schema constraint.|  
|0xC0209077|-1071607689|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC0209078|-1071607688|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_TRUNCATED|The data was truncated.|  
|0xC0209079|-1071607687|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the provider was unsigned.|  
|0xC020907A|-1071607686|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the provider.|  
|0xC020907B|-1071607685|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_UNAVAILABLE|No status is available.|  
|0xC020907C|-1071607684|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|The user did not have the correct permissions to write to the column.|  
|0xC020907D|-1071607683|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|The data value violates integrity constraints.|  
|0xC020907F|-1071607681|DTS_E_TXDATACONVERTSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC0209080|-1071607680|DTS_E_TXDATACONVERTSTATIC_TRUNCATED|The data was truncated.|  
|0xC0209081|-1071607679|DTS_E_TXDATACONVERTSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the provider was unsigned.|  
|0xC0209082|-1071607678|DTS_E_TXDATACONVERTSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the data conversion transform.|  
|0xC0209083|-1071607677|DTS_E_FLATFILESOURCEADAPTERSTATIC_UNAVAILABLE|No status is available.|  
|0xC0209084|-1071607676|DTS_E_FLATFILESOURCEADAPTERSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC0209085|-1071607675|DTS_E_FLATFILESOURCEADAPTERSTATIC_TRUNCATED|The data was truncated.|  
|0xC0209086|-1071607674|DTS_E_FLATFILESOURCEADAPTERSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the flat file source adapter was unsigned.|  
|0xC0209087|-1071607673|DTS_E_FLATFILESOURCEADAPTERSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the flat file source adapter.|  
|0xC020908E|-1071607666|DTS_E_TXDATACONVERTSTATIC_UNAVAILABLE|No status is available.|  
|0xC0209090|-1071607664|DTS_E_FILEOPENERR_FORREAD|Opening the file "%1" for reading failed with error code 0x%2!8.8X!.|  
|0xC0209091|-1071607663|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD|Failed to open file for reading.|  
|0xC0209092|-1071607662|DTS_E_FILEOPENERR_FORWRITE|Opening the file "%1" for writing failed with error code 0x%2!8.8X!.|  
|0xC0209093|-1071607661|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE|Failed to open file for writing.|  
|0xC0209094|-1071607660|DTS_E_TXFILEINSERTERSTATIC_INSERTERCANTREAD|Failed to read from file.|  
|0xC0209095|-1071607659|DTS_E_TXFILEEXTRACTORSTATIC_EXTRACTORCANTWRITE|Failed to write to file.|  
|0xC0209099|-1071607655|DTS_E_DTPXMLINVALIDPROPERTYARRAYTOOMANYVALUES|Too many array elements were found when parsing a property of type array. The elementCount is less than the number of array elements found.|  
|0xC020909A|-1071607654|DTS_E_DTPXMLINVALIDPROPERTYARRAYNOTENOUGHVALUES|Too few array elements were found when parsing a property of type array. The elementCount is more than the number of array elements found.|  
|0xC020909E|-1071607650|DTS_E_FILEOPENERR_FORWRITE_FILENOTFOUND|Opening the file "%1" for writing failed. The file cannot be found.|  
|0xC020909F|-1071607649|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILENOTFOUND|Opening the file for writing failed. The file cannot be found.|  
|0xC02090A0|-1071607648|DTS_E_FILEOPENERR_FORWRITE_PATHNOTFOUND|Opening the file "%1" for writing failed. The path cannot be found.|  
|0xC02090A1|-1071607647|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_PATHNOTFOUND|Opening the file for writing failed. The path cannot be found.|  
|0xC02090A2|-1071607646|DTS_E_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|Opening the file "%1" for writing failed. There are too many files open.|  
|0xC02090A3|-1071607645|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|Opening the file for writing failed. There are too many files open.|  
|0xC02090A4|-1071607644|DTS_E_FILEOPENERR_FORWRITE_ACCESSDENIED|Opening the file "%1" for writing failed. You do not have the correct permissions.|  
|0xC02090A5|-1071607643|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_ACCESSDENIED|Opening the file for writing failed. You do not have the correct permissions.|  
|0xC02090A6|-1071607642|DTS_E_FILEOPENERR_FORWRITE_FILEEXISTS|Opening the file "%1" for writing failed. The file exists and cannot be overwritten. If the AllowAppend property is FALSE and the ForceTruncate property is set to FALSE, the existence of the file will cause this failure.|  
|0xC02090A7|-1071607641|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILEEXISTS|Opening a file for writing failed. The file already exists and cannot be overwritten. If both the AllowAppend property and the ForceTruncate property are set to FALSE, the existence of the file will cause this failure.|  
|0xC02090A8|-1071607640|DTS_E_INCORRECTCUSTOMPROPERTYVALUEFOROBJECT|The value for custom property "%1" on %2 is incorrect.|  
|0xC02090A9|-1071607639|DTS_E_COLUMNSHAVEINCOMPATIBLEMETADATA|Columns "%1" and "%2" have incompatible metadata.|  
|0xC02090AD|-1071607635|DTS_E_FILEWRITEERR_DISKFULL|Opening the file "%1" for writing failed because the disk is full. There is not sufficient disk space to save this file.|  
|0xC02090AE|-1071607634|DTS_E_TXFILEEXTRACTORSTATIC_FILEWRITEERR_DISKFULL|Attempting to open the file for writing failed because the disk is full.|  
|0xC02090B9|-1071607623|DTS_E_TXAGG_SORTKEYGENFAILED|Generating a sort key failed with error 0x%1!8.8X!. The ComparisonFlags are enabled, and generating a sortkey with LCMapString failed.|  
|0xC02090BA|-1071607622|DTS_E_TXCHARMAPLCMAPFAILED|Transform failed to map string and returned error 0x%1!8.8X!. The LCMapString failed.|  
|0xC02090BB|-1071607621|DTS_E_FILEOPENERR_FORREAD_FILENOTFOUND|Opening the file "%1" for reading failed. The file was not found.|  
|0xC02090BC|-1071607620|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_FILENOTFOUND|Opening a file for reading failed. The file was not found.|  
|0xC02090BD|-1071607619|DTS_E_FILEOPENERR_FORREAD_PATHNOTFOUND|Opening the file "%1" for reading failed. The path cannot be found.|  
|0xC02090BE|-1071607618|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_PATHNOTFOUND|Opening a file for reading failed. The path was not found.|  
|0xC02090BF|-1071607617|DTS_E_FILEOPENERR_FORREAD_TOOMANYOPENFILES|Opening the file "%1" for reading failed. There are too many files open.|  
|0xC02090C0|-1071607616|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_TOOMANYOPENFILES|Opening the file for reading failed. There are too many files open.|  
|0xC02090C1|-1071607615|DTS_E_FILEOPENERR_FORREAD_ACCESSDENIED|Attempting to open the file "%1" for reading failed. Access is denied.|  
|0xC02090C2|-1071607614|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_ACCESSDENIED|Opening the file for reading failed. You do not have the correct permissions.|  
|0xC02090C3|-1071607613|DTS_E_INSERTERINVALIDBOM|The byte order mark (BOM) value for the file "%1" is 0x%2!4.4X!, but the expected value is 0x%3!4.4X!. The ExpectBOM property was set for this file, but the BOM value in the file is missing or not valid.|  
|0xC02090C4|-1071607612|DTS_E_TXFILEINSERTERSTATIC_INSERTERINVALIDBOM|The byte order mark (BOM) value for the file is not valid. The ExpectBOM property was set for this file, but the BOM value in the file is missing or not valid.|  
|0xC02090C5|-1071607611|DTS_E_NOCOMPONENTATTACHED|The %1 is not attached to a component.  It is required that a component be attached.|  
|0xC02090C9|-1071607607|DTS_E_TXLOOKUP_INVALIDMAXMEMORYPROP|The value for custom property %1 is incorrect.  It should be a number between %2!d! and %3!I64d!.|  
|0xC02090CA|-1071607606|DTS_E_TXAGG_COMPFLAGS_BADAGGREGATIONTYPE|The custom property "%1" cannot be specified for the aggregation type selected for this column. The comparison flags custom property can only be specified for group by and count distinct aggregation types.|  
|0xC02090CB|-1071607605|DTS_E_TXAGG_COMPFLAGS_BADDATATYPE|The comparison flags custom property "%1" can only be specified for columns of with datatype DT_STR or DT_WSTR.|  
|0xC02090CD|-1071607603|DTS_E_TXAGG_AGGREGATION_FAILURE|Aggregation on %1 failed with error code 0x%2!8.8X!.|  
|0xC02090CF|-1071607601|DTS_E_MAPPINGSETUPERROR|There was an error setting up the mapping. %1|  
|0xC02090D0|-1071607600|DTS_E_XMLSRCUNABLETOREADXMLDATA|The %1 was unable to read the XML data.|  
|0xC02090D1|-1071607599|DTS_E_XMLSRCUNABLETOGETXMLDATAVARIABLE|The %1 was unable to get the variable specified by the "%2" property.|  
|0xC02090D2|-1071607598|DTS_E_NODATATABLEMATCHROWID|The %1 contains a RowsetID with a value of %2 that does not reference a data table in the schema.|  
|0xC02090D6|-1071607594|DTS_E_TXAGG_BADKEYSVALUE|The property %1 must either be empty, or a number between %2!u! and %3!u!. The Keys or CountDistinctKeys property has a invalid value. The property should be a number between 0 and ULONG_MAX, inclusive, or not be set.|  
|0xC02090D7|-1071607593|DTS_E_TXAGG_TOOMANYKEYS|The aggregate component encountered too many distinct key combinations. It cannot accommodate more than %1!u! distinct key values. There are more than ULONG_MAX distinct key values in the main workspace.|  
|0xC02090D8|-1071607592|DTS_E_TXAGG_TOOMANYCOUNTDISTINCTVALUES|The aggregate component encountered too many distinct values while calculating the count distinct aggregate. It cannot accommodate more than %1!u! distinct values. There were more than ULONG_MAX distinct values while calculating the count distinct aggregation.|  
|0xC02090D9|-1071607591|DTS_E_FAILEDTOWRITETOTHEFILENAMECOLUMN|The attempt to write to the filename column failed with error code 0x%1!8.8X!.|  
|0xC02090DC|-1071607588|DTS_E_FAILEDTOFINDERRORCOLUMN|An error occurred, but the column that caused the error cannot be determined.|  
|0xC02090E3|-1071607581|DTS_E_TXLOOKUP_FAILEDUPGRADE_BAD_VERSION|Unable to upgrade lookup metadata from version %1!d! to %2!d!. The Lookup transform was unable to upgrade metadata from the existing version number in a call to PerformUpgrade().|  
|0xC02090E5|-1071607579|DTS_E_TERMEXTRACTIONORLOOKUP_NTEXTSPLITED|Failed to locate the ending boundary of a sentence.|  
|0xC02090E6|-1071607578|DTS_E_TERMEXTRACTION_EXCEED_MAXWORDNUM|The Term Extraction transformation is unable to process the input text because a sentence from the input text is too long. The sentence is segmented into several sentences.|  
|0xC02090E7|-1071607577|DTS_E_XMLSRCFAILEDTOCREATEREADER|The %1 was unable to read the XML data. %2|  
|0xC02090F0|-1071607568|DTS_E_TXLOOKUP_REINITMETADATAFAILED|The call to Lookup transform method, ReinitializeMetadata, failed.|  
|0xC02090F1|-1071607567|DTS_E_TXLOOKUP_NOJOINS|The lookup transform must contain at least one input column joined to a reference column, and none were specified. You must specify at least one join column.|  
|0xC02090F2|-1071607566|DTS_E_MANAGEDERR_BADFORMATSPECIFICATION|The message string being posted by the managed error infrastructure contains a bad format specification. This is an internal error.|  
|0xC02090F3|-1071607565|DTS_E_MANAGEDERR_UNSUPPORTEDTYPE|While formatting a message string using the managed error infrastructure, there was a variant type that does not have formatting support. This is an internal error.|  
|0xC02090F5|-1071607563|DTS_E_DATAREADERSRCUNABLETOPROCESSDATA|The %1 was unable to process the data. %2|  
|0xC02090F6|-1071607562|DTS_E_XMLSRCEMPTYPROPERTY|The property "%1" on the %2 was empty.|  
|0xC02090F7|-1071607561|DTS_E_XMLSRCINVALIDOUTPUTNAME|Attempting to create an output with the name "%1" for the XML table with the path "%2" failed because the name is invalid.|  
|0xC02090F8|-1071607560|DTS_E_MGDSRC_OVERFLOW|The value was too large to fit in the %1.|  
|0xC02090F9|-1071607559|DTS_E_DATAREADERDESTUNABLETOPROCESSDATA|The %1 was unable to process the data.|  
|0xC02090FA|-1071607558|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONTRUNCATION|The "%1" failed because truncation occurred, and the truncation row disposition on "%2"  at "%3" specifies failure on truncation. A truncation error occurred on the specified object of the specified component.|  
|0xC02090FB|-1071607557|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONERROR|The "%1" failed because error code 0x%2!8.8X! occurred, and the error row disposition on "%3" at "%4" specifies failure on error. An error occurred on the specified object of the specified component.|  
|0xC0209291|-1071607151|DTS_E_SQLCEDESTSTATIC_FAILEDTOSETVALUES|The SQLCE destination could not set the column values for the row.|  
|0xC0209292|-1071607150|DTS_E_SQLCEDESTSTATIC_FAILEDTOINSERT|The SQLCE destination could not insert the row.|  
|0xC0209293|-1071607149|DTS_E_TXFUZZYLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|Encountered OLEDB error while loading column metadata.|  
|0xC0209294|-1071607148|DTS_E_TXFUZZYLOOKUP_TOOFEWREFERENCECOLUMNS|Lookup reference metadata contains too few columns.|  
|0xC0209295|-1071607147|DTS_E_TXSCD_OLEDBERR_LOADCOLUMNMETADATA|Encountered OLEDB error while loading column metadata.|  
|0xC0209296|-1071607146|DTS_E_TXSCD_TOOFEWREFERENCECOLUMNS|Lookup reference metadata contains too few columns.|  
|0xC0209297|-1071607145|DTS_E_TXSCD_MALLOCERR_REFERENCECOLUMNINFO|Unable to allocate memory.|  
|0xC0209298|-1071607144|DTS_E_TXSCD_MALLOCERR_BUFFCOL|Unable to allocate memory.|  
|0xC0209299|-1071607143|DTS_E_TXSCD_MAINWORKSPACE_CREATEERR|Unable to create workspace buffer.|  
|0xC020929A|-1071607142|DTS_E_DTPXMLDOMCREATEERROR|Unable to instantiate XML DOM document, please verify that MSXML binaries are properly installed and registered.|  
|0xC020929B|-1071607141|DTS_E_DTPXMLDOMLOADERROR|Unable to load XML data into a local DOM for processing.|  
|0xC020929C|-1071607140|DTS_E_RSTDESTBADVARIABLETYPE|The type of the runtime variable "%1" is incorrect. The runtime variable type must be Object.|  
|0xC020929E|-1071607138|DTS_E_XMLDATAREADERMULTIPLEINLINEXMLSCHEMASNOTSUPPORTED|The XML Source Adapter was unable to process the XML data. Multiple inline schemas are not supported.|  
|0xC020929F|-1071607137|DTS_E_XMLDATAREADERANYTYPENOTSUPPORTED|The XML Source Adapter was unable to process the XML data. The content of an element can not be declared as anyType.|  
|0xC02092A0|-1071607136|DTS_E_XMLDATAREADERGROUPREFNOTSUPPORTED|The XML Source Adapter was unable to process the XML data. The content of an element can not contain a reference (ref) to a group.|  
|0xC02092A1|-1071607135|DTS_E_XMLDATAREADERMIXEDCONTENTFORCOMPLEXTYPESNOTSUPPORTED|The XML Source Adapter does not support mixed content model on Complex Types.|  
|0xC02092A2|-1071607134|DTS_E_XMLDATAREADERINLINESCHEMAFOUNDINSOURCEXML|The XML Source Adapter was unable to process the XML data. An inline schema must be the first child node in the source Xml.|  
|0xC02092A3|-1071607133|DTS_E_XMLDATAREADERNOINLINESCHEMAFOUND|The XML Source Adapter was unable to process the XML data. No inline schema was found in the source XML, but the "UseInlineSchema" property was set to true.|  
|0xC02092A4|-1071607132|DTS_E_CONNECTIONMANAGERTRANSACTEDANDRETAINEDINBULKINSERT|The component cannot use a connection manager that retains its connection in a transaction with fastload or bulk insert.|  
|0xC02092A5|-1071607131|DTS_E_OUTPUTREDIRECTINTRANSACTIONNOTALLOWED|The %1 cannot be set to redirect on error using a connection in a transaction.|  
|0xC02092A6|-1071607130|DTS_E_FOUNDORPHANEDEXTERNALMETADATACOLUMN|The %1 does not have a corresponding input or output column.|  
|0xC02092A9|-1071607127|DTS_E_RAWDESTNOINPUTCOLUMNS|There is no selected column to be written to the file.|  
|0xC02092AA|-1071607126|DTS_E_RAWDESTBLOBDATATYPE|The %1 has an invalid data type. Columns with data types DT_IMAGE, DT_TEXT and DT_NTEXT cannot be written to raw files.|  
|0xC02092AB|-1071607125|DTS_E_RAWDESTWRONGEXTERNALMETADATAUSAGE|The external metadata collection is improperly used by this component. The component should use external metadata when appending or truncating an existing file. Otherwise, the external metadata is not needed.|  
|0xC02092AC|-1071607124|DTS_E_RAWDESTMAPPEDINPUTCOLUMN|The %1 is mapped to an external metadata column with the id %2!d!. Input columns should not be mapped to external metadata columns when selected Write Option value is Create Always.|  
|0xC02092AD|-1071607123|DTS_E_RAWFILECANTOPENFORMETADATA|The file  cannot be opened for reading the metadata. If the file does not exist, and the component has already defined external metadata, you can set the "ValidateExternalMetadata" property to "false" and the file will be created at the runtime.|  
|0xC02092AE|-1071607122|DTS_E_FAILEDTOACCESSLOBCOLUMN|Failed to access LOB data from the data flow buffer for data source column "%1" with error code 0x%2!8.8X!.|  
|0xC02092AF|-1071607121|DTS_E_XMLSRCUNABLETOPROCESSXMLDATA|The %1 was unable to process the XML data. %2|  
|0xC02092B0|-1071607120|DTS_E_XMLSRCSTATIC_UNABLETOPROCESSXMLDATA|The XML Source Adapter was unable to process the XML data.|  
|0xC02092B1|-1071607119|DTS_E_RAWINVALIDACCESSMODE|The value %1!d! is not recognized as a valid access mode.|  
|0xC02092B2|-1071607118|DTS_E_INCOMPLETEDATASOURCECOLUMNFOUND|Complete metadata information for the data source column "%1" is not available.  Make sure the column is correctly defined in the data source.|  
|0xC02092B3|-1071607117|DTS_E_TXAUDIT_ONLYSTRINGLENGTHCHANGEALLOWED|Only lengths of User Name column, Package Name column, Task Name column and Machine Name column can be changed.  All other audit column datatype information is read only.|  
|0xC02092B4|-1071607116|DTS_E_ROWSETUNAVAILABLE|A rowset based on the SQL command was not returned by the OLE DB provider.|  
|0xC02092B5|-1071607115|DTS_E_COMMITFAILED|A commit failed.|  
|0xC02092B6|-1071607114|DTS_E_USEBINARYFORMATREQUIRESANSIFILE|The custom property "%1" on %2 can only be used with ANSI files.|  
|0xC02092B7|-1071607113|DTS_E_USEBINARYFORMATREQUIRESBYTES|The custom property "%1" on %2 can only be used with DT_BYTES.|  
|0xC0209302|-1071607038|DTS_E_OLEDB_NOPROVIDER_ERROR|SSIS Error Code DTS_E_OLEDB_NOPROVIDER_ERROR.  The requested OLE DB provider %2 is not registered. Error code: 0x%1!8.8X!.|  
|0xC0209303|-1071607037|DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR|SSIS Error Code DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR.  The requested OLE DB provider %2 is not registered -- perhaps no 64-bit provider is available.  Error code: 0x%1!8.8X!.|  
|0xC0209306|-1071607034|DTS_E_MULTICACHECOLMAPPINGS|The cache column, "%1", is mapped to more than one column. Remove the duplicate column mappings.|  
|0xC0209307|-1071607033|DTS_E_COLNOTMAPPEDTOCACHECOL|The %1 is not mapped to valid cache column.|  
|0xC0209308|-1071607032|DTS_E_CACHECOLDATATYPEINCOMPAT|Cannot map the input column, "%1", and the cache column, "%2", because the data types do not match.|  
|0xC0209309|-1071607031|DTS_E_INCORRECTINPUTCACHECOLCOUNT|The number of input columns does not match the number of cache columns.|  
|0xC020930A|-1071607030|DTS_E_INVALIDCACHEFILENAME|The cache file name is either not provided or is not valid. Provide a valid cache file name.|  
|0xC020930B|-1071607029|DTS_E_CACHECOLINDEXPOSMISMATCH|The index position of column, "%1", is different from index position of Cache connection manager column, "%2".|  
|0xC020930C|-1071607028|DTS_E_FAILEDTOLOADCACHE|Failed to load the cache from file, "%1".|  
|0xC020930D|-1071607027|DTS_E_TXLOOKUP_REFCOLUMNISNOTINDEX|The lookup input column %1 references non-index cache column %2.|  
|0xC020930E|-1071607026|DTS_E_FAILEDTOGETCONNECTIONSTRING|Failed to get the connection string.|  
|0xC020930F|-1071607025|DTS_E_CACHECOLDATATYPEPROPINCOMPAT|Cannot map the input column, "%1", and the cache column, "%2", because one or more data type properties do not match.|  
|0xC0209311|-1071607023|DTS_E_CACHECOLUMNOTFOUND|Cache column "%1" was not found in the cache.|  
|0xC0209312|-1071607022|DTS_E_CACHECOLUMNMAPPINGFAILED|Failed to map %1 to a cache column. The hresult is 0x%2!8.8X!.|  
|0xC0209313|-1071607021|DTS_E_CACHELOADEDFROMFILE|The %1 cannot write to the cache because the cache has been loaded from a file by %2.|  
|0xC0209314|-1071607020|DTS_E_CACHERELOADEDDIFFERENTFILES|The %1 cannot load the cache from file "%2" because the cache has already been loaded from file "%3".|  
|0xC0209316|-1071607018|DTS_E_OUTPUTNOTUSED|The output with ID %1!d! of Aggregate component is not used by any component. Please either remove it or associate it with an input of some component.|  
|0xC0209317|-1071607017|DTS_E_CACHEFILEWRITEFAILED|The %1 failed to write the cache to file "%2". The hresult is 0x%3!8.8X!.|  
|0xC0209318|-1071607016|DTS_E_XMLDATATYPECHANGED|The XML schema data type information for "%1" on  element "%2" has changed.  Please re-initialize the metadata for this component and review column mappings.|  
|0xC0209319|-1071607015|DTS_E_TXLOOKUP_UNUSEDINPUTCOLUMN|%1 not used in join or copy. Please remove the unused column from the input column list.|  
|0xC020931A|-1071607014|DTS_E_SORTSTACKOVERFLOW|The sort failed due to a stack overflow while sorting an incoming buffer.  Please reduce the DefaultBufferMaxRows property on the Data Flow Task.|  
|0xC020F42A|-1071582166|DTS_E_OLEDB_OLDPROVIDER_ERROR|Consider changing the PROVIDER in the connection string to %1 or visit https://www.microsoft.com/downloads to find and install support for %2.|  
|||DTS_E_INITTASKOBJECTFAILED|Failed to initialize the task object for task "%1!s!", type "%2!s!" due to error 0x%3!8.8X! "%4!s!".|  
|||DTS_E_GETCATMANAGERFAILED|Failed to create COM Component Categories Manager due to error 0x%1!8.8X! "%2!s!".|  
|||DTS_E_COMPONENTINITFAILED|Component %1!s! failed to initialize due to error 0x%2!8.8X! "%3!s!".|  
  
##  <a name="msgWarning"></a> Warning Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] warning messages begin with **DTS_W_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x80000036|-2147483594|DTS_W_COUNTDOWN|There are %1!lu! days left in the evaluation. When it expires, packages will not be able to be executed.|  
|0x80010015|-2147418091|DTS_W_GENERICWARNING|Warning(s) raised. There should be more specific warnings preceding this one that explain the specifics of the warning(s).|  
|0x80012010|-2147409904|DTS_W_FAILEDXMLDOCCREATION|Cannot create an XML document object instance. Verify that MSXML is installed and registered correctly.|  
|0x80012011|-2147409903|DTS_W_FAILEDCONFIGLOAD|Cannot load the XML configuration file. The XML configuration file may be malformed or not valid.|  
|0x80012012|-2147409902|DTS_W_CONFIGFILENAMEINVALID|The configuration file name "%1" is not valid. Check the configuration file name.|  
|0x80012013|-2147409901|DTS_W_CONFIGFILEINVALID|The configuration file loaded, but is not valid. The file is not formatted correctly, may be missing an element, or may be damaged.|  
|0x80012014|-2147409900|DTS_W_CONFIGFILENOTFOUND|The configuration file "%1" cannot be found. Check the directory and file name.|  
|0x80012015|-2147409899|DTS_W_CONFIGKEYNOTFOUND|Configuration registry key "%1" was not found. A configuration entry specifies a registry key that is not available. Check the registry to ensure that the key is there.|  
|0x80012016|-2147409898|DTS_W_CONFIGTYPEINVALID|The configuration type in one of the configuration entries was not valid. Valid types are listed in the DTSConfigurationType enumeration.|  
|0x80012017|-2147409897|DTS_W_CANNOTFINDOBJECT|The package path referenced an object that cannot be found: "%1". This occurs when an attempt is made to resolve a package path to an object that cannot be found.|  
|0x80012018|-2147409896|DTS_W_CONFIGFORMATINVALID_PACKAGEDELIMITER|The configuration entry, "%1", has an incorrect format because it does not begin with the package delimiter. Prepend "\package" to the package path.|  
|0x80012019|-2147409895|DTS_W_CONFIGFORMATINVALID|The configuration entry "%1" had an incorrect format. This can occur because of a missing delimiter or formatting errors, like an invalid array delimiter.|  
|0x8001201A|-2147409894|DTS_W_NOPARENTVARIABLES|Configuration from a parent variable "%1" did not occur because there was no parent variable collection.|  
|0x8001201B|-2147409893|DTS_W_CONFIGFILEFAILEDIMPORT|Failure importing configuration file: "%1".|  
|0x8001201C|-2147409892|DTS_W_PARENTVARIABLENOTFOUND|Configuration from a parent variable "%1" did not occur because there was no parent variable. Error code: 0x%2!8.8X!.|  
|0x8001201D|-2147409891|DTS_W_CONFIGFILEEMPTY|The configuration file was empty and contained no configuration entries.|  
|0x80012023|-2147409885|DTS_W_INVALIDCONFIGURATIONTYPE|The configuration type for configuration "%1" is not valid. This may occur when an attempt is made to set the type property of a configuration object to an invalid configuration type.|  
|0x80012025|-2147409883|DTS_W_REGISTRYCONFIGURATIONTYPENOTFOUND|The configuration type for the registry configuration was not found in key "%1". Add a value called ConfigType to the registry key and give it a string value of "Variable", "Property", "ConnectionManager", "LoggingProvider", or "ForEachEnumerator".|  
|0x80012026|-2147409882|DTS_W_REGISTRYCONFIGURATIONVALUENOTFOUND|The configuration value for the registry configuration was not found in key "%1". Add a value called Value to the registry key of type DWORD or String.|  
|0x80012028|-2147409880|DTS_W_PROCESSCONFIGURATIONFAILEDSET|Process configuration failed to set the destination at the package path of "%1". This occurs when attempting to set the destination property or variable fails. Check the destination property or variable.|  
|0x80012032|-2147409870|DTS_W_CONFIGUREDVALUESECTIONEMPTY|Failed to retrieve value from the .ini file. The ConfiguredValue section is either empty, or does not exist: "%1".|  
|0x80012033|-2147409869|DTS_W_CONFIGUREDTYPESECTIONEMPTY|Failed to retrieve value from the .ini file. The ConfiguredType section is either empty, or does not exist: "%1".|  
|0x80012034|-2147409868|DTS_W_PACKAGEPATHSECTIONEMPTY|Failed to retrieve value from the .ini file. The PackagePath section is either empty, or does not exist: "%1".|  
|0x80012035|-2147409867|DTS_W_CONFIGUREDVALUETYPE|Failed to retrieve value from the .ini file. The ConfiguredValueType section is either empty, or does not exist: "%1".|  
|0x80012051|-2147409839|DTS_W_SQLSERVERFAILEDIMPORT|Configuration from SQL Server was not successfully imported: "%1".|  
|0x80012052|-2147409838|DTS_W_INICONFIGURATIONPROBLEM|The .ini configuration file is not valid due to empty or missing fields.|  
|0x80012054|-2147409836|DTS_W_NORECORDSFOUNDINTABLE|Table "%1" does not have any records for configuration. This occurs when configuring from a SQL Server table that has no records for the configuration.|  
|0x80012055|-2147409835|DTS_W_DUPLICATECUSTOMEVENT|Error using same name for different custom events. The custom event "%1" was defined differently by different children of this container. There may be an error when executing the event handler.|  
|0x80012057|-2147409833|DTS_W_CONFIGREADONLYVARIABLE|The configuration attempted to change a read-only variable. The variable is at the package path "%1".|  
|0x80012058|-2147409832|DTS_W_CONFIGPROCESSCONFIGURATIONFAILED|Calling ProcessConfiguration on the package failed. The configuration attempted to change the property at the package path "%1".|  
|0x80012059|-2147409831|DTS_W_ONEORMORECONFIGLOADFAILED|Failed to load at least one of the configuration entries for the package. Check configuration entries for "%1" and previous warnings to see descriptions of which configuration failed.|  
|0x8001205A|-2147409830|DTS_W_CONFIGNODEINVALID|The configuration entry "%1" in the configuration file was not valid, or failed to configure the variable.  The name indicates which entry failed. In some cases, the name will not be available.|  
|0x80014058|-2147401640|DTS_W_FAILURENOTRESTARTABLE|This task or container has failed, but because FailPackageOnFailure property is FALSE, the package will continue. This warning is posted when the SaveCheckpoints property of the package is set to TRUE and the task or container fails.|  
|0x80017101|-2147389183|DTS_W_EMPTYPATH|The path is empty.|  
|0x80019002|-2147381246|DTS_W_MAXIMUMERRORCOUNTREACHED|SSIS Warning Code DTS_W_MAXIMUMERRORCOUNTREACHED.  The Execution method succeeded, but the number of errors raised (%1!d!) reached the maximum allowed (%2!d!); resulting in failure. This occurs when the number of errors reaches the number specified in MaximumErrorCount. Change the MaximumErrorCount or fix the errors.|  
|0x80019003|-2147381245|DTS_W_CONFIGENVVARNOTFOUND|The configuration environment variable was not found.  The environment variable was: "%1". This occurs when a package specifies an environment variable for a configuration setting but it cannot be found. Check the configurations collection in the package and verify that the specified environment variable is available and valid.|  
|0x80019316|-2147380458|DTS_W_CONNECTIONPROVIDERCHANGE|The provider name for the connection manager "%1" has been changed from "%2" to "%3".|  
|0x80019317|-2147380457|DTS_W_READEXTMAPFAILED|An exception occurred while reading the upgrade mapping files. The exception is "%1".|  
|0x80019318|-2147380456|DTS_W_DUPLICATEMAPPINGKEY|There is a duplicate mapping in file, "%1". The tag is "%2", and the key is "%3".|  
|0x80019319|-2147380455|DTS_W_IMPLICITUPGRADEMAPPING|The extension, "%1", was implicitly upgraded to "%2". Add a mapping for this extension to the UpgradeMappings directory.|  
|0x8001931A|-2147380454|DTS_W_INVALIDEXTENSIONMAPPING|A mapping in the file, "%1", is not valid. Values cannot be null or empty. The tag is "%2", the key is "%3", and the value is "%4".|  
|0x8001931C|-2147380452|DTS_W_ADOCONNECTIONDATATYPECOMPATCHANGE|The DataTypeCompatibility property of ADO type connection manager "%1" was set to 80 for backward compatibility reasons.|  
|0x8001C004|-2147368956|DTS_W_FILEENUMEMPTY|The For Each File enumerator is empty. The For Each File enumerator did not find any files that matched the file pattern, or the specified directory was empty.|  
|0x8001F02F|-2147356625|DTS_W_COULDNOTRESOLVEPACKAGEPATH|Cannot resolve a package path to an object in the package "%1". Verify that the package path is valid.|  
|0x8001F203|-2147356157|DTS_W_ITERATIONEXPRESSIONISNOTASSIGNMENT|The iteration expression is not an assignment expression: "%1". This error usually occurs when the expression in the assignment expression on the ForLoop is not an assignment expression.|  
|0x8001F204|-2147356156|DTS_W_INITIALIZATIONEXPRESSIONISNOTASSIGNMENT|The initialization expression is not an assignment expression: "%1". This error usually occurs when the expression in the iterate expressions on the ForLoop is not an assignment expression.|  
|0x8001F205|-2147356155|DTS_W_LOGPROVIDERNOTDEFINED|The executable "%1" was pasted successfully. However a log provider that was associated with the executable was not found in the collection "LogProviders".  The executable was pasted without log provider information.|  
|0x8001F300|-2147355904|DTS_W_PACKAGEUPGRADED|Succeeded in upgrading the package.|  
|0x8001F42B|-2147355605|DTS_W_LEGACYPROGID|The "%1" ProgID has been deprecated. The new ProgID for this component "%2" should be used instead.|  
|0x80020918|-2147350248|DTS_W_FTPTASK_OPERATIONFAILURE|Operation "%1" failed.|  
|0x800283A5|-2147318875|DTS_W_MSMQTASK_USE_WEAK_ENCRYPTION|The encryption algorithm "%1" uses weak encryption.|  
|0x80029164|-2147315356|DTS_W_FSTASK_OPERATIONFAILURE|Task failed to execute operation "%1".|  
|0x80029185|-2147315323|DTS_W_EXECPROCTASK_FILENOTINPATH|File/Process "%1" is not in path.|  
|0x800291C6|-2147315258|DTS_W_SENDMAILTASK_SUBJECT_MISSING|The subject is empty.|  
|0x800291C7|-2147315257|DTS_W_SENDMAILTASK_ERROR_IN_TO_LINE|The address in the "To" line is malformed. It is either missing the "\@" symbol or is not valid.|  
|0x800291C8|-2147315256|DTS_W_SENDMAILTASK_AT_MISSING_IN_FROM|The address in the "From" line is malformed. It is either missing the "\@" symbol or is not valid.|  
|0x8002927A|-2147315078|DTS_W_XMLTASK_DIFFFAILURE|The two XML documents are different.|  
|0x8002928C|-2147315060|DTS_W_XMLTASK_DTDVALIDATIONWARNING|DTD Validation will use the DTD file defined in the DOCTYPE line in the XML document. It will not use what is assigned to the property "%1".|  
|0x8002928D|-2147315059|DTS_W_XMLTASK_VALIDATIONFAILURE|Task failed to validate "%1".|  
|0x80029291|-2147315055|DTS_W_TRANSFERDBTASK_ACTIONSETTOCOPY|The transfer action value was invalid.  It is being set to copy.|  
|0x80029292|-2147315054|DTS_W_TRANSFERDBTASK_METHODSETTOONLINE|The transfer method value was invalid.  It is being set to an online transfer.|  
|0x8002F304|-2147290364|DTS_W_PROBLEMOCCURREDWITHFOLLOWINGMESSAGE|A problem occurred with the following messages: "%1".|  
|0x8002F322|-2147290334|DTS_W_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|The error message "%1" already exists at destination server.|  
|0x8002F331|-2147290319|DTS_W_JOBSTASK_JOBEXISTSATDEST|The job "%1" already exists at destination server.|  
|0x8002F332|-2147290318|DTS_W_JOBSTASK_SKIPPINGJOBEXISTSATDEST|Skipping the transfer of job "%1" since it already exists at destination.|  
|0x8002F333|-2147290317|DTS_W_JOBSTASK_OVERWRITINGJOB|Overwriting the job "%1" at destination server.|  
|0x8002F339|-2147290311|DTS_W_LOGINSTASK_ENUMVALUEINCORRECT|Persisted enumeration value of property "FailIfExists" was changed and rendered invalid. Resetting to default.|  
|0x8002F343|-2147290301|DTS_W_LOGINSTASK_OVERWRITINGLOGINATDEST|Overwriting Login "%1" at destination.|  
|0x8002F356|-2147290282|DTS_W_TRANSOBJECTSTASK_SPALREADYATDEST|Stored procedure "%1" already exists at destination.|  
|0x8002F360|-2147290272|DTS_W_TRANSOBJECTSTASK_RULEALREADYATDEST|Rule "%1" already exists at destination.|  
|0x8002F364|-2147290268|DTS_W_TRANSOBJECTSTASK_TABLEALREADYATDEST|Table "%1" already exists at destination.|  
|0x8002F368|-2147290264|DTS_W_TRANSOBJECTSTASK_VIEWALREADYATDEST|View "%1" already exists at destination.|  
|0x8002F372|-2147290254|DTS_W_TRANSOBJECTSTASK_UDFALREADYATDEST|User Defined Function "%1" already exists at destination.|  
|0x8002F376|-2147290250|DTS_W_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|Default "%1" already exists at destination.|  
|0x8002F380|-2147290240|DTS_W_TRANSOBJECTSTASK_UDDTALREADYATDEST|User Defined Data Type "%1" already exists at destination.|  
|0x8002F384|-2147290236|DTS_W_TRANSOBJECTSTASK_PFALREADYATDEST|Partition Function "%1" already exists at destination.|  
|0x8002F388|-2147290232|DTS_W_TRANSOBJECTSTASK_PSALREADYATDEST|Partition Scheme "%1" already exists at destination.|  
|0x8002F391|-2147290223|DTS_W_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|Schema "%1" already exists at destination.|  
|0x8002F396|-2147290218|DTS_W_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|SqlAssembly "%1" already exists at destination.|  
|0x8002F400|-2147290112|DTS_W_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|User Defined Aggregate "%1" already exists at destination.|  
|0x8002F404|-2147290108|DTS_W_TRANSOBJECTSTASK_TYPEALREADYATDEST|User Defined Type "%1" already exists at destination.|  
|0x8002F408|-2147290104|DTS_W_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|XmlSchemaCollection "%1" already exists at destination.|  
|0x8002F412|-2147290094|DTS_W_TRANSOBJECTSTASK_NOELEMENTSPECIFIEDTOTRANSFER|There are no elements specified to transfer.|  
|0x8002F415|-2147290091|DTS_W_TRANSOBJECTSTASK_LOGINALREADYATDEST|Login "%1" already exists at destination.|  
|0x8002F41A|-2147290086|DTS_W_TRANSOBJECTSTASK_USERALREADYATDEST|User "%1" already exists at destination.|  
|0x80047007|-2147192825|DTS_W_NOLINEAGEVALIDATION|The lineage IDs of the input columns cannot be validated because the execution trees contain cycles.|  
|0x80047034|-2147192780|DTS_W_EMPTYDATAFLOW|The DataFlow task has no components. Add components or remove the task.|  
|0x80047069|-2147192727|DTS_W_SORTEDOUTPUTHASNOSORTKEYPOSITIONS|The IsSorted property of %1 is set to TRUE, but all of its output columns' SortKeyPositions are set to zero.|  
|0x8004706F|-2147192721|DTS_W_SOURCEREMOVED|Source "%1" (%2!d!) will not be read because none of its data ever becomes visible outside the Data Flow Task.|  
|0x80047076|-2147192714|DTS_W_UNUSEDOUTPUTDATA|The output column "%1" (%2!d!) on output "%3" (%4!d!) and component "%5" (%6!d!) is not subsequently used in the Data Flow task. Removing this unused output column can increase Data Flow task performance.|  
|0x800470AE|-2147192658|DTS_W_COMPONENTREMOVED|Component "%1" (%2!d!) has been removed from the Data Flow task because its output is not used and its inputs either have no side effects or are not connected to outputs of other components. If the component is required, then the HasSideEffects property on at least one of its inputs should be set to true, or its output should be connected to something.|  
|0x800470B0|-2147192656|DTS_W_NOWORKTODO|Rows were given to a thread, but that thread has no work to do. The layout has a disconnected output. Running the pipeline with the RunInOptimizedMode property set to TRUE will be faster, and prevents this warning.|  
|0x800470C8|-2147192632|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|The external columns for %1 are out of synchronization with the data source columns. %2|  
|0x800470C9|-2147192631|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSADDITION|The column "%1" needs to be added to the external columns.|  
|0x800470CA|-2147192630|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSUPDATE|The external column "%1" needs to be updated.|  
|0x800470CB|-2147192629|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSREMOVAL|The %1 needs to be removed from the external columns.|  
|0x800470D8|-2147192616|DTS_W_EXPREVALPOTENTIALSTRINGTRUNCATION|The result string for expression "%1" may be truncated if it exceeds the maximum length of %2!d! characters. The expression could have a result value that exceeds the maximum size of a DT_WSTR.|  
|0x800470E9|-2147192599|DTS_W_COMPONENTLEAKPROCESSINPUT|A call to the ProcessInput method for input %1!d! on %2 unexpectedly kept a reference to the buffer it was passed. The refcount on that buffer was %3!d! before the call, and %4!d! after the call returned.|  
|0x800470EB|-2147192597|DTS_W_EXPREVALUNREFERENCEDINPUTCOLUMN|The "%1" on "%2" has usage type READONLY, but is not referenced by an expression. Remove the column from the list of available input columns, or reference it in an expression.|  
|0x8004801E|-2147188706|DTS_W_COULDNOTFINDCURRENTVERSION|Cannot find the "%1" value for component %2. The CurrentVersion value for the component cannot be located. This error occurs if the component has not set its registry information to contain a CurrentVersion value in the DTSInfo section. This message occurs during component development, or when the component is used in a package, if the component is not registered properly.|  
|0x80049300|-2147183872|DTS_W_BUFFERGETTEMPFILENAME|The buffer manager could not get a temporary file name.|  
|0x80049301|-2147183871|DTS_W_UNUSABLETEMPORARYPATH|The buffer manager could not create a temporary file on the path "%1". The path will not be considered for temporary storage again.|  
|0x80049304|-2147183868|DTS_W_DF_PERFCOUNTERS_DISABLED|Warning: Could not open global shared memory to communicate with performance DLL; data flow performance counters are not available.  To resolve, run this package as an administrator, or on the system's console.|  
|0x8020200F|-2145378289|DTS_W_PARTIALROWFOUNDATENDOFFILE|There is a partial row at the end of the file.|  
|0x8020202B|-2145378261|DTS_W_ENDOFFILEREACHWHILEREADINGHEADERROWS|The end of the data file was reached while reading header rows. Make sure the header row delimiter and the number of header rows to skip are correct.|  
|0x80202066|-2145378202|DTS_W_CANTRETRIEVECODEPAGEFROMOLEDBPROVIDER|Cannot retrieve the column code page info from the OLE DB provider.  If the component supports the "%1" property, the code page from that property will be used.  Change the value of the property if the current string code page values are incorrect.  If the component does not support the property, the code page from the component's locale ID will be used.|  
|0x802020F7|-2145378057|DTS_W_TXSORTSORTISTHESAME|The data is already sorted as specified so the transform can be removed.|  
|0x8020400D|-2145370099|DTS_W_NOPIPELINEDATATYPEMAPPINGAVAILABLE|The %1 references an external data type that cannot be mapped to a Data Flow task data type. The Data Flow task data type DT_WSTR will be used instead.|  
|0x802070CC|-2145357620|DTS_W_STATICTRUNCATIONINEXPRESSION|The expression "%1" will always result in a truncation of data. The expression contains a static truncation (the truncation of a fixed value).|  
|0x8020820C|-2145353204|DTS_W_UNMAPPEDINPUTCOLUMN|The input column "%1" with ID %2!d! at index %3!d! is unmapped. The lineage ID for the column is zero.|  
|0x80208305|-2145352955|DTS_W_TXFUZZYLOOKUP_DELIMITERS_DONT_MATCH|The specified delimiters do not match the delimiters used to build the pre-existing match index "%1". This error occurs when the delimiters used to tokenize fields do not match. This can have unknown effects on the matching behavior or results.|  
|0x80208308|-2145352952|DTS_W_TXFUZZYLOOKUP_MAXRESULTS_IS_ZERO|The MaxOutputMatchesPerInput property on the Fuzzy Lookup transformation is zero. No results will be produced.|  
|0x80208310|-2145352944|DTS_W_TXFUZZYLOOKUP_NO_FUZZY_JOIN_COLUMNS|There were no valid input columns with JoinType column property set to Fuzzy.  Performance on Exact joins may be improved by using the Lookup transform instead of FuzzyLookup.|  
|0x8020831C|-2145352932|DTS_W_TXFUZZYLOOKUP_TIMESTAMPCAVEAT|The reference column "%1" may be a SQL timestamp column. When the fuzzy match index is built, and a copy of the reference table is made, all reference table timestamps will reflect the current state of the table at the time of the copy. Unexpected behavior may occur if the CopyReferenceTable is set to false.|  
|0x80208321|-2145352927|DTS_W_MATCHINDEXALREADYEXISTS|A table with the name '%1' given for MatchIndexName already exists and DropExistingMatchIndex is set to FALSE.  Transform execution will fail unless this table is dropped, a different name is specified, or DropExisitingMatchIndex is set to TRUE.|  
|0x8020832B|-2145352917|DTS_W_TXFUZZYLOOKUP_JOINLENGTHMISMATCH|The length of input column '%1' is not equal to the length of the reference column '%2' that it is being matched against.|  
|0x8020832D|-2145352915|DTS_W_TXFUZZYLOOKUP_CODEPAGE_MISMATCH|The code pages of the DT_STR source column "%1" and the DT_STR dest column "%2" do not match.  This may cause unexpected results.|  
|0x8020832E|-2145352914|DTS_W_FUZZYLOOKUP_TOOMANYEXACTMATCHCOLUMNS|There are more than 16 exact match joins, so performance may not be optimal. Reduce the number of exact match joins to improve performance. SQL Server has a limit of 16 columns per index, the inverted index will be used for all lookups.|  
|0x80208350|-2145352880|DTS_W_FUZZYLOOKUP_MEMLIMITANDEXHAUSTIVESPECIFIED|The Exhaustive option requires that the entire reference be loaded into main memory.  Since a memory limit has been specified for the MaxMemoryUsage property, it is possible that the entire reference table will not fit within this bound and that the match operation will fail at runtime.|  
|0x80208351|-2145352879|DTS_W_FUZZYLOOKUP_EXACTMATCHCOLUMNSEXCEEDBYTELIMIT|The cumulative lengths of the columns specified in the exact match joins exceeds the 900 byte limit for index keys.  Fuzzy Lookup creates an index on the exact match columns to increase lookup performance and there is a possibility that creation of this index may fail and the lookup will fall back to an alternative, possibly slower, method of finding matches. If performance is a problem, try removing some exact match join columns or reduce the maximum lengths of variable length exact match columns.|  
|0x80208352|-2145352878|DTS_W_FUZZYLOOKUP_EXACTMATCHINDEXCREATIONFAILED|Failed to create an index for exact match columns. Reverting to alternative fuzzy lookup method.|  
|0x80208353|-2145352877|DTS_W_FUZZYGROUPINGINTERNALPIPELINEWARNING|The following Fuzzy Grouping internal pipeline warning occurred with warning code 0x%1!8.8X!: "%2".|  
|0x80208375|-2145352843|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTODEFAULT|No maximum length was specified for the %1 with external data type %2. The SSIS Data Flow Task data type "%3" with a length of %4!d! will be used.|  
|0x80208376|-2145352842|DTS_W_XMLSRCOUTPUTCOLUMNDATATYPEMAPPEDTOSTRING|The %1 references external data type %2, which cannot be mapped to a SSIS Data Flow Task data type.  The SSIS Data Flow Task data type DT_WSTR with a length of %3!d! will be used instead.|  
|0x80208385|-2145352827|DTS_W_NOREDIRECTWITHATTACHEDERROROUTPUTS|No rows will be sent to error output(s). Configure error or truncation dispositions to redirect rows to the error output(s), or delete data flow transformations or destinations that are attached to the error output(s).|  
|0x80208386|-2145352826|DTS_W_REDIRECTWITHNOATTACHEDERROROUTPUTS|Rows sent to the error output(s) will be lost. Add new data flow transformations or destinations to receive error rows, or reconfigure the component to stop redirecting rows to the error output(s).|  
|0x80208391|-2145352815|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTOMAXIMUM|For the %1 with external data type %2, the XML schema specified a maxLength constraint of %3!d!, which exceeds the maximum allowed column length of %4!d!. The SSIS Data Flow Task data type "%5" with a length of %6!d! will be used.|  
|0x802090E4|-2145349404|DTS_W_TXLOOKUP_DUPLICATE_KEYS|The %1 encountered duplicate reference key values when caching reference data. This error occurs in Full Cache mode only. Either remove the duplicate key values, or change the cache mode to PARTIAL or NO_CACHE.|  
|0x802092A7|-2145348953|DTS_W_POTENTIALTRUNCATIONFROMDATAINSERTION|Truncation may occur due to inserting data from data flow column "%1" with a length of %2!d! to database column "%3" with a length of %4!d!.|  
|0x802092A8|-2145348952|DTS_W_POTENTIALTRUNCATIONFROMDATARETRIEVAL|Truncation may occur due to retrieving data from database column "%1" with a length of %2!d! to data flow column "%3" with a length of %4!d!.|  
|0x802092AA|-2145348950|DTS_W_ADODESTBATCHNOTSUPPORTEDFORERRORDISPOSITION|Batch mode is not currently supported when error row disposition is used. The BatchSize property will be set to 1.|  
|0x802092AB|-2145348949|DTS_W_ADODESTNOROWSINSERTED|No rows were successfully inserted into the destination. This may be due to a data type mismatch between columns, or due to the use of a datatype that is unsupported by your ADO.NET provider. Since the error disposition for this component is not "Fail component", error messages are not shown here; set the error disposition to "Fail component" to see error messages here.|  
|0x802092AC|-2145348948|DTS_W_ADODESTPOTENTIALDATALOSS|Potential data loss may occur due to inserting data from input column "%1" with data type "%2" to external column "%3" with data type "%4". If this is intended, an alternative way to do conversion is using a Data Conversion component before ADO NET destination component.|  
|0x802092AD|-2145348947|DTS_W_ADODESTEXTERNALCOLNOTMATCHSCHEMACOL|The %1 has been out of synchronization with the database column.  The latest column has %2. Use advanced editor to refresh  available destination columns if needed.|  
|0x802092AE|-2145348946|DTS_W_ADODESTEXTERNALCOLNOTEXIST|The %1 does not exist in the database. It may have been removed or renamed. Use Advanced Editor to refresh the available destination columns if needed.|  
|0x802092AF|-2145348945|DTS_W_ADODESTNEWEXTCOL|A new column with name %1 has been added to the external database table. Use advanced editor to refresh available destination columns if needed.|  
|0x8020930C|-2145348852|DTS_W_NOMATCHOUTPUTGETSNOROWS|No rows will be sent to the no match output. Configure the transformation to redirect rows with no matching entries to the no match output, or delete the data flow transformations or destinations that are attached to the no match output.|  
|0x8020931B|-2145348837|DTS_W_ADODESTINVARIANTEXCEPTION|Exception received while enumerating ADO.Net providers. The invariant was "%1". The exception message is: "%2"|  
|0xC020822C|-1071611348|DTS_W_UNMAPPEDOUTPUTCOLUMN|The %1 has no input column mapped to it.|  
|0x930D|37645|DTS_W_EXTERNALTABLECOLSOUTOFSYNC|The table "%1" has changed. New columns might have been added to the table.|  
  
##  <a name="msgInfo"></a> Informational Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] informational messages begin with **DTS_I_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x4001100A|1073811466|DTS_I_STARTINGTRANSACTION|Starting distributed transaction for this container.|  
|0x4001100B|1073811467|DTS_I_COMMITTINGTRANSACTION|Committing distributed transaction started by this container.|  
|0x4001100C|1073811468|DTS_I_ABORTINGTRANSACTION|Aborting the current distributed transaction.|  
|0x40013501|1073820929|DTS_I_GOTMUTEXFROMWAIT|Mutex "%1" was successfully acquired.|  
|0x40013502|1073820930|DTS_I_RELEASEACQUIREDMUTEX|Mutex "%1" was successfully released.|  
|0x40013503|1073820931|DTS_I_NEWMUTEXCREATED|Mutex "%1" was successfully created.|  
|0x40015101|1073828097|DTS_I_DUMP_ON_ANY_ERR|Debug dump files will be generated for any error event.|  
|0x40015102|1073828098|DTS_I_DUMP_ON_CODES|Debug dump files will be generated for the following event codes: "%1"|  
|0x40015103|1073828099|DTS_I_START_DUMP|Event code, 0x%1!8.8X!, triggered generation of debug dump files in the folder "%2".|  
|0x40015104|1073828100|DTS_I_SSIS_INFO_DUMP|Creating SSIS information dump file "%1".|  
|0x40015106|1073828102|DTS_I_FINISH_DUMP|Debug dump files successfully created.|  
|0x40016019|1073831961|DTS_I_PACKAGEMIGRATED|The package format was migrated from version %1!d! to version %2!d!. It must be saved to retain migration changes.|  
|0x4001601A|1073831962|DTS_I_SCRIPTSMIGRATED|The scripts in the package were migrated. The package must be saved to retain migration changes.|  
|0x40016025|1073831973|DTS_I_FTPRECEIVEFILE|Receiving file "%1".|  
|0x40016026|1073831974|DTS_I_FTPSENDFILE|Sending file "%1".|  
|0x40016027|1073831975|DTS_I_FTPFILEEXISTS|File "%1" already exists.|  
|0x40016028|1073831976|DTS_I_FTPERRORLOADINGMSG|Cannot get extra error information due to an internal error.|  
|0x40016036|1073831990|DTS_I_FTPDELETEFILE|The attempt to delete file "%1" failed. This may occur when the file does not exist, the file name was spelled incorrectly, or you do not have permissions to delete the file.|  
|0x40016037|1073831991|DTS_I_CONFIGFROMREG|The package is attempting to configure from a registry entry using the registry key "%1".|  
|0x40016038|1073831992|DTS_I_CONFIGFROMENVVAR|The package is attempting to configure from the environment variable "%1".|  
|0x40016039|1073831993|DTS_I_CONFIGFROMINIFILE|The package is attempting to configure from the .ini file "%1".|  
|0x40016040|1073832000|DTS_I_CONFIGFROMSQLSERVER|The package is attempting to configure from SQL Server using the configuration string "%1".|  
|0x40016041|1073832001|DTS_I_CONFIGFROMFILE|The package is attempting to configure from the XML file "%1".|  
|0x40016042|1073832002|DTS_I_CONFIGFROMPARENTVARIABLE|The package is attempting to configure from the parent variable "%1".|  
|0x40016043|1073832003|DTS_I_ATTEMPTINGUPGRADEOFDTS|Attempting an upgrade of SSIS from version "%1" to version "%2". The package is attempting to upgrade the runtime.|  
|0x40016044|1073832004|DTS_I_ATTEMPTINGUPGRADEOFANEXTOBJ|Attempting to upgrade "%1". The package is attempting to upgrade an extensible object.|  
|0x40016045|1073832005|DTS_I_SAVECHECKPOINTSTOFILE|The package will be saving checkpoints to file "%1" during execution. The package is configured to save checkpoints.|  
|0x40016046|1073832006|DTS_I_RESTARTFROMCHECKPOINTFILE|The package restarted from checkpoint file "%1". The package was configured to restart from checkpoint.|  
|0x40016047|1073832007|DTS_I_CHECKPOINTSAVEDTOFILE|Checkpoint file "%1" was updated to record completion of this container.|  
|0x40016048|1073832008|DTS_I_CHECKPOINTFILEDELETED|Checkpoint file "%1" was deleted after successful completion of the package.|  
|0x40016049|1073832009|DTS_I_CHECKPOINTSAVINGTOFILE|Checkpoint file "%1" update starting.|  
|0x40016051|1073832017|DTS_I_CHOSENMAXEXECUTABLES|Based on the system configuration, the maximum concurrent executables are set to %1!d!.|  
|0x40016052|1073832018|DTS_I_MAXEXECUTABLES|Maximum concurrent executables are set to %1!d!.|  
|0x40016053|1073832019|DTS_I_PACKAGESTART|Beginning of package execution.|  
|0x40016054|1073832020|DTS_I_PACKAGEEND|End of package execution.|  
|0x40029161|1073910113|DTS_I_FSTASK_DIRECTORYDELETED|Directory "%1" was deleted.|  
|0x40029162|1073910114|DTS_I_FSTASK_FILEDELETED|File or directory "%1" was deleted.|  
|0x400292A8|1073910440|DTS_I_TRANSFERDBTASK_OVERWRITEDB|Overwriting the database "%1" on the destination server "%2".|  
|0x4002F304|1073935108|DTS_I_SOMETHINGHAPPENED|"%1".|  
|0x4002F323|1073935139|DTS_I_ERRMSGTASK_SKIPPINGERRORMESSAGEALREADYEXISTS|Skipping error message "%1" since it already exists on the destination server.|  
|0x4002F326|1073935142|DTS_I_ERRMSGTASK_TRANSFEREDNERRORMESSAGES|"%1" Error Messages were transferred.|  
|0x4002F351|1073935185|DTS_I_STOREDPROCSTASKS_TRANSFEREDNSPS|The task transferred "%1" Stored Procedures.|  
|0x4002F352|1073935186|DTS_I_TRANSOBJECTSTASK_TRANSFEREDNOBJECTS|Transferred "%1" objects.|  
|0x4002F358|1073935192|DTS_I_TRANSOBJECTSTASK_NOSPSTOTRANSFER|There are no Stored Procedures to transfer.|  
|0x4002F362|1073935202|DTS_I_TRANSOBJECTSTASK_NORULESTOTRANSFER|There are no Rules to transfer.|  
|0x4002F366|1073935206|DTS_I_TRANSOBJECTSTASK_NOTABLESTOTRANSFER|There are no Tables to transfer.|  
|0x4002F370|1073935216|DTS_I_TRANSOBJECTSTASK_NOVIEWSTOTRANSFER|There are no Views to transfer.|  
|0x4002F374|1073935220|DTS_I_TRANSOBJECTSTASK_NOUDFSTOTRANSFER|There are no User Defined Functions to transfer.|  
|0x4002F378|1073935224|DTS_I_TRANSOBJECTSTASK_NODEFAULTSTOTRANSFER|There are no Defaults to transfer.|  
|0x4002F382|1073935234|DTS_I_TRANSOBJECTSTASK_NOUDDTSTOTRANSFER|There are no User Defined Data Types to transfer.|  
|0x4002F386|1073935238|DTS_I_TRANSOBJECTSTASK_NOPFSTOTRANSFER|There are no Partition Functions to transfer.|  
|0x4002F390|1073935248|DTS_I_TRANSOBJECTSTASK_NOPSSTOTRANSFER|There are no Partition Schemes to transfer.|  
|0x4002F394|1073935252|DTS_I_TRANSOBJECTSTASK_NOSCHEMASTOTRANSFER|There are no Schemas to transfer.|  
|0x4002F398|1073935256|DTS_I_TRANSOBJECTSTASK_NOSQLASSEMBLIESTOTRANSFER|There are no SqlAssemblies to transfer.|  
|0x4002F402|1073935362|DTS_I_TRANSOBJECTSTASK_NOAGGREGATESTOTRANSFER|There are no User Defined Aggregates to transfer.|  
|0x4002F406|1073935366|DTS_I_TRANSOBJECTSTASK_NOTYPESTOTRANSFER|There are no User Defined Types to transfer.|  
|0x4002F410|1073935376|DTS_I_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONSTOTRANSFER|There are no XmlSchemaCollections to transfer.|  
|0x4002F418|1073935384|DTS_I_TRANSOBJECTSTASK_NOLOGINSTOTRANSFER|There are no Logins to transfer.|  
|0x4002F41D|1073935389|DTS_I_TRANSOBJECTSTASK_NOUSERSTOTRANSFER|There are no Users to transfer.|  
|0x4002F41E|1073935390|DTS_I_TRANSOBJECTSTASK_TRUNCATINGTABLE|Truncating table "%1"|  
|0x40043006|1074016262|DTS_I_EXECUTIONPHASE_PREPAREFOREXECUTE|Prepare for Execute phase is beginning.|  
|0x40043007|1074016263|DTS_I_EXECUTIONPHASE_PREEXECUTE|Pre-Execute phase is beginning.|  
|0x40043008|1074016264|DTS_I_EXECUTIONPHASE_POSTEXECUTE|Post Execute phase is beginning.|  
|0x40043009|1074016265|DTS_I_EXECUTIONPHASE_CLEANUP|Cleanup phase is beginning.|  
|0x4004300A|1074016266|DTS_I_EXECUTIONPHASE_VALIDATE|Validation phase is beginning.|  
|0x4004300B|1074016267|DTS_I_ROWS_WRITTEN|"%1" wrote %2!ld! rows.|  
|0x4004300C|1074016268|DTS_I_EXECUTIONPHASE_EXECUTE|Execute phase is beginning.|  
|0x4004800C|1074036748|DTS_I_CANTRELIEVEPRESSURE|The buffer manager detected that the system was low on virtual memory, but was unable to swap out any buffers. %1!d! buffers were considered and %2!d! were locked. Either not enough memory is available to the pipeline because not enough is installed, other processes are using it, or too many buffers are locked.|  
|0x4004800D|1074036749|DTS_I_CANTALLOCATEMEMORYPRESSURE|The buffer manager failed a memory allocation call for %3!d! bytes, but was unable to swap out any buffers to relieve memory pressure. %1!d! buffers were considered and %2!d! were locked. Either not enough memory is available to the pipeline because not enough are installed, other processes were using it, or too many buffers are locked.|  
|0x4004800E|1074036750|DTS_I_ALLOCATEDDURINGMEMORYPRESSURE|The buffer manager has allocated %1!d! bytes, even though the memory pressure has been detected and repeated attempts to swap buffers have failed.|  
|0x400490F4|1074041076|DTS_I_TXLOOKUP_CACHE_PROGRESS|%1 has cached %2!d! rows.|  
|0x400490F5|1074041077|DTS_I_TXLOOKUP_CACHE_FINAL|%1 has cached a total of %2!d! rows.|  
|0x4020206D|1075847277|DTS_I_RAWSOURCENOCOLUMNS|The raw source adapter opened a file, but the file contains no columns. The adapter will not produce data. This could indicate a damaged file, or that there are zero columns and, therefore, no data.|  
|0x402020DA|1075847386|DTS_I_OLEDBINFORMATIONALMESSAGE|An OLE DB informational message is available.|  
|0x40208327|1075872551|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_COLLATIONS_DONT_MATCH|Fuzzy match performance can be improved if the exact join FuzzyComparisonFlags on the input column "%1" are set to match with the default SQL collation for reference table column "%2".  It is also necessary that no fold flags are set in FuzzyComparisonFlagsEx.|  
|0x40208328|1075872552|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_INDEX_MISSING|Fuzzy match performance can be improved if an index is created upon the reference table across all of the specified exact match columns.|  
|0x40208387|1075872647|DTS_I_DISPSNOTREVIEWED|Error and truncation dispositions were not reviewed. Make sure this component is configured to redirect rows to error outputs, if you wish to further transform those rows.|  
|0x402090DA|1075876058|DTS_I_TXAGG_WORKSPACE_REHASH|The Aggregate transformation has encountered %1!d! key combinations. It has to re-hash data because the number of key combinations is more than expected. The component can be configured to avoid data re-hash by adjusting the Keys, KeyScale, and AutoExtendFactor properties.|  
|0x402090DB|1075876059|DTS_I_TXAGG_COUNTDISTINCT_REHASH|The Aggregate transformation has encountered %1!d! distinct values while performing a "count distinct" aggregation on "%2". The transformation will re-hash data because the number of distinct values is more than expected. The component can be configured to avoid data re-hash by adjusting the CountDistinctKeys, CountDistinctKeyScale, and AutoExtendFactor properties.|  
|0x402090DC|1075876060|DTS_I_STARTPROCESSINGFILE|The processing of file "%1" has started.|  
|0x402090DD|1075876061|DTS_I_FINISHPROCESSINGFILE|The processing of file "%1" has ended.|  
|0x402090DE|1075876062|DTS_I_TOTALDATAROWSPROCESSEDFORFILE|The total number of data rows processed for file "%1" is %2!I64d!.|  
|0x402090DF|1075876063|DTS_I_FINALCOMMITSTARTED|The final commit for the data insertion in "%1" has started.|  
|0x402090E0|1075876064|DTS_I_FINALCOMMITENDED|The final commit for the data insertion  in "%1" has ended.|  
|0x402090E1|1075876065|DTS_I_BEGINHASHINGCACHE|%1!u! rows are added to the cache. The system is processing the rows.|  
|0x402090E2|1075876066|DTS_I_SUCCEEDEDHASHINGCACHE|The %1 processed %2!u! rows in the cache. The processing time was %3 seconds. The cache used %4!I64u! bytes of memory.|  
|0x402090E3|1075876067|DTS_I_FAILEDHASHINGCACHE|The %1 failed to process the rows in the cache.  The processing time was %2 second(s).|  
|0x402090E4|1075876068|DTS_I_SUCCEEDEDPREPARINGCACHE|The %1 succeeded in preparing the cache. The preparation time was %2 seconds.|  
|0x40209314|1075876628|DTS_I_TXLOOKUP_PARTIALPERF|The %1 has performed the following operations: processed %2!I64u! rows, issued %3!I64u! database commands to the reference database, and performed %4!I64u! lookups using partial cache.|  
|0x40209315|1075876629|DTS_I_TXLOOKUP_PARTIALPERF2|The %1 has performed the following operations: processed %2!I64u! rows, issued %3!I64u! database commands to the reference database, performed %4!I64u! lookups using partial cache and %5!I64u! lookups using the cache for rows with no matching entries in the initial lookup.|  
|0x40209316|1075876630|DTS_I_CACHEFILEWRITESTARTED|The %1 is writing the cache to file "%2".|  
|0x40209317|1075876631|DTS_I_CACHEFILEWRITESUCCEEDED|The %1 has written the cache to file "%2".|  
|0x4020F42C|1075901484|DTS_I_OLEDBDESTZEROMAXCOMMITSIZE|The Maximum insert commit size property of the OLE DB destination "%1" is set to 0. This property setting can cause the running package to stop responding. For more information, see the F1 Help topic for OLE DB Destination Editor (Connection Manager Page).|  
  
##  <a name="msgGeneral"></a> General and Event Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] error messages begin with **DTS_MSG_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x1|1|DTS_MSG_CATEGORY_SERVICE_CONTROL|Incorrect function.|  
|0x2|2|DTS_MSG_CATEGORY_RUNNING_PACKAGE_MANAGEMENT|The system cannot find the file specified.|  
|0x100|256|DTS_MSG_SERVER_STARTING|Starting Microsoft SSIS Service.<br /><br /> Server version %1|  
|0x101|257|DTS_MSG_SERVER_STARTED|Microsoft SSIS Service started.<br /><br /> Server version %1|  
|0x102|258|DTS_MSG_SERVER_STOPPING|The wait operation timed out.|  
|0x103|259|DTS_MSG_SERVER_STOPPED|No more data is available.|  
|0x104|260|DTS_MSG_SERVER_START_FAILED|Microsoft SSIS Service failed to start.<br /><br /> Error: %1|  
|0x105|261|DTS_MSG_SERVER_STOP_ERROR|Error stopping Microsoft SSIS Service.<br /><br /> Error: %1|  
|0x110|272|DTS_MSG_SERVER_MISSING_CONFIG|Microsoft SSIS Service configuration file does not exist.<br /><br /> Loading with default settings.|  
|0x111|273|DTS_MSG_SERVER_BAD_CONFIG|Microsoft SSIS Service configuration file is incorrect.<br /><br /> Error reading config file: %1<br /><br /> Loading server with default settings.|  
|0x112|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|Microsoft SSIS Service:<br /><br /> Registry setting specifying configuration file does not exist.<br /><br /> Attempting to load default config file.|  
|0x150|336|DTS_MSG_SERVER_STOPPING_PACKAGE|Microsoft SSIS Service: stopping running package.<br /><br /> Package instance ID: %1<br /><br /> Package ID: %2<br /><br /> Package name: %3<br /><br /> Package description: %4<br /><br /> Package started by: %5.|  
|0x40013000|1073819648|DTS_MSG_PACKAGESTART|Package "%1" started.|  
|0x40013001|1073819649|DTS_MSG_PACKAGESUCCESS|Package "%1" finished successfully.|  
|0x40013002|1073819650|DTS_MSG_PACKAGECANCEL|Package "%1" has been cancelled.|  
|0x40013003|1073819651|DTS_MSG_PACKAGEFAILURE|Package "%1" failed.|  
|0x40013004|1073819652|DTS_MSG_CANTDELAYLOADDLL|Module %1 cannot load DLL %2 to call entry point %3 because of error %4. The product requires that DLL to run, but the DLL could not be found on the path.|  
|0x40013005|1073819653|DTS_MSG_CANTDELAYLOADDLLFUNCTION|Module %1 loaded DLL %2, but cannot find entry point %3 because of error %4. The named DLL could not be found on the path, and the product requires that DLL to run.|  
|0x40103100|1074802944|DTS_MSG_EVENTLOGENTRY|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103101|1074802945|DTS_MSG_EVENTLOGENTRY_PREEXECUTE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103102|1074802946|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103103|1074802947|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103104|1074802948|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103105|1074802949|DTS_MSG_EVENTLOGENTRY_WARNING|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103106|1074802950|DTS_MSG_EVENTLOGENTRY_ERROR|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103107|1074802951|DTS_MSG_EVENTLOGENTRY_TASKFAILED|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103108|1074802952|DTS_MSG_EVENTLOGENTRY_PROGRESS|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103109|1074802953|DTS_MSG_EVENTLOGENTRY_EXECSTATCHANGE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310A|1074802954|DTS_MSG_EVENTLOGENTRY_VARVALCHANGE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310B|1074802955|DTS_MSG_EVENTLOGENTRY_CUSTOMEVENT|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310C|1074802956|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310D|1074802957|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310E|1074802958|DTS_MSG_EVENTLOGENTRY_INFORMATION|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
  
##  <a name="msgSuccess"></a> Success Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] success messages begin with **DTS_S_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x40003|262147|DTS_S_NULLDATA|The value is NULL.|  
|0x40005|262149|DTS_S_TRUNCATED|The string value was truncated. The buffer received a string that was too long for the column, and the string was truncated by the buffer.|  
|0x200001|2097153|DTS_S_EXPREVALTRUNCATIONOCCURRED|A truncation occurred during evaluation of the expression. The truncation occurred during evaluation, which may include any point in an intermediate step.|  
  
##  <a name="msgPipeline"></a> Data Flow Component Error Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] error messages begin with **DTSBC_E_**, where "BC" refers to the native base class from which most Microsoft data flow components are derived.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0xC8000002|-939524094|DTSBC_E_INCORRECTEXACTNUMBEROFTOTALOUTPUTS|The total number of outputs and error outputs, %1!lu!, is incorrect. There must be exactly %2!lu!.|  
|0xC8000003|-939524093|DTSBC_E_FAILEDTOGETOUTPUTBYINDEX|Cannot retrieve output with index %1!lu!.|  
|0xC8000005|-939524091|DTSBC_E_INCORRECTEXACTNUMBEROFERROROUTPUTS|The number of error outputs, %1!lu!,  is incorrect. There must be exactly %2!lu!.|  
|0xC8000006|-939524090|DTSBC_E_INVALIDVALIDATIONSTATUSVALUE|Incorrect validation status value, "%1!lu! ".  It must be one of the values found in the DTSValidationStatus enumeration.|  
|0xC8000007|-939524089|DTSBC_E_INPUTHASNOOUTPUT|The input "%1!lu!" has no synchronous output.|  
|0xC8000008|-939524088|DTSBC_E_INPUTHASNOERROROUTPUT|The input "%1!lu!" has no synchronous error output.|  
|0xC8000009|-939524087|DTSBC_E_INVALIDHTPIVALUE|The HowToProcessInput value, %1!lu!, is not valid. It must be one of the values from the HowToProcessInput enumeration.|  
|0xC800000A|-939524086|DTSBC_E_FAILEDTOGETCOLINFO|Failed to get information for row "%1!ld!", column "%2!ld!" from the buffer.  The error code returned was 0x%3!8.8X!.|  
|0xC800000B|-939524085|DTSBC_E_FAILEDTOSETCOLINFO|Failed to set information for row "%1!ld!", column "%2!ld!" into the buffer.  The error code returned was 0x%3!8.8X!.|  
|0xC800000C|-939524084|DTSBC_E_INVALIDPROPERTY|The property "%1" is not valid.|  
|0xC800000D|-939524083|DTSBC_E_PROPERTYNOTFOUND|The property "%1" was not found.|  
|0xC8000010|-939524080|DTSBC_E_READONLYPROPERTY|Error assigning a value to the read-only property "%1".|  
|0xC8000011|-939524079|DTSBC_E_CANTINSERTOUTPUTCOLUMN|The %1 does not allow the insertion of output columns.|  
|0xC8000012|-939524078|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCH|The output columns' metadata does not match the associated input columns' metadata.  The output columns' metadata will be updated.|  
|0xC8000013|-939524077|DTSBC_E_OUTPUTCOLUMNSMISSING|There are input columns that do not have associated output columns. The output columns will be added.|  
|0xC8000014|-939524076|DTSBC_E_TOOMANYOUTPUTCOLUMNS|There are output columns that do not have associated input columns. The output columns will be removed.|  
|0xC8000015|-939524075|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCHUNMAP|The output columns' metadata does not match the associated input columns' metadata.  The input columns will be unmapped.|  
|0xC8000016|-939524074|DTSBC_E_UNMAPINPUTCOLUMNS|There are input columns that do not have associated output columns. The input columns will be unmapped.|  
|0xC8000017|-939524073|DTSBC_E_MULTIPLEINCOLSTOOUTCOL|There is an input column associated with an output column, and that output column is already associated with another input column on the same input.|  
|0xC8000018|-939524072|DTSBC_E_CANTINSERTEXTERNALMETADATACOLUMN|The %1 does not allow the insertion of external metadata columns.|  
  
  将 SQL Server 上的文件夹“%1\\\\重命名为`2" to "%1\\\\`3”时出错。
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: sql
ms.prod_service: "integration-services"
ms.reviewer: ""
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords: 
  - "error numbers [Integration Services]"
  - "hresults [Integration Services]"
  - "errors [Integration Services], listed"
ms.assetid: 2c825c07-5074-42ad-90ea-0dc5a588dcf7
author: janinezhang
ms.author: janinez
---
# Integration Services Error and Message Reference

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  The following tables list predefined [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] errors, warnings, and informational messages, in ascending numerical order within each category, along with their numeric codes and symbolic names. Each of these errors is defined as a field in the <xref:Microsoft.SqlServer.Dts.Runtime.Hresults> class in the <xref:Microsoft.SqlServer.Dts.Runtime> namespace.  
  
 This list may be useful when you encounter an error code without its description. The list does not include troubleshooting information at this time.  
  
> [!IMPORTANT]  
>  Many of the error messages that you may see while working with [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] come from other components. In this topic, you will find all the errors raised by [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] components. If you do not see your error in the list, the error was raised by a component outside [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. These may include OLE DB providers, other database components such as the [!INCLUDE[ssDE](../includes/ssde-md.md)] and [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , or other services or components such as the file system, the SMTP server, Message Queuing (also known as MSMQ), and so forth. To find information about these external error messages, see the documentation specific to the component.  
  
 This list cadontains the following groups of messages:  
  
-   [Error Messages (DTS_E_*)](#msgError)  
  
-   [Warning Messages (DTS_W_*)](#msgWarning)  
  
-   [Informational Messages(DTS_I_*)](#msgInfo)  
  
-   [General and Event Messages(DTS_MSG_*)](#msgGeneral)  
  
-   [Success Messages(DTS_S_*)](#msgSuccess)  
  
-   [Data Flow Component Error Messages (DTSBC_E_*)](#msgPipeline)  
  
##  <a name="msgError"></a> Error Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] error messages begin with **DTS_E_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x8002F347|-2147290297|DTS_E_STOREDPROCSTASK_OVERWRITINGSPATDESTINATION|Overwriting Stored Procedure "%1" at destination.|  
|0x8020837E|-2145352834|DTS_E_ADOSRCUNKNOWNTYPEMAPPEDTONTEXT|The data type "%1" found on column "%2" is not supported for the %3. This column will be converted to  DT_NTEXT.|  
|0x8020838C|-2145352820|DTS_E_XMLSRCSCHEMACOLUMNNOTINEXTERNALMETADATA|The column %1 in table %2 in the XML schema does not have a mapping in the external metadata columns.|  
|0xC0000032|-1073741774|DTS_E_NOTINITIALIZED|An internal object or variable was not initialized. This is an internal product error.  This error is returned when a variable should have a valid value but does not.|  
|0xC0000033|-1073741773|DTS_E_EXPIRED|Integration Services evaluation period has expired.|  
|0xC0000034|-1073741772|DTS_E_NEGATIVEVALUESNOTALLOWED|This property cannot be assigned a negative value. This error occurs when a negative value is assigned to a property that can only contain positive values, such as the COUNT property.|  
|0xC0000035|-1073741771|DTS_E_NEGATIVEINDEXNOTALLOWED|Indexes cannot be negative. This error occurs when a negative value is used as an index to a collection.|  
|0xC00060AB|-1073717077|DTS_E_INVALIDSSISSERVERNAME|Invalid server name "%1". SSIS service does not support multi-instance, use just server name instead of "server name\instance".|  
|0xC0008445|-1073707963|DTS_E_SCRIPTMIGRATIONFAILED64BIT|Migration for VSA scripts can not be done on 64 bit platforms due to lack of Visual Tools for Applications designer support. Run the migration under WOW64 on 64 bit platforms.|  
|0xC000931A|-1073704166|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_ERRORSINCOMMAND|The command execution generated errors.|  
|0xC000F427|-1073679321|DTS_E_SSISSTANDALONENOTINSTALLED|To run a SSIS package outside of [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] you must install %1 of Integration Services or higher.|  
|0xC0010001|-1073676287|DTS_E_VARIABLENOTFOUND|The variable cannot be found. This occurs when an attempt is made to retrieve a variable from the Variables collection on a container during execution of the package, and the variable is not there. The variable name may have changed or the variable is not being created.|  
|0xC0010003|-1073676285|DTS_E_VARIABLEREADONLY|Error trying to write to a read-only variable, "%1".|  
|0xC0010004|-1073676284|DTS_E_MANAGEDCOMPONENTSTORENOTFOUND|Unable to find the directories containing Tasks and Data Flow Task components. Check the integrity of your installation.|  
|0xC0010006|-1073676282|DTS_E_PACKAGENAMETOOLONG|Package name is too long. The limit is 128 characters. Shorten the package name.|  
|0xC0010007|-1073676281|DTS_E_PACKAGEDESCRIPTIONTOOLONG|Package description is too long. The limit is 1024 characters. Shorten the package description.|  
|0xC0010008|-1073676280|DTS_E_VERCOMMENTSTOOLONG|VersionComments property is too long. The limit is 1024 characters. Try shortening the VersionComments.|  
|0xC0010009|-1073676279|DTS_E_ELEMENTNOTFOUND|The element cannot be found in a collection. This error happens when you try to retrieve an element from a collection on a container during execution of the package and the element is not there.|  
|0xC001000A|-1073676278|DTS_E_PACKAGENOTFOUND|The specified package could not be loaded from the SQL Server database.|  
|0xC001000C|-1073676276|DTS_E_INVALIDVARIABLEVALUE|The variable value assignment is not valid. This error happens when the client or a task assigns a runtime object to a variable value.|  
|0xC001000D|-1073676275|DTS_E_RESERVEDNAMESPACE|Error assigning namespace to the variable. The namespace "System" is reserved for system use. This error happens when a component or task attempts to create a variable with a namespace of "System".|  
|0xC001000E|-1073676274|DTS_E_CONNECTIONNOTFOUND|The connection "%1" is not found. This error is thrown by Connections collection when the specific connection element is not found.|  
|0xC001000F|-1073676273|DTS_E_64BITVARIABLERECAST|The variable "%1" is a 64-bit integer variable, which is not supported on this operating system. The variable has been recast to 32-bit integer.|  
|0xC0010010|-1073676272|DTS_E_CANTCHANGEREADONLYATRUNTIME|An attempt change to a read-only attribute on variable "%1" occurred. This error happens when a read-only attribute for a variable is being changed at runtime. Read-only attributes can be changed only at design time.|  
|0xC0010011|-1073676271|DTS_E_VARIABLEINVALIDCONTAINERREF|Invalid attempt to set a variable to a container reference.  Variables are not allowed to reference containers.|  
|0xC0010013|-1073676269|DTS_E_INVALIDVARVALUE|Assigning invalid value or object to variable "%1". This error happens when a value is not appropriate for variables.|  
|0xC0010014|-1073676268|DTS_E_GENERICERROR|One or more error occurred. There should be more specific errors preceding this one that explains the details of the errors. This message is used as a return value from functions that encounter errors.|  
|0xC0010016|-1073676266|DTS_E_INVALIDARRAYVALUE|Error getting or setting an array value. The type "%1" is not allowed. This occurs when loading an array into a variable.|  
|0xC0010017|-1073676265|DTS_E_UNSUPPORTEDARRAYTYPE|Unsupported type in array. This happens when saving an array of unsupported types into a variable.|  
|0xC0010018|-1073676264|DTS_E_PERSISTENCEERROR|Error loading value "%1" from node "%2".|  
|0xC0010019|-1073676263|DTS_E_INVALIDNODE|Node "%1" is not a valid node. This happens when saving fails.|  
|0xC0010020|-1073676256|DTS_E_ERRORLOADINGTASK|Failed to load task "%1", type "%2". The contact information for this task is "%3".|  
|0xC0010021|-1073676255|DTS_E_ERRORELEMENTNOTINCOLL|Element "%1" does not exist in collection "%2".|  
|0xC0010022|-1073676254|DTS_E_MISSINGOBJECTDATA|The ObjectData element is missing in the XML block of a hosted object. This occurs when the XML parser attempts to locate the data element for an object and it cannot be found.|  
|0xC0010023|-1073676253|DTS_E_VARIABLENOTFOUNDINCOLL|The variable "%1" cannot be found. This error occurs when an attempt to retrieve a variable from a variables collection on a container during execution of the package occurs, and the variable is not there.  A variable name may have changed or the variable is not being created.|  
|0xC0010025|-1073676251|DTS_E_HASEMPTYTASKHOSTS|The package cannot execute because it contains tasks that failed to load.|  
|0xC0010026|-1073676250|DTS_E_TASKISEMPTY|The task has failed to load. The contact information for this task is "%1".|  
|0xC0010027|-1073676249|DTS_E_ERRORLOADINGTASKNOCONTACT|Error loading task "%1".|  
|0xC0010028|-1073676248|DTS_E_ERRORATLOADTASK|Error loading task. This happens when loading a task from XML fails.|  
|0xC0010200|-1073675776|DTS_E_MULTIPLECACHEWRITES|The %1 cannot write to the cache because %2 has already written to it.|  
|0xC0010201|-1073675775|DTS_E_SETCACHEFORINSERTFAILED|Failed to prepare the cache for new data.|  
|0xC0010202|-1073675774|DTS_E_SETCACHEFORFILLFAILED|Failed to mark the cache as filled with data.|  
|0xC0010203|-1073675773|DTS_E_READUNINITIALIZEDCACHE|The cache is not initialized and cannot be read by %1.|  
|0xC0010204|-1073675772|DTS_E_SETCACHEFORREADFAILED|Failed to prepare the cache for providing data.|  
|0xC0010205|-1073675771|DTS_E_READNOTFILLEDCACHE|The cache is being written to by %1, and cannot be read by %2.|  
|0xC0010206|-1073675770|DTS_E_WRITEWHILECACHEINUSE|The cache is being read from %1 and cannot be written to by %2.|  
|0xC0011001|-1073672191|DTS_E_CANTLOADFROMNODE|The runtime object cannot be loaded from the specified XML node.  This happens when trying to load a package or other object from an XML node that is not of the correct type, such as a non-SSIS XML node.|  
|0xC0011002|-1073672190|DTS_E_OPENPACKAGEFILE|Failed to open package file "%1" due to error 0x%2!8.8X! "%3".  This happens when loading a package and the file cannot be opened or loaded correctly into the XML document. This can be the result of either providing an incorrect file name was specified when calling LoadPackage or the XML file was specified and has an incorrect format.|  
|0xC0011003|-1073672189|DTS_E_LOADPACKAGEXML|Failed to load XML due to error 0x%1!8.8X! "%2". This happens when loading a package and the file cannot be opened or loaded correctly into XML document.  This can be the result of either providing an incorrect file name to the LoadPackage method or the XML file specified having an incorrect format.|  
|0xC0011004|-1073672188|DTS_E_LOADPACKAGEXMLFILE|Failed to load XML from package file "%1" due to error 0x%2!8.8X! "%3".  This happens when loading a package and the file cannot be opened or loaded correctly into an XML document. This can be the result of either providing an incorrect file name to the LoadPackage method or the XML file specified having an incorrect format.|  
|0xC0011005|-1073672187|DTS_E_OPENFILE|Failed to open package file. This happens when loading a package and the file cannot be opened or loaded correctly into an XML document. This can be the result of either providing an incorrect file name to the LoadPackage method or the XML file specified having an incorrect format.|  
|0xC0011006|-1073672186|DTS_E_UNABLETODECODEBINARYFORMAT|Unable to decode a binary format in the package.|  
|0xC0011007|-1073672185|DTS_E_FUNDAMENTALLOADINGERROR|Unable to load the package as XML because of package does not have a valid XML format. A specific XML parser error will be posted.|  
|0xC0011008|-1073672184|DTS_E_LOADFROMXML|Error loading from XML. No further detailed error information can be specified for this problem because no Events object was passed where detailed error information can be stored.|  
|0xC0011009|-1073672183|DTS_E_XMLDOMERROR|Cannot create an instance of the XML Document Object Model. MSXML may not be registered.|  
|0xC001100D|-1073672179|DTS_E_CANNOTLOADOLDPACKAGES|The package cannot be loaded. This occurs when attempting to load an older version package, or the package file refers to an invalid structured object.|  
|0xC001100E|-1073672178|DTS_E_SAVEFILE|Failed to save package file.|  
|0xC001100F|-1073672177|DTS_E_SAVEPACKAGEFILE|Failed to save package file "%1" with error 0x%2!8.8X! "%3".|  
|0xC001200D|-1073668083|DTS_E_IDTSNAMENOTSUPPORTED|The object must inherit from IDTSName100 and does not.|  
|0xC0012018|-1073668072|DTS_E_CONFIGFORMATINVALID_PACKAGEDELIMITER|The configuration entry, "%1", has an incorrect format because it does not begin with package delimiter. There was no "\package" delimiter.|  
|0xC0012019|-1073668071|DTS_E_CONFIGFORMATINVALID|The configuration entry "%1" had an incorrect format. This can occur because of a missing delimiter or formatting errors, like an invalid array delimiter.|  
|0xC001201B|-1073668069|DTS_E_CONFIGFILEFAILEDEXPORT|Failure exporting configuration file.|  
|0xC0012021|-1073668063|DTS_E_PROPERTIESCOLLECTIONREADONLY|Properties collection cannot be modified.|  
|0xC0012022|-1073668062|DTS_E_DTRXMLSAVEFAILURE|Unable to save configuration file. The file may be read only.|  
|0xC0012023|-1073668061|DTS_E_FAILPACKAGEONFAILURENA|FailPackageOnFailure property is not applicable to the package container.|  
|0xC0012024|-1073668060|DTS_E_TASKPRODUCTLEVEL|The task "%1" cannot run on installed %2 of Integration Services. It requires %3 or higher.|  
|0xC0012029|-1073668055|DTS_E_UNABLETOSAVETOFILE|Unable to save xml to "%1". The file may be read only.|  
|0xC0012037|-1073668041|DTS_E_CONFIGTYPECONVERSIONFAILED|Failed to convert a type in the configuration "%1" for the package path "%2".  This happens when a configuration value cannot be converted from a string to the appropriate destination type. Check the configuration value to ensure it can be converted to the type of the destination property or variable.|  
|0xC0012049|-1073668023|DTS_E_CONFIGFAILED|Configuration failure. This is a generic warning for all configuration types. Other warnings should precede this with more information.|  
|0xC0012050|-1073668016|DTS_E_REMOTEPACKAGEVALIDATION|Package failed validation from the ExecutePackage task. The package cannot run.|  
|0xC0013001|-1073663999|DTS_E_FAILTOCREATEMUTEX|Failed to create mutex "%1" with error 0x%2!8.8X!.|  
|0xC0013002|-1073663998|DTS_E_MUTEXOWNBYDIFFUSER|Mutex "%1" already exists and is owned by another user.|  
|0xC0013003|-1073663997|DTS_E_WAITFORMUTEXFAILED|Failed to acquire mutex "%1" with error 0x%2!8.8X!.|  
|0xC0013004|-1073663996|DTS_E_FAILTORELEASEMUTEX|Failed to release mutex "%1" with error 0x%2!8.8X!.|  
|0xC0014003|-1073659901|DTS_E_INVALIDTASKPOINTER|The wrappers task pointer is not valid. The wrapper has an invalid pointer to a task.|  
|0xC0014004|-1073659900|DTS_E_ALREADYADDED|The executable has been added to the Executables collection of another container. This occurs when a client tries to add an executable to more than one Executables collection. You need to remove the executable from the current Executables collection before attempting to add it.|  
|0xC0014005|-1073659899|DTS_E_UNKNOWNCONNECTIONMANAGERTYPE|The connection type "%1" specified for connection manager "%2" is not recognized as a valid connection manager type. This error is returned when an attempt is made to create a connection manager for an unknown connection type. Check the spelling in the connection type name.|  
|0xC0014006|-1073659898|DTS_E_COLLECTIONCOULDNTADD|An object was created but the attempt to add it to a collection failed. This can occur due to an out-of-memory condition.|  
|0xC0014007|-1073659897|DTS_E_ODBCERRORENV|There was an error creating an Open Database Connectivity (ODBC) environment.|  
|0xC0014008|-1073659896|DTS_E_ODBCERRORDBC|There was an error creating an Open Database Connectivity (ODBC) database connection.|  
|0xC0014009|-1073659895|DTS_E_ODBCERRORCONNECT|There was an error trying to establish an Open Database Connectivity (ODBC) connection with the database server.|  
|0xC001400A|-1073659894|DTS_E_CONNECTIONMANAGERQUALIFIERALREADYSET|The qualifier is already set on this instance of the connection manager. The qualifier may be set once per instance.|  
|0xC001400B|-1073659893|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSET|The qualifier has not been set on this instance of the connection manager. Setting the qualifier is required to complete initialization.|  
|0xC001400C|-1073659892|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSUPPORTED|This connection manager does not support specification of qualifiers.|  
|0xC001400D|-1073659891|DTS_E_CANNOTCLONECONNECTIONMANAGER|Connection manager "0x%1" cannot be cloned for out-of-process execution.|  
|0xC001400E|-1073659890|DTS_E_NOSQLPROFILERDLL|The log provider for SQL Server Profiler was unable to load pfclnt.dll. Please check that SQL Server Profiler is installed.|  
|0xC001400F|-1073659889|DTS_E_LOGFAILED|The SSIS logging infrastructure failed with error code 0x%1!8.8X!. This error indicates that this logging error is not attributable to a specific log provider.|  
|0xC0014010|-1073659888|DTS_E_LOGPROVIDERFAILED|The SSIS logging provider "%1" failed with error code 0x%2!8.8X! (%3).  This indicates a logging error attributable to the specified log provider.|  
|0xC0014011|-1073659887|DTS_E_SAVETOSQLSERVER_OLEDB|The SaveToSQLServer method has encountered OLE DB error code 0x%1!8.8X! (%2).  The SQL statement that was issued has failed.|  
|0xC0014012|-1073659886|DTS_E_LOADFROMSQLSERVER_OLEDB|The LoadFromSQLServer method has encountered OLE DB error code 0x%1!8.8X! (%2).  The SQL statement that was issued has failed.|  
|0xC0014013|-1073659885|DTS_E_REMOVEFROMSQLSERVER_OLEDB|The RemoveFromSQLServer method encountered OLE DB error code 0x%1!8.8X! (%2) The SQL statement that was issued has failed.|  
|0xC0014014|-1073659884|DTS_E_EXISTSONSQLSERVER_OLEDB|The ExistsOnSQLServer method has encountered OLE DB error code 0x%1!8.8X! (%2). The SQL statement issued has failed.|  
|0xC0014015|-1073659883|DTS_E_CONNECTIONSTRING|OLE DB has failed making a database connection when using the supplied connection string.|  
|0xC0014016|-1073659882|DTS_E_FROMEXECISNOTCHILD|When adding a precedence constraint, a From executable was specified that is not a child of this container.|  
|0xC0014017|-1073659881|DTS_E_TOEXECISNOTCHILD|When adding a precedence constraint, the To executable specified is not a child of this container.|  
|0xC0014018|-1073659880|DTS_E_ODBCTRANSACTIONENLIST|There was an error trying enlist an ODBC connection in a transaction. The SQLSetConnectAttr failed to set the SQL_ATTR_ENLIST_IN_DTC attribute.|  
|0xC0014019|-1073659879|DTS_E_CONNECTIONOFFLINE|The connection manager "%1" will not acquire a connection because the package OfflineMode property is TRUE. When the OfflineMode is TRUE, connections cannot be acquired.|  
|0xC001401A|-1073659878|DTS_E_BEGINTRANSACTION|The SSIS Runtime has failed to start the distributed transaction due to error 0x%1!8.8X! "%2". The DTC transaction failed to start. This could occur because the MSDTC Service is not running.|  
|0xC001401B|-1073659877|DTS_E_SETQUALIFIERDESIGNTIMEONLY|The SetQualifier method cannot be called on a connection manager during package execution. This method is used at design-time only.|  
|0xC001401C|-1073659876|DTS_E_SQLPERSISTENCEVERSION|Storing or modifying packages in SQL Server requires the SSIS runtime and database to be the same version. Storing packages in earlier versions is not supported.|  
|0xC001401D|-1073659875|DTS_E_CONNECTIONVALIDATIONFAILED|Connection "%1" failed validation.|  
|0xC001401E|-1073659874|DTS_E_INVALIDFILENAMEINCONNECTION|The file name "%1" specified in the connection was not valid.|  
|0xC001401F|-1073659873|DTS_E_MULTIPLEFILESONRETAINEDCONNECTION|Multiple file names cannot be specified on a connection when the Retain property is TRUE. Vertical bars were found on the connection string, meaning multiple file names are being specified and, in addition, the Retain property is TRUE.|  
|0xC0014020|-1073659872|DTS_E_ODBCERROR|An ODBC error %1!d! has occurred.|  
|0xC0014021|-1073659871|DTS_E_PRECEDENCECONSTRAINT|There was an error in the precedence constraint between "%1" and "%2".|  
|0xC0014022|-1073659870|DTS_E_FAILEDPOPNATIVEFEE|Failed to populate the ForEachEnumeratorInfos collection with native ForEachEnumerators with the following error code: %1.|  
|0xC0014023|-1073659869|DTS_E_GETENUMERATOR|The GetEnumerator method of the ForEach Enumerator has failed with error 0x%1!8.8X! "%2". This occurs when the ForEach Enumerator cannot enumerate.|  
|0xC0014024|-1073659868|DTS_E_CANTGETCERTDATA|The raw certificate data cannot be obtained from the supplied certificate object (error: %1). This occurs when CPackage::put_CertificateObject cannot instantiate the ManagedHelper object, when the ManagedHelper object fails, or when the ManagedHelper object returns a malformed array.|  
|0xC0014025|-1073659867|DTS_E_CANTCREATECERTCONTEXT|Failed to create certificate context (error: %1). This occurs in CPackage::put_CertificateObject or CPackage::LoadFromXML when the corresponding CryptoAPI function fails.|  
|0xC0014026|-1073659866|DTS_E_CANTOPENCERTSTORE|Opening MY certificate store failed with error "%1".This occurs in CPackage::LoadUserCertificateByName and CPackage::LoadUserCertificateByHash.|  
|0xC0014027|-1073659865|DTS_E_CANTFINDCERTBYNAME|The certificate specified by name in MY store cannot be found (error: %1). This occurs in CPackage::LoadUserCertificateByName.|  
|0xC0014028|-1073659864|DTS_E_CANTFINDCERTBYHASH|Unable to find the specified certificate by hash in "MY" store (error: %1). Occurs in CPackage::LoadUserCertificateByHash.|  
|0xC0014029|-1073659863|DTS_E_INVALIDCERTHASHFORMAT|The hash value is not a one-dimensional array of bytes (error: %1). This occurs in CPackage::LoadUserCertificateByHash.|  
|0xC001402A|-1073659862|DTS_E_CANTACCESSARRAYDATA|The data in the array cannot be accessed (error: %1). This error can occur wherever GetDataFromSafeArray is called.|  
|0xC001402B|-1073659861|DTS_E_CREATEMANAGEDHELPERFAILED|The SSIS managed helper object failed during creation with error 0x%1!8.8X! "%2". This occurs whenever CoCreateInstance CLSID_DTSManagedHelper fails.|  
|0xC001402C|-1073659860|DTS_E_OLEDBTRANSACTIONENLIST|The SSIS Runtime has failed to enlist the OLE DB connection in a distributed transaction with error 0x%1!8.8X! "%2".|  
|0xC001402D|-1073659859|DTS_E_SIGNPACKAGEFAILED|Package signing failed with error 0x%1!8.8X! "%2". This occurs when the ManagedHelper.SignDocument method fails.|  
|0xC001402E|-1073659858|DTS_E_CHECKENVELOPEFAILED|Failed to check for XML signature envelope in package XML with error 0x%1!8.8X! "%2". This occurs in CPackage::LoadFromXML.|  
|0xC001402F|-1073659857|DTS_E_GETXMLSOURCEFAILED|Failed to obtain XML source from XML DOM object with error 0x%1!8.8X! "%2". This occurs when IXMLDOMDocument::get_xml fails.|  
|0xC0014030|-1073659856|DTS_E_PACKAGEVERIFICATIONFAILED|The cryptographic signature of the package failed verification due to error 0x%1!8.8X! "%2". This occurs when the signature verification operation fails.|  
|0xC0014031|-1073659855|DTS_E_GETKEYFROMCERTFAILED|Failed to obtain cryptographic key pair associated with the specified certificate with error 0x%1!8.8X! "%2". Verify that you have the key pair for which the certificate was issued. This error usually occurs when trying to sign a document using a certificate for which the person does not have the private key.|  
|0xC0014032|-1073659854|DTS_E_INVALIDSIGNATURE|The digital signature is not valid. The contents of the package have been modified.|  
|0xC0014033|-1073659853|DTS_E_UNTRUSTEDSIGNATURE|The digital signature is valid; however the signer is not trusted and, therefore, authenticity cannot be guaranteed.|  
|0xC0014034|-1073659852|DTS_E_TRANSACTIONENLISTNOTSUPPORTED|The connection does not support enlisting in distributed transaction.|  
|0xC0014035|-1073659851|DTS_E_PACKAGEPROTECT|Failed to apply package protection with error 0x%1!8.8X! "%2". This error occurs when saving to Xml.|  
|0xC0014036|-1073659850|DTS_E_PACKAGEUNPROTECT|Failed to remove package protection with error 0x%1!8.8X! "%2". This occurs in the CPackage::LoadFromXML method.|  
|0xC0014037|-1073659849|DTS_E_PACKAGEPASSWORD|The package is encrypted with a password. The password was not specified, or is not correct.|  
|0xC0014038|-1073659848|DTS_E_DUPLICATECONSTRAINT|A precedence constraint already exists between the specified executables. More than one precedence constraint is not allowed.|  
|0xC0014039|-1073659847|DTS_E_PACKAGELOADFAILED|The package failed to load due to error 0x%1!8.8X! "%2". This occurs when CPackage::LoadFromXML fails.|  
|0xC001403A|-1073659846|DTS_E_PACKAGEOBJECTNOTENVELOPED|Failed to find package object in signed XML envelope with error 0x%1!8.8X! "%2". This occurs when signed XML does not contain a SSIS package, as expected.|  
|0xC001403B|-1073659845|DTS_E_JAGGEDEVENTINFO|The lengths of parameter names, types, and descriptions arrays are not equal. The lengths must be equal. This occurs when the lengths of the arrays are mismatched. There should be one entry per parameter in each array.|  
|0xC001403C|-1073659844|DTS_E_GETPACKAGEINFOS|An OLE DB error 0x%1!8.8X! (%2) occurred while enumerating packages. A SQL statement was issued and failed.|  
|0xC001403D|-1073659843|DTS_E_UNKNOWNLOGPROVIDERTYPE|The log provider type "%1" specified for log provider "%2" is not recognized as a valid log provider type. This error occurs when an attempt is made to create a log provider for unknown log provider type. Verify the spelling in the log provider type name.|  
|0xC001403E|-1073659842|DTS_E_UNKNOWNLOGPROVIDERTYPENOSUBS|The log provider type is not recognized as a valid log provider type. This error occurs when an attempt is made to create a log provider for unknown log provider type. Verify the spelling in the log provider type name.|  
|0xC001403F|-1073659841|DTS_E_UNKNOWNCONNECTIONMANAGERTYPENOSUBS|The connection type specified for connection manager is not a valid connection manager type. This error occurs when an attempt is made to create a connection manager for unknown connection type. Verify the spelling of the connection type name.|  
|0xC0014040|-1073659840|DTS_E_PACKAGEREMOVEFAILED|An error was encountered when trying to remove the package "%1" from SQL Server.|  
|0xC0014042|-1073659838|DTS_E_FOLDERADDFAILED|An error was encountered when trying to create a folder on SQL Server named "%1" in folder "%2".|  
|0xC0014043|-1073659837|DTS_E_CREATEFOLDERONSQLSERVER_OLEDB|The CreateFolderOnSQLServer method has encountered OLE DB error code 0x%1!8.8X! (%2) The SQL statement issued has failed.|  
|0xC0014044|-1073659836|DTS_E_FOLDERRENAMEFAILED|An error occurred when renaming folder " %1\\\\%2" to "%1\\\\%3" on SQL Server.|  
|0xC0014045|-1073659835|DTS_E_RENAMEFOLDERONSQLSERVER_OLEDB|RenameFolderOnSQLServer 方法遇到了 OLE DB 错误代码 0x%1!8.8X! (%2)。 发出的 SQL 语句已失败。|  
|0xC0014046|-1073659834|DTS_E_FOLDERDELETEFAILED|删除 SQL Server 文件夹“%1”时出错。|  
|0xC0014047|-1073659833|DTS_E_REMOVEFOLDERFROMSQLSERVER_OLEDB|RemoveFolderOnSQLServer 方法遇到了 OLE DB 错误代码 0x%1!8.8X! (%2)。 发出的 SQL 语句已失败。|  
|0xC0014048|-1073659832|DTS_E_INVALIDPATHTOPACKAGE|指定的包路径不包含包名称。 如果路径未包含至少一个反斜杠或正斜杠，会出现这种情况。|  
|0xC0014049|-1073659831|DTS_E_FOLDERNOTFOUND|找不到文件夹“%1”。|  
|0xC001404A|-1073659830|DTS_E_FINDFOLDERONSQLSERVER_OLEDB|尝试在 SQL 上查找某个文件夹时遇到 OLE DB 错误，错误代码为 0x%1!8.8X! (%2)。|  
|0xC001404B|-1073659829|DTS_E_OPENLOGFAILED|SSIS 日志记录提供程序无法打开该日志。 错误代码:0x%1!8.8X!。|  
|0xC001404C|-1073659828|DTS_E_GETCONNECTIONINFOS|无法获取 ConnectionInfos 集合，错误为 0x%1!8.8X! “%2”。 当对 IDTSApplication100::get_ConnectionInfos 的调用失败时，会出现此错误。|  
|0xC001404D|-1073659827|DTS_E_VARIABLEDEADLOCK|试图锁定变量时检测到死锁。 尝试了 16 次后仍无法获取锁。 锁已超时。|  
|0xC001404E|-1073659826|DTS_E_NOTDISPENSED|尚未从 VariableDispenser 返回 Variables 集合。 试图执行只允许对分配的集合执行的操作。|  
|0xC001404F|-1073659825|DTS_E_VARIABLESALREADYUNLOCKED|Variables 集合已经解锁。 对分配的 Variables 集合只能调用一次 Unlock 方法。|  
|0xC0014050|-1073659824|DTS_E_VARIABLEUNLOCKFAILED|一个或多个变量无法解锁。|  
|0xC0014051|-1073659823|DTS_E_DISPENSEDREADONLY|Variables 集合已从 VariableDispenser 返回，并且无法修改。 无法向分配的集合添加项，也无法从中删除项。|  
|0xC0014052|-1073659822|DTS_E_VARIABLEALREADYONREADLIST|变量“%1”已在读取列表中。 一个变量只能向读取锁定列表或写入锁定列表中添加一次。|  
|0xC0014053|-1073659821|DTS_E_VARIABLEALREADYONWRITELIST|变量“%1”已在写入列表中。 一个变量只能向读取锁定列表或写入锁定列表中添加一次。|  
|0xC0014054|-1073659820|DTS_E_LOCKVARIABLEFORREAD|无法锁定变量“%1”进行读访问，错误为 0x%2!8.8X! “%3”。|  
|0xC0014055|-1073659819|DTS_E_LOCKVARIABLEFORWRITE|无法锁定变量“%1”进行读/写访问，错误为 0x%2!8.8X! “%3”。|  
|0xC0014056|-1073659818|DTS_E_CUSTOMEVENTCONFLICT|已用另一个参数列表声明了自定义事件“%1”。 某个任务试图声明自定义事件，但其他任务已用另一个参数列表声明了该事件。|  
|0xC0014057|-1073659817|DTS_E_EVENTHANDLERNOTALLOWED|提供自定义事件“%1”的任务不允许在包内处理此事件。 声明该自定义事件时，将 AllowEventHandlers 设置成了 FALSE。|  
|0xC0014059|-1073659815|DTS_E_UNSAFEVARIABLESALREADYSET|VariableDispenser 接收到不安全的 Variables 集合。 无法重复此操作。|  
|0xC001405A|-1073659814|DTS_E_INVALIDPARENTPACKAGEPATH|对 ForEachEnumerator 调用了 GetPackagePath，但未指定 ForEachLoop 包路径。|  
|0xC001405B|-1073659813|DTS_E_VARIABLEDEADLOCK_READ|试图锁定变量“%1”进行读访问时检测到死锁。 尝试了 16 次后仍无法获取锁，已超时。|  
|0xC001405C|-1073659812|DTS_E_VARIABLEDEADLOCK_READWRITE|试图锁定变量“%1”进行读/写访问时检测到死锁。 尝试了 16 次后仍无法获取锁。 锁已超时。|  
|0xC001405D|-1073659811|DTS_E_VARIABLEDEADLOCK_BOTH|试图锁定变量“%1”进行读访问和变量“%2”进行读/写访问时检测到死锁。 尝试了 16 次后仍无法获取锁。 锁已超时。|  
|0xC001405E|-1073659810|DTS_E_PACKAGEPASSWORDEMPTY|包的保护级别要求使用密码，但 PackagePassword 属性为空。|  
|0xC001405F|-1073659809|DTS_E_DECRYPTXML_PASSWORD|由于未指定密码或密码不正确，无法解密已加密的 XML 节点。 包加载将尝试忽略加密信息，继续执行。|  
|0xC0014060|-1073659808|DTS_E_DECRYPTPACKAGE_USERKEY|无法解密使用用户密钥加密的包。 可能您不是加密此包的用户，或者您现在使用的计算机不是保存该包时使用的计算机。|  
|0xC0014061|-1073659807|DTS_E_SERVERSTORAGEDISALLOWED|保存到此目标时无法使用保护级别 ServerStorage。 系统无法确保该目标支持安全存储功能。|  
|0xC0014062|-1073659806|DTS_E_LOADFROMSQLSERVER|LoadFromSQLServer 方法失败。|  
|0xC0014063|-1073659805|DTS_E_SIGNATUREPOLICYVIOLATION|该包无法加载，其数字签名状态违反了签名策略。 将包文件“%3”加载到 XML 文档时 "%2"|  
|0xC0014064|-1073659804|DTS_E_SIGNATURENOTPRESENT|该包未签名。|  
|0xC0014065|-1073659803|DTS_E_SQLPROFILERDLL_ONLY_X86|因为只有 32 位系统支持 pfclnt.dll，所以 SQL Server Profiler 的日志提供程序无法加载 pfclnt.dll。|  
|0xC0014100|-1073659648|DTS_E_NAMEALREADYADDED|无法添加该对象，因为集合中已存在另一个同名的对象。 使用其他名称，可更正此错误。|  
|0xC0014101|-1073659647|DTS_E_NAMEALREADYEXISTS|无法将对象名从“%1”更改为“%2”，因为集合中已存在一个同名的对象。 使用其他名称，可更正此错误。|  
|0xC0014103|-1073659645|DTS_E_FAILEDDEPENDENCIES|枚举包的依赖项时出错。 有关详细信息，请查看其他消息。|  
|0xC0014104|-1073659644|DTS_E_INVALIDCHECKPOINT_TRANSACTION|不支持当前的包设置。  请更改 SaveCheckpoints 属性或 TransactionOption 属性。|  
|0xC001410E|-1073659634|DTS_E_CONNECTIONMANAGERJOINTRANSACTION|连接管理器无法脱离事务。|  
|0xC0015001|-1073655807|DTS_E_BPDUPLICATE|指定的断点 ID 已存在。 当任务多次使用同一 ID 调用 CreateBreakpoint 时，会出现此错误。 只有当任务在创建第二个断点之前对创建第一个断点调用了 RemoveBreakpoint 时，才能使用同一 ID 多次创建断点。|  
|0xC0015002|-1073655806|DTS_E_BPUNKNOWNID|指定的断点 ID 不存在。 当任务引用了不存在的断点时，会出现此错误。|  
|0xC0015004|-1073655804|DTS_E_CANTWRITETOFILE|无法打开文件“%1”进行写操作。 该文件可能是只读的，或者您没有适当的权限。|  
|0xC0015005|-1073655803|DTS_E_NOROWSETRETURNED|没有与执行此查询相关联的结果行集。 未正确指定结果。|  
|0xC0015105|-1073655547|DTS_E_DUMP_FAILED|没有正确生成调试转储文件。 hresult 为 0x%1!8.8X!。|  
|0xC0016001|-1073651711|DTS_E_INVALIDURL|指定的 URL 无效。 如果服务器或代理 URL 为空或格式不正确，会发生这种情况。 有效的 URL 格式的形式为 https://ServerName:Port/ResourcePath 或 https://ServerName:Port/ResourcePath 。|  
|0xC0016002|-1073651710|DTS_E_INVALIDSCHEME|URL %1 无效。 如果指定了 http 和 https 之外的其他方案，或者该 URL 的格式不正确，会发生这种情况。 有效的 URL 格式的形式为 https://ServerName:Port/ResourcePath 或 https://ServerName:Port/ResourcePath 。|  
|0xC0016003|-1073651709|DTS_E_WINHTTPCANNOTCONNECT|无法建立与服务器 %1 的连接。 如果该服务器不存在，或代理设置不正确，会出现此错误。|  
|0xC0016004|-1073651708|DTS_E_CONNECTIONTERMINATED|与服务器的连接已重置或终止。 请稍后再试。|  
|0xC0016005|-1073651707|DTS_E_LOGINFAILURE|对“%1”的登录尝试失败。 如果提供的登录凭据不正确，会出现此错误。 请验证登录凭据。|  
|0xC0016006|-1073651706|DTS_E_INVALIDSERVERNAME|无法解析 URL %1 中指定的服务器名称。|  
|0xC0016007|-1073651705|DTS_E_PROXYAUTH|代理身份验证失败。 如果未提供登录凭据，或凭据不正确，会出现此错误。|  
|0xC0016008|-1073651704|DTS_E_SECUREFAILURE|从服务器获取的 SSL 证书响应无效。 无法处理请求。|  
|0xC0016009|-1073651703|DTS_E_TIMEOUT|请求已超时。如果指定的超时值过小，或者无法建立与服务器或代理的连接，会出现此错误。 请确保服务器和代理 URL 是正确的。|  
|0xC001600A|-1073651702|DTS_E_CLIENTAUTH|缺少客户端证书。 如果服务器需要 SSL 客户端证书，但用户提供的证书无效或根本未提供证书，会出现此错误。 必须为此连接配置客户端证书。|  
|0xC001600B|-1073651701|DTS_E_REDIRECTFAILURE|指定的服务器(URL 为 %1)包含重定向，但重定向请求失败。|  
|0xC001600C|-1073651700|DTS_E_SERVERAUTH|服务器身份验证失败。 如果未提供登录凭据，或凭据不正确，会出现此错误。|  
|0xC001600D|-1073651699|DTS_E_WINHTTPUNKNOWNERROR|无法处理请求。 请稍后再试。|  
|0xC001600E|-1073651698|DTS_E_UNKNOWNSTATUSCODE|服务器返回状态代码 - %1!u! : %2。 当服务器遇到问题时会出现此错误。|  
|0xC001600F|-1073651697|DTS_E_WINHTTPNOTSUPPORTED|WinHttp 服务不支持此平台。|  
|0xC0016010|-1073651696|DTS_E_INVALIDTIMEOUT|超时值无效。 超时值应介于 %1!d! 到 %2!d! （秒）之间。|  
|0xC0016011|-1073651695|DTS_E_INVALIDCHUNKSIZE|块区大小无效。 ChunkSize 属性应介于 %1!d! 到 %2!d! (KB)之间。|  
|0xC0016012|-1073651694|DTS_E_CERTERROR|处理客户端证书时出错。 如果在个人证书存储区中找不到提供的客户端证书，会出现此错误。 请确保该客户端证书有效。|  
|0xC0016013|-1073651693|DTS_E_FORBIDDEN|服务器返回错误代码“403 - 禁止访问”。 如果指定资源需要使用 "https" 访问，但证书的有效期已过，或者证书对请求的使用无效，或者证书已撤销或无法检查是否已撤销，会出现此错误。|  
|0xC0016014|-1073651692|DTS_E_WINHTTPOPEN|初始化代理为“%1”的 HTTP 会话时出错。 当指定了无效的代理时会出现此错误。 HTTP 连接管理器仅支持 CERN 类型的代理。|  
|0xC0016015|-1073651691|DTS_E_OPENCERTSTORE|打开证书存储区时出错。|  
|0xC0016016|-1073651690|DTS_E_UNPROTECTXMLFAILED|无法解密受保护的 XML 节点“%1”，错误为 0x%2!8.8X! “%3”。 可能您无权访问此信息。 当发生加密错误时会出现此错误。 请确保提供正确的密钥。|  
|0xC0016017|-1073651689|DTS_E_UNPROTECTCONNECTIONSTRINGFAILED|无法解密服务器“%1”的受保护连接字符串，错误为 0x%2!8.8X! “%3”。 可能您无权访问此信息。 当发生加密错误时会出现此错误。 请确保提供正确的密钥。|  
|0xC0016018|-1073651688|DTS_E_NEGATIVEVERSION|版本号不能为负。 如果包的 VersionMajor、VersionMinor 或 VersionBuild 属性设置为负值，会出现此错误。|  
|0xC0016019|-1073651687|DTS_E_PACKAGEMIGRATED|在加载期间已将包迁移到较高版本。 要完成该进程，必须重新加载包。 这是内部错误代码。|  
|0xC0016020|-1073651680|DTS_E_PACKAGEMIGRATIONFAILED|包从版本 %1!d! 到版本 %2!d! 的迁移失败，错误为 0x%3!8.8X! “%4”。|  
|0xC0016021|-1073651679|DTS_E_PACKAGEMIGRATIONMODULELOAD|包迁移模块无法加载。|  
|0xC0016022|-1073651678|DTS_E_PACKAGEMIGRATIONMODULE|包迁移模块失败。|  
|0xC0016023|-1073651677|DTS_E_CANTDETERMINEWHICHPROPTOPERSIST|无法使用默认的持久性对对象进行持久化。 如果默认的持久性无法确定哪些对象属于宿主对象，会出现此错误。|  
|0xC0016024|-1073651676|DTS_E_CANTADDREMOVEWHENEXECUTING|在运行时模式下无法向包中添加元素或从包中删除元素。 如果在包执行时试图向集合添加对象或从中删除对象，会出现此错误。|  
|0xC0016025|-1073651675|DTS_E_NODENOTFOUND|在自定义默认持久性中找不到节点“%1”。 如果可扩展对象的默认保存的 XML 更改后无法再找到保存的对象，或者可扩展对象本身发生了更改，会出现此错误。|  
|0xC0016026|-1073651674|DTS_E_COLLECTIONLOCKED|在包验证或执行期间无法修改此集合。|  
|0xC0016027|-1073651673|DTS_E_COLLOCKED|在包验证或执行期间无法修改“%1”集合。 无法将“%2”添加到该集合。|  
|0xC0016029|-1073651671|DTS_E_FTPNOTCONNECTED|未建立与 FTP 服务器的连接。|  
|0xC001602A|-1073651670|DTS_E_FTPERROR|请求的 FTP 操作中出错。 详细的错误说明: %1。|  
|0xC001602B|-1073651669|DTS_E_FTPINVALIDRETRIES|重试次数无效。 重试次数应介于 %1!d! 和 %2!d! 之间。|  
|0xC001602C|-1073651668|DTS_E_LOADWININET|FTP 连接管理器需要以下 DLL 才能发挥作用: %1。|  
|0xC001602D|-1073651667|DTS_E_FTPINVALIDCONNECTIONSTRING|连接字符串中指定的端口无效。 ConnectionString 的格式为 ServerName:Port。 其中的 Port 应为介于 %1!d! 和 %2!d! 之间。|  
|0xC001602E|-1073651666|DTS_E_FTPCREATEFOLDER|正在创建文件夹“%1”... %2。|  
|0xC001602F|-1073651665|DTS_E_FTPDELETEFOLDER|正在删除文件夹“%1”... %2。|  
|0xC0016030|-1073651664|DTS_E_FTPCHANGEFOLDER|正在将当前目录更改为“%1”。 %2。|  
|0xC0016031|-1073651663|DTS_E_FTPFILESEMPTY|没有要传输的文件。 如果在执行 Send 或 Receive 操作时未指定要传输的文件，会出现此错误。|  
|0xC0016032|-1073651662|DTS_E_FTPINVALIDLOCALPATH|指定的本地路径无效。 请指定有效的本地路径。 指定的本地路径为空时会出现这种情况。|  
|0xC0016033|-1073651661|DTS_E_FTPNOFILESTODELETE|未指定要删除的文件。|  
|0xC0016034|-1073651660|DTS_E_WINHTTPCERTDECODE|加载证书时出现内部错误。 当证书数据无效时会出现此错误。|  
|0xC0016035|-1073651659|DTS_E_WINHTTPCERTENCODE|保存证书数据时出现内部错误。|  
|0xC0016049|-1073651639|DTS_E_CHECKPOINTMISMATCH|检查点文件“%1”与此包不匹配。 包 ID 和检查点文件中的 ID 不匹配。|  
|0xC001604A|-1073651638|DTS_E_CHECKPOINTFILEALREADYEXISTS|发现现有检查点文件中包含似乎并非用于此包的内容，因此无法覆盖该文件以开始保存新的检查点。 请删除该现有检查点文件，然后重试。 如果存在检查点文件，而包被设置为不使用检查点文件但保存检查点，则会出现此错误。 将不会覆盖该现有检查点文件。|  
|0xC001604B|-1073651637|DTS_E_CHECKPOINTFILELOCKED|检查点文件“%1”已由其他进程锁定。 如果此包的另一个实例当前正在执行，会出现这种情况。|  
|0xC001604C|-1073651636|DTS_E_OPENCHECKPOINTFILE|由于错误 0x%2!8.8X!，无法打开检查点文件“%1” “%3”。|  
|0xC001604D|-1073651635|DTS_E_CREATECHECKPOINTFILE|创建检查点文件“%1”失败，错误原因为 0x%2!8.8X! “%3”。|  
|0xC0016050|-1073651632|DTS_E_FTPINVALIDPORT|FTP Port 包含无效值。 FTP Port 值应为介于 %1!d! 和 %2!d! 之间。|  
|0xC00160AA|-1073651542|DTS_E_CONNECTTOSERVERFAILED|与计算机“%1”上的 SSIS 服务连接失败:<br /><br /> %2。|  
|0xC0017002|-1073647614|DTS_E_PROPERTYEXPRESSIONSDISABLEDONVARIABLES|Variable 对象不支持 Expression 属性。 请改用 EvaluateAsExpression 属性。|  
|0xC0017003|-1073647613|DTS_E_PROPERTYEXPRESSIONEVAL|无法计算属性“%2”的表达式“%1”。 请修改该表达式，使其有效。|  
|0xC0017004|-1073647612|DTS_E_PROPERTYEXPRESSIONSET|无法将属性“%2”的表达式“%1”的结果写入该属性。 已计算该表达式，但无法对该属性进行设置。|  
|0xC0017005|-1073647611|DTS_E_FORLOOPEVALEXPRESSIONINVALID|循环的求值表达式无效。 需要修改该表达式。 应该还有其他错误消息。|  
|0xC0017006|-1073647610|DTS_E_EXPRESSIONNOTBOOLEAN|表达式“%1”的结果必须为 True 或 False。 请更改该表达式，使其结果为布尔值。|  
|0xC0017007|-1073647609|DTS_E_FORLOOPHASNOEXPRESSION|循环没有要计算的表达式。 当 For 循环的表达式为空时会出现此错误。 请添加一个表达式。|  
|0xC0017008|-1073647608|DTS_E_FORLOOPASSIGNEXPRESSIONINVALID|循环的赋值表达式无效，需要修改。 应该还有其他错误消息。|  
|0xC0017009|-1073647607|DTS_E_FORLOOPINITEXPRESSIONINVALID|循环的初始化表达式无效，需要修改。 应该还有其他错误消息。|  
|0xC001700A|-1073647606|DTS_E_INVALIDVERSIONNUMBER|包中的版本号无效。 该版本号不能大于当前的版本号。|  
|0xC001700C|-1073647604|DTS_E_INVALIDVERNUMCANTBENEGATIVE|包中的版本号无效。 该版本号为负。|  
|0xC001700D|-1073647603|DTS_E_PACKAGEUPDATEDISABLED|该包的格式属于较低的版本，但现在禁用了包格式自动升级功能。|  
|0xC001700E|-1073647602|DTS_E_EXPREVALTRUNCATIONASERROR|在对表达式求值期间发生了截断。|  
|0xC0019001|-1073639423|DTS_E_FAILEDSETEXECVALVARIABLE|包装无法设置 ExecutionValueVariable 属性中指定的变量的值。|  
|0xC0019004|-1073639420|DTS_E_VARIABLEEXPRESSIONERROR|无法对变量“%1”的表达式求值。 该表达式中存在错误。|  
|0xC0019305|-1073638651|DTS_E_UNSUPPORTEDSQLVERSION|此数据库版本不支持所尝试的操作。|  
|0xC001A003|-1073635325|DTS_E_TXNSPECINVALID|使用保留连接时不能指定事务。 如果连接管理器的 Retain 设置为 TRUE，但调用 AcquireConnection 时使用了非空的事务参数，会出现此错误。|  
|0xC001A004|-1073635324|DTS_E_INCOMPATIBLETRANSACTIONCONTEXT|为保留连接指定了不兼容的事务上下文。 已在其他事务上下文中建立了此连接。 只能在一个事务上下文中使用保留连接。|  
|0xC001B001|-1073631231|DTS_E_NOTSUSPENDED|由于包并未挂起，Resume 调用失败。 如果客户端调用恢复操作，但包并未挂起，会出现这种情况。|  
|0xC001B002|-1073631230|DTS_E_ALREADYEXECUTING|由于可执行文件已经在执行，Execute 调用失败。 如果客户端对容器调用 Execute，但该容器仍处于上次调用 Execute 后的执行期间，会出现此错误。|  
|0xC001B003|-1073631229|DTS_E_NOTEXECUTING|由于该可执行文件不在执行或不是顶级可执行文件，Suspend 或 Resume 调用失败。 如果客户端对可执行文件调用 Suspend 或 Resume，但该可执行文件当前不在处理 Execute 调用，会出现这种情况。|  
|0xC001C002|-1073627134|DTS_E_INVALIDFILE|For Each 文件枚举器中指定的文件无效。 请确保 For Each 文件枚举器中指定的文件存在。|  
|0xC001C010|-1073627120|DTS_E_VALUEINDEXNOTINTEGER|值索引不是整数。 将 For Each Variable 编号 %1!d! 映射到变量“%2”。|  
|0xC001C011|-1073627119|DTS_E_VALUEINDEXNEGATIVE|值索引为负。 将 ForEach Variable 编号 %1!d! 映射到变量“%2”。|  
|0xC001C012|-1073627118|DTS_E_FOREACHVARIABLEMAPPING|无法应用 ForEach Variable 编号 %1!d! 到变量“%2”的映射。|  
|0xC001C013|-1073627117|DTS_E_OBJECTNOTINFOREACHLOOP|将对象添加到 ForEachPropertyMapping 时出错，后者不是 ForEachLoop 容器的直接子级。|  
|0xC001F001|-1073614847|DTS_E_FAILEDSYSTEMVARIABLEREMOVE|无法删除系统变量。 删除必需变量时会出现此错误。  必需变量是由运行库创建的变量，用于在任务和运行库之间进行通信。|  
|0xC001F002|-1073614846|DTS_E_CHANGESYSTEMVARIABLEREADONLYFAILED|更改变量属性失败，因为该变量为系统变量。 系统变量是只读的。|  
|0xC001F003|-1073614845|DTS_E_CHANGESYSTEMVARIABLENAMEFAILED|更改变量名称失败，因为该变量为系统变量。 系统变量是只读的。|  
|0xC001F004|-1073614844|DTS_E_CHANGESYSTEMVARIABLENAMESPACEFAILED|更改变量的命名空间失败，因为该变量为系统变量。 系统变量是只读的。|  
|0xC001F006|-1073614842|DTS_E_EVENTHANDLERNAMEREADONLY|更改事件处理程序名称失败。 事件处理程序名称是只读的。|  
|0xC001F008|-1073614840|DTS_E_PATHUNKNOWN|无法检索对象的路径。 这是系统错误。|  
|0xC001F009|-1073614839|DTS_E_RUNTIMEVARIABLETYPECHANGE|赋给变量“%1”的值类型不同于当前变量的类型。 在执行期间变量不能更改类型。 变量类型非常严格，类型为 Object 的变量除外。|  
|0xC001F010|-1073614832|DTS_E_INVALIDSTRING|字符串“%1”中存在无效字符。 如果为属性值提供的字符串包含不可打印的字符，会出现这种情况。|  
|0xC001F011|-1073614831|DTS_E_INVALIDOBJECTNAME|SSIS 对象名无效。 可能已产生了详细说明该命名问题的更具体的错误。|  
|0xC001F021|-1073614815|DTS_E_PROPERTYREADONLY|属性“%1”是只读的。 试图更改只读属性时会出现这种情况。|  
|0xC001F022|-1073614814|DTS_E_FAILEDGETTYPEINFO|该对象不支持类型信息。 如果运行库尝试从对象获取类型信息来填充 Properties 集合，会出现这种情况。  该对象必须支持类型信息。|  
|0xC001F023|-1073614813|DTS_E_FAILEDPROPERTYGET|检索属性“%1”的值时出错。 错误代码为 0x%2!8.8X!。|  
|0xC001F024|-1073614812|DTS_E_FAILEDPROPERTYGET_ERRORINFO|检索属性“%1”的值时出错。 错误代码为 0x%2!8.8X! “%3”。|  
|0xC001F025|-1073614811|DTS_E_FAILEDPROPERTYSET|设置属性“%1”的值时出错。 返回的错误为 0x%2!8.8X!。|  
|0xC001F026|-1073614810|DTS_E_FAILEDPROPERTYSET_ERRORINFO|设置属性“%1”的值时出错。 返回的错误为 0x%2!8.8X! “%3”。|  
|0xC001F027|-1073614809|DTS_E_PROPERTYWRITEONLY|属性“%1”是只写的。 如果试图通过属性对象检索属性的值，但该属性是只写的，会出现此错误。|  
|0xC001F028|-1073614808|DTS_E_NODISPATCH|该对象没有实现 IDispatch。 如果属性对象或属性集合试图访问对象的 IDispatch 接口，会出现此错误。|  
|0xC001F029|-1073614807|DTS_E_NOCONTAININGTYPELIB|无法检索该对象的类型库。 如果 Properties 集合试图通过某对象的 IDispatch 接口来检索其类型库，会出现此错误。|  
|0xC001F02A|-1073614806|DTS_E_INVALIDTASKMONIKER|由于错误 0x%3!8.8X!“%4!s!”，无法从类型为“%2!s!”的任务“%1!s!”的 XML 创建 任务对象。|  
|0xC001F02C|-1073614804|DTS_E_FAILEDCREATEXMLDOCUMENT|无法创建 XML 文档“%1”。|  
|0xC001F02D|-1073614803|DTS_E_PMVARPROPTYPESDIFFERENT|由于将类型不同的变量和属性进行了属性映射，导致出现错误。 属性类型必须与变量类型相匹配。|  
|0xC001F02E|-1073614802|DTS_E_PMINVALIDPROPMAPTARGET|试图将属性映射设置为不支持的目标对象类型。 将不支持的对象类型传递给属性映射时会出现此错误。|  
|0xC001F02F|-1073614801|DTS_E_COULDNOTRESOLVEPACKAGEPATH|无法解析包“%1”中某个对象的包路径。  请确保该包路径有效。|  
|0xC001F030|-1073614800|DTS_E_PMNODESTPROPERTY|属性映射的目标属性为空。 请设置目标属性名称。|  
|0xC001F031|-1073614799|DTS_E_INVALIDPROPERTYMAPPINGSFOUND|包无法还原至少一个属性映射。|  
|0xC001F032|-1073614798|DTS_E_AMBIGUOUSVARIABLENAME|变量名不明确，因为不同的命名空间中存在多个同名的变量。 请指定限定命名空间的名称，以避免产生混乱。|  
|0xC001F033|-1073614797|DTS_E_DESTINATIONOBJECTPARENTLESS|属性映射中的目标对象没有父级。 该目标对象不是任何序列容器的子级。 可能已将其从包中删除。|  
|0xC001F036|-1073614794|DTS_E_INVALIDPROPERTYMAPPING|属性映射无效。 忽略该映射。|  
|0xC001F038|-1073614792|DTS_E_PMFAILALERTREMOVE|通知属性映射有个目标正被删除的警报失败。|  
|0xC001F03A|-1073614790|DTS_E_INVALIDFOREACHPROPERTYMAPPING|发现 For Each 循环存在无效的属性映射。 如果 ForEach 属性映射无法还原，会出现这种情况。|  
|0xC001F040|-1073614784|DTS_E_PMPROPERTYINVALID|为属性映射指定的目标属性无效。 如果指定某个目标对象的属性，但在该对象上找不到该属性，会出现这种情况。|  
|0xC001F041|-1073614783|DTS_E_INVALIDTASKMONIKERNOPARAM|无法从 XML 创建任务。 如果运行库无法解析名称以创建任务，会出现这种情况。 请确保该名称正确。|  
|0xC001F080|-1073614720|DTS_E_COULDNOTREPLACECHECKPOINTFILE|无法用该更新过的检查点文件替换现有检查点文件。 在临时文件中成功创建了检查点，但用新文件覆盖现有文件时失败。|  
|0xC001F081|-1073614719|DTS_E_CHECKPOINTFILENOTSPECIFIED|该包被配置为始终从检查点重新启动，但未指定检查点文件。|  
|0xC001F082|-1073614718|DTS_E_CHECKPOINTLOADXML|尝试加载 XML 检查点文件“%1”失败，错误为 0x%2!8.8X! “%3”。 请确保指定的文件名正确，并且存在该文件。|  
|0xC001F083|-1073614717|DTS_E_LOADCHECKPOINT|由于无法加载检查点文件，包在执行期间失败。 要继续执行包，需要检查点文件。 如果 CheckpointUsage 属性设置为 ALWAYS (指定包始终重新启动)，通常会出现此错误。|  
|0xC001F185|-1073614459|DTS_E_NOEVALEXPRESSION|For 循环“%1”的求值条件表达式为空。 For 循环中必须有布尔求值表达式。|  
|0xC001F186|-1073614458|DTS_E_EXPREVALASSIGNMENTTYPEMISMATCH|无法将赋值表达式“%1”的结果转换成与该结果被赋予的变量兼容的类型。|  
|0xC001F187|-1073614457|DTS_E_EXPREVALASSIGNMENTTOREADONLYVARIABLE|在赋值表达式中使用只读变量“%1”时出错。 该变量是只读的，无法将表达式结果赋给它。 请选用可以写入的变量，或从此变量删除该表达式。|  
|0xC001F188|-1073614456|DTS_E_EXPREVALASSIGNMENTVARIABLELOCKFORWRITEFAILED|无法计算表达式“%1”，因为变量“%2”不存在或无法对其进行写访问。 无法将表达式结果赋给变量，原因是找不到该变量，或无法将其锁定以进行写访问。|  
|0xC001F189|-1073614455|DTS_E_EXPREVALRESULTTYPENOTSUPPORTED|表达式“%1”的结果类型为“%2”，无法将其转换为支持的类型。|  
|0xC001F18A|-1073614454|DTS_E_EXPREVALRESULTTYPECONVERSIONFAILED|无法将表达式“%1”的结果从类型“%2”转换为支持的类型，错误代码为 0x%3!8.8X!。 试图将表达式结果转换为运行时引擎支持的类型时出现意外错误，虽然支持该类型转换。|  
|0xC001F200|-1073614336|DTS_E_DTSNAME_NOTNULL|对象名无效。 该名称不能设置为 NULL。|  
|0xC001F201|-1073614335|DTS_E_DTSNAME_NOTEMPTY|对象名无效。 该名称不能为空。|  
|0xC001F202|-1073614334|DTS_E_DTSNAME_LEGAL|对象名“%1”无效。 该名称不能包含以下任何字符: / \ : [ ] . =|  
|0xC001F203|-1073614333|DTS_E_DTSNAME_PRINTABLE|对象名“%1”无效。 该名称不能包含使其无法打印的控制字符。|  
|0xC001F204|-1073614332|DTS_E_DTSNAME_NOLEADWHITESP|对象名“%1”无效。 名称不能以空白开头。|  
|0xC001F205|-1073614331|DTS_E_DTSNAME_NOTRAILWHITESP|对象名“%1”无效。 名称不能以空白结尾。|  
|0xC001F206|-1073614330|DTS_E_DTSNAME_BEGINSWITHALPHA|对象名“%1”无效。 名称必须以字母字符开头。|  
|0xC001F207|-1073614329|DTS_E_DTSNAME_BEGINSWITHALPHAUNDERBAR|对象名“%1”无效。 名称必须以字母字符或下划线“_”开头。|  
|0xC001F208|-1073614328|DTS_E_DTSNAME_ALPHADIGITUNDERBAR|对象名“%1”无效。 名称只能包含字母数字字符或下划线“_”。|  
|0xC001F209|-1073614327|DTS_E_DTSNAME_VALIDFILENAME|对象名“%1”无效。 该名称不能包含以下任何字符: / \ : ? " < > &#124;|  
|0xC001F420|-1073613792|DTS_E_FAILLOADINGPROPERTY|无法使用默认持久性加载值属性“%1”。|  
|0xC001F422|-1073613790|DTS_E_NODELISTENUM_INVALIDCONNMGRTYPE|连接管理器“%1”不属于类型“%2”|  
|0xC001F423|-1073613789|DTS_E_NODELISTENUM_XPATHISEMPTY|“%1”为空|  
|0xC001F424|-1073613788|DTS_E_NODELISTENUM_INVALIDDATANODE|节点列表枚举器部分中的数据节点无效|  
|0xC001F425|-1073613787|DTS_E_NODELISTENUM_NOENUMERATORCREATED|无法创建枚举器|  
|0xC001F427|-1073613785|DTS_E_OPERATIONFAILCACHEINUSE|由于缓存正在使用中，操作失败。|  
|0xC001F428|-1073613784|DTS_E_PROPERTYCANNOTBEMODIFIED|不能修改此属性。|  
|0xC001F429|-1073613783|DTS_E_PACKAGEUPGRADEFAILED|包升级失败。|  
|0xC00220DE|-1073602338|DTS_E_TKEXECPACKAGE_UNABLETOLOADFILE|将包文件“%3”加载到 XML 文档时 出现错误 0x%1!8.8X!。 %2。|  
|0xC00220DF|-1073602337|DTS_E_TKEXECPACKAGE_UNSPECIFIEDPACKAGE|未指定包。|  
|0xC00220E0|-1073602336|DTS_E_TKEXECPACKAGE_UNSPECIFIEDCONNECTION|未指定连接。|  
|0xC00220E2|-1073602334|DTS_E_TKEXECPACKAGE_INCORRECTCONNECTIONMANAGERTYPE|连接管理器“%1”属于不支持的类型“%2”。 仅支持 "FILE" 和 "OLEDB" 连接管理器。|  
|0xC00220E3|-1073602333|DTS_E_TKEXECPACKAGE_UNABLETOLOADXML|将包文件“%3”加载到 XML 文档时 出现错误 0x%1!8.8X!。 %2。|  
|0xC00220E4|-1073602332|DTS_E_TKEXECPACKAGE_UNABLETOLOAD|将包文件“%3”加载到 XML 文档时 出现错误 0x%1!8.8X!。 %2。|  
|0xC0024102|-1073594110|DTS_E_TASKVALIDATIONFAILED|该任务的 Validate 方法失败，返回错误代码 0x%1!8.8X! (%2)。 Validate 方法必须成功，并使用 "out" 参数指示结果。|  
|0xC0024104|-1073594108|DTS_E_TASKEXECUTEFAILED|任务的 Execute 方法返回错误代码 0x%1!8.8X! (%2)。 Execute 方法必须成功，并使用 "out" 参数指示该结果。|  
|0xC0024105|-1073594107|DTS_E_RETRIEVINGDEPENDENCIES|在检索依赖项时任务“%1”出错:0x%2!8.8X! 。 出现错误时，运行库正从任务的依赖项集合中检索依赖项。 可能该任务未能正确地实现一个依赖关系接口。|  
|0xC0024107|-1073594105|DTS_E_TASKVALIDATIONERROR|任务验证期间出错。|  
|0xC0024108|-1073594104|DTS_E_CONNECTIONSTRINGFORMAT|连接字符串的格式无效。 它必须包含一个或多个形式为 X=Y 并以分号分隔的成分。 如果为数据库连接管理器设置了不含任何成分的连接字符串，会出现此错误。|  
|0xC0024109|-1073594103|DTS_E_UNQUOTEDSEMICOLON|连接字符串成分中不能包含分号却不加引号。 如果值必须包含分号，请用引号将整个值引起来。 如果连接字符串中的值包含分号，却未加引号(例如 InitialCatalog 属性)，会出现此错误。|  
|0xC002410A|-1073594102|DTS_E_LOGPROVIDERVALIDATIONFAILED|一个或多个日志提供程序的验证失败。 无法执行包。 当日志提供程序验证失败时，不会执行包。|  
|0xC002410B|-1073594101|DTS_E_INVALIDVALUEINARRAY|数组中的值无效。|  
|0xC002410C|-1073594100|DTS_E_ENUMERATIONELEMENTNOTENUMERABLE|ForEach 枚举器返回的枚举器的某个元素未实现 IEnumerator，这与 ForEach 枚举器的 CollectionEnumerator 属性冲突。|  
|0xC002410D|-1073594099|DTS_E_INVALIDENUMERATORINDEX|枚举器未能在索引“%1!d!”处检索到元素。|  
|0xC0029100|-1073573632|DTS_E_AXTASK_MISSING_ENTRY_METHOD_NAME|找不到函数。|  
|0xC0029101|-1073573631|DTS_E_AXTASK_EMPTY_SCRIPT|找不到函数。|  
|0xC0029102|-1073573630|DTS_E_AXTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|ActiveX 脚本任务是使用错误的 XML 元素初始化的。|  
|0xC0029105|-1073573627|DTS_E_AXTASK_HANDLER_NOT_FOUND|找不到处理程序。|  
|0xC0029106|-1073573626|DTS_E_AXTASKUTIL_ENUMERATE_LANGUAGES_FAILED|尝试检索系统上安装的脚本语言时出错。|  
|0xC0029107|-1073573625|DTS_E_AXTASKUTIL_SCRIPTHOST_CREATE_FAILED|创建 ActiveX 脚本主机时出错。 请确保您已正确安装了脚本主机。|  
|0xC0029108|-1073573624|DTS_E_AXTASKUTIL_SCRIPTHOSTINIT_FAILED|尝试实例化所选语言的脚本主机时出错。 请确保系统中已安装了您选择的脚本语言。|  
|0xC0029109|-1073573623|DTS_E_AXTASKUTIL_ADDVARIABLES_FAILED|将 SSIS 变量添加到脚本主机命名空间时出错。 这可能会阻止任务使用脚本中的 SSIS 变量。|  
|0xC002910A|-1073573622|DTS_E_AXTASKUTIL_SCRIPT_PARSING_FAILED|尝试分析脚本文本时出错。 请确保所选语言的脚本引擎已正确安装。|  
|0xC002910B|-1073573621|DTS_E_AXTASKUTIL_MSG_BAD_FUNCTION|输入的函数名称无效。 请确保指定了有效的函数名称。|  
|0xC002910C|-1073573620|DTS_E_AXTASKUTIL_EXECUTION_FAILED|执行脚本时出错。 请确保所选语言的脚本引擎已正确安装。|  
|0xC002910D|-1073573619|DTS_E_AXTASKUTIL_ADDTYPELIB_FAILED|将托管类型库添加到脚本主机时出错。 请确保 DTS 2000 运行库已安装。|  
|0xC002910E|-1073573618|DTS_E_BITASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|大容量插入任务是使用错误的 XML 元素初始化的。|  
|0xC002910F|-1073573617|DTS_E_BITASK_DATA_FILE_NOT_SPECIFIED|未指定数据文件名。|  
|0xC0029110|-1073573616|DTS_E_BITASK_HANDLER_NOT_FOUND|找不到处理程序。|  
|0xC0029111|-1073573615|DTS_E_BITASK_CANNOT_ACQUIRE_CONNECTION|无法获得指定连接:“%1”。|  
|0xC0029112|-1073573614|DTS_E_BITASK_NO_CONNECTION_MANAGER_SPECIFIED|尝试获取连接管理器失败。|  
|0xC0029113|-1073573613|DTS_E_BITASK_INVALID_CONNECTION|连接无效。|  
|0xC0029114|-1073573612|DTS_E_BITASK_NULL_CONNECTION|连接为空。|  
|0xC0029115|-1073573611|DTS_E_BITASK_EXECUTE_FAILED|执行失败。|  
|0xC0029116|-1073573610|DTS_E_BITASK_CANNOT_RETRIEVE_TABLES|检索数据库中的表时出错。|  
|0xC0029117|-1073573609|DTS_E_BITASK_CANNOT_RETRIEVE_COLUMN_INFO|检索表中的列时出错。|  
|0xC0029118|-1073573608|DTS_E_BITASK_ERROR_IN_DB_OPERATION|执行数据库操作时出错。|  
|0xC0029119|-1073573607|DTS_E_BITASK_INVALIDSOURCECONNECTIONNAME|指定的连接“%1”无效，或者所指的对象无效。 若要继续，请指定一个有效的连接。|  
|0xC002911A|-1073573606|DTS_E_BITASK_INVALIDDESTCONNECTIONNAME|指定的目标连接无效。 若要继续，请提供有效的连接。|  
|0xC002911B|-1073573605|DTS_E_BITASK_DESTINATION_TABLE_NOT_SPECIFIED|必须指定表名称，然后才能继续。|  
|0xC002911C|-1073573604|DTS_E_BITASK_ERROR_IN_LOAD_FROM_XML|LoadFromXML 中的标记“%1”处出错。|  
|0xC002911D|-1073573603|DTS_E_BITASK_ERROR_IN_SAVE_TO_XML|SaveToXML 中的标记“%1”处出错。|  
|0xC002911E|-1073573602|DTS_E_BITASKUNMANCONNECTION_INVALID_CONNECTION|连接无效。|  
|0xC002911F|-1073573601|DTS_E_BITASKUNMANCONNECTION_EXECUTE_FAILED|执行失败。|  
|0xC0029120|-1073573600|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_TABLES|检索数据库中的表时出错。|  
|0xC0029121|-1073573599|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_COLUMN_INFO|检索表中的列时出错。|  
|0xC0029122|-1073573598|DTS_E_BITASKUNMANCONNECTION_CANNOT_OPEN_FILE|尝试打开该数据文件时出错。|  
|0xC0029123|-1073573597|DTS_E_BITASKUNMANCONNECTION_OEM_CONVERSION_FAILED|无法将输入 OEM 文件转换为指定格式。|  
|0xC0029124|-1073573596|DTS_E_BITASKUNMANCONNECTION_ERROR_IN_DB_OPERATION|执行数据库操作时出错。|  
|0xC0029125|-1073573595|DTS_E_DTSPROCTASK_NOCONNECTIONSPECIFIED|未指定连接管理器。|  
|0xC0029126|-1073573594|DTS_E_DTSPROCTASK_CONNECTIONMANAGERNOTOLAP|连接“%1”不是 Analysis Services 连接。|  
|0xC0029127|-1073573593|DTS_E_DTSPROCTASK_UNABLETOLOCATECONNECTIONMANAGER|找不到连接“%1”。|  
|0xC0029128|-1073573592|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEEXE|Analysis Services 执行 DDL 任务接收到的任务数据节点无效。|  
|0xC0029129|-1073573591|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEPROC|Analysis Services 处理任务接收到的任务数据节点无效。|  
|0xC002912A|-1073573590|DTS_E_DTSPROCTASK_INVALIDDDL|该 DDL 无效。|  
|0xC002912B|-1073573589|DTS_E_DTSPROCTASK_INVALIDDDLPROCESSINGCOMMANDS|ProcessingCommands 中找到的 DDL 无效。|  
|0xC002912C|-1073573588|DTS_E_DTSPROCTASK_CANNOTWRITEINAREADONLYVARIABLE|不能在只读变量中保存执行结果。|  
|0xC002912D|-1073573587|DTS_E_DTSPROCTASK_INVALIDVARIABLE|未定义变量“%1”。|  
|0xC002912E|-1073573586|DTS_E_DTSPROCTASK_CONNECTIONNOTFOUND|未定义连接管理器“%1”。|  
|0xC002912F|-1073573585|DTS_E_DTSPROCTASK_INVALIDCONNECTION|连接管理器“%1”不是文件连接管理器。|  
|0xC0029130|-1073573584|DTS_E_DTSPROCTASK_NONEXISTENTATTRIBUTE|在反序列化期间找不到“%1”。|  
|0xC0029131|-1073573583|DTS_E_DTSPROCTASK_TRACEHASBEENSTOPPED|由于出现异常，跟踪已停止。|  
|0xC0029132|-1073573582|DTS_E_DTSPROCTASK_DDLEXECUTIONFAILED|执行 DDL 失败。|  
|0xC0029133|-1073573581|DTS_E_DTSPROCTASK_FILEDOESNOTEXIST|没有任何文件与连接“%1”相关联。|  
|0xC0029134|-1073573580|DTS_E_DTSPROCTASK_VARIABLENOTDEFINED|未定义变量“%1”。|  
|0xC0029135|-1073573579|DTS_E_DTSPROCTASK_FILECONNECTIONNOTDEFINED|未定义文件连接“%1”。|  
|0xC0029136|-1073573578|DTS_E_EXEC2000PKGTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|执行 DTS 2000 包任务是使用错误的 XML 元素初始化的。|  
|0xC0029137|-1073573577|DTS_E_EXEC2000PKGTASK_HANDLER_NOT_FOUND|找不到处理程序。|  
|0xC0029138|-1073573576|DTS_E_EXEC2000PKGTASK_PACKAGE_NAME_NOT_SPECIFIED|未指定包名称。|  
|0xC0029139|-1073573575|DTS_E_EXEC2000PKGTASK_PACKAGE_ID_NOT_SPECIFIED|未指定包 ID。|  
|0xC002913A|-1073573574|DTS_E_EXEC2000PKGTASK_PACKAGE_VERSIONGUID_NOT_SPECIFIED|未指定包版本 GUID。|  
|0xC002913B|-1073573573|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_SPECIFIED|未指定 SQL Server。|  
|0xC002913C|-1073573572|DTS_E_EXEC2000PKGTASK_SQL_USERNAME_NOT_SPECIFIED|未指定 SQL Server 用户名。|  
|0xC002913D|-1073573571|DTS_E_EXEC2000PKGTASK_FILE_NAME_NOT_SPECIFIED|未指定存储文件名。|  
|0xC002913E|-1073573570|DTS_E_EXEC2000PKGTASK_DTS2000CANTBEEMPTY|DTS 2000 包属性为空。|  
|0xC002913F|-1073573569|DTS_E_EXEC2000PKGTASK_ERROR_IN_PACKAGE_EXECUTE|执行 DTS 2000 包时出错。|  
|0xC0029140|-1073573568|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_AVAILABLE_NETWORK|无法从网络加载可用的 SQL Server。 请检查网络连接。|  
|0xC0029141|-1073573567|DTS_E_EXEC2000PKGTASK_DATATYPE_NULL|数据类型不能为空。 请指定用于验证值的正确数据类型。|  
|0xC0029142|-1073573566|DTS_E_EXEC2000PKGTASK_NULL_VALUE|无法对任何数据类型验证 Null 值。|  
|0xC0029143|-1073573565|DTS_E_EXEC2000PKGTASK_NULL_VALUE_ARGUMENT|某个必需的参数为 Null。|  
|0xC0029144|-1073573564|DTS_E_EXEC2000PKGTASK_CLS_NOT_REGISTRED_EXCEPTION|若要执行 DTS 2000 包任务，请启动 SQL Server 安装程序，单击“要安装的组件”页中的“高级”按钮，然后选择“早期组件”。|  
|0xC0029145|-1073573563|DTS_E_EXEC2000PKGTASK_NOT_PRIMITIVE_TYPE|“%1”不是值类型。|  
|0xC0029146|-1073573562|DTS_E_EXEC2000PKGTASK_CONVERT_FAILED|无法将“%1”转换为“%2”。|  
|0xC0029147|-1073573561|DTS_E_EXEC2000PKGTASK_ERROR_IN_VALIDATE|无法验证“%1”(针对“%2”)。|  
|0xC0029148|-1073573560|DTS_E_EXEC2000PKGTASK_ERROR_IN_LOAD_FROM_XML|LoadFromXML 中的标记“%1”处出错。|  
|0xC0029149|-1073573559|DTS_E_EXEC2000PKGTASK_ERROR_IN_SAVE_TO_XML|SaveToXML 中的标记“%1”处出错。|  
|0xC002914A|-1073573558|DTS_E_EXECPROCTASK_INVALIDTIMEOUT|提供的超时值无效。 请指定任务允许进程运行的秒数。 最小超时值为 0，表示不使用超时值，进程一直运行到处理完毕或出错为止。 最大超时值为 2147483 (((2^31) - 1)/1000)。|  
|0xC002914B|-1073573557|DTS_E_EXECPROCTASK_CANTREDIRECTIO|如果进程在任务的生存期结束后仍可以继续执行，则无法重定向流。|  
|0xC002914C|-1073573556|DTS_E_EXECPROCTASK_PROCESSHASTIMEDOUT|该进程超时。|  
|0xC002914D|-1073573555|DTS_E_EXECPROCTASK_EXECUTABLENOTSPECIFIED|未指定可执行文件。|  
|0xC002914E|-1073573554|DTS_E_EXECPROCTASK_STDOUTVARREADONLY|标准输出变量是只读的。|  
|0xC002914F|-1073573553|DTS_E_EXECPROCTASK_STDERRVARREADONLY|标准错误变量是只读的。|  
|0xC0029150|-1073573552|DTS_E_EXECPROCTASK_RECEIVEDINVALIDTASKDATANODE|执行进程任务接收到的任务数据节点无效。|  
|0xC0029151|-1073573551|DTS_E_EXECPROCTASK_PROCESSEXITCODEEXCEEDS|在“%1”处执行“%2”“%3”时，进程退出代码为“%4”，但实际上该代码应该是“%5”。|  
|0xC0029152|-1073573550|DTS_E_EXECPROCTASK_WORKINGDIRDOESNOTEXIST|目录“%1”不存在。|  
|0xC0029153|-1073573549|DTS_E_EXECPROCTASK_FILEDOESNOTEXIST|目录“%2”中没有文件/进程“%1”。|  
|0xC0029154|-1073573548|DTS_E_EXECPROCTASK_FILENOTINPATH|文件/进程“%1”不在路径中。|  
|0xC0029156|-1073573546|DTS_E_EXECPROCTASK_WORKINGDIRECTORYDOESNOTEXIST|工作目录“%1”不存在。|  
|0xC0029157|-1073573545|DTS_E_EXECPROCTASK_ERROREXECUTIONVALUE|进程退出，返回的代码为“%1”。 但实际上应返回“%2”。|  
|0xC0029158|-1073573544|DTS_E_FSTASK_SYNCFAILED|同步对象失败。|  
|0xC0029159|-1073573543|DTS_E_FSTASK_INVALIDDATA|文件系统任务接收到的任务数据节点无效。|  
|0xC002915A|-1073573542|DTS_E_FSTASK_DIRECTORYEXISTS|该目录已存在。|  
|0xC002915B|-1073573541|DTS_E_FSTASK_PATHNOTVALID|“%1”对于操作类型“%2”无效。|  
|0xC002915C|-1073573540|DTS_E_FSTASK_DESTINATIONNOTSET|未设置操作“%1”的目标属性。|  
|0xC002915D|-1073573539|DTS_E_FSTASK_SOURCENOTSET|未设置操作“%1”的源属性。|  
|0xC002915E|-1073573538|DTS_E_FSTASK_CONNECTIONTYPENOTFILE|连接“%1”的类型不是文件。|  
|0xC002915F|-1073573537|DTS_E_FSTASK_VARIABLEDOESNTEXIST|变量“%1”不存在。|  
|0xC0029160|-1073573536|DTS_E_FSTASK_VARIABLENOTASTRING|变量“%1”不是字符串。|  
|0xC0029163|-1073573533|DTS_E_FSTASK_FILEDOESNOTEXIST|连接“%2”表示的文件或目录“%1”不存在。|  
|0xC0029165|-1073573531|DTS_E_FSTASK_DESTCONNUSAGETYPEINVALID|目标文件连接管理器“%1”有无效的使用类型:“%2”。|  
|0xC0029166|-1073573530|DTS_E_FSTASK_SRCCONNUSAGETYPEINVALID|源文件连接管理器“%1”有无效的使用类型“%2”。|  
|0xC0029167|-1073573529|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATION|FileSystemOperation|  
|0xC0029168|-1073573528|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATIONDESC|提供有关文件系统操作的信息。|  
|0xC0029169|-1073573527|DTS_E_FSTASK_TASKDISPLAYNAME|文件系统任务|  
|0xC002916A|-1073573526|DTS_E_FSTASK_TASKDESCRIPTION|执行文件系统操作，如复制和删除文件。|  
|0xC002916B|-1073573525|DTS_E_FTPTASK_SYNCOBJFAILED|同步对象失败。|  
|0xC002916C|-1073573524|DTS_E_FTPTASK_UNABLETOOBTAINFILELIST|无法获取文件列表。|  
|0xC002916D|-1073573523|DTS_E_FTPTASK_LOCALPATHEMPTY|本地路径为空。|  
|0xC002916E|-1073573522|DTS_E_FTPTASK_REMOTEPATHEMPTY|远程路径为空。|  
|0xC002916F|-1073573521|DTS_E_FTPTASK_LOCALVARIBALEEMPTY|本地变量为空。|  
|0xC0029170|-1073573520|DTS_E_FTPTASK_REMOTEVARIBALEEMPTY|远程变量为空。|  
|0xC0029171|-1073573519|DTS_E_FTPTASK_FTPRCVDINVLDDATANODE|FTP 任务接收到的任务数据节点无效。|  
|0xC0029172|-1073573518|DTS_E_FTPTASK_CONNECTION_NAME_NULL|该连接为空。 请确保提供了有效的 FTP 连接。|  
|0xC0029173|-1073573517|DTS_E_FTPTASK_CONNECTION_NOT_FTP|指定的连接不是 FTP 连接。 请确保提供了有效的 FTP 连接。|  
|0xC0029175|-1073573515|DTS_E_FTPTASK__INITIALIZATION_WITH_NULL_XML_ELEMENT|无法使用空的 XML 元素对任务进行初始化。|  
|0xC0029176|-1073573514|DTS_E_FTPTASK_SAVE_TO_NULL_XML_ELEMENT|无法将该任务保存到空的 XML 文档。|  
|0xC0029177|-1073573513|DTS_E_FTPTASK_ERROR_IN_LOAD_FROM_XML|LoadFromXML 中的标记“%1”处出错。|  
|0xC0029178|-1073573512|DTS_E_FTPTASK_NOFILESATLOCATION|“%1”处没有文件。|  
|0xC0029179|-1073573511|DTS_E_FTPTASK_LOCALVARIABLEISEMPTY|变量“%1”为空。|  
|0xC002917A|-1073573510|DTS_E_FTPTASK_REMOTEVARIABLEISEMPTY|变量“%1”为空。|  
|0xC002917B|-1073573509|DTS_E_FTPTASK_NOFILESINCONNMGR|文件“%1”不包含文件路径。|  
|0xC002917C|-1073573508|DTS_E_FTPTASK_NOFILEPATHSINLOCALVAR|变量“%1”不包含文件路径。|  
|0xC002917D|-1073573507|DTS_E_FTPTASK_VARIABLENOTASTRING|变量“%1”不是字符串。|  
|0xC002917E|-1073573506|DTS_E_FTPTASK_VARIABLENOTFOUND|变量“%1”不存在。|  
|0xC002917F|-1073573505|DTS_E_FTPTASK_INVALIDPATHONOPERATION|执行操作“%1”时路径无效。|  
|0xC0029180|-1073573504|DTS_E_FTPTASK_DIRECTORYEXISTS|“%1”已存在。|  
|0xC0029182|-1073573502|DTS_E_FTPTASK_CONNECTIONTYPENOTFILE|连接“%1”的类型不是文件。|  
|0xC0029183|-1073573501|DTS_E_FTPTASK_FILEDOESNOTEXIST|没有“%1”表示的文件。|  
|0xC0029184|-1073573500|DTS_E_FTPTASK_INVALIDDIRECTORY|变量“%1”中未指定目录。|  
|0xC0029185|-1073573499|DTS_E_FTPTASK_NOFILESFOUND|“%1”中找不到文件。|  
|0xC0029186|-1073573498|DTS_E_FTPTASK_NODIRECTORYPATHINCONMGR|文件连接管理器“%1”中未指定目录。|  
|0xC0029187|-1073573497|DTS_E_FTPTASK_UNABLETODELETELOCALEFILE|无法删除本地文件“%1”。|  
|0xC0029188|-1073573496|DTS_E_FTPTASK_UNABLETOREMOVELOCALDIRECTORY|无法删除本地目录“%1”。|  
|0xC0029189|-1073573495|DTS_E_FTPTASK_UNABLETOCREATELOCALDIRECTORY|无法创建本地目录“%1”。|  
|0xC002918A|-1073573494|DTS_E_FTPTASK_UNABLETORECEIVEFILES|无法使用“%1”接收文件。|  
|0xC002918B|-1073573493|DTS_E_FTPTASK_UNABLETOSENDFILES|无法使用“%1”发送文件。|  
|0xC002918C|-1073573492|DTS_E_FTPTASK_UNABLETOMAKEDIRREMOTE|无法使用“%1”创建远程目录。|  
|0xC002918D|-1073573491|DTS_E_FTPTASK_UNABLETOREMOVEDIRREMOTE|无法使用“%1”删除远程目录。|  
|0xC002918E|-1073573490|DTS_E_FTPTASK_UNABLETODELETEREMOTEFILES|无法使用“%1”删除远程文件。|  
|0xC002918F|-1073573489|DTS_E_FTPTASK_UNABLETOCONNECTTOSERVER|无法使用“%1”连接到 FTP 服务器。|  
|0xC0029190|-1073573488|DTS_E_FTPTASK_INVALIDVARIABLEVALUE|变量“%1”未以“/”开头。|  
|0xC0029191|-1073573487|DTS_E_FTPTASK_INVALIDREMOTEPATH|远程路径“%1”未以“/”开头。|  
|0xC0029192|-1073573486|DTS_E_DTS_E_FTPTASK_CANNOT_ACQUIRE_CONNECTION|获取 FTP 连接时出错。 请检查您是否指定了有效的连接类型“%1”。|  
|0xC0029193|-1073573485|DTS_E_MSGQTASKUTIL_CERT_OPEN_STORE_FAILED|打开证书存储区失败。|  
|0xC0029194|-1073573484|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_DISPLAY_NAME|检索证书的显示名称时出错。|  
|0xC0029195|-1073573483|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_ISSUER_NAME|检索证书的颁发者名称时出错。|  
|0xC0029196|-1073573482|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_FRIENDLY_NAME|检索证书的友好名称时出错。|  
|0xC0029197|-1073573481|DTS_E_MSMQTASK_NO_CONNECTION|未设置 MSMQ 连接名称。|  
|0xC0029198|-1073573480|DTS_E_MSMQTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|任务是使用错误的 XML 元素进行初始化的。|  
|0xC0029199|-1073573479|DTS_E_MSMQTASK_DATA_FILE_NAME_EMPTY|数据文件名为空。|  
|0xC002919A|-1073573478|DTS_E_MSMQTASK_DATA_FILE_SAVE_NAME_EMPTY|为要保存的数据文件指定的名称为空。|  
|0xC002919B|-1073573477|DTS_E_MSMQTASK_DATA_FILE_SIZE_ERROR|文件大小应小于 4 MB。|  
|0xC002919C|-1073573476|DTS_E_MSMQTASK_DATA_FILE_SAVE_FAILED|保存数据文件失败。|  
|0xC002919D|-1073573475|DTS_E_MSMQTASK_STRING_COMPARE_VALUE_MISSING|字符串筛选器值为空。|  
|0xC002919E|-1073573474|DTS_E_MSMQTASK_INVALID_QUEUE_PATH|队列路径无效。|  
|0xC002919F|-1073573473|DTS_E_MSMQTASK_NOT_TRANSACTIONAL|消息队列任务不支持在分布式事务中登记。|  
|0xC00291A0|-1073573472|DTS_E_MSMQTASK_INVALID_MESSAGE_TYPE|消息类型无效。|  
|0xC00291A1|-1073573471|DTS_E_MSMQTASK_TASK_TIMEOUT|消息队列超时。未接收到任何消息。|  
|0xC00291A2|-1073573470|DTS_E_MSMQTASK_INVALID_PROPERTY_VALUE|指定的属性无效。 请确保参数类型正确无误。|  
|0xC00291A3|-1073573469|DTS_E_MSMQTASK_MESSAGE_NON_AUTHENTICATED|消息未经过身份验证。|  
|0xC00291A4|-1073573468|DTS_E_MSMQTASK_INVALID_ENCRYPTION_ALGO_WRAPPER|您正试图使用无效的对象来设置加密算法的值。|  
|0xC00291A5|-1073573467|DTS_E_MSMQTASK_VARIABLE_TO_RECEIVE_STRING_MSG_EMPTY|用于接收字符串消息的变量为空。|  
|0xC00291A6|-1073573466|DTS_E_MSMQTASK_RECEIVE_VARIABLE_EMPTY|用于接收变量消息的变量为空。|  
|0xC00291A7|-1073573465|DTS_E_MSMQTASK_CONNECTIONTYPENOTMSMQ|连接“%1”不属于 MSMQ 类型。|  
|0xC00291A8|-1073573464|DTS_E_MSMQTASK_DATAFILE_ALREADY_EXISTS|在指定的位置上已存在数据文件“%1”。 由于覆盖选项被设置为 False，因此无法覆盖此文件。|  
|0xC00291A9|-1073573463|DTS_E_MSMQTASK_STRING_MSG_TO_VARIABLE_NOT_FOUND|在包变量集合中找不到用于接收字符串消息的指定变量“%1”。|  
|0xC00291AA|-1073573462|DTS_E_MSMQTASK_CONNMNGRNULL|连接管理器“%1”为空。|  
|0xC00291AB|-1073573461|DTS_E_MSMQTASK_CONNMNGRDOESNOTEXIST|连接管理器“%1”不存在。|  
|0xC00291AC|-1073573460|DTS_E_SCRIPTTASK_COMPILEERRORMSG|错误“%1”:“%2”\r\n第“%3”行   第“%4”至“%5”列。|  
|0xC00291AD|-1073573459|DTS_E_SCRIPTTASK_COMPILEERRORMSG2|编译脚本时出错:“%1”。|  
|0xC00291AE|-1073573458|DTS_E_SCRIPTTASK_COMPILEERRORMSG3|错误“%1”:“%2”\r\n第“%3”行 第“%4”-“%5”列\r\n行文本:“%6”。|  
|0xC00291AF|-1073573457|DTS_E_SCRIPTTASK_SCRIPTREPORTEDFAILURE|用户脚本返回了失败结果。|  
|0xC00291B0|-1073573456|DTS_E_SCRIPTTASK_SCRIPTFILESFAILEDTOLOAD|未能加载用户脚本文件。|  
|0xC00291B1|-1073573455|DTS_E_SCRIPTTASK_SCRIPTTHREWEXCEPTION|用户脚本出现异常:“%1”。|  
|0xC00291B2|-1073573454|DTS_E_SCRIPTTASK_COULDNOTCREATEENTRYPOINTCLASS|无法创建入口点类“%1”的实例。|  
|0xC00291B3|-1073573453|DTS_E_SCRIPTTASK_LOADFROMXMLEXCEPTION|从 XML 加载脚本任务时发生了异常:“%1”。|  
|0xC00291B4|-1073573452|DTS_E_SCRIPTTASK_SOURCEITEMNOTFOUNDEXCEPTION|在该包中找不到源项“%1”。|  
|0xC00291B5|-1073573451|DTS_E_SCRIPTTASK_BINARYITEMNOTFOUNDEXCEPTION|在该包中找不到二进制项“%1”。|  
|0xC00291B6|-1073573450|DTS_E_SCRIPTTASK_UNRECOGNIZEDSCRIPTLANGUAGEEXCEPTION|“%1”被认为是无效的脚本语言。|  
|0xC00291B7|-1073573449|DTS_E_SCRIPTTASK_ILLEGALSCRIPTNAME|脚本名称无效。 它不能包含空格、斜杠或特殊字符，也不能以数字开头。|  
|0xC00291B8|-1073573448|DTS_E_SCRIPTTASK_INVALIDSCRIPTLANGUAGE|指定的脚本语言无效。|  
|0xC00291B9|-1073573447|DTS_E_SCRIPTTASK_CANTINITNULLTASK|不能使用空任务进行初始化。|  
|0xC00291BA|-1073573446|DTS_E_SCRIPTTASK_MUSTINITWITHRIGHTTASK|必须使用脚本任务对脚本任务用户界面进行初始化。|  
|0xC00291BB|-1073573445|DTS_E_SCRIPTTASK_WASNOTINITED|脚本任务用户界面未初始化。|  
|0xC00291BC|-1073573444|DTS_E_SCRIPTTASK_HOST_NAME_CANT_EMPTY|名称不能为空。|  
|0xC00291BD|-1073573443|DTS_E_SCRIPTTASK_INVALID_SCRIPT_NAME|项目名称无效。 它不能包含空格、斜杠或特殊字符，也不能以数字开头。|  
|0xC00291BE|-1073573442|DTS_E_SCRIPTTASK_INVALID_SCRIPT_LANGUAGE|指定的脚本语言无效。|  
|0xC00291BF|-1073573441|DTS_E_SCRIPTTASK_INVALID_ENTRY_POINT|找不到入口点。|  
|0xC00291C0|-1073573440|DTS_E_SCRIPTTASK_LANGUAGE_EMPTY|未指定脚本语言。 请确保指定了有效的脚本语言。|  
|0xC00291C1|-1073573439|DTS_E_SCRIPTTASK_INITIALIZATION_WITH_NULL_TASK|用户界面初始化:任务为 NULL。|  
|0xC00291C2|-1073573438|DTS_E_SCRIPTTASK_UI_INITIALIZATION_WITH_WRONG_TASK|脚本任务用户界面是使用错误的任务进行初始化的。|  
|0xC00291C3|-1073573437|DTS_E_SENDMAILTASK_RECIPIENT_EMPTY|未指定收件人。|  
|0xC00291C4|-1073573436|DTS_E_SENDMAILTASK_SMTP_SERVER_NOT_SPECIFIED|未指定简单邮件传输协议(SMTP)服务器。 请提供一个有效的 SMTP 服务器名称或 IP 地址。|  
|0xC00291C5|-1073573435|DTS_E_SENDMAILTASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|发送邮件任务是使用错误的 XML 元素启动的。|  
|0xC00291CB|-1073573429|DTS_E_SENDMAILTASK_INVALIDATTACHMENT|文件“%1”不存在，或者您不具备访问该文件的权限。|  
|0xC00291CD|-1073573427|DTS_E_SENDMAILTASK_CHECK_VALID_SMTP_SERVER|请确保指定的简单邮件传输协议(SMTP)服务器有效。|  
|0xC00291CE|-1073573426|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTFILE|连接“%1”不属于文件类型。|  
|0xC00291CF|-1073573425|DTS_E_SENDMAILTASK_FILEDOESNOTEXIST|执行操作“%1”时，文件“%2”不存在。|  
|0xC00291D0|-1073573424|DTS_E_SENDMAILTASK_VARIABLETYPEISNOTSTRING|变量“%1”的类型不是字符串。|  
|0xC00291D1|-1073573423|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTSMTP|连接“%1”不属于 SMTP 类型。|  
|0xC00291D2|-1073573422|DTS_E_SENDMAILTASK_CONNMNGRNULL|连接“%1”为空。|  
|0xC00291D3|-1073573421|DTS_E_SENDMAILTASK_NOCONNMNGR|指定的连接“%1”不存在。|  
|0xC00291D4|-1073573420|DTS_E_SQLTASK_NOSTATEMENTSPECIFIED|未指定 Transact-SQL 语句。|  
|0xC00291D5|-1073573419|DTS_E_SQLTASK_NOXMLSUPPORT|该连接不支持 XML 结果集。|  
|0xC00291D6|-1073573418|DTS_E_SQLTASK_NOHANDLERFORCONNECTION|找不到指定的连接类型的处理程序。|  
|0xC00291D7|-1073573417|DTS_E_SQLTASK_NOCONNECTIONMANAGER|未指定连接管理器。|  
|0xC00291D8|-1073573416|DTS_E_SQLTASK_CANNOTACQUIRECONNMANAGER|无法从连接管理器获取连接。|  
|0xC00291D9|-1073573415|DTS_E_SQLTASK_NULLPARAMETERNAME|不能使用空参数名称。|  
|0xC00291DA|-1073573414|DTS_E_SQLTASK_INVALIDPARAMETERNAME|参数名称无效。|  
|0xC00291DB|-1073573413|DTS_E_SQLTASK_VALIDPARAMETERTYPES|有效的参数名称为 Int 或 String 类型。|  
|0xC00291DC|-1073573412|DTS_E_SQLTASK_READONLYVARIABLE|变量“%1”不能用于结果绑定中，因为它是只读的。|  
|0xC00291DD|-1073573411|DTS_E_SQLTASK_INDESNOTINCOLLECTION|此集合中未分配索引。|  
|0xC00291DE|-1073573410|DTS_E_SQLTASK_ROVARINOUTPARAMETER|变量“%1”不能用作参数绑定中的“out”参数或返回值，因为它是只读的。|  
|0xC00291DF|-1073573409|DTS_E_SQLTASK_OBJECTNOTINCOLLECTION|此集合中不存在该对象。|  
|0xC00291E0|-1073573408|DTS_E_SQLTASK_UNABLETOACQUIREMANAGEDCONN|无法获取托管连接。|  
|0xC00291E1|-1073573407|DTS_E_UNABLETOPOPRESULT|无法为单行结果类型填充结果列。 查询返回了一个空的结果集。|  
|0xC00291E2|-1073573406|DTS_E_SQLTASK_INVALIDNUMOFRESULTBINDINGS|为 ResultSetType 返回的结果绑定数无效:“%1”。|  
|0xC00291E3|-1073573405|DTS_E_SQLTASK_RESULTBINDTYPEFORROWSETXML|对于完整结果集和 XML 结果，结果绑定名称必须设置为零。|  
|0xC00291E4|-1073573404|DTS_E_SQLTASK_INVALIDEPARAMDIRECTIONFALG|参数方向标志无效。|  
|0xC00291E5|-1073573403|DTS_E_SQLTASK_NOSQLTASKDATAINXMLFRAGMENT|该 XML 片断不包含 SQL 任务数据。|  
|0xC00291E6|-1073573402|DTS_E_SQLTASK_MULTIPLERETURNVALUEPARAM|类型为返回值的参数不是第一个参数，或者有多个类型为返回值的参数。|  
|0xC00291E7|-1073573401|DTS_E_SQLTASK_CONNECTIONTYPENOTFILE|连接“%1”不是文件连接管理器。|  
|0xC00291E8|-1073573400|DTS_E_SQLTASK_FILEDOESNOTEXIST|没有“%1”表示的文件。|  
|0xC00291E9|-1073573399|DTS_E_SQLTASK_VARIABLETYPEISNOTSTRING|变量“%1”的类型不是字符串。|  
|0xC00291EA|-1073573398|DTS_E_SQLTASK_VARIABLENOTFOUND|变量“%1”不存在或无法锁定。|  
|0xC00291EB|-1073573397|DTS_E_SQLTASK_CANNOTLOCATECONNMANAGER|连接管理器“%1”不存在。|  
|0xC00291EC|-1073573396|DTS_E_SQLTASK_FAILEDTOACQUIRECONNECTION|未能获取连接“%1”。 原因可能是连接配置不正确，或者您没有访问该连接的适当权限。|  
|0xC00291ED|-1073573395|DTS_E_SQLTASK_RESULTBYNAMENOTSUPPORTED|此连接类型不支持按名称“%1”进行的结果绑定。|  
|0xC00291EE|-1073573394|DTS_E_SQLTASKCONN_ERR_NO_ROWS|指定了单行的结果集类型，但没有返回任何行。|  
|0xC00291EF|-1073573393|DTS_E_SQLTASKCONN_ERR_NO_DISCONNECTED_RS|没有用于 Transact-SQL 语句的断开连接的记录集。|  
|0xC00291F0|-1073573392|DTS_E_SQLTASKCONN_ERR_UNSUPPORTED_TYPE|不支持的类型。|  
|0xC00291F1|-1073573391|DTS_E_SQLTASKCONN_ERR_UNKNOWN_TYPE|未知类型。|  
|0xC00291F2|-1073573390|DTS_E_SQLTASKCONN_ERR_PARAM_DATA_TYPE|参数绑定 \\"%s\\" 不支持的数据类型。|  
|0xC00291F3|-1073573389|DTS_E_SQLTASKCONN_ERR_PARAM_NAME_MIX|参数名称不能由序号和已命名类型混合组成。|  
|0xC00291F4|-1073573388|DTS_E_SQLTASKCONN_ERR_PARAM_DIR|参数绑定 \\"%s\\" 的参数方向无效。|  
|0xC00291F5|-1073573387|DTS_E_SQLTASKCONN_ERR_RESULT_DATA_TYPE|不支持结果集绑定 \\"%s\\" 的数据类型。|  
|0xC00291F6|-1073573386|DTS_E_SQLTASKCONN_ERR_RESULT_COL_INDEX|结果列索引 %d 无效。|  
|0xC00291F7|-1073573385|DTS_E_SQLTASKCONN_ERR_UNKNOWN_RESULT_COL|在该结果集中找不到列 \\"%s\\"。|  
|0xC00291F9|-1073573383|DTS_E_SQLTASKCONN_ERR_NOROWSET|没有与执行此查询相关联的结果行集。|  
|0xC00291FA|-1073573382|DTS_E_SQLTASKCONN_ERR_ODBC_DISCONNECTED|无法通过 ODBC 连接获得已断开连接的记录集。|  
|0xC00291FB|-1073573381|DTS_E_SQLTASKCONN_ERR_RESULT_SET_DATA_TYPE|不支持该结果集内列 %hd 中的数据类型。|  
|0xC00291FC|-1073573380|DTS_E_SQLTASKCONN_ERR_CANT_LOAD_XML|无法加载包含查询结果的 XML。|  
|0xC00291FD|-1073573379|DTS_E_TTGENTASK_NOCONNORVARIABLE|必须指定包的连接名或变量名。|  
|0xC00291FE|-1073573378|DTS_E_TTGENTASK_FAILEDCREATE|无法创建该包。|  
|0xC00291FF|-1073573377|DTS_E_TTGENTASK_BADTABLEMETADATA|TableMetaDataNode 不是 XMLNode。|  
|0xC0029200|-1073573376|DTS_E_TTGENTASK_FAILEDCREATEPIPELINE|无法创建该管道。|  
|0xC0029201|-1073573375|DTS_E_TTGENTASK_BADVARIABLETYPE|变量的类型不正确。|  
|0xC0029202|-1073573374|DTS_E_TTGENTASK_NOTFILECONNECTION|指定的连接管理器不是“文件”连接管理器。|  
|0xC0029203|-1073573373|DTS_E_TTGENTASK_BADFILENAME|在连接管理器“%1”上指定了无效的文件名。|  
|0xC0029204|-1073573372|DTS_E_WEBSERVICETASK_CONNECTION_NAME_NULL|该连接为空。 请确保指定的 HTTP 连接有效。|  
|0xC0029205|-1073573371|DTS_E_WEBSERVICETASK_CONNECTION_NOT_FOUND|该连接不存在。 请确保指定的 HTTP 连接存在并有效。|  
|0xC0029206|-1073573370|DTS_E_WEBSERVICETASK_CONNECTION_NOT_HTTP|指定的连接不是 HTTP 连接。 请确保指定的 HTTP 连接有效。|  
|0xC0029207|-1073573369|DTS_E_WEBSERVICETASK_SERVICE_NULL|Web 服务名称为空。 请确保指定的 Web 服务名称有效。|  
|0xC0029208|-1073573368|DTS_E_WEBSERVICETASK_METHODNAME_NULL|Web 方法名称为空。 请确保指定的 Web 方法有效。|  
|0xC0029209|-1073573367|DTS_E_WEBSERVICETASK_WEBMETHODINFO_NULL|Web 方法为空或不存在。 请确保指定的 Web 方法存在。|  
|0xC002920A|-1073573366|DTS_E_WEBSERVICETASK_OUTPUTLOC_NULL|输出位置为空。 请确保指定了现有的文件连接或变量。|  
|0xC002920B|-1073573365|DTS_E_WEBSERVICETASK_VARIABLE_NOT_FOUND|找不到该变量。 请确保包中存在该变量。|  
|0xC002920C|-1073573364|DTS_E_WEBSERVICETASK_VARIABLE_READONLY|无法保存结果。 请确保该变量不是只读的。|  
|0xC002920D|-1073573363|DTS_E_WEBSERVICETASK_ERROR_IN_LOAD_FROM_XML|LoadFromXML 中的标记“%1”处出错。|  
|0xC002920E|-1073573362|DTS_E_WEBSERVICETASK_ERROR_IN_SAVE_TO_XML|SaveToXML 中的标记“%1”处出错。|  
|0xC002920F|-1073573361|DTS_E_WEBSERVICETASK_TASK_SAVE_TO_NULL_XML_ELEMENT|无法将该任务保存到空的 XML 文档。|  
|0xC0029210|-1073573360|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_NULL_XML_ELEMENT|无法使用空的 XML 元素对任务进行初始化。|  
|0xC0029211|-1073573359|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Web 服务任务是使用错误的 XML 元素初始化的。|  
|0xC0029212|-1073573358|DTS_E_WEBSERVICETASK_UNEXPECTED_XML_ELEMENT|发现了意外的 XML 元素。|  
|0xC0029213|-1073573357|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_CONNECTION|获取 HTTP 连接时出错。 请确保指定的连接类型有效。|  
|0xC0029214|-1073573356|DTS_E_WEBSERVICETASK_FILE_CONN_NOT_FOUND|无法保存结果。 请确保该文件连接已存在。|  
|0xC0029215|-1073573355|DTS_E_WEBSERVICETASK_FILE_NOT_FOUND|无法保存结果。 请确保该文件已存在。|  
|0xC0029216|-1073573354|DTS_E_WEBSERVICETASK_FILE_NULL|无法保存结果。 文件名为空，或文件正由另一进程使用。|  
|0xC0029217|-1073573353|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_FILE_CONNECTION|获取文件连接时出错。 请确保指定的文件连接有效。|  
|0xC0029218|-1073573352|DTS_E_WEBSERVICETASK_DATATYPE_NOT_SUPPORTED|仅支持具有 Primitive 值、Primitive 数组和枚举的复杂类型。|  
|0xC0029219|-1073573351|DTS_E_WEBSERVICETASK_PARAMTYPE_NOT_SUPPORTED|仅支持 Primitive、Enum、Complex、PrimitiveArray 和 ComplexArray 类型。|  
|0xC002921A|-1073573350|DTS_E_WEBSERVICETASK_WSDL_VERSION_NOT_SUPPORTED|不支持此版本的 WSDL。|  
|0xC002921B|-1073573349|DTS_E_WEBSERVICETASK_WRONG_XML_ELEMENT|使用了错误的 XML 元素进行初始化。|  
|0xC002921C|-1073573348|DTS_E_WEBSERVICETASK_XML_ATTRIBUTE_NOT_FOUND|找不到某个必需的属性。|  
|0xC002921D|-1073573347|DTS_E_WEBSERVICETASK_ENUM_NO_VALUES|枚举“%1”没有任何值。 该 WSDL 已损坏。|  
|0xC002921E|-1073573346|DTS_E_WEBSERVICETASK_CONNECTIONNOTFOUND|找不到该连接。|  
|0xC002921F|-1073573345|DTS_E_WEBSERVICETASK_CONNECTION_ALREADY_EXISTS|已存在使用此名称的连接。|  
|0xC0029220|-1073573344|DTS_E_WEBSERVICETASK_NULL_CONNECTION|连接不能是 Null，也不能为空。|  
|0xC0029221|-1073573343|DTS_E_WEBSERVICETASK_NOT_HTTP_CONNECTION|指定的连接不是 HTTP 连接。 请确保指定的 HTTP 连接有效。|  
|0xC0029222|-1073573342|DTS_E_WEBSERVICETASK_WSDL_NOT_FOUND|指定的统一资源标识符(URI)包含的 WSDL 无效。|  
|0xC0029223|-1073573341|DTS_E_WEBSERVICETASK_ERROR_IN_DOWNLOAD|无法读取 WSDL 文件。 输入 WSDL 文件无效。 读取器出现以下错误:“%1”。|  
|0xC0029224|-1073573340|DTS_E_WEBSERVICETASK_SERVICE_DESC_NULL|服务说明不能为 Null。|  
|0xC0029225|-1073573339|DTS_E_WEBSERVICETASK_SERVICENULL|服务名称不能为 Null。|  
|0xC0029226|-1073573338|DTS_E_WEBSERVICETASK_WSDL_NULL|URL 不能为 Null。|  
|0xC0029227|-1073573337|DTS_E_WEBSERVICETASK_SERVICE_NOT_FOUND|该服务当前不可用。|  
|0xC0029228|-1073573336|DTS_E_WEBSERVICETASK_SOAPPORT_NOT_FOUND|SOAP 端口无此服务。|  
|0xC0029229|-1073573335|DTS_E_WEBSERVICETASK_SOAPBINDING_NOT_FOUND|无法分析 Web 服务描述语言(WSDL)。 找不到与 SOAP 端口对应的绑定。|  
|0xC002922A|-1073573334|DTS_E_WEBSERVICETASK_SOAPPORTTYPE_NOT_FOUND|无法分析 Web 服务描述语言(WSDL)。 找不到与 SOAP 端口对应的 PortType。|  
|0xC002922B|-1073573333|DTS_E_WEBSERVICETASK_MSG_NOT_FOUND|找不到与指定的方法对应的消息。|  
|0xC002922C|-1073573332|DTS_E_WEBSERVICETASK_CANNOT_GEN_PROXY|无法为给定的 Web 服务生成代理。 生成代理“%1”时遇到以下错误。|  
|0xC002922D|-1073573331|DTS_E_WEBSERVICETASK_CANNOT_LOAD_PROXY|无法为给定的 Web 服务加载代理。 具体错误如下:“%1”。|  
|0xC002922E|-1073573330|DTS_E_WEBSERVICETASK_INVALID_SERVICE|找不到指定的服务。 具体错误如下:“%1”。|  
|0xC002922F|-1073573329|DTS_E_WEBSERVICETASK_WEBMETHOD_INVOKE_FAILED|执行方法时 Web 服务产生以下错误:“%1”。|  
|0xC0029230|-1073573328|DTS_E_WEBSERVICETASK_INVOKE_ERR|无法执行该 Web 方法。 具体错误如下:“%1”。|  
|0xC0029231|-1073573327|DTS_E_WEBSERVICETASK_METHODINFO_NULL|MethodInfo 不能为空。|  
|0xC0029232|-1073573326|DTS_E_WEBSERVICETASK_VALUE_NOT_PRIMITIVE|指定的 WebMethodInfo 不正确。 所提供的 ParamValue 与 ParamType 不匹配。 DTSParamValue 不属于 PrimitiveValue 类型。|  
|0xC0029233|-1073573325|DTS_E_WEBSERVICETASK_VALUE_NOT_ENUM|指定的 WebMethodInfo 不正确。 所提供的 ParamValue 与 ParamType 不匹配。 所找到的 DTSParamValue 不属于 EnumValue 类型。|  
|0xC0029234|-1073573324|DTS_E_VALUE_WEBSERVICETASK_NOT_COMPLEX|指定的 WebMethodInfo 不正确。 所提供的 ParamValue 与 ParamType 不匹配。 所找到的 DTSParamValue 不属于 ComplexValue 类型。|  
|0xC0029235|-1073573323|DTS_E_WEBSERVICETASK_VALUE_NOT_ARRAY|指定的 WebMethodInfo 不正确。 所提供的 ParamValue 与 ParamType 不匹配。 所找到的 DTSParamValue 不属于 ArrayValue 类型。|  
|0xC0029236|-1073573322|DTS_E_WEBSERVICETASK_TYPE_NOT_PRIMITIVE|您指定的 WebMethodInfo 是错误的。 “%1”不是 Primitive 类型。|  
|0xC0029237|-1073573321|DTS_E_WEBSERVICETASK_ARRAY_VALUE_INVALID|ArrayValue 的格式无效。 数组中应至少有一个元素。|  
|0xC0029238|-1073573320|DTS_E_WEBSERVICETASK_SELECTED_VALUE_NULL|枚举值不能为空。 请为枚举选择一个默认值。|  
|0xC0029239|-1073573319|DTS_E_WEBSERVICETASK_NULL_VALUE|无法对任何数据类型验证Null。|  
|0xC002923A|-1073573318|DTS_E_WEBSERVICETASK_ENUM_VALUE_NOT_FOUND|枚举值不正确。|  
|0xC002923B|-1073573317|DTS_E_WEBSERVICETASK_PROP_NOT_EXISTS|指定的类不包含名为“%1”的公共属性。|  
|0xC002923C|-1073573316|DTS_E_WEBSERVICETASK_CONVERT_FAILED|无法将“%1”转换为“%2”。|  
|0xC002923D|-1073573315|DTS_E_WEBSERVICETASK_CLEANUP_FAILED|清除失败。 不能删除为 Web 服务创建的代理。|  
|0xC002923E|-1073573314|DTS_E_WEBSERVICETASK_CREATE_INSTANCE_FAILED|无法创建类型为“%1”的对象。 请检查是否存在默认的构造函数。|  
|0xC002923F|-1073573313|DTS_E_WEBSERVICETASK_NOT_PRIMITIVE_TYPE|“%1”不是值类型。|  
|0xC0029240|-1073573312|DTS_E_WEBSERVICETASK_ERROR_IN_VALIDATE|无法验证“%1”(针对“%1”)。|  
|0xC0029241|-1073573311|DTS_E_WEBSERVICETASK_DATATYPE_NULL|数据类型不能为空。 请指定要验证的数据类型的值。|  
|0xC0029242|-1073573310|DTS_E_WEBSERVICETASK_INDEX_OUT_OF_BOUNDS|无法将 ParamValue 插入此处。 指定的索引可能小于零或大于该长度。|  
|0xC0029243|-1073573309|DTS_E_WEBSERVICETASK_WRONG_WSDL|输入 WSDL 文件无效。|  
|0xC0029244|-1073573308|DTS_E_WMIDRTASK_SYNCOBJECTFAILED|同步对象失败。|  
|0xC0029245|-1073573307|DTS_E_WMIDRTASK_MISSINGWQLQUERY|缺少 WQL 查询。|  
|0xC0029246|-1073573306|DTS_E_WMIDRTASK_DESTINATIONMUSTBESET|必须设置目标。|  
|0xC0029247|-1073573305|DTS_E_WMIDRTASK_MISSINGCONNECTION|未设置 WMI 连接。|  
|0xC0029248|-1073573304|DTS_E_WMIDRTASK_INVALIDDATANODE|WMI 数据读取器任务接收到的任务数据节点无效。|  
|0xC0029249|-1073573303|DTS_E_WMIDRTASK_FAILEDVALIDATION|任务未能通过验证。|  
|0xC002924A|-1073573302|DTS_E_WMIDRTASK_FILEDOESNOTEXIST|文件“%1”不存在。|  
|0xC002924B|-1073573301|DTS_E_WMIDRTASK_CONNECTIONMNGRDOESNTEXIST|连接管理器“%1”不存在。|  
|0xC002924C|-1073573300|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRINGOROBJECT|变量“%1”的类型不是字符串或对象。|  
|0xC002924D|-1073573299|DTS_E_WMIDRTASK_CONNECTIONTYPENOTFILE|连接“%1”不属于“文件”类型。|  
|0xC002924E|-1073573298|DTS_E_WMIDRTASK_CONNECTIONTYPENOTWMI|连接“%1”不属于“WMI”类型。|  
|0xC002924F|-1073573297|DTS_E_WMIDRTASK_FILEALREADYEXISTS|文件“%1”已存在。|  
|0xC0029250|-1073573296|DTS_E_WMIDRTASK_CONNECTIONMANAGEREMPTY|连接管理器“%1”为空。|  
|0xC0029251|-1073573295|DTS_E_WMIDRTASK_VARNOTOBJECT|变量“%1”应为要向其分配数据表的对象类型。|  
|0xC0029252|-1073573294|DTS_E_WMIDRTASK_TASKFAILURE|任务失败，原因是 WMI 查询“%1”无效。|  
|0xC0029253|-1073573293|DTS_E_WMIDRTASK_CANTWRITETOVAR|由于变量“%1”被设置为保留其原始值，所以无法对其执行写操作。|  
|0xC0029254|-1073573292|DTS_E_WMIEWTASK_SYNCOBJECTFAILED|同步对象失败。|  
|0xC0029255|-1073573291|DTS_E_WMIEWTASK_MISSINGWQLQUERY|缺少 WQL 查询。|  
|0xC0029256|-1073573290|DTS_E_WMIEWTASK_MISSINGCONNECTION|缺少 WMI 连接。|  
|0xC0029257|-1073573289|DTS_E_WMIEWTASK_QUERYFAILURE|任务未能执行 WMI 查询。|  
|0xC0029258|-1073573288|DTS_E_WMIEWTASK_INVALIDDATANODE|WMI 事件观察器任务接收到的任务数据节点无效。|  
|0xC0029259|-1073573287|DTS_E_WMIEWTASK_CONNECTIONMNGRDOESNTEXIST|连接管理器“%1”不存在。|  
|0xC002925A|-1073573286|DTS_E_WMIEWTASK_FILEDOESNOTEXIST|文件“%1”不存在。|  
|0xC002925B|-1073573285|DTS_E_WMIEWTASK_VARIABLETYPEISNOTSTRING|变量“%1”的类型不是字符串。|  
|0xC002925C|-1073573284|DTS_E_WMIEWTASK_CONNECTIONTYPENOTFILE|连接“%1”不属于“文件”类型。|  
|0xC002925D|-1073573283|DTS_E_WMIEWTASK_CONNECTIONTYPENOTWMI|连接“%1”不属于“WMI”类型。|  
|0xC002925E|-1073573282|DTS_E_WMIEWTASK_FILEALREADYEXISTS|文件“%1”已存在。|  
|0xC002925F|-1073573281|DTS_E_WMIEWTASK_CONNECTIONMANAGEREMPTY|连接管理器“%1”为空。|  
|0xC0029260|-1073573280|DTS_E_WMIEWTASK_TIMEOUTOCCURRED|在“%2”表示的事件发生之前已超时“%1”秒。|  
|0xC0029261|-1073573279|DTS_E_WMIEWTASK_ERRMESSAGE|因监视该 Wql 查询而导致以下系统异常:“%1”。 请检查该查询中是否有错误，或检查 WMI 连接是否具有访问权限。|  
|0xC0029262|-1073573278|DTS_E_XMLTASK_NODEFAULTOPERTION|未定义指定的操作。|  
|0xC0029263|-1073573277|DTS_E_XMLTASK_CONNECTIONTYPENOTFILE|连接类型不是文件。|  
|0xC0029264|-1073573276|DTS_E_XMLTASK_CANTGETREADERFROMSOURCE|无法从源 XML 文档获取 XmlReader。|  
|0xC0029265|-1073573275|DTS_E_XMLTASK_CANTGETREADERFROMDEST|无法从更改后的 XML 文档获取 XmlReader。|  
|0xC0029266|-1073573274|DTS_E_XMLTASK_CANTGETREADERFROMDIFFGRAM|无法从 XDL diffgram XML 获取 XDL diffgram 读取器。|  
|0xC0029268|-1073573272|DTS_E_XMLTASK_EMPTYNODELIST|节点列表为空。|  
|0xC0029269|-1073573271|DTS_E_XMLTASK_NOELEMENTFOUND|找不到该元素。|  
|0xC002926A|-1073573270|DTS_E_XMLTASK_UNDEFINEDOPERATION|未定义指定的操作。|  
|0xC002926B|-1073573269|DTS_E_XMLTASK_XPATHNAVERROR|XPathNavigator 中包含意外的内容项。|  
|0xC002926C|-1073573268|DTS_E_XMLTASK_NOSCHEMAFOUND|找不到用来强制验证的架构。|  
|0xC002926D|-1073573267|DTS_E_XMLTASK_VALIDATIONERROR|验证实例文档时出现验证错误。|  
|0xC002926E|-1073573266|DTS_E_XMLTASK_SYNCOBJECTFAILED|同步对象失败。|  
|0xC002926F|-1073573265|DTS_E_XMLTASK_ROOTNOODESNOTMATCHED|根节点不匹配。|  
|0xC0029270|-1073573264|DTS_E_XMLTASK_INVALIDEDITSCRIPT|最终编辑脚本中的编辑脚本操作类型无效。|  
|0xC0029271|-1073573263|DTS_E_XMLTASK_CDATANODESISSUE|应将 CDATA 节点与 DiffgramAddSubtrees 类一起添加。|  
|0xC0029272|-1073573262|DTS_E_XMLTASK_COMMENTSNODEISSUE|应将注释节点与 DiffgramAddSubtrees 类一起添加。|  
|0xC0029273|-1073573261|DTS_E_XMLTASK_TEXTNODEISSUES|应将文本节点与 DiffgramAddSubtrees 类一起添加。|  
|0xC0029274|-1073573260|DTS_E_XMLTASK_WHITESPACEISSUE|应将有效空格节点与 DiffgramAddSubtrees 类一起添加。|  
|0xC0029275|-1073573259|DTS_E_XMLTASK_DIFFENUMISSUE|请更正 OperationCost 数组，使其能够反映 XmlDiffOperation 枚举。|  
|0xC0029276|-1073573258|DTS_E_XMLTASK_TASKISEMPTY|任务中没有任何操作。|  
|0xC0029277|-1073573257|DTS_E_XMLTASK_DOCUMENTHASDATA|文档已包含数据，不应再次使用。|  
|0xC0029278|-1073573256|DTS_E_XMLTASK_INVALIDENODETYPE|节点类型无效。|  
|0xC0029279|-1073573255|DTS_E_XMLTASK_INVALIDDATANODE|XML 任务接收到的任务数据节点无效。|  
|0xC002927B|-1073573253|DTS_E_XMLTASK_VARIABLETYPEISNOTSTRING|变量数据类型不是字符串。|  
|0xC002927C|-1073573252|DTS_E_XMLTASK_COULDNOTGETENCODINGFROMDOCUMENT|无法从 XML 获取编码。|  
|0xC002927D|-1073573251|DTS_E_XMLTASK_MISSINGSOURCE|未指定源。|  
|0xC002927E|-1073573250|DTS_E_XMLTASK_MISSINGSECONDOPERAND|未指定第二操作数。|  
|0xC002927F|-1073573249|DTS_E_XMLTASK_INVALIDPATHDESCRIPTOR|XDL diffgram 无效。 “%1”不是有效的路径描述符。|  
|0xC0029280|-1073573248|DTS_E_XMLTASK_NOMATCHINGNODE|XDL diffgram 无效。 没有与路径描述符“%1”相匹配的节点。|  
|0xC0029281|-1073573247|DTS_E_XMLTASK_EXPECTINGDIFFGRAMELEMENT|XDL diffgram 无效。 xd:xmldiff 应当是命名空间 URI 为“%1”的根元素。|  
|0xC0029282|-1073573246|DTS_E_XMLTASK_MISSINGSRCDOCATTRIBUTE|XDL diffgram 无效。 xd:xmldiff 元素缺少 srcDocHash 属性。|  
|0xC0029283|-1073573245|DTS_E_XMLTASK_MISSINGOPTIONSATTRIBUTE|XDL diffgram 无效。 xd:xmldiff 元素缺少 options 属性。|  
|0xC0029284|-1073573244|DTS_E_XMLTASK_INVALIDSRCDOCATTRIBUTE|XDL diffgram 无效。 srcDocHash 属性包含无效值。|  
|0xC0029285|-1073573243|DTS_E_XMLTASK_INVALIDOPTIONSATTRIBUTE|XDL diffgram 无效。 options 属性包含无效值。|  
|0xC0029286|-1073573242|DTS_E_XMLTASK_SRCDOCMISMATCH|XDL diffgram 不适用于此 XML 文档。 rcDocHash 值不匹配。|  
|0xC0029287|-1073573241|DTS_E_XMLTASK_MORETHANONENODEMATCHED|XDL diffgram 无效；有多个节点与 xd:node 或 xd:change 元素的“%1”路径描述符相匹配。|  
|0xC0029288|-1073573240|DTS_E_XMLTASK_XMLDECLMISMATCH|XDL diffgram 不适用于此 XML 文档。 无法添加新的 XML 声明。|  
|0xC0029289|-1073573239|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODEINLIST|内部错误。 XmlDiffPathSingleNodeList 只能包含一个节点。|  
|0xC002928A|-1073573238|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODELEFT|内部错误。 修补后剩余“%1”个节点，应为 1 个。|  
|0xC002928B|-1073573237|DTS_E_XMLTASK_XSLTRESULTFILEISNOTXML|由 XSLT 生成的文件/文本不是有效的 XmlDocument，因此不能将其设置为操作结果:“%1”。|  
|0xC002928E|-1073573234|DTS_E_XMLTASK_FILEDOESNOTEXIST|没有任何文件与连接“%1”相关联。|  
|0xC002928F|-1073573233|DTS_E_XMLTASK_XMLTEXTEMPTY|属性“%1”没有源 Xml 文本；Xml 文本无效、为 Null 或是空字符串。|  
|0xC0029290|-1073573232|DTS_E_XMLTASK_FILEALREADYEXISTS|文件“%1”已存在。|  
|0xC0029293|-1073573229|DTS_E_TRANSFERTASKS_SRCCONNECTIONREQUIRED|必须指定源连接。|  
|0xC0029294|-1073573228|DTS_E_TRANSFERTASKS_DESTCONNECTIONREQUIRED|必须指定目标连接。|  
|0xC0029295|-1073573227|DTS_E_TRANSFERTASKS_CONNECTIONNOTFOUND|在该包中找不到连接“%1”。|  
|0xC0029296|-1073573226|DTS_E_TRANSFERTASKS_SERVERVERSIONNOTALLOWED|传输不支持连接“%1”指定的 SQL Server 实例版本，  仅支持 SQL Server 7、2000 和 2005 版本。|  
|0xC0029297|-1073573225|DTS_E_TRANSFERTASKS_SRCSERVERLESSEQUALDESTSERVER|源连接“%1”指定的 SQL Server 实例版本不得高于目标连接“%2”指定的版本。|  
|0xC0029298|-1073573224|DTS_E_TRANSFERTASKS_SRCDBREQUIRED|必须指定源数据库。|  
|0xC0029299|-1073573223|DTS_E_TRANSFERTASKS_SRCDBMUSTEXIST|源数据库“%1”必须位于源服务器上。|  
|0xC002929A|-1073573222|DTS_E_TRANSFERTASKS_DESTDBREQUIRED|必须指定目标数据库。|  
|0xC002929B|-1073573221|DTS_E_TRANSFERTASKS_SRCDBANDDESTDBTHESAME|源数据库和目标数据库不能是同一个数据库。|  
|0xC002929C|-1073573220|DTS_E_TRANSFERDBTASK_FILENAMEREQUIRED|传输文件信息 %1 中缺少文件名。|  
|0xC002929D|-1073573219|DTS_E_TRANSFERDBTASK_FOLDERREQUIRED|传输文件信息 %1 中缺少文件夹。|  
|0xC002929E|-1073573218|DTS_E_TRANSFERTASKS_NETSHAREREQUIRED|传输文件信息 %1 中缺少网络共享。|  
|0xC002929F|-1073573217|DTS_E_TRANSFERTASKS_FILELISTSCOUNTMISMATCH|源传输文件和目标传输文件的数目必须相等。|  
|0xC00292A0|-1073573216|DTS_E_DOESNOTSUPPORTTRANSACTIONS|不支持在事务中登记。|  
|0xC00292A1|-1073573215|DTS_E_TRANSFERDBTASK_OFFLINEERROR|在脱机传输数据库期间发生以下异常: %1。|  
|0xC00292A2|-1073573214|DTS_E_TRANSFERDBTASK_NETSHAREDOESNOTEXIST|找不到网络共享“%1”。|  
|0xC00292A3|-1073573213|DTS_E_TRANSFERDBTASK_NETSHARENOACCESS|无法访问网络共享“%1”。  错误: %2。|  
|0xC00292A4|-1073573212|DTS_E_TRANSFERDBTASK_USERMUSTBEDBOORSYSADMIN|用户“%1”必须是 DBO 或“%2”的 sysadmin，才能联机传输数据库。|  
|0xC00292A5|-1073573211|DTS_E_TRANSFERDBTASK_USERMUSTBESYSADMIN|用户“%1”必须是“%2”的 sysadmin，才能脱机传输数据库。|  
|0xC00292A6|-1073573210|DTS_E_TRANSFERDBTASK_FTCATALOGSOFFLINEYUKONONLY|仅在两台 SQL Server 2005 服务器之间脱机传输数据库的情况下，才能包含全文目录。|  
|0xC00292A7|-1073573209|DTS_E_TRANSFERDBTASK_NOOVERWRITEDB|目标服务器“%2”上已有数据库“%1”。|  
|0xC00292A8|-1073573208|DTS_E_TRANSFERDBTASK_MUSTHAVESOURCEFILES|必须指定至少一个源文件。|  
|0xC00292A9|-1073573207|DTS_E_TRANSFERDBTASKS_SRCFILENOTFOUND|在源数据库“%2”中找不到文件“%1”。|  
|0xC00292B3|-1073573197|DTS_E_MSMQTASK_FIPS1402COMPLIANCE|在符合 U.S. FIPS 140-2 标准的系统中不允许请求的操作。|  
|0xC002F210|-1073548784|DTS_E_SQLTASK_ERROREXECUTINGTHEQUERY|执行查询“%1”失败，错误如下:“%2”。 失败的原因可能有:查询本身有问题、未正确设置“ResultSet”属性、未正确设置参数或未正确建立连接。|  
|0xC002F300|-1073548544|DTS_E_TRANSFERSPTASK_ERRORREADINGSPNAMES|从该 xml 文件中读取存储过程名称时出错。|  
|0xC002F301|-1073548543|DTS_E_TRANSFERSPTASK_INVALIDDATANODE|传输存储过程任务的数据节点无效。|  
|0xC002F302|-1073548542|DTS_E_TRANSFERTASKS_CONNECTIONTYPEISNOTSMOSERVER|连接“%1”不属于“SMOServer”类型。|  
|0xC002F303|-1073548541|DTS_E_TRANSFERSPTASK_EXECUTIONFAILED|执行失败，出现以下错误“%1”。|  
|0xC002F304|-1073548540|DTS_E_ERROROCCURREDWITHFOLLOWINGMESSAGE|出现错误，错误消息如下:“%1”。|  
|0xC002F305|-1073548539|DTS_E_BITASK_EXECUTION_FAILED|大容量插入执行失败。|  
|0xC002F306|-1073548538|DTS_E_FSTASK_INVALIDDESTPATH|目标路径无效。|  
|0xC002F307|-1073548537|DTS_E_FSTASK_CANTCREATEDIR|无法创建目录。 用户已选择在目录存在时使任务失败。|  
|0xC002F308|-1073548536|DTS_E_SQLTASK_ODBCNOSUPPORTTRANSACTION|该任务有一个事务选项“Required”，且连接“%1”的类型为“ODBC”。 ODBC 连接不支持事务。|  
|0xC002F309|-1073548535|DTS_E_SQLTASK_ERRORASSIGINGVALUETOVAR|向变量“%1”赋值时出错:“%2”。|  
|0xC002F30A|-1073548534|DTS_E_FSTASK_SOURCEISEMPTY|源为空。|  
|0xC002F30B|-1073548533|DTS_E_FSTASK_DESTINATIONISEMPTY|目标为空。|  
|0xC002F30C|-1073548532|DTS_E_FSTASK_FILEDIRNOTFOUND|文件或目录“%1”不存在。|  
|0xC002F30D|-1073548531|DTS_E_FSTASK_VARSRCORDESTISEMPTY|变量“%1”用作源或目标且为空。|  
|0xC002F30E|-1073548530|DTS_E_FSTASK_FILEDELETED|文件或目录“%1”已删除。|  
|0xC002F30F|-1073548529|DTS_E_FSTASK_DIRECTORYDELETED|目录“%1”已删除。|  
|0xC002F310|-1073548528|DTS_E_WMIDRTASK_VARIABLETYPEISNOTOBJECT|变量“%1”应为要向其分配数据表的对象类型。|  
|0xC002F311|-1073548527|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRING|变量“%1”的数据类型不是字符串。|  
|0xC002F312|-1073548526|DTS_E_FTPTASK_CANNOTACQUIRECONNECTION|获取 FTP 连接时出错。 请验证在“%1”中是否指定了有效的连接类型。|  
|0xC002F313|-1073548525|DTS_E_FTPTASK_CONNECTIONNOTFOUND|找不到 FTP 连接管理器“%1”。|  
|0xC002F314|-1073548524|DTS_E_FTPTASK_FILEUSAGETYPEERROR|对于操作“%3”，连接“%1”的文件使用类型应为“%2”。|  
|0xC002F315|-1073548523|DTS_E_TRANSFERTASKS_SOURCECANTBESAMEASDESTINATION|源服务器不能与目标服务器相同。|  
|0xC002F316|-1073548522|DTS_E_ERRMSGTASK_EMPTYSOURCELIST|没有要传输的错误消息。|  
|0xC002F317|-1073548521|DTS_E_ERRMSGTASK_DIFFERENTMESSAGEANDLANGUAGESIZES|错误消息列表与其对应的语言列表的大小不同。|  
|0xC002F318|-1073548520|DTS_E_ERRMSGTASK_ERRORMESSAGEOUTOFRANGE|错误消息 id“%1”超出了用户定义的错误消息所允许的范围。 用户定义的错误消息 id 应介于 50000 和 2147483647 之间。|  
|0xC002F319|-1073548519|DTS_E_TRANSFERTASKS_NOTRANSACTIONSUPPORT|此任务不能参与事务。|  
|0xC002F320|-1073548512|DTS_E_ERRMSGTASK_FAILEDTOTRANSFERERRORMESSAGES|无法传输部分或所有错误消息。|  
|0xC002F321|-1073548511|DTS_E_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|目标服务器上已存在错误消息“%1”。|  
|0xC002F324|-1073548508|DTS_E_ERRMSGTASK_ERRORMESSAGECANTBEFOUND|在源服务器上找不到错误消息“%1”。|  
|0xC002F325|-1073548507|DTS_E_TRANSFERTASKS_EXECUTIONFAILED|执行失败，出现以下错误:“%1”。|  
|0xC002F327|-1073548505|DTS_E_JOBSTASK_FAILEDTOTRANSFERJOBS|无法传输该(这些)作业。|  
|0xC002F330|-1073548496|DTS_E_JOBSTASK_EMPTYSOURCELIST|没有要传输的作业。|  
|0xC002F331|-1073548495|DTS_E_JOBSTASK_JOBEXISTSATDEST|目标服务器上已存在作业“%1”。|  
|0xC002F334|-1073548492|DTS_E_JOBSTASK_JOBCANTBEFOUND|在源服务器上找不到作业“%1”。|  
|0xC002F337|-1073548489|DTS_E_LOGINSTASK_EMPTYLIST|要传输的“登录名”列表为空。|  
|0xC002F338|-1073548488|DTS_E_LOGINSTASK_CANTGETLOGINSNAMELIST|无法从源服务器获得“登录名”列表。|  
|0xC002F340|-1073548480|DTS_E_LOGINSTASK_ERRORLOGINEXISTS|目标服务器上已存在登录名“%1”。|  
|0xC002F342|-1073548478|DTS_E_LOGINSTASK_LOGINNOTFOUND|源中不存在登录名“%1”。|  
|0xC002F344|-1073548476|DTS_E_LOGINSTASK_FAILEDTOTRANSFERLOGINS|无法传输部分或所有登录名。|  
|0xC002F345|-1073548475|DTS_E_STOREDPROCSTASK_FAILEDTOTRANSFERSPS|无法传输该(这些)存储过程。 应该已经产生了更详细的错误。|  
|0xC002F346|-1073548474|DTS_E_STOREDPROCSTASK_STOREDPROCNOTFOUND|在源中找不到存储过程“%1”。|  
|0xC002F349|-1073548471|DTS_E_STOREDPROCSTASK_ERRORSTOREDPROCEDUREEXISTS|目标服务器上已存在存储过程“%1”。|  
|0xC002F350|-1073548464|DTS_E_STOREDPROCSTASK_EMPTYSOURCELIST|没有要传输的存储过程。|  
|0xC002F353|-1073548461|DTS_E_TRANSOBJECTSTASK_FAILEDTOTRANSFEROBJECTS|无法传输该(这些)对象。|  
|0xC002F354|-1073548460|DTS_E_TRANSOBJECTSTASK_EMPTYLIST|要传输的“对象”列表为空。|  
|0xC002F355|-1073548459|DTS_E_TRANSOBJECTSTASK_NOSPATSOURCE|在源中不存在存储过程“%1”。|  
|0xC002F356|-1073548458|DTS_E_TRANSOBJECTSTASK_SPALREADYATDEST|目标中已存在存储过程“%1”。|  
|0xC002F357|-1073548457|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSPS|在尝试获取或设置要传输的“存储过程”列表时出错:“%1”。|  
|0xC002F359|-1073548455|DTS_E_TRANSOBJECTSTASK_NORULEATSOURCE|源中不存在规则“%1”。|  
|0xC002F360|-1073548448|DTS_E_TRANSOBJECTSTASK_RULEALREADYATDEST|目标中已存在规则“%1”。|  
|0xC002F361|-1073548447|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGRULES|在尝试获取或设置要传输的“规则”列表时出错:“%1”。|  
|0xC002F363|-1073548445|DTS_E_TRANSOBJECTSTASK_NOTABLEATSOURCE|源中不存在表“%1”。|  
|0xC002F364|-1073548444|DTS_E_TRANSOBJECTSTASK_TABLEALREADYATDEST|目标中已存在表“%1”。|  
|0xC002F365|-1073548443|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTABLES|在尝试获取或设置要传输的“表”列表时出错:“%1”。|  
|0xC002F367|-1073548441|DTS_E_TRANSOBJECTSTASK_NOVIEWATSOURCE|源中不存在视图“%1”。|  
|0xC002F368|-1073548440|DTS_E_TRANSOBJECTSTASK_VIEWALREADYATDEST|目标中已存在视图“%1”。|  
|0xC002F369|-1073548439|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGVIEWS|在尝试获取或设置要传输的“视图”列表时出错:“%1”。|  
|0xC002F371|-1073548431|DTS_E_TRANSOBJECTSTASK_NOUDFATSOURCE|源中不存在用户定义函数“%1”。|  
|0xC002F372|-1073548430|DTS_E_TRANSOBJECTSTASK_UDFALREADYATDEST|目标中已存在用户定义函数“%1”。|  
|0xC002F373|-1073548429|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDFS|在尝试获取或设置要传输的“用户定义函数”列表时出错:“%1”。|  
|0xC002F375|-1073548427|DTS_E_TRANSOBJECTSTASK_NODEFAULTATSOURCE|源中不存在默认值“%1”。|  
|0xC002F376|-1073548426|DTS_E_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|目标中已存在默认值“%1”。|  
|0xC002F377|-1073548425|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGDEFAULTS|在尝试获取或设置要传输的“默认值”列表时出错:“%1”。|  
|0xC002F379|-1073548423|DTS_E_TRANSOBJECTSTASK_NOUDDTATSOURCE|源中不存在用户定义数据类型“%1”。|  
|0xC002F380|-1073548416|DTS_E_TRANSOBJECTSTASK_UDDTALREADYATDEST|目标中已存在用户定义数据类型“%1”。|  
|0xC002F381|-1073548415|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDDTS|在尝试获取或设置要传输的“用户定义数据类型”列表时出错:“%1”。|  
|0xC002F383|-1073548413|DTS_E_TRANSOBJECTSTASK_NOPFATSOURCE|源中不存在分区函数“%1”。|  
|0xC002F384|-1073548412|DTS_E_TRANSOBJECTSTASK_PFALREADYATDEST|目标中已存在分区函数“%1”。|  
|0xC002F385|-1073548411|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPFS|在尝试获取或设置要传输的“分区函数”列表时出错:“%1”。|  
|0xC002F387|-1073548409|DTS_E_TRANSOBJECTSTASK_NOPSATSOURCE|源中不存在分区方案“%1”。|  
|0xC002F388|-1073548408|DTS_E_TRANSOBJECTSTASK_PSALREADYATDEST|目标中已存在分区方案“%1”。|  
|0xC002F389|-1073548407|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPSS|在尝试获取或设置要传输的“分区方案”列表时出错:“%1”。|  
|0xC002F391|-1073548399|DTS_E_TRANSOBJECTSTASK_NOSCHEMAATSOURCE|源中不存在架构“%1”。|  
|0xC002F392|-1073548398|DTS_E_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|目标中已存在架构“%1”。|  
|0xC002F393|-1073548397|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSCHEMAS|在尝试获取或设置要传输的“架构”列表时出错:“%1”。|  
|0xC002F395|-1073548395|DTS_E_TRANSOBJECTSTASK_NOSQLASSEMBLYATSOURCE|源中不存在 SqlAssembly“%1”。|  
|0xC002F396|-1073548394|DTS_E_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|目标中已存在 SqlAssembly“%1”。|  
|0xC002F397|-1073548393|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSQLASSEMBLIES|在尝试获取或设置要传输的 SqlAssemblies 列表时出错:“%1”。|  
|0xC002F399|-1073548391|DTS_E_TRANSOBJECTSTASK_NOAGGREGATEATSOURCE|源中不存在用户定义聚合“%1”。|  
|0xC002F400|-1073548288|DTS_E_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|目标中已存在用户定义聚合“%1”。|  
|0xC002F401|-1073548287|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGAGGREGATES|在尝试获取或设置要传输的“用户定义聚合”列表时出错:“%1”。|  
|0xC002F403|-1073548285|DTS_E_TRANSOBJECTSTASK_NOTYPEATSOURCE|源中不存在用户定义类型“%1”。|  
|0xC002F404|-1073548284|DTS_E_TRANSOBJECTSTASK_TYPEALREADYATDEST|目标中已存在用户定义类型“%1”。|  
|0xC002F405|-1073548283|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTYPES|在尝试获取或设置要传输的“用户定义类型”列表时出错:“%1”。|  
|0xC002F407|-1073548281|DTS_E_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONATSOURCE|源中不存在 XmlSchemaCollection“%1”。|  
|0xC002F408|-1073548280|DTS_E_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|目标中已存在 XmlSchemaCollection“%1”。|  
|0xC002F409|-1073548279|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGXMLSCHEMACOLLECTIONS|在尝试获取或设置要传输的 XmlSchemaCollections 列表时出错:“%1”。|  
|0xC002F411|-1073548271|DTS_E_TRANSOBJECTSTASK_SUPPORTEDONYUKONONLY|只有 SQL Server 2005 服务器或更高版本的服务器之间支持“%1”类型的对象。|  
|0xC002F413|-1073548269|DTS_E_LOGINSTASK_EMPTYDATABASELIST|数据库列表为空。|  
|0xC002F414|-1073548268|DTS_E_TRANSOBJECTSTASK_NOLOGINATSOURCE|源中不存在登录名“%1”。|  
|0xC002F416|-1073548266|DTS_E_TRANSOBJECTSTASK_LOGINALREADYATDEST|目标中已存在登录名“%1”。|  
|0xC002F417|-1073548265|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGLOGINS|在尝试获取或设置要传输的“登录名”列表时出错:“%1”。|  
|0xC002F419|-1073548263|DTS_E_TRANSOBJECTSTASK_NOUSERATSOURCE|源中不存在用户“%1”。|  
|0xC002F41B|-1073548261|DTS_E_TRANSOBJECTSTASK_USERALREADYATDEST|目标中已存在用户“%1”。|  
|0xC002F41C|-1073548260|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUSERS|在尝试获取或设置要传输的“用户”列表时出错:“%1”。|  
|0xC002F41F|-1073548257|DTS_E_BITASK_CANNOTRETAINCONNINTRANSACTION|该任务在事务中不能有保留的连接管理器。|  
|0xC002F421|-1073548255|DTS_E_SQLTASKOUTPUTENCODINGNOTSUPPORTED|该提供程序不支持 OUTPUTENCODING 属性，所以无法以 Unicode 形式从 SQL Server 获取 XML 数据。|  
|0xC002F426|-1073548250|DTS_E_FTPTASK_FILECONNECTIONNOTFOUND|对于 FTP 操作“%1”，找不到 FILE 连接管理器“%2”。|  
|0xC002F428|-1073548248|DTS_E_TRANSOBJECTSTASK_CANNOTDROPOBJECTS|登录名是服务器级对象，无法首先删除，因为源服务器和目标服务器是同一服务器。 首先删除对象也会同时从源服务器中删除登录名。|  
|0xC002F429|-1073548247|DTS_E_SQLTASK_PARAMSIZEERROR|参数“%1”不能为负。 (-1) 用作默认值。|  
|0xC0040019|-1073479655|DTS_E_UNREGISTEREDPIPELINEXML_LOAD|无法加载数据流对象。 请检查是否已正确注册 Microsoft.SqlServer.PipelineXml.dll。|  
|0xC0040020|-1073479648|DTS_E_UNREGISTEREDPIPELINEXML_SAVE|无法保存数据流对象。 请检查是否已正确注册 Microsoft.SqlServer.PipelineXml.dll。|  
|0xC0040040|-1073479616|DTS_E_PIPELINE_SAVE|无法保存数据流对象。|  
|0xC0040041|-1073479615|DTS_E_PIPELINE_LOAD|无法加载数据流对象|  
|0xC0040042|-1073479614|DTS_E_SAVE_PERSTFORMAT|无法保存数据流对象。 不支持指定的格式。|  
|0xC0040043|-1073479613|DTS_E_LOAD_PERSTFORMAT|无法加载数据流对象。 不支持指定的格式。|  
|0xC0040044|-1073479612|DTS_E_SETPERSIST_PROPEVENTS|无法为数据流对象设置 XML 持久性事件属性。|  
|0xC0040045|-1073479611|DTS_E_SETPERSIST_XMLDOM|无法为数据流对象设置持久性 XML DOM 属性。|  
|0xC0040046|-1073479610|DTS_E_SETPERSIST_XMLNODE|无法为数据流对象设置持久性 XML ELEMENT 属性。|  
|0xC0040047|-1073479609|DTS_E_SETPERSISTPROP_FAILED|无法为数据流对象设置 xml 持久性属性。|  
|0xC0040048|-1073479608|DTS_E_NOCUSTOMPROPCOL|无法为数据流组件获取自定义属性集合。|  
|0xC0047000|-1073451008|DTS_E_CYCLEINEXECUTIONTREE|某个执行树包含循环。|  
|0xC0047001|-1073451007|DTS_E_DISCONNECTEDOBJECT|%1 对象“%2”(%3!d!)已断开与布局的连接。|  
|0xC0047002|-1073451006|DTS_E_INVALIDOBJECTID|布局对象的 ID 无效。|  
|0xC0047003|-1073451005|DTS_E_INPUTWITHOUTPATHS|一个必需的输入对象未连接到路径对象。|  
|0xC0047005|-1073451003|DTS_E_INVALIDSYNCHRONOUSINPUT|%1 的同步输入 ID %2!d! 无效。|  
|0xC0047006|-1073451002|DTS_E_INVALIDOUTPUTLINEAGEID|%1 的沿袭 ID 为 %2!d!，但应当为 %3!d!。|  
|0xC0047008|-1073451000|DTS_E_DUPLICATENAMESINCOLLECTION|该包中包含两个具有重复名称“%1”和“%2”的对象。|  
|0xC0047009|-1073450999|DTS_E_INVALIDEXCLUSIONGROUP|“%1”和“%2”位于同一排除组中，但是它们的同步输入却不相同。|  
|0xC004700A|-1073450998|DTS_E_DUPLICATELINEAGEIDSINCOLLECTION|同一集合中的两个对象具有重复的沿袭 ID %1!d!。 这两个对象是 %2 和 %3。|  
|0xC004700B|-1073450997|DTS_E_VALIDATIONFAILEDONLAYOUT|布局未能通过验证。|  
|0xC004700C|-1073450996|DTS_E_VALIDATIONFAILEDONCOMPONENTS|一个或多个组件未能通过验证。|  
|0xC004700D|-1073450995|DTS_E_VALIDATIONFAILED|该布局和一个或多个组件未能通过验证。|  
|0xC004700E|-1073450994|DTS_E_THREADSTARTUPFAILED|数据流任务引擎在启动时失败，因为它无法创建一个或多个必需的线程。|  
|0xC004700F|-1073450993|DTS_E_CANTGETMUTEX|某个线程在初始化时未能创建互斥体。|  
|0xC0047010|-1073450992|DTS_E_CANTGETSEMAPHORE|某个线程在初始化时未能创建信号量。|  
|0xC0047011|-1073450991|DTS_E_BUFFERFAILUREDETAILS|系统报告了百分之 %1!d! 的内存负载。 物理内存为 %2 个字节，其中有 %3 个可用字节。 虚拟内存为 %4 个字节，其中有 %5 个可用字节。 分页文件为 %6 个字节，其中有 %7 个可用字节。|  
|0xC0047012|-1073450990|DTS_E_BUFFERALLOCFAILED|分配 %1!d! 个字节时某个缓冲区 个字节的结果值。|  
|0xC0047013|-1073450989|DTS_E_CANTCREATEBUFFERMANAGER|无法创建缓冲区管理器。|  
|0xC0047015|-1073450987|DTS_E_BUFFERBADSIZE|缓冲区类型 %1!d! 的大小为 %2!I64d! 个 个字节的结果值。|  
|0xC0047016|-1073450986|DTS_E_DANGLINGWITHPATH|%1 被标记为无关联，但是它有一个与之相连的路径。|  
|0xC0047017|-1073450985|DTS_E_INDIVIDUALVALIDATIONFAILED|%1 未能通过验证，返回的错误代码为 0x%2!8.8X!。|  
|0xC0047018|-1073450984|DTS_E_INDIVIDUALPOSTEXECUTEFAILED|%1 在执行后阶段失败，返回的错误代码为 0x%2!8.8X!。|  
|0xC0047019|-1073450983|DTS_E_INDIVIDUALPREPAREFAILED|%1 在准备阶段失败，返回的错误代码为 0x%2!8.8X!。|  
|0xC004701A|-1073450982|DTS_E_INDIVIDUALPREEXECUTEFAILED|%1 在执行前阶段失败，返回的错误代码为 0x%2!8.8X!。|  
|0xC004701B|-1073450981|DTS_E_INDIVIDUALCLEANUPFAILED|%1 在清除阶段失败，返回的错误代码为 0x%2!8.8X!。|  
|0xC004701C|-1073450980|DTS_E_INVALIDINPUTLINEAGEID|%1 的沿袭 ID 为 %2!d!， 数据流任务中以前未使用过该沿袭 ID。|  
|0xC004701E|-1073450978|DTS_E_EXECUTIONTREECYCLE|无法将 %1 连接到 %2，因为这会产生循环。|  
|0xC004701F|-1073450977|DTS_E_CANTCOMPARE|数据类型“%1”不可比较。 不支持与该数据类型比较，因此不能对其进行排序或将其用作键。|  
|0xC0047020|-1073450976|DTS_E_REFUSEDFORSHUTDOWN|此线程已关闭，不接受用于输入的缓冲区。|  
|0xC0047021|-1073450975|DTS_E_THREADFAILED|SSIS 错误代码 DTS_E_THREADFAILED。  线程“%1”已退出，错误代码为 0x%2!8.8X!。  可能在此之前已经发出错误消息，提供了有关线程退出原因的详细信息。|  
|0xC0047022|-1073450974|DTS_E_PROCESSINPUTFAILED|SSIS 错误代码 DTS_E_PROCESSINPUTFAILED。  处理输入“%4”(%5!d!) 时，组件“%1”(%2!d!)的 ProcessInput 方法失败，错误代码为 0x%3!8.8X! 。 标识的这个组件从 ProcessInput 方法返回了一个错误。 虽然该错误是此组件特有的，但却是致命的，将导致数据流任务停止运行。  可能在此之前已经发出错误消息，提供了有关失败的详细信息。|  
|0xC0047023|-1073450973|DTS_E_CANTREALIZEVIRTUALBUFFERS|无法实现一组虚拟缓冲区。|  
|0xC0047024|-1073450972|DTS_E_PIPELINETOOCOMPLEX|此管道所需的线程数为 %1!d!，超出了系统限制值 %2!d!。 此管道所需的线程超出了配置限制。 可能是因为异步输出过多，或者 EngineThreads 属性的值设置过高。 请将此管道拆分为多个包，或者减小 EngineThreads 属性的值。|  
|0xC0047028|-1073450968|DTS_E_SCHEDULERCOULDNOTCOUNTSOURCES|数据流引擎计划程序无法获取布局中的源的计数。|  
|0xC0047029|-1073450967|DTS_E_SCHEDULERCOULDNOTCOUNTDESTINATIONS|数据流引擎计划程序无法获取布局中的目标的计数。|  
|0xC004702A|-1073450966|DTS_E_COMPONENTVIEWISUNAVAILABLE|没有该组件视图。 请确保已创建了该组件视图。|  
|0xC004702B|-1073450965|DTS_E_INCORRECTCOMPONENTVIEWID|组件视图 ID 不正确。 此组件视图可能不同步。 请尝试释放此组件视图，然后重新创建它。|  
|0xC004702C|-1073450964|DTS_E_BUFFERNOTLOCKED|未锁定此缓冲区，不能对它进行操作。|  
|0xC004702D|-1073450963|DTS_E_CANTBUILDBUFFERTYPE|数据流任务无法分配内存来生成缓冲区定义。 该缓冲区定义有 %1!d! 列。|  
|0xC004702E|-1073450962|DTS_E_CANTREGISTERBUFFERTYPE|数据流任务无法注册缓冲区类型。 该类型有 %1!d! 列，用于执行树 %2!d!。|  
|0xC004702F|-1073450961|DTS_E_INVALIDUSESDISPOSITIONSVALUE|不能更改 UsesDispositions 属性的初始值。 如果编辑了 XML 并修改了 UsesDispositions 值，就会发生这种情况。 该值是在将组件添加到包时由该组件设置的，不可以更改。|  
|0xC0047030|-1073450960|DTS_E_THREADFAILEDINITIALIZE|数据流任务无法初始化一个必需的线程，因此无法开始执行。 该线程先前已报告了一个特定的错误。|  
|0xC0047031|-1073450959|DTS_E_THREADFAILEDCREATE|数据流任务无法创建一个必需的线程，因此无法开始运行。 内存不足时通常会发生这种情况。|  
|0xC0047032|-1073450958|DTS_E_EXECUTIONTREECYCLEADDINGSYNCHRONOUSINPUT|不能将“%1”的同步输入设置为“%2”，因为这会产生循环。|  
|0xC0047033|-1073450957|DTS_E_INVALIDCUSTOMPROPERTYNAME|名为“%1”的自定义属性无效，因为已有一个同名的常用属性。 自定义属性不能与同一对象的常用属性同名。|  
|0xC0047035|-1073450955|DTS_E_BUFFERLOCKUNDERFLOW|缓冲区已解锁。|  
|0xC0047036|-1073450954|DTS_E_INDIVIDUALCACHEINTERFACESFAILED|%1 初始化失败，返回的错误代码为 0x%2!8.8X!。|  
|0xC0047037|-1073450953|DTS_E_INDIVIDUALRELEASEINTERFACESFAILED|%1 在关闭过程中失败，返回的错误代码为 0x%2!8.8X!。 某个组件无法释放其接口。|  
|0xC0047038|-1073450952|DTS_E_PRIMEOUTPUTFAILED|SSIS 错误代码 DTS_E_PRIMEOUTPUTFAILED。  %1 的 PrimeOutput 方法返回了错误代码 0x%2!8.8X!。  管道引擎调用 PrimeOutput() 时该组件返回了一个失败代码。 虽然该失败代码只与该组件有关，但这个错误是致命的，管道已停止执行。  可能在此之前已经发出错误消息，提供了有关失败的详细信息。|  
|0xC0047039|-1073450951|DTS_E_THREADCANCELLED|SSIS 错误代码 DTS_E_THREADCANCELLED。  线程“%1”接收到关闭信号，正在终止。 原因是用户请求了关闭，或另一线程中的错误导致该管道关闭。  可能在此之前已经发出错误消息，提供了有关取消线程的原因的详细信息。|  
|0xC004703A|-1073450950|DTS_E_DISTRIBUTORCANTSETPROPERTY|由于出现错误 0x%8.8X，线程“%1”的分发服务器无法初始化组件“%3”的属性“%2”。 该分发服务器无法初始化该组件的属性且无法继续运行。|  
|0xC004703B|-1073450949|DTS_E_CANTREGISTERVIEWBUFFERTYPE|数据流任务无法注册某个视图缓冲区类型。 该类型有 %1!d! 列，用于输入 ID %2!d!。|  
|0xC004703F|-1073450945|DTS_E_CANTCREATEEXECUTIONTREE|内存不足，无法创建执行树。|  
|0xC0047040|-1073450944|DTS_E_CANTINSERTINTOHASHTABLE|内存不足，无法将对象插入哈希表中。|  
|0xC0047041|-1073450943|DTS_E_OBJECTNOTINHASHTABLE|该对象不在哈希表中。|  
|0xC0047043|-1073450941|DTS_E_CANTCREATECOMPONENTVIEW|无法创建组件视图，因为已经有一个组件视图。 不能同时存在多个组件视图。|  
|0xC0047046|-1073450938|DTS_E_LAYOUTCANTSETUSAGETYPE|在输入“%1”(%2!d!)中，虚拟输入列集合未包含沿袭 ID 为 %3!d! 的虚拟输入列。|  
|0xC0047047|-1073450937|DTS_E_WRONGOBJECTTYPE|所请求的对象的对象类型不正确。|  
|0xC0047048|-1073450936|DTS_E_CANTCREATESPOOLFILE|缓冲区管理器无法按照 BufferTempStoragePath 属性中的任何路径创建临时存储文件。 原因可能是文件名错误，也可能是没有权限，或者路径已满。|  
|0xC0047049|-1073450935|DTS_E_SEEKFAILED|缓冲区管理器在文件“%2”中找不到偏移量 %1!d! 。 文件已被损坏。|  
|0xC004704A|-1073450934|DTS_E_EXTENDFAILED|缓冲区管理器无法将文件“%1”的长度扩展到 %2!lu! 个字节的结果值。  磁盘空间不足。|  
|0xC004704B|-1073450933|DTS_E_FILEWRITEFAILED|缓冲区管理器无法将 %1!d! 个字节。 磁盘空间不足或配额不足。|  
|0xC004704C|-1073450932|DTS_E_FILEREADFAILED|缓冲区管理器无法读取文件“%2”中的 %1!d! 个字节时遇到意外的文件结束。 文件已被损坏。|  
|0xC004704D|-1073450931|DTS_E_VIRTUALNOTSEQUENTIAL|缓冲区 ID %1!d! 支持其他虚拟缓冲区，但不能置于顺序模式。 IDTSBuffer100.SetSequentialMode 是对支持虚拟缓冲区的缓冲区调用的。|  
|0xC004704E|-1073450930|DTS_E_BUFFERISREADONLY|无法执行此操作，因为缓冲区为只读模式。 无法修改只读缓冲区。|  
|0xC004704F|-1073450929|DTS_E_EXECUTIONTREECYCLESETTINGID|不能将 ID %1!s! 设置为 %2!d!， 因为这会产生循环。|  
|0xC0047050|-1073450928|DTS_E_NOMOREBUFFERTYPES|缓冲区管理器在试图扩展缓冲区类型的表时用尽了内存。 这是由于内存不足造成的。|  
|0xC0047051|-1073450927|DTS_E_CANTCREATENEWTYPE|缓冲区管理器无法创建新的缓冲区类型。|  
|0xC0047053|-1073450925|DTS_E_SCHEDULERBADTREE|数据流引擎计划程序无法从布局中检索索引为 %1!d! 的对象。 该计划程序接收到的计数包含的执行树多于实际存在的执行树。|  
|0xC0047056|-1073450922|DTS_E_CANTCREATEPRIMEOUTPUTBUFFER|数据流任务创建缓冲区失败，因而无法通过对组件“%1”(%2!d!)调用 PrimeOutput 来获得输出“%3”(%4!d!)。 此错误通常是由于内存不足造成的。|  
|0xC0047057|-1073450921|DTS_E_SCHEDULERTHREADMEMORY|由于没有足够的内存，数据流引擎计划程序无法创建线程对象。 这是由于内存不足造成的。|  
|0xC004705A|-1073450918|DTS_E_SCHEDULEROBJECT|数据流引擎计划程序无法从布局中检索 ID 为 %1!d! 的对象。 数据流引擎计划程序先前找到的对象现已不再存在。|  
|0xC004705B|-1073450917|DTS_E_PREPARETREENODEFAILED|对于以“%1”(%2!d!)输出开始的执行树节点，数据流任务无法为其准备缓冲区。|  
|0xC004705C|-1073450916|DTS_E_CANTCREATEVIRTUALBUFFER|数据流任务无法创建虚拟缓冲区来为执行作准备。|  
|0xC004705E|-1073450914|DTS_E_NOMOREIDS|已经达到了最大 ID。 再没有 ID 可以分配给对象。|  
|0xC004705F|-1073450913|DTS_E_ALREADYATTACHED|已附加 %1，不能再次附加它。  请将其分离，然后重试。|  
|0xC0047060|-1073450912|DTS_E_OUTPUTCOLUMNNAMECONFLICT|列名“%1”与同步输入“%3”中的一个同名列冲突，因而不能用在输出“%2”中。|  
|0xC0047061|-1073450911|DTS_E_EOFANNOUNCEMENTFAILED|数据流任务无法创建缓冲区来标记行集的结尾。|  
|0xC0047062|-1073450910|DTS_E_USERCOMPONENTEXCEPTION|某个托管用户组件引发了异常“%1”。|  
|0xC0047063|-1073450909|DTS_E_SCHEDULERMEMORY|数据流引擎计划程序无法为执行结构分配足够的内存。 在开始执行之前系统内存不足。|  
|0xC0047064|-1073450908|DTS_E_BUFFERNOOBJECTMEMORY|内存不足，无法创建该缓冲区对象。|  
|0xC0047065|-1073450907|DTS_E_BUFFERNOMAPMEMORY|内存不足，无法将缓冲区的沿袭 ID 映射到 DTP_HCOL 索引。|  
|0xC0047066|-1073450906|DTS_E_INDIVIDUALPUTVARIABLESFAILED|“%1!s!” 无法缓存 Variables 集合，返回的错误代码为 0x%2!8.8X。|  
|0xC0047067|-1073450905|DTS_E_INDIVIDUALPUTCOMPONENTMETADATAFAILED|“%1”无法缓存组件元数据对象，返回的错误代码为 0x%2!8.8X!。|  
|0xC0047068|-1073450904|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITION|“%1”有一个非零 SortKeyPosition，但是其值(%2!ld!)太大。 该值必须小于等于列数。|  
|0xC004706A|-1073450902|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITIONS|%1 的 IsSorted 属性设置为 TRUE，但是非零输出列 SortKeyPositions 的绝对值没有形成一个以 1 开头的单调递增序列。|  
|0xC004706B|-1073450901|DTS_E_INDIVIDUALVALIDATIONSTATUSFAILED|“%1”验证失败，返回的验证状态为“%2”。|  
|0xC004706C|-1073450900|DTS_E_CANTCREATECOMPONENT|无法创建组件“%1!s!”， 返回了错误代码 0x%2!8.8X! “%3!s!”。 请确保该组件已正确注册。|  
|0xC004706D|-1073450899|DTS_E_COMPONENTNOTREGISTERED|包含“%1”的模块未正确注册或安装。|  
|0xC004706E|-1073450898|DTS_E_COMPONENTNOTFOUND|即使包含“%1”的模块已经注册，也找不到该模块。|  
|0xC004706F|-1073450897|DTS_E_BINARYCODENOTFOUND|根据配置，脚本组件应预编译该脚本，但找不到二进制代码。 请单击“设计脚本”按钮，使用脚本组件编辑器中的 IDE 来生成二进制代码。|  
|0xC0047070|-1073450896|DTS_E_CANTCREATEBLOBFILE|缓冲区管理器无法创建一个文件来假脱机 BLOBTempStoragePath 属性中指定的目录下的长对象。  原因可能是提供的文件名不正确、没有权限或者路径已满。|  
|0xC0047071|-1073450895|DTS_E_SYNCHRONOUSIDMISMATCH|“%1”的 SynchronousInputID 属性为 %2!d!，但应为 %3!d! 。|  
|0xC0047072|-1073450894|DTS_E_OBJECTIDNOTFOUND|不存在 ID 为 %1!d! 的对象。|  
|0xC0047073|-1073450893|DTS_E_OBJECTIDLOOKUPFAILED|找不到 ID 为 %1!d! 的对象， 因为错误代码为 0x%2!8.8X!。|  
|0xC0047074|-1073450892|DTS_E_INVALIDCODEPAGE|对输出列“%2”(%3!d!) 指定的代码页 %1!d! 无效。 请为输出列“%2”另选一个代码页。|  
|0xC0047075|-1073450891|DTS_E_INDIVIDUALPUTEVENTINFOSFAILED|“%1”无法缓存 EventInfos 集合，返回的错误代码为 0x%2!8.8X!。|  
|0xC0047077|-1073450889|DTS_E_DUPLICATEOUTPUTCOLUMNNAMES|“%1”的名称是一个重复名称。  所有名称都必须是唯一的。|  
|0xC0047078|-1073450888|DTS_E_NOOUTPUTCOLUMNFORINPUTCOLUMN|没有与输入列“%1”(%2!d!)关联的输出列。|  
|0xC0047079|-1073450887|DTS_E_EXCLGRPNOSYNCINP|“%1”有一个从根源扩展而来的虚拟缓冲区。 某个非零排除组的同步输入为零。|  
|0xC004707A|-1073450886|DTS_E_ERROROUTCANTBEONSYNCNONEXCLUSIVEOUTPUT|“%1”不能是错误输出，因为不能将错误输出放在同步的非排他输出中。|  
|0xC004707B|-1073450885|DTS_E_EXPREVALDIVBYZERO|出现被零除错误。 表达式“%1”的右侧操作数的值为零。|  
|0xC004707C|-1073450884|DTS_E_EXPREVALLITERALOVERFLOW|文本“%1”太大，在 %2 类型中容纳不下。 此文本的大小溢出了该类型。|  
|0xC004707D|-1073450883|DTS_E_EXPREVALBINARYOPNUMERICOVERFLOW|对数据类型 %2 和 %3 进行二元运算“%1”得到的结果超出了数值类型的最大大小。 若不降低精度或减少小数位数，就无法将操作数类型隐式转换为数值(DT_NUMERIC)结果。 若要执行此运算，需要使用转换运算符来显式转换两个操作数或其中的一个操作数。|  
|0xC004707E|-1073450882|DTS_E_EXPREVALBINARYOPOVERFLOW|二元运算“%1”的结果超出了结果数据类型“%2”的最大大小。 运算结果的大小溢出了结果类型。|  
|0xC004707F|-1073450881|DTS_E_EXPREVALFUNCTIONOVERFLOW|函数调用“%1”的结果太大，“%2”类型中容纳不下。 函数调用结果的大小溢出了该操作数的类型。 可能需要显式转换为较大的类型。|  
|0xC0047080|-1073450880|DTS_E_EXPREVALBINARYTYPEMISMATCH|数据类型“%1”和“%2”与二元运算符“%3”不兼容。 无法将操作数类型隐式转换为与此运算兼容的类型。 若要执行此运算，需要使用转换运算符来显式转换两个操作数或其中的一个操作数。|  
|0xC0047081|-1073450879|DTS_E_EXPREVALUNSUPPORTEDBINARYTYPE|数据类型“%1”不能用于二元运算符“%2”。 此运算不支持两个操作数的类型或其中一个操作数的类型。 若要执行此运算，需要使用转换运算符来显式转换两个操作数或其中的一个操作数。|  
|0xC0047082|-1073450878|DTS_E_EXPREVALBINARYSIGNMISMATCH|在运算“%2”中，位二元运算符“%1”存在符号不匹配的情况。 此运算符的两个操作数必须同时为正或同时为负。|  
|0xC0047083|-1073450877|DTS_E_EXPREVALBINARYOPERATIONFAILED|二元运算“%1”失败，错误代码为 0x%2!8.8X!。 可能出现了内部错误，或者内存不足。|  
|0xC0047084|-1073450876|DTS_E_EXPREVALBINARYOPERATIONSETTYPEFAILED|尝试设置二元运算“%1”的结果类型失败，错误代码为 0x%2!8.8X!。|  
|0xC0047085|-1073450875|DTS_E_EXPREVALSTRINGCOMPARISONFAILED|比较“%1”和字符串“%2”失败。|  
|0xC0047086|-1073450874|DTS_E_EXPREVALUNSUPPORTEDUNNARYTYPE|数据类型“%1”不能用于一元运算符“%2”。 此运算不支持此操作数类型。 若要执行此运算，需要使用转换运算符显式转换该操作数。|  
|0xC0047087|-1073450873|DTS_E_EXPREVALUNARYOPERATIONFAILED|二元运算“%1”失败，错误代码为 0x%2!8.8X!。 可能出现了内部错误，或者内存不足。|  
|0xC0047088|-1073450872|DTS_E_EXPREVALUNARYOPERATIONSETTYPEFAILED|尝试设置一元运算“%1”的结果类型失败，错误代码为 0x%2!8.8X!。|  
|0xC0047089|-1073450871|DTS_E_EXPREVALPARAMTYPEMISMATCH|对于参数 %3!d!，函数“%1”不支持数据类型“%2”。 无法将参数类型隐式转换为与该函数兼容的类型。 若要执行此运算，需要使用转换运算符显式转换该操作数。|  
|0xC004708A|-1073450870|DTS_E_EXPREVALINVALIDFUNCTION|无法识别函数“%1”。 函数名称不正确或者不存在。|  
|0xC004708B|-1073450869|DTS_E_EXPREVALFNSUBSTRINGINVALIDLENGTH|长度 %1!d! 对函数“%2”无效。 长度参数不能为负值。 请将长度参数更改为零或正数。|  
|0xC004708C|-1073450868|DTS_E_EXPREVALFNSUBSTRINGINVALIDSTARTINDEX|起始索引 %1!d! 对函数“%2”无效。 起始索引值必须是大于 0 的整数。 起始索引是从 1 开始的，而不是从 0 开始的。|  
|0xC004708E|-1073450866|DTS_E_EXPREVALCHARMAPPINGFAILED|函数“%1”无法对字符串“%2”执行字符映射。|  
|0xC004708F|-1073450865|DTS_E_EXPREVALINVALIDDATEPART|“%1”不是函数“%2”的有效日期部分。|  
|0xC0047090|-1073450864|DTS_E_EXPREVALINVALIDNULLPARAM|函数 NULL 中数据类型为“%2”的参数 %1!d! 无效。 NULL() 的参数必须是静态的，不能包含输入列之类的动态元素。|  
|0xC0047091|-1073450863|DTS_E_EXPREVALINVALIDNULLPARAMTYPE|函数 NULL 中数据类型为“%2”的参数 %1!d! 不是整数。 NULL() 的参数必须是整数或者可以转换为整数的类型。|  
|0xC0047092|-1073450862|DTS_E_EXPREVALFUNCTIONPARAMNOTSTATIC|函数 NULL 中数据类型为“%2”的参数 %1!d! 不是静态的。 此参数必须是静态的，不能包含输入列之类的动态元素。|  
|0xC0047093|-1073450861|DTS_E_EXPREVALINVALIDCASTPARAM|函数 NULL 中数据类型为“%2”的参数 %1!d! 无效。 转换运算符的参数必须是静态的，不能包含输入列之类的动态元素。|  
|0xC0047094|-1073450860|DTS_E_EXPREVALINVALIDCASTPARAMTYPE|函数 NULL 中数据类型为“%2”的参数 %1!d! 不是整数。 转换运算符的参数必须是整数或者可以转换为整数的类型。|  
|0xC0047095|-1073450859|DTS_E_EXPREVALINVALIDCAST|无法将表达式“%1”从数据类型“%2”转换成数据类型“%3”。 不支持所请求的转换。|  
|0xC0047096|-1073450858|DTS_E_EXPREVALINVALIDTOKEN|尝试分析表达式“%1”失败。  无法识别第“%3”行的第“%4”个字符处的标记“%2”。 该表达式在指定位置包含无效元素，无法对其进行分析。|  
|0xC0047097|-1073450857|DTS_E_EXPREVALUNEXPECTEDPARSEERROR|分析表达式“%1”时出错。 由于某种未知的原因，无法分析表达式。|  
|0xC0047098|-1073450856|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONWITHHR|尝试分析表达式“%1”失败，返回的错误代码为 0x%2!8.8X!。 无法分析该表达式。 原因可能是它包含无效元素或其格式不正确， 也可能是内存不足。|  
|0xC0047099|-1073450855|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSION|表达式“%1”无效，因而无法对其进行分析。 此表达式可能包含无效元素，也可能格式不正确。|  
|0xC004709A|-1073450854|DTS_E_EXPREVALEXPRESSIONEMPTY|没有要计算的表达式。 试图计算或获取一个空表达式的字符串。|  
|0xC004709B|-1073450853|DTS_E_EXPREVALCOMPUTEFAILED|尝试计算表达式“%1”失败，错误代码为 0x%2!8.8X!。|  
|0xC004709C|-1073450852|DTS_E_EXPREVALBUILDSTRINGFAILED|尝试生成表达式的字符串表示形式失败，错误代码为 0x%1!8.8X!。 未能生成表示表达式的可显示字符串。|  
|0xC004709D|-1073450851|DTS_E_EXPREVALCANNOTCONVERTRESULT|无法将表达式结果数据类型“%1”转换为列数据类型“%2”。 应将表达式的结果写入输入/输出列，但无法将表达式的数据类型转换为列的数据类型。|  
|0xC004709E|-1073450850|DTS_E_EXPREVALCONDITIONALOPINVALIDCONDITIONTYPE|条件运算符的条件表达式“%1”的数据类型“%2”无效。 此条件运算符的条件表达式必须返回一个类型为 DT_BOOL 的布尔值。|  
|0xC004709F|-1073450849|DTS_E_EXPREVALCONDITIONALOPTYPEMISMATCH|数据类型“%1”和“%2”与条件运算符不兼容。 不能将操作数类型隐式转换为与条件运算兼容的类型。 若要执行此运算，需要使用转换运算符来显式转换两个操作数或其中的一个操作数。|  
|0xC00470A0|-1073450848|DTS_E_EXPREVALCONDITIONALOPSETTYPEFAILED|尝试设置条件运算“%1”的结果类型失败，错误代码为 0x%2!8.8X!。|  
|0xC00470A1|-1073450847|DTS_E_BUFFERORPHANED|此缓冲区已被孤立。 缓冲区管理器已关闭，但还有一个未完成的缓冲区，而且不会对该缓冲区执行清除操作。 这可能会引起内存泄漏和其他问题。|  
|0xC00470A2|-1073450846|DTS_E_EXPREVALINPUTCOLUMNNAMENOTFOUND|尝试查找名为“%1”的输入列失败，错误代码为 0x%2!8.8X!。 在输入列集合中找不到指定的输入列。|  
|0xC00470A3|-1073450845|DTS_E_EXPREVALINPUTCOLUMNIDNOTFOUND|尝试查找沿袭 ID 为 %1!d! 的输入列失败， 错误代码为 0x%2!8.8X!。 在输入列集合中找不到此输入列。|  
|0xC00470A4|-1073450844|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNNAME|表达式包含无法识别的标记“%1”。 如果“%1”是变量，则应将其表示为“\@%1”。 此指定标记无效。 如果此标记应用作变量名，它的前缀应为 \@ 符号。|  
|0xC00470A5|-1073450843|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNID|表达式包含无法识别的标记“#%1!d!”。|  
|0xC00470A6|-1073450842|DTS_E_EXPREVALVARIABLENOTFOUND|在 Variables 集合中找不到变量“%1”。 此变量可能不在正确的作用域内。|  
|0xC00470A7|-1073450841|DTS_E_EXPREVALINVALIDTOKENSTATE|尝试分析表达式“%1”失败。 此表达式可能包含无效标记、不完整标记或无效元素， 可能格式不正确，也可能缺少某个必需元素的一部分(例如圆括号不成对)。|  
|0xC00470A8|-1073450840|DTS_E_BLANKOUTPUTCOLUMNNAME|“%1”的名称为空白，但名称不能为空白。|  
|0xC00470A9|-1073450839|DTS_E_HASSIDEEFFECTSWITHSYNCINP|“%1”的 HasSideEffects 属性设置为 TRUE，但“%1”是同步的，不能有副作用。 请将 HasSideEffects 属性设置为 FALSE。|  
|0xC00470AA|-1073450838|DTS_E_EXPREVALINVALIDCASTCODEPAGE|在向数据类型“%2”转换时，为转换运算的代码页参数指定的值 %1!d! 无效。 计算机上没有安装此代码页。|  
|0xC00470AB|-1073450837|DTS_E_EXPREVALINVALIDCASTPRECISION|值 %1!d! 在向数据类型“%2”转换时，为精度参数指定的值 %1!d! 无效。 精度必须在 %3!d! 到 %4!d! 范围内， 但该类型转换运算的精度值超出了此范围。|  
|0xC00470AC|-1073450836|DTS_E_EXPREVALINVALIDCASTSCALE|值 %1!d! 在向数据类型“%2”转换时，为小数位数参数指定的值 %1!d! 无效。 小数位数必须在 %3!d! 到 %4!d! 范围内， 但该类型转换运算的小数位数值超出了此范围。 小数位数不能超过指定的精度且必须为正值。|  
|0xC00470AD|-1073450835|DTS_E_NONSORTEDOUTPUTHASSORTKEYPOSITIONS|“%1”的 IsSorted 属性为 False，但其输出列的 SortKeyPositions 的 %2!lu! 为非零值。|  
|0xC00470AF|-1073450833|DTS_E_EXPREVALCONDITIONALOPCODEPAGEMISMATCH|对于 %2 类型的条件运算“%1”的操作数，它们的代码页必须匹配。 左操作数的代码页与右操作数的代码页不匹配。 对于指定类型的条件运算符，代码页必须相同。|  
|0xC00470B1|-1073450831|DTS_E_REFERENCEDMETADATABADCOUNT|输入“%1”(%2!d!)引用了输入“%3”(%4!d!)，但是它们的列数不相同。 输入 %5!d! 有 %6!d! 列，而输入 %7!d! 有 %8!d! 列。|  
|0xC00470B2|-1073450830|DTS_E_OBJECTLINEAGEIDNOTFOUND|不存在沿袭 ID 为 %1!d! 的对象。|  
|0xC00470B3|-1073450829|DTS_E_FILENAMEOUTPUTCOLUMNOTFOUND|找不到此文件名的输出列。|  
|0xC00470B4|-1073450828|DTS_E_FILENAMEOUTPUTCOLUMNINVALIDDATATYPE|此文件名的输出列不是 Null 结束的 Unicode 字符串，其数据类型为 DT_WSTR。|  
|0xC00470B5|-1073450827|DTS_E_DISTRIBUTORADDFAILED|由于出现错误 0x%2!8.8X!，分发服务器无法为线程“%1”提供缓冲区。 此目标线程可能正在关闭。|  
|0xC00470B6|-1073450826|DTS_E_LOCALENOTINSTALLED|此系统中没有安装 LocaleID %1!ld! 。|  
|0xC00470B7|-1073450825|DTS_E_EXPREVALILLEGALHEXESCAPEINSTRINGLITERAL|字符串文字“%1”包含非法的十六进制转义序列“\x%2”。 表达式计算器中的字符串文字不支持此转义序列。 十六进制转义序列的格式必须是 \xhhhh，其中 h 是有效的十六进制数字。|  
|0xC00470B8|-1073450824|DTS_E_EXPREVALILLEGALESCAPEINSTRINGLITERAL|The string literal "%1" contains an illegal escape sequence of "\\%2!c!". The escape sequence is not supported in string literals in the expression evaluator. If a backslash is needed in the string, use a double backslash, "\\\\".|  
|0xC00470B9|-1073450823|DTS_E_NOOUTPUTCOLUMNS|"%1" contains no output columns. An asynchronous output must contain output columns.|  
|0xC00470BA|-1073450822|DTS_E_LOBDATATYPENOTSUPPORTED|The "%1" has a long object data type of DT_TEXT, DT_NTEXT, or DT_IMAGE, which is not supported.|  
|0xC00470BB|-1073450821|DTS_E_OUTPUTWITHMULTIPLEERRORS|Output ID %1!d! was given multiple error output configurations. First %2!d! and %3!d!, then %4!d! and %5!d!.|  
|0xC00470BC|-1073450820|DTS_E_FAILEDDURINGOLEDBDATATYPECONVERSIONCHECK|The OLE DB provider failed during the data type conversion verification for "%1".|  
|0xC00470BD|-1073450819|DTS_E_BUFFERISEOR|This buffer represents the end of the rowset and its row count cannot be altered.  An attempt was made to call AddRow or RemoveRow on a buffer that has the end of rowset flag.|  
|0xC00470BE|-1073450818|DTS_E_EXPREVALUNSUPPORTEDTYPE|The data type "%1" is not supported in an expression. The specified type is not supported or is not valid.|  
|0xC00470BF|-1073450817|DTS_E_PRIMEOUTPUTNOEOR|The PrimeOutput method on "%1" returned success, but did not report an end of the rowset. There is an error in the component. It should have reported an end-of-row. The pipeline will shut down execution to avoid unpredictable results.|  
|0xC00470C0|-1073450816|DTS_E_EXPREVALDATACONVERSIONOVERFLOW|An overflow occurred while converting from data type "%1" to data type "%2". The source type is too large for the destination type.|  
|0xC00470C1|-1073450815|DTS_E_EXPREVALDATACONVERSIONNOTSUPPORTED|Conversion from data type "%1" to data type "%2" is unsupported. The source type cannot be converted to the destination type.|  
|0xC00470C2|-1073450814|DTS_E_EXPREVALDATACONVERSIONFAILED|Error code 0x%1!8.8X! occurred attempting to convert from data type %2 to data type %3.|  
|0xC00470C3|-1073450813|DTS_E_EXPREVALCONDITIONALOPERATIONFAILED|The conditional operation "%1" failed with error code 0x%2!8.8X!. There was an internal error or an out-of-memory error.|  
|0xC00470C4|-1073450812|DTS_E_EXPREVALCASTFAILED|Casting expression "%1" from data type "%2" to data type "%3" failed with error code 0x%4!8.8X!.|  
|0xC00470C5|-1073450811|DTS_E_EXPREVALFUNCTIONCOMPUTEFAILED|Evaluating function "%1" failed with error code 0x%2!8.8X!.|  
|0xC00470C6|-1073450810|DTS_E_EXPREVALFUNCTIONCONVERTPARAMTOMEMBERFAILED|Parameter number %1!d! of the function "%2" cannot be converted to a static value.|  
|0xC00470C7|-1073450809|DTS_E_REDIRECTROWUNAVAILABLEWITHFASTLOADANDZEROMAXINSERTCOMMITSIZE|The error row disposition on "%1" cannot be set to redirect the row when the fast load option is turned on, and the maximum insert commit size is set to zero.|  
|0xC00470CE|-1073450802|DTS_E_EXPREVALBINARYOPERATORCODEPAGEMISMATCH|The code pages for operands of binary operator "%1" for type "%2" must match. Currently, the code page of the left operand does not match the code page of the right operand. For the specified binary operator on the specified type, the code pages must be the same.|  
|0xC00470CF|-1073450801|DTS_E_EXPREVALVARIABLECOMPUTEFAILED|Retrieving the value of Variable "%1" failed with error code 0x%2!8.8X!.|  
|0xC00470D0|-1073450800|DTS_E_EXPREVALVARIABLETYPENOTSUPPORTED|The data type of variable "%1" is not supported in an expression.|  
|0xC00470D1|-1073450799|DTS_E_EXPREVALCASTCODEPAGEMISMATCH|Unable to cast expression "%1" from data type "%2" to data type "%3" because the code page of the value being cast (%4!d!) does not match the requested result code page (%5!d!). The code page of the source must match the code page requested for the destination.|  
|0xC00470D2|-1073450798|DTS_E_BUFFERSIZEOUTOFRANGE|The default buffer size must be between %1!d! and %2!d! bytes. An attempt was made to set the DefaultBufferSize property to a value that is too small or too large.|  
|0xC00470D3|-1073450797|DTS_E_BUFFERMAXROWSIZEOUTOFRANGE|The default buffer maximum rows must be larger than %1!d! rows. An attempt was made to set the DefaultBufferMaxRows property to a value that is too small.|  
|0xC00470D4|-1073450796|DTS_E_EXTERNALCOLUMNMETADATACODEPAGEMISMATCH|The code page on %1 is %2!d! and is required to be %3!d!.|  
|0xC00470D5|-1073450795|DTS_E_THREADCOUNTOUTOFRANGE|Failed to assign %3!d! to the EngineThreads property of the Data Flow task. The value must be between %1!d! and %2!d!.|  
|0xC00470D6|-1073450794|DTS_E_EXPREVALINVALIDTOKENSINGLEQUOTE|Parsing the expression "%1" failed. The single quotation mark at line number "%2", character number "%3", was not expected.|  
|0xC00470D7|-1073450793|DTS_E_EXPREVALINVALIDTOKENSINGLEEQUAL|Parsing the expression "%1" failed. The equal sign (=) at line number "%2", character number "%3", was not expected. A double equals sign (==) may be required at the location specified.|  
|0xC00470DA|-1073450790|DTS_E_INDIVIDUALPUTREFTRACKERFAILED|Component "%1" failed to cache the runtime object reference tracker collection and returned error code 0x%2!8.8X!.|  
|0xC00470DB|-1073450789|DTS_E_EXPREVALAMBIGUOUSINPUTCOLUMNNAME|There are multiple input columns with the name "%1". The desired input column must be specified uniquely as [Component Name].[%2] or referenced by lineage ID. Currently, the input column specified exists on more than one component.|  
|0xC00470DC|-1073450788|DTS_E_EXPREVALDOTTEDINPUTCOLUMNNAMENOTFOUND|Locating the input column named "[%1].[%2]" failed with error code 0x%3!8.8X!. The input column was not found in the input column collection.|  
|0xC00470DD|-1073450787|DTS_E_EXPREVALAMBIGUOUSVARIABLENNAME|There are multiple variables with the name "%1". The desired variable must be specified uniquely as \@[Namespace::%2]. The variable exists in more than one namespace.|  
|0xC00470DE|-1073450786|DTS_E_REDUCTIONFAILED|The Data Flow engine scheduler failed to reduce the execution plan for the pipeline. Set the OptimizedMode property to false.|  
|0xC00470DF|-1073450785|DTS_E_EXPREVALSQRTINVALIDPARAM|The function SQRT cannot operate on negative values, and a negative value was passed to the SQRT function.|  
|0xC00470E0|-1073450784|DTS_E_EXPREVALLNINVALIDPARAM|The function LN cannot operate on zero or negative values, and a zero or negative value was passed to the LN function.|  
|0xC00470E1|-1073450783|DTS_E_EXPREVALLOGINVALIDPARAM|The function LOG cannot operate on zero or negative values, and a zero or negative value was passed to the LOG function.|  
|0xC00470E2|-1073450782|DTS_E_EXPREVALPOWERINVALIDPARAM|The parameters passed to the function POWER cannot be evaluated and yield an indeterminate result.|  
|0xC00470E3|-1073450781|DTS_E_NOCANCELEVENT|The runtime cannot provide a cancel event because of error 0x%1!8.8X!.|  
|0xC00470E4|-1073450780|DTS_E_CANCELRECEIVED|The pipeline received a request to cancel and is shutting down.|  
|0xC00470E5|-1073450779|DTS_E_EXPREVALUNARYOPOVERFLOW|The result of the unary minus (negation) operation "%1" exceeds the maximum size for result data type "%2". The magnitude of the result of the operation overflows the type of the result.|  
|0xC00470E6|-1073450778|DTS_E_EXPREVALPLACEHOLDERINEXPRESSION|The placeholder "%1" was found in an expression. This must be replaced with an actual parameter or operand.|  
|0xC00470E7|-1073450777|DTS_E_EXPREVALFNRIGHTINVALIDLENGTH|The length %1!d! specified for function "%2" is negative, and is not valid. The length parameter must be positive.|  
|0xC00470E8|-1073450776|DTS_E_EXPREVALFNREPLICATEINVALIDREPEATCOUNT|The repeat count %1!d! is negative and is not valid for function "%2". The repeat count parameter cannot be negative.|  
|0xC00470EA|-1073450774|DTS_E_EXPREVALVARIABLECOULDNOTBEREAD|Reading the variable "%1" failed with error code 0x%2!8.8X!.|  
|0xC00470EC|-1073450772|DTS_E_EXPREVALBINARYOPDTSTRNOTSUPPORTED|For operands of a binary operation, the data type DT_STR is supported only for input columns and cast operations. The expression "%1" has a DT_STR operand that is not an input column or the result of a cast, and cannot be used in a binary operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC00470ED|-1073450771|DTS_E_EXPREVALCONDITIONALOPDTSTRNOTSUPPORTED|For operands of the conditional operator, the data type DT_STR is supported only for input columns and cast operations. The expression "%1" has a DT_STR operand that is not an input column or the result of a cast, and cannot be used with the conditional operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC00470EE|-1073450770|DTS_E_EXPREVALFNFINDSTRINGINVALIDOCCURRENCECOUNT|The occurrence count %1!d! is not valid for function "%2". This parameter must be greater than zero.|  
|0xC00470EF|-1073450769|DTS_E_INDIVIDUALPUTLOGENTRYINFOS|"%1" failed to cache the LogEntryInfos collection and returned error code 0x%2!8.8X!.|  
|0xC00470F0|-1073450768|DTS_E_EXPREVALINVALIDDATEPARTNODE|The date part parameter specified for function "%1" is not valid. It must be a static string.  The date part parameter cannot contain dynamic elements, such as input columns, and must be of type DT_WSTR.|  
|0xC00470F1|-1073450767|DTS_E_EXPREVALINVALIDCASTLENGTH|The value %1!d! specified for the length parameter of the cast to data type %2 is negative and not valid. The length must be positive.|  
|0xC00470F2|-1073450766|DTS_E_EXPREVALINVALIDNULLCODEPAGE|The value %1!d! specified for the code page parameter of the NULL function with data type "%2" is not valid. The code page is not installed on the computer.|  
|0xC00470F3|-1073450765|DTS_E_EXPREVALINVALIDNULLPRECISION|The value %1!d! specified for the precision parameter of the NULL function with data type "%2" is out of range. Precision must be in the range %3!d! to %4!d!.|  
|0xC00470F4|-1073450764|DTS_E_EXPREVALINVALIDNULLSCALE|The value %1!d! specified for the scale parameter of the NULL function with data type %2 is out of range. Scale must be in the range %3!d! to %4!d!. Scale must not exceed precision and must not be negative.|  
|0xC00470F5|-1073450763|DTS_E_EXPREVALINVALIDNULLLENGTH|The value %1!d! specified for the length parameter of the "NULL" function with data type %2 is negative and not valid. The length must be positive.|  
|0xC00470F6|-1073450762|DTS_E_NEGATIVESNOTALLOWED|The %1 can't be assigned a negative value.|  
|0xC00470F7|-1073450761|DTS_E_FASTPARSENOTALLOWED|The "%1" custom property for "%2" cannot be set to true.  The column data type must be one of the following:  DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4, DT_UI8, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAMPOFFSET, DT_DATE, DT_DBDATE, DT_DBTIME, DT_DBTIME2, or DT_FILETIME.|  
|0xC00470F8|-1073450760|DTS_E_CANNOTREATTACHPATH|The "%1" cannot be reattached. Delete the path, add a new one, and attach it.|  
|0xC00470F9|-1073450759|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALSINGULAR|The function "%1" requires %2!d! parameters, not %3!d! parameter. The function name was recognized, but the number of parameters is not valid.|  
|0xC00470FA|-1073450758|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSSINGULARPLURAL|The function "%1" requires %2!d! parameter, not %3!d! parameters. The function name was recognized, but the number of parameters is not valid.|  
|0xC00470FB|-1073450757|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALPLURAL|The function "%1" requires %2!d! parameters, not %3!d! parameters. The function name was recognized, but the number of parameters is not valid.|  
|0xC00470FC|-1073450756|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONOUTOFMEMORY|Attempt to parse the expression "%1" failed because there was an out-of-memory error.|  
|0xC00470FD|-1073450755|DTS_E_INDIVIDUALCHECKPRODUCTLEVELFAILED|The %1 failed to be able to perform its required product level check and returned error code 0x%2!8.8X!.|  
|0xC00470FE|-1073450754|DTS_E_PRODUCTLEVELTOLOW|SSIS Error Code DTS_E_PRODUCTLEVELTOLOW.  The %1 cannot run on installed %2 of Integration Services. It requires %3 or higher.|  
|0xC00470FF|-1073450753|DTS_E_EXPREVALSTRINGLITERALTOOLONG|A string literal in the expression exceeds the maximum allowed length of %1!d! characters.|  
|0xC0047100|-1073450752|DTS_E_EXPREVALSTRINGVARIABLETOOLONG|The variable %1 contains a string that exceeds the maximum allowed length of %2!d! characters.|  
|0xC0047101|-1073450751|DTS_E_COMPONENT_NOINTERFACE|The %1 was found, but it does not support a required Integration Services interface (IDTSRuntimeComponent100).  Obtain an updated version of this component from the component provider.|  
|0xC0048000|-1073446912|DTS_E_CANNOTOPENREGISTRYKEY|The registry key "%1" cannot be opened.|  
|0xC0048001|-1073446911|DTS_E_INVALIDCOMPONENTFILENAME|Cannot get the file name for the component with a CLSID of "%1". Verify that the component is registered properly or that the CLSID provided is correct.|  
|0xC0048002|-1073446910|DTS_E_UNKNOWNCOMPONENTHASINVALIDCLSID|The CLSID for one of the components is not valid. Verify that all the components in the pipeline have valid CLSIDs.|  
|0xC0048003|-1073446909|DTS_E_COMPONENTHASINVALIDCLSID|The CLSID for one of the components with ID %1!d! is not valid.|  
|0xC0048004|-1073446908|DTS_E_INVALIDINDEX|The index is not valid.|  
|0xC0048005|-1073446907|DTS_E_CANNOTACCESSDTSAPPLICATIONOBJECT|The Application object cannot be accessed. Verify that SSIS is correctly installed.|  
|0xC0048006|-1073446906|DTS_E_ERROROCCURREDWHILERETRIEVINGFILENAME|Retrieving the file name for a component failed with error code 0x%1!8.8X!.|  
|0xC0048007|-1073446905|DTS_E_CANNOTRETRIEVEPROPERTYFORCOMPONENT|Cannot retrieve property "%1" from component with ID %2!d!.|  
|0xC0048008|-1073446904|DTS_E_DUPLICATEIDFOUND|Attempting to use ID %1!d! more than once in the Data Flow Task.|  
|0xC0048009|-1073446903|DTS_E_CANNOTRETRIEVEBYLINEAGE|Cannot retrieve an item by lineage ID from a collection that does not contain columns.|  
|0xC004800B|-1073446901|DTS_E_CANNOTMAPRUNTIMECONNECTIONMANAGER|Cannot find the connection manager with ID "%1" in the connection manager collection due to error code 0x%2!8.8X!. That connection manager is needed by "%3" in the connection manager collection of "%4". Verify that a connection manager in the connection manager collection, Connections, has been created with that ID.|  
|0xC004800E|-1073446898|DTS_E_INPUTNOTKNOWN|Thread "%1" received a buffer for input %2!d!, but this thread is not responsible for that input. An error occurred, causing the Data Flow engine scheduler to build a bad execution plan.|  
|0xC004800F|-1073446897|DTS_E_GETRTINTERFACEFAILED|The component "%1" (%2!d!) cannot provide an IDTSRuntimeComponent100 interface.|  
|0xC0048011|-1073446895|DTS_E_CANTGIVEAWAYBUFFER|The Data Flow task engine attempted to copy a buffer to assign another thread, but failed.|  
|0xC0048012|-1073446894|DTS_E_CANTCREATEVIEWBUFFER|The Data Flow task engine failed to create a view buffer of type %1!d! over type %2!d! for buffer %3!d.|  
|0xC0048013|-1073446893|DTS_E_UNUSABLETEMPORARYPATH|The buffer manager could not create a temporary file on the path "%1". The path will not be considered for temporary storage again.|  
|0xC0048014|-1073446892|DTS_E_DIRECTTONONERROROUTPUT|The buffer manager attempted to push an error row to an output that was not registered as an error output. There was a call to DirectErrorRow on an output that does not have the IsErrorOut property set to TRUE.|  
|0xC0048015|-1073446891|DTS_E_BUFFERISPRIVATE|A call was made to a buffer method on a private buffer and private buffers do not support this operation.|  
|0xC0048016|-1073446890|DTS_E_BUFFERISFLAT|Private mode buffers do not support this operation.|  
|0xC0048017|-1073446889|DTS_E_BUFFERISPRIMEOUTPUT|This operation cannot be called on a buffer passed to PrimeOutput. A call was made to a buffer method during PrimeOutput, but that call is not allowed during PrimeOutput.|  
|0xC0048018|-1073446888|DTS_E_BUFFERISPROCESSINPUT|This operation cannot be called on a buffer passed to ProcessInput. A call was made to a buffer method during ProcessInput, but that call is not allowed during ProcessInput.|  
|0xC0048019|-1073446887|DTS_E_BUFFERGETTEMPFILENAME|The buffer manager could not get a temporary file name.|  
|0xC004801A|-1073446886|DTS_E_REFERENCECOLUMNTOOWIDE|The code encountered a column that was too wide.|  
|0xC004801B|-1073446885|DTS_E_CANNOTGETRUNTIMECONNECTIONMANAGERID|Cannot get the ID of the runtime connection manager specified by "%1" in the connection manager collection, Connections, of "%2" due to error code 0x%3!8.8X!. Verify that the ConnectionManager.ID property of the runtime connection object has been set for the component.|  
|0xC004801C|-1073446884|DTS_E_EMPTYRUNTIMECONNECTIONMANAGERID|The "%1" in the connection manager collection, Connections, of "%2" does not have a value for the ID property. Verify that the ConnectionManagerID property of the runtime connection object has been set for the component.|  
|0xC004801D|-1073446883|DTS_E_METADATAREADONLY|Metadata cannot be changed during execution.|  
|0xC004801F|-1073446881|DTS_E_UPGRADEFAILED|The component metadata for "%1" could not be upgraded to the newer version of the component. The PerformUpgrade method failed.|  
|0xC0048020|-1073446880|DTS_E_COMPONENTVERSIONMISMATCH|The version of %1 is not compatible with this version of the DataFlow.|  
|0xC0048021|-1073446879|DTS_E_ERRORCOMPONENT|The component is missing, not registered, not upgradeable, or missing required interfaces. The contact information for this component is "%1".|  
|0xC0048022|-1073446878|DTS_E_BUFFERISNOTPRIMEOUTPUT|The method was called on the wrong buffer. Buffers that are not used for component output do not support this operation.|  
|0xC0049014|-1073442796|DTS_E_EXPREVALSTATIC_COMPUTATIONFAILED|An error occurred during computation of the expression.|  
|0xC0049030|-1073442768|DTS_E_EXPREVALSTATIC_DIVBYZERO|Division by zero occurred in the expression.|  
|0xC0049031|-1073442767|DTS_E_EXPREVALSTATIC_LITERALOVERFLOW|The magnitude of the literal value was too big to fit in the type requested.|  
|0xC0049032|-1073442766|DTS_E_EXPREVALSTATIC_BINARYOPNUMERICOVERFLOW|The result of a binary operation was too big for the maximum size for numeric types. The operand types could not be implicitly cast into a numeric (DT_NUMERIC) result without loss of precision or scale. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0049033|-1073442765|DTS_E_EXPREVALSTATIC_BINARYOPOVERFLOW|The magnitude of the result of a binary operation overflows the maximum size for result data type.|  
|0xC0049034|-1073442764|DTS_E_EXPREVALSTATIC_FUNCTIONOVERFLOW|The magnitude of the result of a function call was too big to fit in the result type, and overflowed the type of the operand. An explicit cast to a larger type may be required.|  
|0xC0049035|-1073442763|DTS_E_EXPREVALSTATIC_BINARYTYPEMISMATCH|Incompatible data types were used with a binary operator. The operand types could not be implicitly cast into compatible types for the operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0049036|-1073442762|DTS_E_EXPREVALSTATIC_UNSUPPORTEDBINARYTYPE|An unsupported data type was used with a binary operator. The type of one, or both, of the operands is not supported for the operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0049037|-1073442761|DTS_E_EXPREVALSTATIC_BINARYSIGNMISMATCH|There is a sign mismatch for the bitwise binary operator. The operands for this operator must be both positive or both negative.|  
|0xC0049038|-1073442760|DTS_E_EXPREVALSTATIC_BINARYOPERATIONFAILED|A binary operation failed. There was an out-of-memory condition, or an internal error occurred.|  
|0xC0049039|-1073442759|DTS_E_EXPREVALSTATIC_BINARYOPERATIONSETTYPEFAILED|Setting the result type of a binary operation failed.|  
|0xC004903A|-1073442758|DTS_E_EXPREVALSTATIC_STRINGCOMPARISONFAILED|Cannot compare two strings.|  
|0xC004903B|-1073442757|DTS_E_EXPREVALSTATIC_UNSUPPORTEDUNNARYTYPE|An unsupported data type is used with a unary operator. The operand type is not supported for the operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC004903C|-1073442756|DTS_E_EXPREVALSTATIC_UNARYOPERATIONFAILED|A unary operation failed. An out-of-memory condition occurred, or there was an internal error.|  
|0xC004903D|-1073442755|DTS_E_EXPREVALSTATIC_UNARYOPERATIONSETTYPEFAILED|Setting the result type of a unary operation failed.|  
|0xC004903E|-1073442754|DTS_E_EXPREVALSTATIC_PARAMTYPEMISMATCH|A function has a parameter with an unsupported data type. The type of the parameter cannot be implicitly cast into a compatible type for the function. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC004903F|-1073442753|DTS_E_EXPREVALSTATIC_INVALIDFUNCTION|An invalid function name appeared in the expression. Verify that the function name is correct and does exist.|  
|0xC0049040|-1073442752|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDLENGTH|The length parameter was not valid for function SUBSTRING. The length parameter cannot be negative.|  
|0xC0049041|-1073442751|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDSTARTINDEX|The start index was not valid for function SUBSTRING. The start index value must be an integer greater than zero. The start index is 1-based, not 0-based.|  
|0xC0049042|-1073442750|DTS_E_EXPREVALSTATIC_INVALIDNUMBEROFPARAMS|An incorrect number of parameters was given to a function. The function name was recognized, but the number of parameters was not correct.|  
|0xC0049043|-1073442749|DTS_E_EXPREVALSTATIC_CHARMAPPINGFAILED|A character mapping function failed.|  
|0xC0049044|-1073442748|DTS_E_EXPREVALSTATIC_INVALIDDATEPART|An unrecognized date part parameter was specified for a date function.|  
|0xC0049045|-1073442747|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAM|An invalid parameter was given for function NULL. The parameters of NULL must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0049046|-1073442746|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAMTYPE|An invalid parameter was given for function NULL. A parameter of NULL must be an integer, or a type that can be converted to an integer.|  
|0xC0049047|-1073442745|DTS_E_EXPREVALSTATIC_FUNCTIONPARAMNOTSTATIC|An invalid parameter was given for a function. This parameter must be static and cannot contain dynamic elements such as input columns.|  
|0xC0049048|-1073442744|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAM|An invalid parameter was given for a cast operation. Parameters of cast operators must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0049049|-1073442743|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAMTYPE|An invalid parameter was given for a cast operation. A parameter of a cast operator must be an integer, or a type that can be converted to an integer.|  
|0xC004904A|-1073442742|DTS_E_EXPREVALSTATIC_INVALIDCAST|The expression contained an unsupported type cast.|  
|0xC004904B|-1073442741|DTS_E_EXPREVALSTATIC_INVALIDTOKEN|The expression contained a token that was not recognized. The expression could not be parsed because it contains invalid elements.|  
|0xC004904C|-1073442740|DTS_E_EXPREVALSTATIC_FAILEDTOPARSEEXPRESSION|The expression is not valid and could not be parsed. It might contain invalid elements, or it might not be well-formed.|  
|0xC004904D|-1073442739|DTS_E_EXPREVALSTATIC_UNARYOPOVERFLOW|The result of a unary minus (negation) operation overflowed the maximum size for result data type. The magnitude of the result of the operation overflows the type of the result.|  
|0xC004904E|-1073442738|DTS_E_EXPREVALSTATIC_COMPUTEFAILED|Attempt to compute the expression failed.|  
|0xC004904F|-1073442737|DTS_E_EXPREVALSTATIC_BUILDSTRINGFAILED|Attempt to generate a string representation of the expression failed.|  
|0xC0049050|-1073442736|DTS_E_EXPREVALSTATIC_CANNOTCONVERTRESULT|Cannot convert the expression result data type to the column data type. The result of the expression should be written to an input/output column, but the data type of the expression cannot be converted to the data type of the column.|  
|0xC0049051|-1073442735|DTS_E_EXPREVALSTATIC_CONDITIONALOPINVALIDCONDITIONTYPE|The conditional expression of the conditional operator has invalid data type. The conditional expression must be of type DT_BOOL.|  
|0xC0049052|-1073442734|DTS_E_EXPREVALSTATIC_CONDITIONALOPTYPEMISMATCH|The data types of the operands of the conditional operator were incompatible. The operand types could not be implicitly cast into compatible types for the conditional operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0049053|-1073442733|DTS_E_EXPREVALSTATIC_CONDITIONALOPSETTYPEFAILED|Setting the result type of a conditional operation failed.|  
|0xC0049054|-1073442732|DTS_E_EXPREVALSTATIC_INPUTCOLUMNNAMENOTFOUND|The input column specified was not found in the input column collection.|  
|0xC0049055|-1073442731|DTS_E_EXPREVALSTATIC_INPUTCOLUMNIDNOTFOUND|Attempt to find an input column by lineage ID failed. The input column was not found in the input column collection.|  
|0xC0049056|-1073442730|DTS_E_EXPREVALSTATIC_NOINPUTCOLUMNCOLLECTION|The expression contains an unrecognized token that appears to be an input column reference, but the input column collection is not available to process input columns. The input column collection has not been provided to the expression evaluator, but an input column was included in the expression.|  
|0xC0049057|-1073442729|DTS_E_EXPREVALSTATIC_VARIABLENOTFOUND|A variable specified was not found in the collection. It might not exist in the correct scope. Verify that the variable exists and that the scope is correct.|  
|0xC0049058|-1073442728|DTS_E_EXPREVALSTATIC_INVALIDTOKENSTATE|Attempt to parse the expression failed. The expression contains an invalid or incomplete token. It may contain invalid elements, be missing part of a required element such as closing parentheses, or may not be well formed.|  
|0xC0049059|-1073442727|DTS_E_EXPREVALSTATIC_INVALIDCASTCODEPAGE|The value specified for the code page parameter of the cast to data type DT_STR or DT_TEXT is not valid. The specified code page is not installed on the computer.|  
|0xC004905A|-1073442726|DTS_E_EXPREVALSTATIC_INVALIDCASTPRECISION|The value specified for the precision parameter of a cast operation is out of range for the type cast.|  
|0xC004905B|-1073442725|DTS_E_EXPREVALSTATIC_INVALIDCASTSCALE|The value specified for the scale parameter of a cast operation is out of range for the type cast. Scale must not exceed precision and must not be negative.|  
|0xC004905C|-1073442724|DTS_E_EXPREVALSTATIC_CONDITIONALOPCODEPAGEMISMATCH|The code pages do not match in a conditional operation. The code page of the left operand does not match the code page of the right operand. For the conditional operator of that type, the code pages must be the same.|  
|0xC004905D|-1073442723|DTS_E_EXPREVALSTATIC_ILLEGALHEXESCAPEINSTRINGLITERAL|A string literal contains an illegal hexadecimal escape sequence. The escape sequence is not supported in string literals in the expression evaluator. Hexadecimal escape sequences must be of the form \xhhhh where h is a valid hexadecimal digit.|  
|0xC004905E|-1073442722|DTS_E_EXPREVALSTATIC_ILLEGALESCAPEINSTRINGLITERAL|The string literal contains an illegal escape sequence. The escape sequence is not supported in string literals in the expression evaluator. If a backslash is needed in the string, format it as a double backslash, "\\\\".|  
|0xC004905F|-1073442721|DTS_E_EXPREVALSTATIC_UNSUPPORTEDTYPE|An unsupported or unrecognized data type was used in the expression.|  
|0xC0049060|-1073442720|DTS_E_EXPREVALSTATIC_DATACONVERSIONOVERFLOW|An overflow occurred while converting between data types. The source type is too large to fit in the destination type.|  
|0xC0049061|-1073442719|DTS_E_EXPREVALSTATIC_DATACONVERSIONNOTSUPPORTED|The expression contains an unsupported data type conversion. The source type cannot be converted to the destination type.|  
|0xC0049062|-1073442718|DTS_E_EXPREVALSTATIC_DATACONVERSIONFAILED|An error occurred while attempting to perform data conversion. The source type could not be converted to the destination type.|  
|0xC0049063|-1073442717|DTS_E_EXPREVALSTATIC_CONDITIONALOPERATIONFAILED|The conditional operation failed.|  
|0xC0049064|-1073442716|DTS_E_EXPREVALSTATIC_CASTFAILED|An error occurred while attempting to perform a type cast.|  
|0xC0049065|-1073442715|DTS_E_EXPREVALFAILEDTOCONVERTSTRCOLUMNTOWSTR|Converting "%1" from type DT_STR to type DT_WSTR failed with error code 0x%2!8.8X!. An error occurred while performing the implicit conversion on the input column.|  
|0xC0049066|-1073442714|DTS_E_EXPREVALSTATIC_FAILEDTOCONVERTSTRCOLUMNTOWSTR|Converting an input column from type DT_STR to type DT_WSTR failed. An error occurred while performing the  implicit conversion on the input column.|  
|0xC0049067|-1073442713|DTS_E_EXPREVALSTATIC_FUNCTIONCOMPUTEFAILED|An error occurred while evaluating the function.|  
|0xC0049068|-1073442712|DTS_E_EXPREVALSTATIC_FUNCTIONCONVERTPARAMTOMEMBERFAILED|A function parameter cannot be converted to a static value. The parameter must be static and cannot contain dynamic elements such as input columns.|  
|0xC0049088|-1073442680|DTS_E_EXPREVALSTATIC_FNRIGHTINVALIDLENGTH|The length parameter is not valid for function RIGHT. The length parameter cannot be negative.|  
|0xC0049089|-1073442679|DTS_E_EXPREVALSTATIC_FNREPLICATEINVALIDREPEATCOUNT|The repeat count parameter is not valid for function REPLICATE. This parameter cannot be negative.|  
|0xC0049096|-1073442666|DTS_E_EXPREVALSTATIC_BINARYOPERATORCODEPAGEMISMATCH|The code pages do not match in a binary operation. The code page of the left operand does not match the code page of the right operand. For this binary operation, the code pages must be the same.|  
|0xC0049097|-1073442665|DTS_E_EXPREVALSTATIC_VARIABLECOMPUTEFAILED|Retrieving the value for a variable failed.|  
|0xC0049098|-1073442664|DTS_E_EXPREVALSTATIC_VARIABLETYPENOTSUPPORTED|The expression contains a variable with an unsupported data type.|  
|0xC004909B|-1073442661|DTS_E_EXPREVALSTATIC_CASTCODEPAGEMISMATCH|Unable to cast the expression because the code page of the value being cast does not match the requested result code page. The code page of the source must match the code page requested for the destination.|  
|0xC004909C|-1073442660|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEQUOTE|The expression contains an unexpected single quotation mark. A double quotation mark may be required.|  
|0xC004909D|-1073442659|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEEQUAL|The expression contains an unexpected equal sign (=). This error usually occurs when a double equals sign (==) is needed.|  
|0xC00490AA|-1073442646|DTS_E_EXPREVALSTATIC_AMBIGUOUSINPUTCOLUMNNAME|An ambiguous input column name was specified.  The column must be qualified as [Component Name].[Column Name] or referenced by lineage ID. This error occurs when the input column exists on more than one component, and must be differentiated by the addition of component name or by using the lineage ID.|  
|0xC00490AB|-1073442645|DTS_E_EXPREVALSTATIC_PLACEHOLDERINEXPRESSION|A placeholder function parameter or operand was found in an expression. This should be replaced with an actual parameter or operand.|  
|0xC00490AC|-1073442644|DTS_E_EXPREVALSTATIC_AMBIGUOUSVARIABLENNAME|An ambiguous variable name was specified. The desired variable must be qualifed as \@[Namespace::Variable]. This error occurs when the variable exists in more than one namespace.|  
|0xC00490D3|-1073442605|DTS_E_EXPREVALSTATIC_BINARYOPDTSTRNOTSUPPORTED|For operands of binary operation, the data type DT_STR is only supported for input columns and cast operations. A DT_STR operand that is not an input column or the result of a cast cannot be used with a binary operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC00490D4|-1073442604|DTS_E_EXPREVALSTATIC_CONDITIONALOPDTSTRNOTSUPPORTED|For operands of the conditional operator, the data type DT_STR is only supported for input columns and cast operations. A DT_STR operand that is not an input column or the result of a cast cannot be used with the conditional operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC00490D5|-1073442603|DTS_E_EXPREVALSTATIC_FNFINDSTRINGINVALIDOCCURRENCECOUNT|The occurrence count parameter is not valid for function FINDSTRING. This parameter must be greater than zero.|  
|0xC00490DD|-1073442595|DTS_E_EXPREVALSTATIC_INVALIDDATEPARTNODE|The "date part" parameter specified for a date function is not valid. "Date part" parameters must be static strings, and cannot contain dynamic elements such as input columns. They must be of type DT_WSTR.|  
|0xC00490DE|-1073442594|DTS_E_EXPREVALSTATIC_INVALIDCASTLENGTH|The value specified for the length parameter of a cast operation is not valid. The length must be positive. The length specified for the type cast is negative. Change to a positive value.|  
|0xC00490DF|-1073442593|DTS_E_EXPREVALSTATIC_INVALIDNULLLENGTH|The value specified for the length parameter of a NULL function is not valid. The length must be positive. The length specified for the NULL function is negative. Change to a positive value.|  
|0xC00490E0|-1073442592|DTS_E_EXPREVALSTATIC_INVALIDNULLCODEPAGE|The value specified for the code page parameter of the NULL function with data type DT_STR or DT_TEXT is not valid. The code page specified is not installed on the computer. Either change the code page that is specified, or install the code page on the computer.|  
|0xC00490E1|-1073442591|DTS_E_EXPREVALSTATIC_INVALIDNULLPRECISION|The value specified for the precision parameter of a NULL function is not valid. The precision that was specified is out of range for the NULL function.|  
|0xC00490E2|-1073442590|DTS_E_EXPREVALSTATIC_INVALIDNULLSCALE|The value specified for the scale parameter of a NULL function is not valid. The scale that was specified is out of range for the NULL function. Scale must not exceed precision and must be positive.|  
|0xC00490E8|-1073442584|DTS_E_XMLSRCERRORSETTINGERROROUTPUTCOLUMNDATA|The %1 failed attempting to write data to %2 on %3. %4|  
|0xC00490F5|-1073442571|DTS_E_TXLOOKUP_CANCEL_REQUESTED|Lookup transform has received a cancel request from the user.|  
|0xC00490F6|-1073442570|DTS_E_LOBLENGTHLIMITEXCEEDED|Processing of character or binary large object (LOB) data has stopped because the 4-GB limit was reached.|  
|0xC00490F7|-1073442569|DTS_E_CANNOTLOADCOMPONENT|The managed pipeline component "%1" could not be loaded.  The exception was: %2.|  
|0xC00F9304|-1072721148|DTS_E_OLEDB_EXCEL_NOT_SUPPORTED|SSIS Error Code DTS_E_OLEDB_EXCEL_NOT_SUPPORTED: The Excel Connection Manager is not supported in the 64-bit version of SSIS, as no OLE DB provider is available.|  
|0xC00F9310|-1072721136|DTS_E_CACHEBADHEADER|The cache file is damaged, or the file was not created by using the Cache connection manager.  Provide a valid cache file.|  
|0xC0202001|-1071636479|DTS_E_MISSINGSQLCOMMAND|The SQL command has not been set correctly. Check SQLCommand property.|  
|0xC0202002|-1071636478|DTS_E_COMERROR|COM error object information is available.  Source: "%1"  error code: 0x%2!8.8X!  Description: "%3".|  
|0xC0202003|-1071636477|DTS_E_ACQUIREDCONNECTIONUNAVAILABLE|Unable to access the acquired connections.|  
|0xC0202004|-1071636476|DTS_E_INCORRECTCOLUMNCOUNT|The number of columns is incorrect.|  
|0xC0202005|-1071636475|DTS_E_COLUMNNOTFOUND|Column "%1" cannot be found at the datasource.|  
|0xC0202007|-1071636473|DTS_E_OLEDBRECORD|An OLE DB record is available.  Source: "%1"  Hresult: 0x%2!8.8X!  Description: "%3".|  
|0xC0202009|-1071636471|DTS_E_OLEDBERROR|SSIS Error Code DTS_E_OLEDBERROR.  An OLE DB error has occurred. Error code: 0x%1!8.8X!.|  
|0xC020200A|-1071636470|DTS_E_ALREADYCONNECTED|Component is already connected. The component needs to be disconnected before attempting to connect it.|  
|0xC020200B|-1071636469|DTS_E_INCORRECTSTOCKPROPERTYVALUE|The value of the property "%1" is incorrect.|  
|0xC020200E|-1071636466|DTS_E_CANNOTOPENDATAFILE|Cannot open the datafile "%1".|  
|0xC0202010|-1071636464|DTS_E_DESTINATIONFLATFILEREQUIRED|No destination flat file name was provided. Make sure the flat file connection manager is configured with a connection string. If the flat file connection manager is used by multiple components, ensure that the connection string contains enough file names.|  
|0xC0202011|-1071636463|DTS_E_TEXTQUALIFIERNOTFOUND|The text qualifier for column "%1" cannot be found.|  
|0xC0202014|-1071636460|DTS_E_CANNOTCONVERTTYPES|Conversion from "%1" to "%2" is not supported.|  
|0xC0202015|-1071636459|DTS_E_PROBLEMDETECTINGTYPECOMPATIBILITY|The error code 0x%1!8.8X! was returned when validating type conversion from %2 to %3.|  
|0xC0202016|-1071636458|DTS_E_CANNOTMAPINPUTCOLUMNTOOUTPUTCOLUMN|Cannot find input column with lineage ID "%1!d!" which is needed by "%2". Check SourceInputColumnLineageID custom property of the output column.|  
|0xC0202017|-1071636457|DTS_E_INCORRECTMINIMUMNUMBEROFOUTPUTS|The number of outputs is incorrect. There must be at least %1!d! outputs.|  
|0xC0202018|-1071636456|DTS_E_INCORRECTEXACTNUMBEROFOUTPUTS|The number of outputs is incorrect. There must be exactly %1!d! output(s).|  
|0xC0202019|-1071636455|DTS_E_STRINGCONVERSIONTOOLONG|A string was too long to be converted.|  
|0xC020201A|-1071636454|DTS_E_INCORRECTEXACTNUMBEROFINPUTS|The number of inputs is incorrect. There must be exactly %1!d! inputs.|  
|0xC020201B|-1071636453|DTS_E_CANNOTHAVEZEROINPUTCOLUMNS|The number of input columns for %1 cannot be zero.|  
|0xC020201C|-1071636452|DTS_E_CANNOTHAVEINPUTS|This component has %1!d! inputs.  No input is allowed on this component.|  
|0xC020201D|-1071636451|DTS_E_PROCESSINPUTCALLEDWITHINVALIDINPUTID|ProcessInput was called with an invalid input ID of %1!d!.|  
|0xC020201F|-1071636449|DTS_E_INCORRECTCUSTOMPROPERTYTYPE|The custom property "%1" needs to be of type %2.|  
|0xC0202020|-1071636448|DTS_E_INVALIDBUFFERTYPE|The buffer type is not valid. Make sure the Pipeline layout and all components pass validation.|  
|0xC0202021|-1071636447|DTS_E_INCORRECTCUSTOMPROPERTYVALUE|The value for custom property "%1" is incorrect.|  
|0xC0202022|-1071636446|DTS_E_CONNECTIONREQUIREDFORMETADATA|An error occurred due to no connection. A connection is required when requesting metadata. If you are working offline, uncheck Work Offline on the SSIS menu to enable the connection.|  
|0xC0202023|-1071636445|DTS_E_CANTCREATECUSTOMPROPERTY|The custom property "%1" cannot be created.|  
|0xC0202024|-1071636444|DTS_E_CANTGETCUSTOMPROPERTYCOLLECTION|The custom property collection cannot be retrieved for initialization.|  
|0xC0202025|-1071636443|DTS_E_CANNOTCREATEACCESSOR|Cannot create an OLE DB accessor. Verify that the column metadata is valid.|  
|0xC0202026|-1071636442|DTS_E_PRIMEOUTPUTCALLEDWITHINVALIDOUTPUTID|PrimeOutput was called with an invalid output ID of %1!d!.|  
|0xC0202027|-1071636441|DTS_E_INCORRECTSTOCKPROPERTY|The value for property "%1" on "%2" is not valid.|  
|0xC0202028|-1071636440|DTS_E_CONNECTIONREQUIREDFORREAD|A connection is required to read data.|  
|0xC020202C|-1071636436|DTS_E_ERRORWHILEREADINGHEADERROWS|An error occurred while reading header rows.|  
|0xC020202D|-1071636435|DTS_E_DUPLICATECOLUMNNAME|Duplicate column name "%1".|  
|0xC0202030|-1071636432|DTS_E_CANNOTGETCOLUMNNAME|Cannot get the name of the column with ID %1!d!.|  
|0xC0202031|-1071636431|DTS_E_CANTDIRECTROW|Direct row to output "%1" (%2!d!) failed.|  
|0xC020203A|-1071636422|DTS_E_CANNOTCREATEBULKINSERTHREAD|Cannot create the bulk insert thread due to error "%1".|  
|0xC020203B|-1071636421|DTS_E_BULKINSERTHREADINITIALIZATIONFAILED|The thread for the SSIS Bulk Insert task failed initialization.|  
|0xC020203E|-1071636418|DTS_E_BULKINSERTTHREADALREADYRUNNING|The thread for the SSIS Bulk Insert task is already running.|  
|0xC020203F|-1071636417|DTS_E_BULKINSERTTHREADABNORMALCOMPLETION|The thread for the SSIS Bulk Insert task terminated with errors or warnings.|  
|0xC0202040|-1071636416|DTS_E_CANNOTGETIROWSETFASTLOAD|Failed to open a fastload rowset for "%1". Check that the object exists in the database.|  
|0xC0202041|-1071636415|DTS_E_CONNECTREQUIREDFORMETADATAVALIDATION|Error due to no connection. A connection is required before metadata validation can proceed.|  
|0xC0202042|-1071636414|DTS_E_DESTINATIONTABLENAMENOTPROVIDED|A destination table name has not been provided.|  
|0xC0202043|-1071636413|DTS_E_ICONVERTTYPEUNAVAILABLE|The OLE DB provider used by the OLE DB adapter does not support IConvertType. Set the adapter's ValidateColumnMetaData property to FALSE.|  
|0xC0202044|-1071636412|DTS_E_OLEDBPROVIDERDATATYPECONVERSIONUNSUPPORTED|The OLE DB provider used by the OLE DB adapter cannot convert between types "%1" and "%2" for "%3".|  
|0xC0202045|-1071636411|DTS_E_VALIDATECOLUMNMETADATAFAILED|Column metadata validation failed.|  
|0xC0202047|-1071636409|DTS_E_ATTEMPTINGTOINSERTINTOAROWIDCOLUMN|"%1" is a row ID column and cannot be included in a data insertion operation.|  
|0xC0202048|-1071636408|DTS_E_ATTEMPTINGTOINSERTINTOAROWVERCOLUMN|Attempting insertion into the row version column "%1". Cannot insert into a row version column.|  
|0xC0202049|-1071636407|DTS_E_ATTEMPTINGTOINSERTINTOAREADONLYCOLUMN|Failure inserting into the read-only column "%1".|  
|0xC020204A|-1071636406|DTS_E_UNABLETORETRIEVECOLUMNINFO|Unable to retrieve column information from the data source. Make sure your target table in the database is available.|  
|0xC020204B|-1071636405|DTS_E_CANTLOCKBUFFER|A buffer could not be locked. The system is out of memory or the buffer manager has reached its quota.|  
|0xC020204C|-1071636404|DTS_E_INVALIDCOMPARISONFLAGS|The %1 has a ComparisonFlags property that includes extra flags with the value %2!d!.|  
|0xC020204D|-1071636403|DTS_E_COLUMNMETADATAUNAVAILABLEFORVALIDATION|The column metadata was unavailable for validation.|  
|0xC0202053|-1071636397|DTS_E_CANNOTWRITETODATAFILE|Cannot write to the data file.|  
|0xC0202055|-1071636395|DTS_E_COLUMNDELIMITERNOTFOUND|The column delimiter for column "%1" was not found.|  
|0xC0202058|-1071636392|DTS_E_COLUMNPARSEFAILED|Failed to parse the column "%1" in the data file.|  
|0xC020205A|-1071636390|DTS_E_RAWFILENAMEREQUIRED|The file name is not properly specified.  Supply the path and name to the raw file either directly in the FileName property or by specifying a variable in the FileNameVariable property.|  
|0xC020205B|-1071636389|DTS_E_RAWFILECANTOPEN|File "%1" cannot be opened for writing. Error may occur when there are no file privileges or the disk is full.|  
|0xC020205C|-1071636388|DTS_E_RAWFILECANTBUFFER|An I/O buffer cannot be created for the output file. Error may occur when there are no file privileges or the disk is full.|  
|0xC020205D|-1071636387|DTS_E_RAWCANTWRITE|Cannot write %1!d! bytes to file "%2". See previous error messages for details.|  
|0xC020205E|-1071636386|DTS_E_RAWBADHEADER|Encountered bad metadata in file header. The file is damaged or not a SSIS-produced raw data file.|  
|0xC020205F|-1071636385|DTS_E_RAWEXISTSCREATEONCE|Error occurred because the output file already exists and the WriteOption is set to Create Once. Set the WriteOption property to Create Always, or delete the file.|  
|0xC0202060|-1071636384|DTS_E_RAWCANTAPPENDTRUNCATE|Error caused by conflicting property settings. Both the AllowAppend property and the ForceTruncate property are set to TRUE. Both properties cannot be set to TRUE. Set one of the two properties to FALSE.|  
|0xC0202061|-1071636383|DTS_E_RAWBADVERSION|The file had bad version and flags information. The file is damaged or not a SSIS-produced raw data file.|  
|0xC0202062|-1071636382|DTS_E_RAWVERSIONINCOMPATIBLEAPPEND|The output file was written by an incompatible version and cannot be appended. The file may be an older file format that is no longer useable.|  
|0xC0202064|-1071636380|DTS_E_RAWMETADATAMISMATCH|Cannot append output file because no column in the existing file matches column "%1" from the input. Old file does not match in metadata.|  
|0xC0202065|-1071636379|DTS_E_RAWMETADATACOUNTMISMATCH|Cannot append output file because the number of columns in the output file does not match the number of columns in this destination. The old file does not match in metadata.|  
|0xC0202067|-1071636377|DTS_E_ERRORRETRIEVINGCOLUMNCODEPAGE|There was an error retrieving column code page information.|  
|0xC0202068|-1071636376|DTS_E_RAWCANTREAD|Cannot read %1!d! bytes from file "%2". The cause of the failure should have been previously reported.|  
|0xC0202069|-1071636375|DTS_E_RAWUNEXPECTEDEOF|Unexpected end-of-file encountered while reading %1!d! bytes from file "%2". The file ended prematurely because of an invalid file format.|  
|0xC020206A|-1071636374|DTS_E_RAWNOLONGTYPES|The column %1 cannot be used. The raw adapters do not support image, text, or ntext data.|  
|0xC020206B|-1071636373|DTS_E_RAWUNEXPECTEDTYPE|The adapter encountered an unrecognized data type of %1!d!. This could be caused by a damaged input file (source) or by an invalid buffer type (destination).|  
|0xC020206C|-1071636372|DTS_E_RAWSTRINGTOOLONG|String too long. The adapter read a string that was %1!d! bytes long, and expected a string no longer than %2!d! bytes, at offset %3!d!. This could indicate a damaged input file. The file shows a string length that is too large for the buffer column.|  
|0xC020206E|-1071636370|DTS_E_RAWSKIPFAILED|The raw adapter attempted to skip %1!d! bytes in the input file for unreferenced column "%2" with lineage ID %3!d!, but there was an error. The error returned from the operating system should have been previously reported.|  
|0xC020206F|-1071636369|DTS_E_RAWREADFAILED|The raw adapter attempted to read %1!d! bytes in the input file for column "%2" with lineage ID %3!d!, but there was an error. The error returned from the operating system should have been previously reported.|  
|0xC0202070|-1071636368|DTS_E_RAWFILENAMEINVALID|The file name property is not valid. The file name is a device or contains invalid characters.|  
|0xC0202071|-1071636367|DTS_E_BULKINSERTAPIPREPARATIONFAILED|Unable to prepare the SSIS bulk insert for data insertion.|  
|0xC0202072|-1071636366|DTS_E_INVALIDDATABASEOBJECTNAME|Database object name "%1" is not valid.|  
|0xC0202073|-1071636365|DTS_E_INVALIDORDERCLAUSE|Order clause is not valid.|  
|0xC0202074|-1071636364|DTS_E_RAWFILECANTOPENREAD|File "%1" cannot be opened for reading. Error may occur when there are no privileges or the file is not found. Exact cause is reported in previous error message.|  
|0xC0202075|-1071636363|DTS_E_TIMEGENCANTCREATE|Unable to create the Microsoft.AnalysisServices.TimeDimGenerator.TimeDimGenerator.|  
|0xC0202076|-1071636362|DTS_E_TIMEGENCANTCONFIGURE|Unable to configure the Microsoft.AnalysisServices.TimeDimGenerator.|  
|0xC0202077|-1071636361|DTS_E_TIMEGENCANTCONVERT|Unsupported datatype for column %1!d!.|  
|0xC0202079|-1071636359|DTS_E_TIMEGENCANTREAD|The attempt to read from the Microsoft.AnalysisServices.TimeDimGenerator failed with error code 0x%1!8.8X!.|  
|0xC020207A|-1071636358|DTS_E_TIMEGENCANTREADCOLUMN|The attempt to read column "%2!d!" data from the Microsoft.AnalysisServices.TimeDimGenerator failed with error code 0x%2!8.8X!.|  
|0xC020207B|-1071636357|DTS_E_RSTDESTBADVARIABLENAME|The VariableName property is not set to the name of a valid variable. Need a runtime variable name to write to.|  
|0xC020207C|-1071636356|DTS_E_RSTDESTRSTCONFIGPROBLEM|Unable to create or configure the ADODB.Recordset object.|  
|0xC020207D|-1071636355|DTS_E_RSTDESTRSTWRITEPROBLEM|Error writing to the ADODB.Recordset object.|  
|0xC020207E|-1071636354|DTS_E_FILENAMEINVALID|The file name is not valid. The file name is a device or contains invalid characters.|  
|0xC020207F|-1071636353|DTS_E_FILENAMEINVALIDWITHPARAM|The file name "%1" is not valid. The file name is a device or contains invalid characters.|  
|0xC0202080|-1071636352|DTS_E_CMDDESTNOPARAMS|Unable to retrieve destination column descriptions from the parameters of the SQL command.|  
|0xC0202081|-1071636351|DTS_E_CMDDESTNOTBOUND|Parameters are not bound. All parameters in the SQL command must be bound to input columns.|  
|0xC0202082|-1071636350|DTS_E_TXPIVOTBADUSAGE|The PivotUsage value for the input column "%1" (%2!d!) is not valid.|  
|0xC0202083|-1071636349|DTS_E_TXPIVOTTOOMANYPIVOTKEYS|Too many Pivot Keys found. Only one input column can be used as the Pivot Key.|  
|0xC0202084|-1071636348|DTS_E_TXPIVOTNOPIVOTKEY|No Pivot Key found. One input column must be used as the Pivot Key.|  
|0xC0202085|-1071636347|DTS_E_TXPIVOTINPUTALREADYMAPPED|More than one output column (such as "%1" (%2!d!)) is mapped to input column "%3" (%4!d!).|  
|0xC0202086|-1071636346|DTS_E_TXPIVOTCANTMAPPIVOTKEY|Output column "%1" (%2!d!) cannot be mapped to PivotKey input column.|  
|0xC0202087|-1071636345|DTS_E_TXPIVOTCANTMAPPINGNOTFOUND|Output column "%1" (%2!d!) has a SourceColumn %3!d! that is not a valid input column lineage ID.|  
|0xC0202088|-1071636344|DTS_E_TXPIVOTEMPTYPIVOTKEYVALUE|Output column "%1" (%2!d!) is mapped to a Pivoted Value input column, but its PivotKeyValue property value is missing.|  
|0xC0202089|-1071636343|DTS_E_TXPIVOTDUPLICATEPIVOTKEYVALUE|Output column "%1" (%2!d!) is mapped to a Pivoted Value input column with a non-unique PivotKeyValue property value.|  
|0xC020208A|-1071636342|DTS_E_TXPIVOTOUTPUTNOTMAPPED|Input column "%1" (%2!d!) is not mapped to any output column.|  
|0xC020208B|-1071636341|DTS_E_TXPIVOTCANTCOMPARESETKEYS|Failure occurred while comparing values for the set keys.|  
|0xC020208D|-1071636339|DTS_E_TXPIVOTNOBLOB|The Input column "%1" (%2!d!) cannot be used as a Set Key, Pivot Key, or Pivot Value because it contains long data.|  
|0xC020208E|-1071636338|DTS_E_TXPIVOTBADOUTPUTTYPE|Incorrect output type. The output column "%1" (%2!d!) must have the same data type and metadata as the input column to which it is mapped.|  
|0xC020208F|-1071636337|DTS_E_TXPIVOTPROCESSERROR|Failure when trying to pivot the source records.|  
|0xC0202090|-1071636336|DTS_E_TXPIVOTBADPIVOTKEYVALUE|The pivot key value "%1" is not valid.|  
|0xC0202091|-1071636335|DTS_E_ERRORWHILESKIPPINGDATAROWS|An error occurred while skipping data rows.|  
|0xC0202092|-1071636334|DTS_E_ERRORWHILEREADINGDATAROWS|An error occurred while processing file "%1" on data row %2!I64d!.|  
|0xC0202093|-1071636333|DTS_E_FAILEDTOINITIALIZEFLATFILEPARSER|An error occurred while initializing the flat file parser.|  
|0xC0202094|-1071636332|DTS_E_UNABLETORETRIEVECOLUMNINFOFROMFLATFILECONNECTIONMANAGER|Unable to retrieve column information from the flat file connection manager.|  
|0xC0202095|-1071636331|DTS_E_FAILEDTOWRITEOUTCOLUMNNAME|Failed to write out column name for column "%1".|  
|0xC0202096|-1071636330|DTS_E_INVALIDFLATFILECOLUMNTYPE|The column type for column "%1" is incorrect. It is type "%2". It can only be either "%3" or "%4".|  
|0xC0202097|-1071636329|DTS_E_DISKIOBUFFEROVERFLOW|The attempt to write data of %1!d! bytes into the disk I/O failed. The disk I/O buffer has %2!d! free bytes.|  
|0xC0202098|-1071636328|DTS_E_FAILEDTOWRITEOUTHEADER|An error occurred while writing out the file header.|  
|0xC0202099|-1071636327|DTS_E_FAILEDTOGETFILESIZE|An error occurred while getting the file size for file "%1".|  
|0xC020209A|-1071636326|DTS_E_FAILEDTOSETFILEPOINTER|An error occurred while setting the file pointer for file "%1".|  
|0xC020209B|-1071636325|DTS_E_UNABLETOSETUPDISKIOBUFFER|An error occurred while setting up the disk I/O buffer.|  
|0xC020209C|-1071636324|DTS_E_COLUMNDATAOVERFLOWDISKIOBUFFER|The column data for column "%1" overflowed the disk I/O buffer.|  
|0xC020209D|-1071636323|DTS_E_DISKIOFAILED|An unexpected disk I/O error occurred while reading the file.|  
|0xC020209E|-1071636322|DTS_E_DISKIOTIMEDOUT|An disk I/O time out occurred while reading the file.|  
|0xC020209F|-1071636321|DTS_E_INPUTSNOTREADONLY|The Usage Type specified for the input columns to this transform cannot be read/write. Change the Usage Type to be read-only.|  
|0xC02020A0|-1071636320|DTS_E_CANNOTCOPYORCONVERTFLATFILEDATA|Cannot copy or convert flat file data for column "%1".|  
|0xC02020A1|-1071636319|DTS_E_FAILEDCOLUMNDATACONVERSIONSTATUS|Data conversion failed. The data conversion for column "%1" returned status value %2!d! and status text "%3".|  
|0xC02020A2|-1071636318|DTS_E_VARIABLESCOLLECTIONUNAVAILABLE|The Variables collection is not available.|  
|0xC02020A3|-1071636317|DTS_E_TXUNPIVOTDUPLICATEPIVOTKEYVALUE|Duplicate PivotKeyValue. Input column "%1" (%2!d!) is mapped to a Pivoted Value output column and has a non-unique PivotKeyValue.|  
|0xC02020A4|-1071636316|DTS_E_TXUNPIVOTNOUNPIVOTDESTINATION|No unpivot destination found. At least one input column must be mapped with a PivotKeyValue to an DestinationColumn in the output.|  
|0xC02020A5|-1071636315|DTS_E_TXUNPIVOTBADKEYLIST|PivotKeyValue is not valid. In an UnPivot transform with more than one unpivoted DestinationColumn, the set of PivotKeyValues per destination must match exactly.|  
|0xC02020A6|-1071636314|DTS_E_TXUNPIVOTBADUNPIVOTMETADATA|Incorrect UnPivot metadata. In an UnPivot transform, all input columns with a PivotKeyValue that is set, and are pointing to the same DestinationColumn, must have metadata that exactly matches the DestinationColumn.|  
|0xC02020A7|-1071636313|DTS_E_TXPIVOTBADPIVOTKEYCONVERT|Cannot convert the pivot key value "%1" to the data type of the pivot key column.|  
|0xC02020A8|-1071636312|DTS_E_TXUNPIVOTTOOMANYPIVOTKEYS|Too many Pivot Keys specified. Only one output column can be used as the Pivot Key.|  
|0xC02020A9|-1071636311|DTS_E_TXUNPIVOTUNMAPPEDOUTPUT|Output column "%1" (%2!d!) is not mapped by any input column's DestinationColumn property.|  
|0xC02020AA|-1071636310|DTS_E_TXUNPIVOTNOPIVOT|No output column is marked as the PivotKey.|  
|0xC02020AB|-1071636309|DTS_E_TXUNPIVOTNOTINPUTMAP|Input column "%1" (%2!d!) has a DestinationColumn property value that does not refer to a valid output column LineageID.|  
|0xC02020AC|-1071636308|DTS_E_TXUNPIVOTDUPLICATEDESTINATION|Duplicate destination error. More than one non-pivoted input column is mapped to the same destination output column.|  
|0xC02020AD|-1071636307|DTS_E_TOTALINPUTCOLSCANNOTBEZERO|No input columns found. At least one input column must be mapped to an output column.|  
|0xC02020AE|-1071636306|DTS_E_TXMERGEJOINMUSTHAVESAMENUMBEROFINPUTANDOUTPUTCOLS|The number of input and output columns are not equal. The total number of input columns on all inputs must be the same as the total number of output columns.|  
|0xC02020AF|-1071636305|DTS_E_INPUTMUSTBESORTED|The input is not sorted. The "%1" must be sorted.|  
|0xC02020B0|-1071636304|DTS_E_TXMERGEJOININVALIDJOINTYPE|The JoinType custom property for the %1 contains a value of %2!ld!, which is not valid. Valid values are 0 (full), 1 (left), or 2 (inner).|  
|0xC02020B1|-1071636303|DTS_E_TXMERGEJOININVALIDNUMKEYCOLS|The NumKeyColumns value is not valid. In the %1, the value for the NumKeyColumns custom property must be between 1 and %2!lu!.|  
|0xC02020B2|-1071636302|DTS_E_NOKEYCOLS|No key columns are found. The %1 must have at least one column with a SortKeyPosition that is non-zero.|  
|0xC02020B3|-1071636301|DTS_E_TXMERGEJOINNOTENOUGHKEYCOLS|Not enough key columns. The %1 must have at least %2!ld! columns with non-zero SortKeyPosition values.|  
|0xC02020B4|-1071636300|DTS_E_TXMERGEJOINDATATYPEMISMATCH|Datatype mismatch occurred. The datatypes for the columns with SortKeyPosition value %1!ld! do not match.|  
|0xC02020B5|-1071636299|DTS_E_TXMERGEJOININVALIDSORTKEYPOS|The column with the SortKeyPosition value of %1!ld! is not valid. It should be %2!ld!.|  
|0xC02020B6|-1071636298|DTS_E_TXMERGEJOINSORTDIRECTIONMISMATCH|Sort direction mismatch. The sort directions for the columns with SortKeyPosition value %1!ld! do not match.|  
|0xC02020B7|-1071636297|DTS_E_TXMERGEJOINOUTPUTCOLMUSTHAVEASSOCIATEDINPUTCOL|Missing column. The %1 must have an associated input column.|  
|0xC02020B8|-1071636296|DTS_E_TXMERGEJOINREADONLYINPUTCOLSWITHNOOUTPUTCOL|Input columns must have output columns. There are input columns with a usage type of read-only that do not have associated output columns.|  
|0xC02020B9|-1071636295|DTS_E_TXMERGEJOINNONSTRINGCOMPARISONFLAGSNOTZERO|The comparison flags are not zero. The comparison flags for non-string columns must be zero.|  
|0xC02020BA|-1071636294|DTS_E_TXMERGEJOINCOMPARISONFLAGSMISMATCH|The comparison flags for the columns with SortKeyPosition value %1!ld! do not match.|  
|0xC02020BB|-1071636293|DTS_E_TXPIVOTBADPIVOTKEYVALUENOSTRING|Unrecognized pivot key value.|  
|0xC02020BC|-1071636292|DTS_E_TXLINEAGEINVALIDLINEAGEITEM|Lineage item value %1!ld! is not valid. The valid range is between %2!ld! and %3!ld!.|  
|0xC02020BD|-1071636291|DTS_E_CANNOTHAVEANYINPUTCOLUMNS|Input columns not allowed. The number of input columns must be zero.|  
|0xC02020BE|-1071636290|DTS_E_TXLINEAGEDATATYPEMISMATCH|The datatype for "%1" is not valid for the specified lineage item.|  
|0xC02020BF|-1071636289|DTS_E_TXLINEAGEINVALIDLENGTH|The length for "%1" is not valid for the specified lineage item.|  
|0xC02020C1|-1071636287|DTS_E_METADATAMISMATCHWITHOUTPUTCOLUMN|The metadata for "%1" does not match the metadata for the associated output column.|  
|0xC02020C3|-1071636285|DTS_E_TXMERGESORTKEYPOSMISMATCH|There are output columns that have SortKeyPosition values that don't match the associated input columns' SortKeyPosition.|  
|0xC02020C4|-1071636284|DTS_E_ADDROWTOBUFFERFAILED|The attempt to add a row to the Data Flow task buffer failed with error code 0x%1!8.8X!.|  
|0xC02020C5|-1071636283|DTS_E_DATACONVERSIONFAILED|Data conversion failed while converting column "%1" (%2!d!) to column "%3" (%4!d!).  The conversion returned status value %5!d! and status text "%6".|  
|0xC02020C6|-1071636282|DTS_E_FAILEDTOALLOCATEROWHANDLEBUFFER|The attempt to allocate a row handle buffer failed with error code 0x%1!8.8X!.|  
|0xC02020C7|-1071636281|DTS_E_FAILEDTOSENDROWTOSQLSERVER|The attempt to send a row to SQL Server failed with error code 0x%1!8.8X!.|  
|0xC02020C8|-1071636280|DTS_E_FAILEDTOPREPAREBUFFERSTATUS|The attempt to prepare the buffer status failed with error code 0x%1!8.8X!.|  
|0xC02020C9|-1071636279|DTS_E_FAILEDTOBUFFERROWSTARTS|The attempt to retrieve the start of the buffer row failed with error code 0x%1!8.8X!.|  
|0xC02020CA|-1071636278|DTS_E_BULKINSERTTHREADTERMINATED|The thread for the SSIS Bulk Insert is no longer running.  No more rows can be inserted. Try increasing the bulk insert thread timeout.|  
|0xC02020CB|-1071636277|DTS_E_RAWTOOMANYCOLUMNS|The source file is not valid. The source file is returning a count of more than 131,072 columns. This usually occurs when the source file is not produced by the raw file destination.|  
|0xC02020CC|-1071636276|DTS_E_TXUNIONALL_EXTRADANGLINGINPUT|The %1 is an extra unattached input and will be removed.|  
|0xC02020CD|-1071636275|DTS_E_TXUNIONALL_NONDANGLINGUNATTACHEDINPUT|The %1 is not attached but is not marked as dangling.  It will be marked as dangling.|  
|0xC02020CF|-1071636273|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUE|Duplicate pivot key value "%1".|  
|0xC02020D0|-1071636272|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUENOSTRING|Duplicate pivot key value.|  
|0xC02020D1|-1071636271|DTS_E_FAILEDTOGETCOMPONENTLOCALEID|Failure retrieving component locale ID. Error code 0x%1!8.8X!.|  
|0xC02020D2|-1071636270|DTS_E_MISMATCHCOMPONENTCONNECTIONMANAGERLOCALEID|Mismatched locale IDs. The component locale ID (%1!d!) does not match the connection manager locale ID (%2!d!).|  
|0xC02020D3|-1071636269|DTS_E_LOCALEIDNOTSET|The component locale ID has not been set. Flat file adapters need to have the locale ID on the flat file connection manager set.|  
|0xC02020D4|-1071636268|DTS_E_RAWBYTESTOOLONG|The binary field is too large. The adapter attempted to read a binary field that was %1!d! bytes long, but expected a field no longer than %2!d! bytes at offset %3!d!. This usually occurs when the input file is not valid. The file contains a string length that is too large for the buffer column.|  
|0xC02020D5|-1071636267|DTS_E_TXSAMPLINGINVALIDPCT|The percentage, %2!ld!, is not valid for the "%1" property. It must be between 0 and 100.|  
|0xC02020D6|-1071636266|DTS_E_TXSAMPLINGINVALIDROWS|The number of rows, %2!ld!, is not valid for the "%1" property. It must be greater than 0.|  
|0xC02020D7|-1071636265|DTS_E_RAWSTRINGINPUTTOOLONG|The adapter was asked to write a string that was %1!I64d! bytes long, but all data must be less than 4294967295 bytes in length.|  
|0xC02020D9|-1071636263|DTS_E_ATLEASTONEINPUTMUSTBEMAPPEDTOOUTPUT|No inputs were mapped to an output. The "%1" must have at least one input column mapped to an output column.|  
|0xC02020DB|-1071636261|DTS_E_CANNOTCONVERTDATATYPESWITHDIFFERENTCODEPAGES|Conversion from "%1" with code page %2!d! to "%3" with code page %4!d! is not supported.|  
|0xC02020DC|-1071636260|DTS_E_COLUMNNOTMAPPEDTOEXTERNALMETADATACOLUMN|The external metadata column mapping for %1 is not valid.  The external metadata column ID cannot be zero.|  
|0xC02020DD|-1071636259|DTS_E_COLUMNMAPPEDTONONEXISTENTEXTERNALMETADATACOLUMN|The %1 is mapped to an external metadata column that does not exist.|  
|0xC02020E5|-1071636251|DTS_E_UNABLETOWRITELOBDATATOBUFFER|Writing long object data of type DT_TEXT, DT_NTEXT, or DT_IMAGE to Data Flow task buffer failed for column "%1".|  
|0xC02020E8|-1071636248|DTS_E_CANNOTGETIROWSET|Opening a rowset for "%1" failed. Check that the object exists in the database.|  
|0xC02020E9|-1071636247|DTS_E_VARIABLEACCESSFAILED|Accessing variable "%1" failed with error code 0x%2!8.8X!.|  
|0xC02020EA|-1071636246|DTS_E_CONNECTIONMANAGERNOTFOUND|The connection manager "%1" is not found. A component failed to find the connection manager in the Connections collection.|  
|0xC02020EB|-1071636245|DTS_E_VERSIONUPGRADEFAILED|The upgrade from version "%1" to version %2!d! failed.|  
|0xC02020EC|-1071636244|DTS_E_RSTDESTBIGBLOB|A value in an input column is too large to be stored in the ADODB.Recordset object.|  
|0xC02020ED|-1071636243|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|Columns "%1" and "%2" cannot convert between unicode and non-unicode string data types.|  
|0xC02020EE|-1071636242|DTS_E_ROWCOUNTBADVARIABLENAME|The variable "%1" specified by VariableName property is not a valid variable. Need a valid variable name to write to.|  
|0xC02020EF|-1071636241|DTS_E_ROWCOUNTBADVARIABLETYPE|The variable "%1" specified by VariableName property is not an integer. Change the variable to be of type VT_I4, VT_UI4, VT_I8, or VT_UI8.|  
|0xC02020F0|-1071636240|DTS_E_NOCOLUMNADVANCETHROUGHFILE|No column was specified to allow the component to advance through the file.|  
|0xC02020F1|-1071636239|DTS_E_MERGEJOINSORTEDOUTPUTHASNOSORTKEYPOSITIONS|The "%1" has IsSorted set to TRUE, but the SortKeyPosition on all output columns are zero. Either change the IsSorted to FALSE, or select at least one output column to contain a non-zero SortKeyPosition.|  
|0xC02020F2|-1071636238|DTS_E_METADATAMISMATCHWITHINPUTCOLUMN|The "%1" metadata does not match the metadata of the input column.|  
|0xC02020F3|-1071636237|DTS_E_RSTDESTBADVARIABLE|The value of the specified variable cannot be located, locked, or set.|  
|0xC02020F4|-1071636236|DTS_E_CANTPROCESSCOLUMNTYPECODEPAGE|The column "%1" cannot be processed because more than one code page (%2!d! and %3!d!) are specified for it.|  
|0xC02020F5|-1071636235|DTS_E_CANTINSERTCOLUMNTYPE|The column "%1" can't be inserted because the conversion between types %2 and %3 is not supported.|  
|0xC02020F6|-1071636234|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|Column "%1" cannot convert between unicode and non-unicode string data types.|  
|0xC02020F8|-1071636232|DTS_E_COULDNOTFINDINPUTBUFFERCOLUMNBYLINEAGE|The %1 cannot find the column with LineageID %2!ld! in its input buffer.|  
|0xC02020F9|-1071636231|DTS_E_COULDNOTGETCOLUMNINFOFORINPUTBUFFER|The %1 cannot get the column information for column %2!lu! from its input buffer.|  
|0xC02020FA|-1071636230|DTS_E_COULDNOTGETCOLUMNINFOFORCOPYBUFFER|The %1 cannot get the column information for column "%2!lu!" from its copy buffer.|  
|0xC02020FB|-1071636229|DTS_E_COULDNOTREGISTERCOPYBUFFER|The %1 cannot register a buffer type for its copy buffer.|  
|0xC02020FC|-1071636228|DTS_E_COULDNOTCREATECOPYBUFFER|The %1 cannot create a buffer to copy its data into for sorting.|  
|0xC02020FD|-1071636227|DTS_E_DATAREADERDESTREADFAILED|DataReader client has failed to call Read or has closed the DataReader.|  
|0xC02020FE|-1071636226|DTS_E_NOSCHEMAINFOFOUND|No column information was returned by the SQL command.|  
|0xC02020FF|-1071636225|DTS_E_GETSCHEMATABLEFAILED|The %1 was unable to retrieve column information for the SQL command. The following error occurred: %2|  
|0xC0202100|-1071636224|DTS_E_SOURCETABLENAMENOTPROVIDED|A source table name has not been provided.|  
|0xC0203110|-1071632112|DTS_E_CACHE_INVALID_INDEXPOS|The cache index position, %1!d!, is not valid. For non-index columns, the index position should be 0. For index columns, the index position should be a sequential, positive number.|  
|0xC0203111|-1071632111|DTS_E_CACHE_DUPLICATE_INDEXPOS|The index position, %1!d!, is a duplicate. For non-index columns, the index position should be 0. For index columns, the index position should be a sequential, positive number.|  
|0xC0203112|-1071632110|DTS_E_CACHE_TOO_FEW_INDEX_COLUMNS|At least one index column should be specified for the Cache connection manager. To specify an index column, set the Index Position property of the cache column.|  
|0xC0203113|-1071632109|DTS_E_CACHE_INDEXPOS_NOT_CONTINUOUS|Cache index positions must be contiguous. For non-index columns, the index position should be 0. For index columns, the index position should be a sequential, positive number.|  
|0xC0204000|-1071628288|DTS_E_PROPERTYNOTSUPPORTED|The property "%1" cannot be set on "%2". The property being set is not supported on the specified object. Check the property name, case, and spelling.|  
|0xC0204002|-1071628286|DTS_E_CANTCHANGEPROPERTYTYPE|The property type cannot be changed from the type that was set by the component.|  
|0xC0204003|-1071628285|DTS_E_CANTADDOUTPUTID|Output ID %1!d! failed during insert. The new output was not created.|  
|0xC0204004|-1071628284|DTS_E_CANTDELETEOUTPUTID|Cannot delete output ID %1!d! from the output collection.  The ID may not be valid, or the ID may have been the default or error output.|  
|0xC0204006|-1071628282|DTS_E_FAILEDTOSETPROPERTY|Failed to set property "%1" on "%2".|  
|0xC0204007|-1071628281|DTS_E_FAILEDTOSETOUTPUTCOLUMNTYPE|Failed to set the type of %1 to type: "%2", length: %3!d!, precision: %4!d!, scale: %5!d!, codepage: %6!d!.|  
|0xC0204008|-1071628280|DTS_E_MORETHANONEERROROUTPUTFOUND|More than one error output was found on the component, and there can be only one.|  
|0xC020400A|-1071628278|DTS_E_CANTSETOUTPUTCOLUMNPROPERTY|The property on an output column cannot be set.|  
|0xC020400B|-1071628277|DTS_E_CANTMODIFYERROROUTPUTCOLUMNDATATYPE|The data type for "%1" cannot be modified in the error "%2".|  
|0xC020400E|-1071628274|DTS_E_CANONLYSETISSORTEDONSOURCE|The "%1" cannot have its IsSorted property set to TRUE because it is not a source output. A source output has a SynchronousInputID value of zero.|  
|0xC020400F|-1071628273|DTS_E_CANONLYSETSORTKEYONSOURCE|The "%1" cannot have a SortKeyPosition property set to non-zero because "%2" is not a source output. The output column "colname" (ID) cannot have its SortKeyPosition property set to non-zero because its output "outputname" (ID) is not a source output.|  
|0xC0204010|-1071628272|DTS_E_CANONLYSETCOMPFLAGSONSOURCE|The ComparisonFlags property cannot be set to a non-zero value for "%1" because the "%2" is not a source output. The output column "colname" (ID) cannot have a ComparisonFlags property set to non-zero because its output "outputname" (ID) is not a source output.|  
|0xC0204011|-1071628271|DTS_E_NONSTRINGCOMPARISONFLAGSNOTZERO|The comparison flags for "%1" must be zero because its type is not a string type. ComparisonFlags can only be non-zero for string type columns.|  
|0xC0204012|-1071628270|DTS_E_COMPFLAGSONLYONSORTCOL|The "%1" cannot have a ComparisonFlags property set to non-zero because its SortKeyPosition is set to zero. An output column's ComparisonFlags can only be non-zero if its SortKeyPosition is also non-zero.|  
|0xC0204013|-1071628269|DTS_E_READONLYSTOCKPROPERTY|The property is read-only.|  
|0xC0204014|-1071628268|DTS_E_INVALIDDATATYPE|The %1 had an invalid datatype value (%2!ld!) set.|  
|0xC0204015|-1071628267|DTS_E_CODEPAGEREQUIRED|The "%1" requires a code page to be set but the value passed was zero.|  
|0xC0204016|-1071628266|DTS_E_INVALIDSTRINGLENGTH|The "%1" has a length that is not valid. The length must be between %2!ld! and %3!ld!.|  
|0xC0204017|-1071628265|DTS_E_INVALIDSCALE|The "%1" has a scale that is not valid. The scale must be between %2!ld! and %3!ld!.|  
|0xC0204018|-1071628264|DTS_E_INVALIDPRECISION|The "%1" has a precision that is not valid. The precision must be between %2!ld! and %3!ld!.|  
|0xC0204019|-1071628263|DTS_E_PROPVALUEIGNORED|The "%1" has a value set for length, precision, scale, or code page that is a value other than zero, but the data type requires the value to be zero.|  
|0xC020401A|-1071628262|DTS_E_CANTSETOUTPUTCOLUMNDATATYPEPROPERTIES|The %1 does not allow setting output column datatype properties.|  
|0xC020401B|-1071628261|DTS_E_INVALIDDATATYPEFORERRORCOLUMNS|The "%1" contains an invalid data type. "%1 " is a special error column,  and the only valid data type is DT_I4.|  
|0xC020401C|-1071628260|DTS_E_NOERRORDESCFORCOMPONENT|The component does not supply error code descriptions.|  
|0xC020401D|-1071628259|DTS_E_UNRECOGNIZEDERRORCODE|The specified error code is not associated with this component.|  
|0xC020401F|-1071628257|DTS_E_TRUNCATIONTRIGGEREDREDIRECTION|A truncation caused a row to be redirected, based on the truncation disposition settings.|  
|0xC0204020|-1071628256|DTS_E_CANTSETUSAGETYPETOREADWRITE|The "%1" is unable to make the column with lineage ID %2!d! read/write because that usage type is not allowed on this column. An attempt was made to change the usage type of an input column to a type, UT_READWRITE, that is not supported on this component.|  
|0xC0204023|-1071628253|DTS_E_CANTSETUSAGETYPE|The %1 has forbidden the requested use of the input column with lineage ID %2!d!.|  
|0xC0204024|-1071628252|DTS_E_FAILEDTOSETUSAGETYPE|The "%1" was unable to make the requested change to the input column with lineage ID %2!d!. The request failed with error code 0x%3!8.8X!. The specified error occurred while attempting to set the usage type of an input column.|  
|0xC0204025|-1071628251|DTS_E_FAILEDTOSETOUTPUTCOLUMNDATATYPEPROPERTIES|Attempt to set the data type properties on "%1" failed with error code 0x%2!8.8X!. The error occurred while attempting to set one or more of the data type properties of the output column.|  
|0xC0204026|-1071628250|DTS_E_UNABLETORETRIEVEMETADATA|The metadata for "%1" cannot be retrieved. Make sure the object name is correct and the object exists.|  
|0xC0204027|-1071628249|DTS_E_CANNOTMAPOUTPUTCOLUMN|The output column cannot be mapped to an external metadata column.|  
|0xC0204028|-1071628248|DTS_E_UNSUPPORTEDVARIABLETYPE|The variable %1 is required to be of type "%2".|  
|0xC020402A|-1071628246|DTS_E_CANTSETEXTERNALMETADATACOLUMNDATATYPEPROPERTIES|The %1 does not allow setting external metadata column datatype properties.|  
|0xC020402B|-1071628245|DTS_E_IDNOTINPUTNOROUTPUT|The ID, %1!lu!, is neither an input ID nor an output ID. The specified ID must be the input ID or the output ID that the external metadata collection is associated with.|  
|0xC020402C|-1071628244|DTS_E_METADATACOLLECTIONNOTUSED|The external metadata collection on "%1" is marked as not used, so no operations can be performed on it.|  
|0xC020402D|-1071628243|DTS_E_NOBUFFERTYPEONSYNCOUTPUT|The %1 is a synchronous output and the buffer type cannot be retrieved for a synchronous output.|  
|0xC0207000|-1071616000|DTS_E_INPUTCOLUMNUSAGETYPENOTREADONLY|The input column "%1" must be read-only. The input column has a usage type other than read-only, which is not allowed.|  
|0xC0207001|-1071615999|DTS_E_MISSINGCUSTOMPROPERTY|The "%1" is missing the required property "%2". The object is required to have the specified custom property.|  
|0xC0207002|-1071615998|DTS_E_ILLEGALCUSTOMOUTPUTPROPERTY|The output %1 cannot not have property "%2", but currently has that property assigned.|  
|0xC0207003|-1071615997|DTS_E_INVALIDOUTPUTEXCLUSIONGROUP|The %1 must be in exclusion group %2!d!. All outputs must be in the specified exclusion group.|  
|0xC0207004|-1071615996|DTS_E_PROPERTYISEMPTY|The property "%1" is empty. The property cannot be empty.|  
|0xC0207005|-1071615995|DTS_E_CREATEEXPRESSIONOBJECTFAILED|Memory cannot be allocated for the expression "%1". There was an out-of-memory error while creating an internal object to hold the expression.|  
|0xC0207006|-1071615994|DTS_E_EXPRESSIONPARSEFAILED|Cannot parse the expression "%1". The expression was not valid, or there is an out-of-memory error.|  
|0xC0207007|-1071615993|DTS_E_EXPRESSIONCOMPUTEFAILED|Computing the expression "%1" failed with error code 0x%2!8.8X!. The expression may have errors, such as divide by zero, that cannot be detected at parse time, or there may be an out-of-memory error.|  
|0xC0207008|-1071615992|DTS_E_FAILEDTOCREATEEXPRESSIONARRAY|Memory cannot be allocated for the Expression objects. An out-of-memory error occurred while creating the array of Expression object pointers.|  
|0xC020700A|-1071615990|DTS_E_FAILEDTOCREATEEXPRESSIONMANANGER|The %1 failed with error code 0x%2!8.8X! while creating the Expression Manager.|  
|0xC020700B|-1071615989|DTS_E_SPLITEXPRESSIONNOTBOOLEAN|The expression "%1" is not Boolean. The result type of the expression must be Boolean.|  
|0xC020700C|-1071615988|DTS_E_EXPRESSIONVALIDATIONFAILED|The expression "%1" on "%2" is not valid.|  
|0xC020700E|-1071615986|DTS_E_COLUMNNOTMATCHED|The column "%1" (%2!d!) cannot be matched to any input file column. The output column name or input column name cannot be found in the file.|  
|0xC020700F|-1071615985|DTS_E_SETRESULTCOLUMNFAILED|Attempting to set the result column for the expression "%1" on %2 failed with error code 0x%3!8.8X!. The input or output column that was to receive the result of the expression cannot be determined, or the expression result cannot be cast to the column type.|  
|0xC0207011|-1071615983|DTS_E_FAILEDTOGETLOCALEIDFROMPACKAGE|The %1 failed to get the locale ID from the package.|  
|0xC0207012|-1071615982|DTS_E_INCORRECTPARAMETERMAPPINGFORMAT|The parameter mapping string is not in the correct format.|  
|0xC0207013|-1071615981|DTS_E_NOTENOUGHPARAMETERSPROVIDED|The SQL command requires %1!d! parameters, but the parameter mapping only has %2!d! parameters.|  
|0xC0207014|-1071615980|DTS_E_PARAMETERNOTFOUNDINMAPPING|The SQL command requires a parameter named "%1", which is not found in the parameter mapping.|  
|0xC0207015|-1071615979|DTS_E_DUPLICATEDATASOURCECOLUMNNAME|There is more than one data source column with the name "%1".  The data source column names must be unique.|  
|0xC0207016|-1071615978|DTS_E_DATASOURCECOLUMNWITHNONAMEFOUND|There is a data source column with no name.  Each data source column must have a name.|  
|0xC0208001|-1071611903|DTS_E_DISCONNECTEDCOMPONENT|A component is disconnected from the layout.|  
|0xC0208002|-1071611902|DTS_E_INVALIDCOMPONENTID|The ID for a layout component is not valid.|  
|0xC0208003|-1071611901|DTS_E_INVALIDINPUTCOUNT|A component has an invalid number of inputs.|  
|0xC0208004|-1071611900|DTS_E_INVALIDOUTPUTCOUNT|A component has an invalid number of outputs.|  
|0xC0208005|-1071611899|DTS_E_NOINPUTSOROUTPUTS|A component does not have any inputs or outputs.|  
|0xC0208007|-1071611897|DTS_E_CANTALLOCATECOLUMNINFO|Not enough memory was available to allocate a list of the columns that are being manipulated by this component.|  
|0xC0208008|-1071611896|DTS_E_OUTPUTCOLUMNNOTININPUT|Output column "%1" (%2!d!) references input column with lineage ID %3!d!, but no input could be found with that lineage ID.|  
|0xC0208009|-1071611895|DTS_E_SORTNEEDSONEKEY|At least one input column must be marked as a sort key, but no keys were found.|  
|0xC020800A|-1071611894|DTS_E_SORTDUPLICATEKEYWEIGHT|Both column "%1" (%2!d!) and column "%3" (%4!d!) were marked with sort key weight %5!d!.|  
|0xC020800D|-1071611891|DTS_E_CANTMODIFYINVALID|The component cannot perform the requested metadata change until the validation problem is fixed.|  
|0xC020800E|-1071611890|DTS_E_CANTADDINPUT|An input cannot be added to the inputs collection.|  
|0xC020800F|-1071611889|DTS_E_CANTADDOUTPUT|An output cannot be added to the outputs collection.|  
|0xC0208010|-1071611888|DTS_E_CANTDELETEINPUT|An input cannot be deleted from the inputs collection.|  
|0xC0208011|-1071611887|DTS_E_CANTDELETEOUTPUT|An output cannot be removed from the outputs collection.|  
|0xC0208014|-1071611884|DTS_E_CANTCHANGEUSAGETYPE|The usage type of the column cannot be changed.|  
|0xC0208016|-1071611882|DTS_E_INVALIDUSAGETYPEFORCUSTOMPROPERTY|The %1 must be read/write to have custom property "%2". The input or output column has the specified custom property, but is not read/write. Remove the property, or make the column read/write.|  
|0xC0208017|-1071611881|DTS_E_READWRITECOLUMNMISSINGREQUIREDCUSTOMPROPERTY|The %1 is read/write and is required to have custom property "%2". Add the property, or make remove the read/write attribute from the column.|  
|0xC0208018|-1071611880|DTS_E_CANTDELETECOLUMN|The column cannot be deleted. The component does not allow columns to be deleted from this input or output.|  
|0xC0208019|-1071611879|DTS_E_CANTADDCOLUMN|The component does not allow adding columns to this input or output.|  
|0xC020801A|-1071611878|DTS_E_CANNOTTFINDRUNTIMECONNECTIONOBJECT|The connection "%1" cannot be found. Verify that the connection manager has a connection with that name.|  
|0xC020801B|-1071611877|DTS_E_CANNOTFINDRUNTIMECONNECTIONMANAGER|The runtime connection manager with the ID "%1" cannot be found. Verify that the connection manager collection has a connection manager with that ID.|  
|0xC020801C|-1071611876|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|SSIS Error Code DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER.  The AcquireConnection method call to the connection manager "%1" failed with error code 0x%2!8.8X!.  There may be error messages posted before this with more information on why the AcquireConnection method call failed.|  
|0xC020801D|-1071611875|DTS_E_ACQUIREDCONNECTIONISINVALID|The connection acquired from the connection manager "%1" is not valid.|  
|0xC020801E|-1071611874|DTS_E_INCORRECTCONNECTIONMANAGERTYPE|The connection manager "%1" is an incorrect type.  The type required is "%2". The type available to the component is "%3".|  
|0xC020801F|-1071611873|DTS_E_CANNOTACQUIREMANAGEDCONNECTIONFROMCONNECTIONMANAGER|Cannot acquire a managed connection from the run-time connection manager.|  
|0xC0208020|-1071611872|DTS_E_CANTINITINPUT|An input cannot be created to initialize the inputs collection.|  
|0xC0208021|-1071611871|DTS_E_CANTINITOUTPUT|An output cannot be created to initialize the outputs collection.|  
|0xC0208023|-1071611869|DTS_E_EXTRACTORCANTWRITE|Writing to the file "%1" failed with error code 0x%2!8.8X!.|  
|0xC0208024|-1071611868|DTS_E_INCORRECTCONNECTIONOBJECTTYPE|The connection manager "%1" returned an object of an  incorrect type from the AcquireConnection method.|  
|0xC0208025|-1071611867|DTS_E_INPUTCOLPROPERTYNOTFOUND|The "%3" property is required on input column "%1" (%2!d!), but is not found. The missing property should be added.|  
|0xC0208026|-1071611866|DTS_E_EXTRACTORUNREFERENCED|The "%1" is marked read-only, but is not referenced by any other column. Unreferenced columns are not allowed.|  
|0xC0208027|-1071611865|DTS_E_EXTRACTORREFERENCEDCOLUMNNOTFOUND|The "%1" references column ID %2!d!, and that column is not found on the input. A reference points to a nonexistent column.|  
|0xC0208028|-1071611864|DTS_E_EXTRACTORDATACOLUMNNOTBLOB|The "%1" references "%2", and that column is not of a BLOB type.|  
|0xC0208029|-1071611863|DTS_E_INSERTERREFERENCEDCOLUMNNOTFOUND|The "%1" references output column ID %2!d!, and that column is not found on the output.|  
|0xC020802A|-1071611862|DTS_E_INSERTERCANTREAD|Reading from the file "%1" failed with error code 0x%2!8.8X!.|  
|0xC020802B|-1071611861|DTS_E_TXSCD_NOTYPEDCOLUMNSATINPUT|There must be at least one column of Fixed, Changing, or Historical type on the input of a Slowly Changing Dimension transform. Verify that at least one column is a FixedAttribute, ChangingAttribute, or HistoricalAttribute.|  
|0xC020802C|-1071611860|DTS_E_TXSCD_INVALIDINPUTCOLUMNTYPE|The ColumnType property of "%1" is not valid. The current value is outside the range of acceptable values.|  
|0xC020802D|-1071611859|DTS_E_TXSCD_CANNOTMAPDIFFERENTTYPES|The input column "%1" cannot be mapped to external column "%2" because they have different data types. The Slowly Changing Dimension transform does not allow mapping between column of different types except for DT_STR and DT_WSTR.|  
|0xC020802E|-1071611858|DTS_E_NTEXTDATATYPENOTSUPPORTEDWITHANSIFILES|The data type for "%1" is DT_NTEXT, which is not supported with ANSI files. Use DT_TEXT instead and convert the data to DT_NTEXT using the data conversion component.|  
|0xC020802F|-1071611857|DTS_E_TEXTDATATYPENOTSUPPORTEDWITHUNICODEFILES|The data type for "%1" is DT_TEXT, which is not supported with Unicode files. Use DT_NTEXT instead and convert the data to DT_TEXT using the data conversion component.|  
|0xC0208030|-1071611856|DTS_E_IMAGEDATATYPENOTSUPPORTED|The data type for "%1" is DT_IMAGE, which is not supported. Use DT_TEXT or DT_NTEXT instead and convert the data from, or to, DT_IMAGE using the data conversion component.|  
|0xC0208031|-1071611855|DTS_E_FLATFILEFORMATNOTSUPPORTED|Format "%1" is not supported by Flat File Connection Manager. Supported formats are Delimited, FixedWidth, RaggedRight, and Mixed.|  
|0xC0208032|-1071611854|DTS_E_EXTRACTORFILENAMECOLUMNNOTSTRING|The "%1" should contain a file name, but it is not of a String type.|  
|0xC0208033|-1071611853|DTS_E_EXTRACTORCANTAPPENDTRUNCATE|Error caused by conflicting property settings. The "%1" has both the AllowAppend property and the ForceTruncate property set to TRUE. Both properties cannot be set to TRUE. Set one of the two properties to FALSE.|  
|0xC0208034|-1071611852|DTS_E_EXTRACTORCOLUMNALREADYREFERENCED|The %1 references column ID %2!d!, but that column is already referenced by %3. Remove one of the two reference to the column.|  
|0xC0208035|-1071611851|DTS_E_CONNECTIONMANANGERNOTASSIGNED|A connection manager has not been assigned to the %1.|  
|0xC0208036|-1071611850|DTS_E_INSERTERCOLUMNALREADYREFERENCED|The %1 references the output column with ID %2!d!, but that column is already referenced by %3.|  
|0xC0208037|-1071611849|DTS_E_INSERTERCOLUMNNOTREFERENCED|The "%1" is not referenced by any input column. Each output column must be referenced by exactly one input column.|  
|0xC0208038|-1071611848|DTS_E_INSERTERDATACOLUMNNOTBLOB|The "%1" references "%2", and that column is not the correct type. It must be DT_TEXT, DT_NTEXT, or DT_IMAGE. A reference points to a column that must be a BLOB.|  
|0xC0208039|-1071611847|DTS_E_INSERTERFILENAMECOLUMNNOTSTRING|The "%1" should contain a file name, but it is not a String type.|  
|0xC020803A|-1071611846|DTS_E_INSERTEREXPECTBOMINVALIDTYPE|The "%1" has the ExpectBOM property set to TRUE for %2, but the column is not NT_NTEXT. The ExpectBOM specifies that the Import Column transformation expects a byte-order mark (BOM). Either set the ExpectBOM property to false or change the output column data type to DT_NTEXT.|  
|0xC020803B|-1071611845|DTS_E_INSERTERINVALIDDATACOLUMNSETTYPE|Data output columns must be DT_TEXT, DT_NTEXT, or DT_IMAGE. The data output column may only be set to a BLOB type.|  
|0xC020803C|-1071611844|DTS_E_TXSCD_FIXEDATTRIBUTECHANGE|If the FailOnFixedAttributeChange property is set to TRUE, the transformation will fail when a fixed attribute change is detected. To send rows to the Fixed Attribute output, set the FailOnFixedAttributeChange property to FALSE.|  
|0xC020803D|-1071611843|DTS_E_TXSCD_LOOKUPFAILURE|The Lookup transformation failed to retrieve any rows. The transform fails when the FailOnLookupFailure is set to TRUE and no rows are retrieved.|  
|0xC020803E|-1071611842|DTS_E_TXSCD_INVALIDNUMBERSOFPARAMETERS|There must be at least one column type of Key on the input of a Slowly Changing Dimension transformation. Set at least one column type to Key.|  
|0xC020803F|-1071611841|DTS_E_TXSCD_CANNOTFINDEXTERNALCOLUMN|Cannot find external column with name "%1".|  
|0xC0208040|-1071611840|DTS_E_TXSCD_INFFEREDINDICATORNOTBOOL|Inferred indicator column "%1" must be of type DT_BOOL.|  
|0xC0208107|-1071611641|DTS_E_ERRORROWDISPMUSTBENOTUSED|The %1 must have its error row disposition value set to RD_NotUsed.|  
|0xC0208108|-1071611640|DTS_E_TRUNCROWDISPMUSTBENOTUSED|The %1 must have its truncation row disposition value set to RD_NotUsed.|  
|0xC0208201|-1071611391|DTS_E_TXAGG_INPUTNOTFOUNDFOROUTPUT|Cannot find input column with lineage ID %1!d! needed by output column with ID %2!d!.|  
|0xC0208202|-1071611390|DTS_E_TXAGG_INVALIDOUTPUTDATATYPEFORAGGREGATE|Invalid output data type for aggregate type specified at output column ID %1!d!.|  
|0xC0208203|-1071611389|DTS_E_TXAGG_INVALIDINPUTDATATYPEFORAGGREGATE|Invalid input data type for %1 used for the specified aggregate at %2.|  
|0xC0208204|-1071611388|DTS_E_TXAGG_INPUTOUTPUTDATATYPEMISMATCH|Data types of input column lineage ID %1!d! and output column ID %2!d! do not match.|  
|0xC0208205|-1071611387|DTS_E_UNABLETOGETINPUTBUFFERHANDLE|Cannot get input buffer handle for input ID %1!d!.|  
|0xC0208206|-1071611386|DTS_E_UNABLETOGETOUTPUTBUFFERHANDLE|Cannot get output buffer handle for output ID %1!d!.|  
|0xC0208207|-1071611385|DTS_E_UNABLETOFINDCOLUMNHANDLEINOUTPUTBUFFER|Cannot find column with lineage ID %1!d! in output buffer.|  
|0xC0208208|-1071611384|DTS_E_UNABLETOFINDCOLUMNHANDLEININPUTBUFFER|Cannot find column with lineage ID %1!d! in input buffer.|  
|0xC0208209|-1071611383|DTS_E_CANNOTHAVEZEROOUTPUTCOLUMNS|The number of output columns for %1 cannot be zero.|  
|0xC020820A|-1071611382|DTS_E_CONNECTIONMANAGERCOLUMNCOUNTMISMATCH|The number of columns in the flat file connection manager must be the same as the number of columns in the flat file adapter. The number of columns for the flat file connection manager is %1!d!, while the number of columns for the flat file adapter is %2!d!.|  
|0xC020820B|-1071611381|DTS_E_MISMATCHCONNECTIONMANAGERCOLUMN|The column "%1" at index %2!d! in the flat file connection manager was not found at index %3!d! in the column collection of the flat file adapter.|  
|0xC020820D|-1071611379|DTS_E_EXTERNALMETADATACOLUMNISALREADYMAPPED|The external metadata column with ID %1!d! has already been mapped to %2.|  
|0xC020820E|-1071611378|DTS_E_TXAGG_STRING_TOO_LONG|The transform encountered a key column that was larger than %1!u! characters.|  
|0xC020820F|-1071611377|DTS_E_DERIVEDRESULT_TOO_LONG|The transform encountered a result value that was longer than %1!u! bytes.|  
|0xC0208210|-1071611376|DTS_E_TXAGG_MEMALLOCERROUTPUTDESCRIPTORS|Unable to allocate memory.|  
|0xC0208211|-1071611375|DTS_E_TXAGG_MEMALLOCERRWORKSPACEDESCRIPTORS|Unable to allocate memory.|  
|0xC0208212|-1071611374|DTS_E_TXAGG_MEMALLOCERRSORTORDERDESCRIPTORS|Unable to allocate memory.|  
|0xC0208213|-1071611373|DTS_E_TXAGG_MEMALLOCERRNUMERICDESCRIPTORS|Unable to allocate memory.|  
|0xC0208214|-1071611372|DTS_E_TXAGG_MEMALLOCERRCOUNTDISTINCTDESCRIPTOR|Unable to allocate memory.|  
|0xC0208215|-1071611371|DTS_E_TXAGG_MEMALLOCERRWORKSPACESORTORDERDESCRIPTORS|Unable to allocate memory.|  
|0xC0208216|-1071611370|DTS_E_TXAGG_MEMALLOCERRWORKSPACENUMERICDESCRIPTORS|Unable to allocate memory.|  
|0xC0208217|-1071611369|DTS_E_TXAGG_MEMALLOCERRWORKSPACEBUFFCOLS|Unable to allocate memory.|  
|0xC0208218|-1071611368|DTS_E_UNREFERENCEDINPUTCOLUMN|The input column "%1" is not referenced.|  
|0xC0208219|-1071611367|DTS_E_CANTBUILDTHREADPOOL|The Sort transformation could not create a thread pool with %1!d! threads. Not enough memory is available.|  
|0xC020821A|-1071611366|DTS_E_QUEUEWORKITEMFAILED|The Sort transformation cannot queue a work item to its thread pool. There is not enough memory available.|  
|0xC020821B|-1071611365|DTS_E_SORTTHREADSTOPPED|A worker thread in the Sort transformation stopped with error code 0x%1!8.8X!. A catastrophic error was encountered while sorting a buffer.|  
|0xC020821E|-1071611362|DTS_E_SORTBADTHREADCOUNT|MaxThreads was %1!ld!, and should be between 1 and %2!ld!, inclusive or -1 to default to the number of CPUs.|  
|0xC020821F|-1071611361|DTS_E_DTPXMLLOADFAILURE|Unable to load from XML.|  
|0xC0208220|-1071611360|DTS_E_DTPXMLSAVEFAILURE|Unable to save to XML.|  
|0xC0208221|-1071611359|DTS_E_DTPXMLINT32CONVERTERR|Unable to convert the value "%1" to an integer.|  
|0xC0208222|-1071611358|DTS_E_DTPXMLBOOLCONVERTERR|Unable to convert the value "%1" to a Boolean.|  
|0xC0208223|-1071611357|DTS_E_DTPXMLPARSEERRORNEARID|Load error encountered near object with ID %1!d!.|  
|0xC0208226|-1071611354|DTS_E_DTPXMLPROPERTYTYPEERR|The value "%1" is not valid for the attribute "%2".|  
|0xC0208228|-1071611352|DTS_E_DTPXMLSETUSAGETYPEERR|The value "%1" is not valid for the attribute "%2".|  
|0xC0208229|-1071611351|DTS_E_DTPXMLDATATYPEERR|The value "%1" is not valid for the attribute "%2".|  
|0xC020822A|-1071611350|DTS_E_UNMAPPEDINPUTCOLUMN|The %1 is not mapped to an output column.|  
|0xC020822B|-1071611349|DTS_E_INPUTCOLUMNBADMAP|The %1 has a mapping that is not valid.  An output column with an ID of %2!ld! does not exist on this component.|  
|0xC020822D|-1071611347|DTS_E_MULTIPLYMAPPEDOUTCOL|The %1 is mapped to an output column that already has a mapping on this input.|  
|0xC020822E|-1071611346|DTS_E_TXAGG_STRINGPROMOTIONFAILED|Could not convert input column with Lineage ID %1!ld! to DT_WSTR due to error 0x%2!8.8X!.|  
|0xC0208230|-1071611344|DTS_E_DTPXMLIDLOOKUPERR|Referenced object with ID %1!d! not found in package.|  
|0xC0208231|-1071611343|DTS_E_DTPXMLINVALIDXMLPERSISTPROPERTY|Cannot read a persistence property required for the pipelinexml module. The property was not provided by the pipeline.|  
|0xC0208232|-1071611342|DTS_E_DTPXMLPROPERTYSTATEERR|The value "%1" is not valid for the attribute "%2".|  
|0xC0208233|-1071611341|DTS_E_CANTGETCUSTOMPROPERTY|Cannot retrieve custom property "%1".|  
|0xC0208234|-1071611340|DTS_E_UNABLETOLOCATEINPUTCOLUMNID|An input column with the lineage ID %1!d!, referenced in the ParameterMap custom property with the parameter on position number %2!d!, cannot be found in the input columns collection.|  
|0xC0208235|-1071611339|DTS_E_TXLOOKUP_UNABLETOLOCATEREFCOLUMN|Unable to locate reference column "%1".|  
|0xC0208236|-1071611338|DTS_E_TXLOOKUP_INCOMPATIBLEDATATYPES|%1 and reference column named "%2" have incompatible data types.|  
|0xC0208237|-1071611337|DTS_E_TXLOOKUP_PARAMMETADATAMISMATCH|The parameterized SQL statement yields metadata which does not match the main SQL statement.|  
|0xC0208238|-1071611336|DTS_E_TXLOOKUP_INCORRECTNUMOFPARAMETERS|The parameterized SQL statement contains an incorrect number of parameters. Expected %1!d!, but found %2!d!.|  
|0xC0208239|-1071611335|DTS_E_TXLOOKUP_INVALIDJOINTYPE|%1 has a datatype which cannot be joined on.|  
|0xC020823A|-1071611334|DTS_E_TXLOOKUP_INVALIDCOPYTYPE|%1 has a datatype which cannot be copied.|  
|0xC020823B|-1071611333|DTS_E_INSERTERINVALIDCOLUMNDATATYPE|The %1 has an unsupported datatype. It must be DT_STR or DT_WSTR.|  
|0xC020823C|-1071611332|DTS_E_EXTRACTORINVALIDCOLUMNDATATYPE|The %1 has an unsupported datatype. It must be DT_STR, DT_WSTR, DT_TEXT, DT_NTEXT, or DT_IMAGE.|  
|0xC020823D|-1071611331|DTS_E_TXCHARMAPINVALIDCOLUMNDATATYPE|The %1 has an unsupported datatype. It must be DT_STR, DT_WSTR, DT_TEXT, or DT_NTEXT.|  
|0xC020823E|-1071611330|DTS_E_SORTCANTCREATEEVENT|The Sort transformation cannot create an event to communicate with its worker threads. Not enough system handles are available to the Sort transformation.|  
|0xC020823F|-1071611329|DTS_E_SORTCANTCREATETHREAD|The Sort transformation cannot create a worker thread. Not enough memory is available to Sort transformation.|  
|0xC0208240|-1071611328|DTS_E_SORTCANTCOMPARE|The Sort transformation failed to compare row %1!d! in buffer ID %2!d! to row %3!d! in buffer ID %4!d!.|  
|0xC0208242|-1071611326|DTS_E_TXLOOKUP_TOOFEWREFERENCECOLUMNS|The Lookup transformation reference metadata contains too few columns. Check the SQLCommand property. The SELECT statement must return at least one column.|  
|0xC0208243|-1071611325|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNINFO|Unable to allocate memory for an array of ColumnInfo structures.|  
|0xC0208244|-1071611324|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNPAIR|Could not allocate memory for an array of ColumnPair structures.|  
|0xC0208245|-1071611323|DTS_E_TXLOOKUP_MALLOCERR_BUFFCOL|Unable to allocate memory for an array of BUFFCOL structures for the creation of a main workspace.|  
|0xC0208246|-1071611322|DTS_E_TXLOOKUP_MAINWORKSPACE_CREATEERR|Unable to create a main workspace buffer.|  
|0xC0208247|-1071611321|DTS_E_TXLOOKUP_HASHTABLE_MALLOCERR|Unable to allocate memory for hash table.|  
|0xC0208248|-1071611320|DTS_E_TXLOOKUP_HASHNODEHEAP_CREATEERR|Unable to allocate memory to create a heap for hash nodes.|  
|0xC0208249|-1071611319|DTS_E_TXLOOKUP_HASHNODEHEAP_MALLOCERR|Unable to allocate memory for a hash node heap.|  
|0xC020824A|-1071611318|DTS_E_TXLOOKUP_LRUNODEHEAP_CREATEERR|Unable to create a heap for LRU nodes. An out-of-memory condition occurred.|  
|0xC020824B|-1071611317|DTS_E_TXLOOKUP_LRUNODEHEAP_MALLOCERR|Unable to allocate memory for the LRU node heap. An out-of-memory condition occurred.|  
|0xC020824C|-1071611316|DTS_E_TXLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|OLE DB error occurred while loading column metadata. Check SQLCommand and SqlCommandParam properties.|  
|0xC020824D|-1071611315|DTS_E_TXLOOKUP_OLEDBERR_GETIROWSET|OLE DB error occurred while fetching rowset. Check SQLCommand and SqlCommandParam properties.|  
|0xC020824E|-1071611314|DTS_E_TXLOOKUP_OLEDBERR_FILLBUFFER|OLE DB error occurred while populating internal cache. Check SQLCommand and SqlCommandParam properties.|  
|0xC020824F|-1071611313|DTS_E_TXLOOKUP_OLEDBERR_BINDPARAMETERS|OLE DB error occurred while binding parameters. Check SQLCommand and SqlCommandParam properties.|  
|0xC0208250|-1071611312|DTS_E_TXLOOKUP_OLEDBERR_CREATEBINDING|OLE DB error occurred while creating bindings. Check SQLCommand and SqlCommandParam properties.|  
|0xC0208251|-1071611311|DTS_E_TXLOOKUP_INVALID_CASE|An invalid case was encountered in a switch statement during runtime.|  
|0xC0208252|-1071611310|DTS_E_TXLOOKUP_MAINWORKSPACE_MALLOCERR|Unable to allocate memory for a new row for the main workspace buffer. An out-of-memory condition occurred.|  
|0xC0208253|-1071611309|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMIROWSET|OLE DB error occurred while fetching parameterized rowset. Check SQLCommand and SqlCommandParam properties.|  
|0xC0208254|-1071611308|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMSINGLEROW|OLE DB error occurred while fetching parameterized row. Check SQLCommand and SqlCommandParam properties.|  
|0xC0208255|-1071611307|DTS_E_TXAGG_MAINWORKSPACE_MALLOCERR|Unable to allocate memory for a new row for the main workspace buffer. An out-of-memory condition occurred.|  
|0xC0208256|-1071611306|DTS_E_TXAGG_MAINWORKSPACE_CREATEERR|Unable to create a main workspace buffer.|  
|0xC0208257|-1071611305|DTS_E_TXAGG_HASHTABLE_MALLOCERR|Unable to allocate memory for the hash table.|  
|0xC0208258|-1071611304|DTS_E_TXAGG_HASHNODEHEAP_CREATEERR|Unable to allocate memory to create a heap for the hash nodes.|  
|0xC0208259|-1071611303|DTS_E_TXAGG_HASHNODEHEAP_MALLOCERR|Unable to allocate memory for the hash node heap.|  
|0xC020825A|-1071611302|DTS_E_TXAGG_CDNODEHEAP_CREATEERR|Unable to allocate memory to create a heap for CountDistinct nodes.|  
|0xC020825B|-1071611301|DTS_E_TXAGG_CDNODEHEAP_MALLOCERR|Unable to allocate memory for CountDistinct node heap.|  
|0xC020825C|-1071611300|DTS_E_TXAGG_CDCHAINHEAP_CREATEERR|Unable to allocate memory to create a heap for CountDistinct chains.|  
|0xC020825D|-1071611299|DTS_E_TXAGG_CDHASHTABLE_CREATEERR|Unable to allocate memory for CountDistinct hash table.|  
|0xC020825E|-1071611298|DTS_E_TXAGG_CDWORKSPACE_MALLOCERR|Unable to allocate memory for a new row for the CountDistinct workspace buffer.|  
|0xC020825F|-1071611297|DTS_E_TXAGG_CDWORKSPACE_CREATEERR|Unable to create a CountDistinct workspace buffer.|  
|0xC0208260|-1071611296|DTS_E_TXAGG_CDCOLLASSEARRAY_MALLOCERR|Unable to allocate memory for CountDistinct Collapse array.|  
|0xC0208261|-1071611295|DTS_E_TXAGG_CDCHAINHEAP_MALLOCERR|Unable to allocate memory for CountDistinct chains.|  
|0xC0208262|-1071611294|DTS_E_TXCOPYMAP_MISMATCHED_COLUMN_METADATA|Columns with lineage IDs %1!d! and %2!d! have mismatched metadata. The input column that is mapped to an output column for copymap does not have the same metadata (datatype, precision, scale, length, or codepage).|  
|0xC0208263|-1071611293|DTS_E_TXCOPYMAP_INCORRECT_OUTPUT_COLUMN_MAPPING|The output column with lineage ID "%1!d!" is incorrectly mapped to an input column. The CopyColumnId property of the output column is not correct.|  
|0xC0208265|-1071611291|DTS_E_CANTGETBLOBDATA|Failed to retrieve long data for column "%1".|  
|0xC0208266|-1071611290|DTS_E_CANTADDBLOBDATA|Long data was retrieved for a column but cannot be added to the Data Flow task buffer.|  
|0xC0208267|-1071611289|DTS_E_MCASTOUTPUTCOLUMNS|Output "%1" (%2!d!) has output columns, but multicast outputs do not declare columns. The package is damaged.|  
|0xC0208273|-1071611277|DTS_E_UNABLETOGETLOCALIZEDRESOURCE|Unable to load a localized resource ID %1!d!. Verify that the RLL file is present.|  
|0xC0208274|-1071611276|DTS_E_DTPXMLEVENTSCACHEERR|Cannot acquire Events Interface. An invalid Events interface was passed to the data flow module for persisting to XML.|  
|0xC0208275|-1071611275|DTS_E_DTPXMLPATHLOADERR|An error occurred while setting a path object during XML load.|  
|0xC0208276|-1071611274|DTS_E_DTPXMLINPUTLOADERR|Error setting input object during XML load.|  
|0xC0208277|-1071611273|DTS_E_DTPXMLOUTPUTLOADERR|Error setting output object during XML load.|  
|0xC0208278|-1071611272|DTS_E_DTPXMLINPUTCOLUMNLOADERR|Error setting input column object during XML load.|  
|0xC0208279|-1071611271|DTS_E_DTPXMLOUTPUTCOLUMNLOADERR|Error setting output column object during XML load.|  
|0xC0208280|-1071611264|DTS_E_DTPXMLPROPERTYLOADERR|Error setting property object during XML load.|  
|0xC0208281|-1071611263|DTS_E_DTPXMLCONNECTIONLOADERR|Error setting connection object during XML load.|  
|0xC0208282|-1071611262|DTS_E_FG_MISSING_OUTPUT_COLUMNS|Special transformation-specific columns are either missing or have incorrect types.|  
|0xC0208283|-1071611261|DTS_E_FG_PREPARE_TABLES_AND_ACCESSORS|Fuzzy Grouping transformation failed to create required tables and accessors.|  
|0xC0208284|-1071611260|DTS_E_FG_COPY_INPUT|Fuzzy Grouping transformation failed to copy input.|  
|0xC0208285|-1071611259|DTS_E_FG_GENERATE_GROUPS|Fuzzy Grouping transformation failed to generate groups.|  
|0xC0208286|-1071611258|DTS_E_FG_LEADING_TRAILING|An unexpected error occurred in Fuzzy Grouping when applying the settings of property '%1'.|  
|0xC0208287|-1071611257|DTS_E_FG_PICK_CANONICAL|The Fuzzy Grouping transformation failed to pick a canonical row of data to use in standardizing the data.|  
|0xC0208288|-1071611256|DTS_E_FG_NOBLOBS|Fuzzy Grouping does not support input columns of type IMAGE, TEXT, or NTEXT.|  
|0xC0208289|-1071611255|DTS_E_FG_FUZZY_MATCH_ON_NONSTRING|A fuzzy match is specified on column "%1" (%2!d!) that is not a data type of DT_STR or DT_WSTR.|  
|0xC020828A|-1071611254|DTS_E_FUZZYGROUPINGINTERNALPIPELINEERROR|A Fuzzy Grouping transformation pipeline error occurred and returned error code 0x%1!8.8X!: "%2".|  
|0xC020828B|-1071611253|DTS_E_CODE_PAGE_NOT_SUPPORTED|The code page %1!d! specified on column "%2" (%3!d!) is not supported.  You must first convert this column to DT_WSTR which can be done by inserting a Data Conversion Transform before this one.|  
|0xC0208294|-1071611244|DTS_E_SETEODFAILED|Failure encountered while setting end of data flag for the buffer driving output "%1" (%2!d!).|  
|0xC0208296|-1071611242|DTS_E_CANTCLONE|The input buffer could not be cloned. An out-of-memory condition occurred or there was an internal error.|  
|0xC02082F9|-1071611143|DTS_E_TXCHARMAP_CANTKATAKANAHIRAGANA|Column "%1" requests that Katakana and Hiragana characters be produced at the same time.|  
|0xC02082FA|-1071611142|DTS_E_TXCHARMAP_CANTSIMPLECOMPLEX|Column "%1" requests that Simple Chinese and Traditional Chinese characters be produced at the same time.|  
|0xC02082FB|-1071611141|DTS_E_TXCHARMAP_CANTFULLHALF|Column "%1" requests operations to generate both full width and half width characters.|  
|0xC02082FC|-1071611140|DTS_E_TXCHARMAP_CANTCHINAJAPAN|Column "%1" combines operations on Japanese characters with operations for Chinese characters.|  
|0xC02082FD|-1071611139|DTS_E_TXCHARMAP_CANTCASECHINESE|Column "%1" combines operations on Chinese characters with uppercase and lowercase operations.|  
|0xC02082FE|-1071611138|DTS_E_TXCHARMAP_CANTCASEJAPANESE|Column "%1" combines operations on Japanese characters with uppercase and lowercase operations.|  
|0xC02082FF|-1071611137|DTS_E_TXCHARMAP_CANTBOTHCASE|Column "%1" maps the column to both uppercase and lowercase.|  
|0xC0208300|-1071611136|DTS_E_TXCHARMAP_CANTLINGUISTIC|Column "%1" combines flags other than uppercase and lowercase with the linguistic casing operation.|  
|0xC0208301|-1071611135|DTS_E_TXCHARMAP_INVALIDMAPFLAGANDDATATYPE|The data type of column "%1" cannot be mapped as specified.|  
|0xC0208302|-1071611134|DTS_E_TXFUZZYLOOKUP_UNSUPPORTED_MATCH_INDEX_VERSION|The version (%1) of the pre-existing match index "%2" is not supported. The version expected is "%3". This error occurs if the version persisted in the index metadata does not match the version which the current code was built for. Fix the error by rebuilding the index with the current version of the code.|  
|0xC0208303|-1071611133|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX|The table "%1" does not appear to be a valid pre-built match index. This error occurs if the metadata record cannot be loaded from the specified pre-built index.|  
|0xC0208304|-1071611132|DTS_E_TXFUZZYLOOKUP_UNABLE_TO_READ_MATCH_INDEX|Unable to read specified pre-built match index "%1".  OLEDB Error code: 0x%2!8.8X!.|  
|0xC0208305|-1071611131|DTS_E_TXFUZZYLOOKUP_NO_JOIN_COLUMNS|There were no input columns with a valid join to a reference table column.  Make sure that there is at least one join defined using the input column properties JoinToReferenceColumn and JoinType.|  
|0xC0208306|-1071611130|DTS_E_TXFUZZYLOOKUP_INDEX_DOES_NOT_CONTAIN_COLUMN|The specified pre-existing match index "%1" was not originally built with fuzzy match information for column "%2".  It must be rebuilt to include this information. This error occurs when the index was built with the column not being a fuzzy join column.|  
|0xC0208307|-1071611129|DTS_E_TXFUZZYLOOKUP_IDENTIFIER_PROPERTY|The name "%1" given for property "%2" is not a valid SQL identifier name. This error occurs if the name for the property does not conform to the specifications for a valid SQL identifier name.|  
|0xC0208309|-1071611127|DTS_E_TXFUZZYLOOKUP_MINSIMILARITY_INVALID|The MinSimilarity threshold property on the Fuzzy Lookup transformation must be a value greater than or equal to 0.0 but less than 1.0.|  
|0xC020830A|-1071611126|DTS_E_TXFUZZYLOOKUP_INVALID_PROPERTY_VALUE|The value "%1" for property "%2" is not valid.|  
|0xC020830B|-1071611125|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_FUZZY_JOIN_DATATYPES|The fuzzy lookup specified between input column "%1" and reference column "%2" is not valid because fuzzy joins are only supported between string columns, types DT_STR and DT_WSTR.|  
|0xC020830C|-1071611124|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_EXACT_JOIN_DATATYPES|The exact lookup columns, "%1" and "%2", do not have equal data types or are not comparable string types. Exact joins are supported between columns with equal data types or a DT_STR and DT_WSTR combination.|  
|0xC020830D|-1071611123|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_COPYCOLUMN_DATATYPES|The copy columns, "%1" and "%2", do not have equal data types or are not trivially convertible string types. This occurs because copying from reference to output between columns with equal data types, or a DT_STR and DT_WSTR combination, is supported, but other types are not.|  
|0xC020830E|-1071611122|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_PASSTHRUCOLUMN_DATATYPES|The passthrough columns, "%1" and "%2", do not have equal data types. Only columns with equal data types are supported as passthrough columns from input to output.|  
|0xC020830F|-1071611121|DTS_E_TXFUZZYLOOKUP_UNABLETOLOCATEREFCOLUMN|Cannot locate reference column "%1".|  
|0xC0208311|-1071611119|DTS_E_TXFUZZYLOOKUP_OUTPUT_COLUMN_MUST_BE_PASSTHRU_COLUMN_OR_A_COPY_COLUMN|An output column must have exactly one CopyColumn or PassThruColumn property specified. This error occurs when neither the CopyColumn or the PassThruColumn properties, or both the CopyColumn and PassThruColumn properties, are set to non-empty values.|  
|0xC0208312|-1071611118|DTS_E_TXFUZZYLOOKUP_PASSTHRU_COLUMN_NOT_FOUND|The source lineage id '%1!d!' specified for property '%2' on output column '%3' was not found in the input column collection. This occurs when the input column id specified on an output column as a passthrough column is not found in the set of inputs.|  
|0xC0208313|-1071611117|DTS_E_TXFUZZYLOOKUP_INDEXED_COLUMN_NOT_FOUND_IN_REF_TABLE|The column "%1" in the pre-built index "%2" was not found in the reference table/query. This happens if the schema/query of the reference table has changed since the pre-existing match index was built.|  
|0xC0208314|-1071611116|DTS_E_TXFUZZYLOOKUP_TOKEN_TOO_LONG|The component encountered a token that was larger than 2147483647 characters.|  
|0xC0208315|-1071611115|DTS_E_RAWMETADATAMISMATCHTYPE|The output file cannot be appended. Column "%1" matches by name, but the column in the file has type %2 and the input column has type %3. The metadata for the column does not match on data type.|  
|0xC0208316|-1071611114|DTS_E_RAWMETADATAMISMATCHSIZE|The output file cannot be appended. Column "%1" matches by name, but the column in the file has maximum length %2!d! and the input column has maximum length %3!d!. The metadata for the column does not match in length.|  
|0xC0208317|-1071611113|DTS_E_RAWMETADATAMISMATCHCODEPAGE|The output file cannot be appended. Column "%1" matches by name, but the column in the file has code page %2!d! and the input column has code page %3!d!. The metadata for the named column does not match on code page.|  
|0xC0208318|-1071611112|DTS_E_RAWMETADATAMISMATCHPRECISION|The output file cannot be appended. Column "%1" matches by name, but the column in the file has precision %2!d! and the input column has precision %3!d!. The metadata for the named column does not match on precision.|  
|0xC0208319|-1071611111|DTS_E_RAWMETADATAMISMATCHSCALE|The output file cannot be appended. Column "%1" matches by name, but the column in the file has scale %2!d! and the input column has scale %3!d!.  The metadata for the named column does not match on scale.|  
|0xC020831A|-1071611110|DTS_E_COULD_NOT_DETERMINE_DATASOURCE_DBMSNAME|Unable to determine the DBMS name and version on "%1". This occurs if the IDBProperties on the connection did not return information needed to verify the DBMS name and version.|  
|0xC020831B|-1071611109|DTS_E_INCORRECT_SQL_SERVER_VERSION|The DBMS type or version of "%1" is not supported.  A connection to Microsoft SQL Server version 8.0 or later is required. This occurs if IDBProperties on the connection did not return a the correct version.|  
|0xC020831D|-1071611107|DTS_E_CANTDELETEERRORCOLUMNS|The %1 is a special error output column and cannot be deleted.|  
|0xC020831E|-1071611106|DTS_E_UNEXPECTEDCOLUMNDATATYPE|The data type specified for column "%1" is not the expected type "%2".|  
|0xC020831F|-1071611105|DTS_E_INPUTCOLUMNNOTFOUND|The input column lineage ID "%1" referenced by property "%2" on output column "%3" could not be located in the input column collection.|  
|0xC0208320|-1071611104|DTS_E_TXGROUPDUPS_INPUTCOLUMNNOTJOINED|The input column "%1" referenced by the "%2" property on output column "%3" must have property ToBeCleaned=True and have a valid ExactFuzzy property value.|  
|0xC0208322|-1071611102|DTS_E_TXFUZZYLOOKUP_REF_TABLE_MISSING_IDENTITY_INDEX|The reference table '%1' does not have a clustered index on an integer identity column, which is required if the property 'CopyRefTable' is set to FALSE. If CopyRefTable is false, the reference table must have a clustered index on an integer identity column.|  
|0xC0208323|-1071611101|DTS_E_TXFUZZYLOOKUP_REF_CONTAINS_NON_INTEGER_IDENT_COLUMN|The reference table '%1' contains a non-integer type identity column which is not supported. Use a view of the table without the column '%2'.  This error occurs  because when a copy is made of the reference table, an integer identity column is added, and only one identity column is allowed per table.|  
|0xC0208324|-1071611100|DTS_E_TXFUZZY_MATCHCONTRIBUTION_AND_HIERARCHY_SPECIFIED|Both MatchContribution and hierarchy information cannot be specified at the same time. This is not allowed because these properties are both weighing factors for scoring.|  
|0xC0208325|-1071611099|DTS_E_TXFUZZY_HIERARCHY_INCORRECT|Levels in hierarchy should be unique numbers . Valid  level in hierarchy values are integers greater than or equal to 1. The smaller the number is, the lower the column is in the hierarchy. The default value is 0, indicating that the column is not part of a hierarchy. Overlaps and gaps are not allowed.|  
|0xC0208326|-1071611098|DTS_E_TXFUZZYGROUPING_INSUFFICIENT_FUZZY_JOIN_COLUMNS|No columns to fuzzy group on were defined.  There must be at least one input column with column properties ToBeCleaned=true and ExactFuzzy=2.|  
|0xC0208329|-1071611095|DTS_E_TXFUZZYLOOKUP_COLUMNINVALID|The column with ID '%1!d!' was not valid for an undetermined reason.|  
|0xC020832A|-1071611094|DTS_E_TXFUZZYLOOKUP_UNSUPPORTEDDATATYPE|The data type of column '%1' is not supported.|  
|0xC020832C|-1071611092|DTS_E_TXFUZZYLOOKUP_OUTPUTLENGTHMISMATCH|The length of output column '%1' is less than that of its source column '%2'.|  
|0xC020832F|-1071611089|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFINPUTCOLUMNS|There should be only one input column.|  
|0xC0208330|-1071611088|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFOUTPUTCOLUMNS|There should be exactly two output columns.|  
|0xC0208331|-1071611087|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFINPUTCOLUMN|The input column can only have DT_WSTR or DT_NTEXT as its data type.|  
|0xC0208332|-1071611086|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFOUTPUTCOLUMN|The output column [%1!d!] can only have '%2' as its data type.|  
|0xC0208333|-1071611085|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFREFERENCECOLUMN|The reference column can only have DT_STR or DT_WSTR as its data type.|  
|0xC0208334|-1071611084|DTS_E_TERMEXTRACTION_UNABLETOLOCATEREFCOLUMN|An error occurred while locating the reference column '%1'.|  
|0xC0208335|-1071611083|DTS_E_TERMEXTRACTION_INCORRECTTERMTYPE|The Term Type of the transformation can only be WordOnly, PhraseOnly or WordPhrase.|  
|0xC0208336|-1071611082|DTS_E_TERMEXTRACTION_INCORRECTFREQUENCYTHRESHOLD|The value of Frequency Threshold should not be lower than '%1!d!'.|  
|0xC0208337|-1071611081|DTS_E_TERMEXTRACTION_INCORRECTMAXLENOFTERM|The value of Max Length of Term should not be lower than '%1!d!'.|  
|0xC0208338|-1071611080|DTS_E_TERMEXTRACTION_TOOFEWREFERENCECOLUMNS|Term Extraction reference metadata contains too few columns.|  
|0xC0208339|-1071611079|DTS_E_TERMEXTRACTION_MALLOCERR_REFERENCECOLUMNINFO|An error occurred while allocating memory.|  
|0xC020833A|-1071611078|DTS_E_TERMEXTRACTION_MAINWORKSPACE_CREATEERR|An error occurred while creating a workspace buffer.|  
|0xC020833B|-1071611077|DTS_E_TERMEXTRACTION_OLEDBERR_CREATEBINDING|An OLEDB error occurred while creating bindings.|  
|0xC020833C|-1071611076|DTS_E_TERMEXTRACTION_OLEDBERR_GETIROWSET|An OLEDB error occurred while fetching rowsets.|  
|0xC020833D|-1071611075|DTS_E_TERMEXTRACTION_OLEDBERR_FILLBUFFER|An OLEDB error occurred while populating internal cache.|  
|0xC020833E|-1071611074|DTS_E_TERMEXTRACTION_PROCESSERR|An error occurred while extracting terms on row %1!ld!, column %2!ld!. The error code returned was 0x%3!8.8X!. Please remove it from the input as a work-around.|  
|0xC020833F|-1071611073|DTS_E_TERMEXTRACTIONORLOOKUP_PROCESSERR_DEPOSITFULL|The number of the term candidates exceeds its limit, 4G.|  
|0xC0208340|-1071611072|DTS_E_TERMEXTRACTION_INVALIDOUTTERMTABLEORCOLUMN|The reference table, view, or column that is used for Exclusion Terms is not valid.|  
|0xC0208341|-1071611071|DTS_E_TXFUZZYLOOKUP_STRINGCOLUMNTOOLONG|The length of string column '%1' exceeds 4000 characters.  A conversion from DT_STR to DT_WSTR is necessary, so a truncation would occur.  Either reduce the column width or use only DT_WSTR column types.|  
|0xC0208342|-1071611070|DTS_E_TERMEXTRACTION_OUTTERMTABLEANDCOLUMNNOTSET|The reference table, view, or column to be used for an Exclusion Terms has not been set.|  
|0xC0208343|-1071611069|DTS_E_TERMLOOKUP_TOOFEWOUTPUTCOLUMNS|Term Lookup contains too few output columns.|  
|0xC0208344|-1071611068|DTS_E_TERMLOOKUP_INCORRECTDATATYPEOFREFERENCECOLUMN|The reference column can only have DT_STR or DT_WSTR as its data type.|  
|0xC0208345|-1071611067|DTS_E_TERMLOOKUP_UNABLETOLOCATEREFCOLUMN|An error occurred while locating the reference column '%1'.|  
|0xC0208346|-1071611066|DTS_E_TERMLOOKUP_TOOFEWREFERENCECOLUMNS|Term Lookup reference metadata contains too few columns.|  
|0xC0208347|-1071611065|DTS_E_TERMEXTRACTIONORLOOKUP_TESTOFFSETERROR|An error occurred while normalizing words.|  
|0xC0208348|-1071611064|DTS_E_TERMLOOKUP_MAINWORKSPACE_CREATEERR|An error occurred while creating a workspace buffer.|  
|0xC0208349|-1071611063|DTS_E_TERMLOOKUP_OLEDBERR_CREATEBINDING|An OLEDB error occurred while creating bindings.|  
|0xC020834A|-1071611062|DTS_E_TERMLOOKUP_OLEDBERR_GETIROWSET|An OLEDB error occurred while fetching rowsets.|  
|0xC020834B|-1071611061|DTS_E_TERMLOOKUP_OLEDBERR_FILLBUFFER|An OLEDB error occurred while populating internal cache.|  
|0xC020834C|-1071611060|DTS_E_TERMLOOKUP_PROCESSERR|An error occurred while looking up terms on row %1!ld!, column %2!ld!. The error code returned was 0x%3!8.8X!. Please remove it from the input as a work-around.|  
|0xC020834D|-1071611059|DTS_E_TERMLOOKUP_TEXTIDINPUTCOLUMNNOTMAPPEDWITHOUTPUTCOLUMN|At least one Passthrough column is not mapped to an output column.|  
|0xC020834E|-1071611058|DTS_E_TERMLOOKUP_INCORRECTEXACTNUMBEROFTEXTCOLUMNS|There should be exactly one input column mapped to one reference column.|  
|0xC020834F|-1071611057|DTS_E_TERMLOOKUP_TEXTINPUTCOLUMNHAVEINCORRECTDATATYPE|The input column mapped to a reference column can only have DT_NTXT or DT_WSTR as its data type.|  
|0xC0208354|-1071611052|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX_NAME|The reference table name "%1" is not a valid SQL identifier. This error occurs if the table name cannot be parsed from the input string. There may be unquoted spaces in the name. Verify that the name is correctly quoted.|  
|0xC0208355|-1071611051|DTS_E_TERMEXTRACTION_TERMFILTERSTARTITERATIONERROR|An error occurred while the Term Filter was starting its iteration.|  
|0xC0208356|-1071611050|DTS_E_TERMEXTRACTION_EMPTYTERMRESULTERROR|An error occurred while reclaiming the buffer used for caching terms. The error code returned was 0x%1!8.8X!.|  
|0xC0208357|-1071611049|DTS_E_TERMEXTRACTION_STDLENGTHERROR|An std::length_error occurred from the STL containers.|  
|0xC0208358|-1071611048|DTS_E_TERMLOOKUP_SAVEWORDWITHPUNCTERROR|An error occurred while saving words with punctuation characters. The error code returned was 0x%1!8.8X!.|  
|0xC0208359|-1071611047|DTS_E_TERMLOOKUP_ADDREFERENCETERM|An error occurred while processing the %1!ld!th reference term. The error code returned was 0x%2!8.8X!. Please remove the reference term from your reference table as a work-around.|  
|0xC020835A|-1071611046|DTS_E_TERMLOOKUP_SORREFERENCETERM|An error occurred while sorting reference terms. The error code returned was 0x%1!8.8X!.|  
|0xC020835B|-1071611045|DTS_E_TERMLOOKUP_COUNTTERM|An error occurred while counting term candidates. The error code returned was 0x%1!8.8X!.|  
|0xC020835C|-1071611044|DTS_E_FUZZYLOOKUP_REFERENCECACHEFULL|Fuzzy Lookup was unable to load the entire reference table into main memory as is required when the Exhaustive property is enabled.  Either we ran out of system memory or a limit was specified for MaxMemoryUsage which was not sufficient to load the reference table.  Either set MaxMemoryUsage to 0 or increase it significantly.  Alternatively, disable Exhaustive.|  
|0xC020835D|-1071611043|DTS_E_TERMLOOKUP_INITIALIZE|An error occurred while initializing the engine of Term Lookup. The error code returned was 0x%1!8.8X!.|  
|0xC020835E|-1071611042|DTS_E_TERMLOOKUP_PROCESSSENTENCE|An error occurred while processing sentences. The error code returned was 0x%1!8.8X!.|  
|0xC020835F|-1071611041|DTS_E_TEXTMININGBASE_APPENDTOTEMPBUFFER|An error occurred while adding strings to an internal buffer. The error code returned was 0x%1!8.8X!.|  
|0xC0208360|-1071611040|DTS_E_TERMEXTRACTION_SAVEPOSTAG|An error occurred while saving part-of-speech tags from an internal buffer. The error code returned was 0x%1!8.8X!.|  
|0xC0208361|-1071611039|DTS_E_TERMEXTRACTION_COUNTTERM|An error occurred while counting term candidates. The error code returned was 0x%1!8.8X!.|  
|0xC0208362|-1071611038|DTS_E_TERMEXTRACTION_INITPOSPROCESSOR|An error occurred while initializing the part-of-speech processor. The error code returned was 0x%1!8.8X!.|  
|0xC0208363|-1071611037|DTS_E_TERMEXTRACTION_INITFSA|An error occurred while loading the finite state automata. The error code returned was 0x%1!8.8X!.|  
|0xC0208364|-1071611036|DTS_E_TERMEXTRACTION_INITIALIZE|An error occurred while initializing the engine of Term Extraction. The error code returned was 0x%1!8.8X!.|  
|0xC0208365|-1071611035|DTS_E_TERMEXTRACTION_PROCESSSENTENCE|An error occurred while processing within a sentence. The error code returned was 0x%1!8.8X!.|  
|0xC0208366|-1071611034|DTS_E_TERMEXTRACTION_INITPOSTAGVECTOR|An error occurred while initializing the part-of-speech processor. The error code returned was 0x%1!8.8X!.|  
|0xC0208367|-1071611033|DTS_E_TERMEXTRACTION_SAVEPTRSTRING|An error occurred while adding strings to an internal buffer. The error code returned was 0x%1!8.8X!.|  
|0xC0208368|-1071611032|DTS_E_TERMEXTRACTION_ADDWORDTODECODER|An error occurred while adding words to a statistical decoder. The error code returned was 0x%1!8.8X!.|  
|0xC0208369|-1071611031|DTS_E_TERMEXTRACTION_DECODE|An error occurred while decoding for a sentence. The error code returned was 0x%1!8.8X!.|  
|0xC020836A|-1071611030|DTS_E_TERMEXTRACTION_SETEXCLUDEDTERM|An error occurred while setting exclusion terms. The error code returned was 0x%1!8.8X!.|  
|0xC020836B|-1071611029|DTS_E_TERMEXTRACTION_PROCESSDOCUMENT|An error occurred while processing a document in the input. The error code returned was 0x%1!8.8X!.|  
|0xC020836C|-1071611028|DTS_E_TEXTMININGBASE_TESTPERIOD|An error occurred while testing whether a dot is a part of an acronym. The error code returned was 0x%1!8.8X!.|  
|0xC020836D|-1071611027|DTS_E_TERMLOOKUP_ENGINEADDREFERENCETERM|An error occurred while setting reference terms. The error code returned was 0x%1!8.8X!.|  
|0xC020836E|-1071611026|DTS_E_TERMLOOKUP_PROCESSDOCUMENT|An error occurred while processing a document in the input. The error code returned was 0x%1!8.8X!.|  
|0xC020836F|-1071611025|DTS_E_INVALIDBULKINSERTPROPERTYVALUE|The value for the property %1 is %2!d!, which is not allowed.  The value must be greater than or equal to %3!d!.|  
|0xC0208370|-1071611024|DTS_E_INVALIDBULKINSERTFIRSTROWLASTROWVALUES|The value for the property %1 is %2!d!, which must be less than or equal to the value of %3!d! for property %4.|  
|0xC0208371|-1071611023|DTS_E_FUZZYLOOKUPUNABLETODELETEEXISTINGMATCHINDEX|An error was encountered when trying to delete the existing fuzzy match index named "%1". It is possible that this table was not created by Fuzzy Lookup (or this version of Fuzzy Lookup), it has been damaged, or there is another problem. Try manually deleting the table named "%2" or specify a different name for the MatchIndexName property.|  
|0xC0208372|-1071611022|DTS_E_TERMEXTRACTION_INCORRECTSCORETYPE|The Score Type of the transformation can only be Frequency or TFIDF.|  
|0xC0208373|-1071611021|DTS_E_FUZZYLOOKUPREFTABLETOOBIG|The reference table specified has too many rows. Fuzzy Lookup only works with reference tables having less than 1 billion rows. Consider using a smaller view of your reference table.|  
|0xC0208374|-1071611020|DTS_E_FUZZYLOOKUPUNABLETODETERMINEREFERENCETABLESIZE|Unable to determine the size of the reference table '%1'.  It is possible that this object is a view and not a table.  Fuzzy Lookup does not support views when CopyReferentaceTable=false.  Make sure that the table exists and that CopyReferenceTable=true.|  
|0xC0208377|-1071611017|DTS_E_XMLSRCOUTPUTCOLUMNDATATYPENOTSUPPORTED|The SSIS Data Flow Task data type "%1" on the %2 is not supported for the %3.|  
|0xC0208378|-1071611016|DTS_E_XMLSRCCANNOTFINDCOLUMNTOSETDATATYPE|Unable to set data type properties for the output column with ID %1!d! on the output with ID %2!d!. The output or column could not be found.|  
|0xC0208379|-1071611015|DTS_E_CUSTOMPROPERTYISREADONLY|The value of custom property "%1" on the %2 cannot be changed.|  
|0xC020837A|-1071611014|DTS_E_OUTPUTCOLUMNHASNOERRORCOLUMN|The %1 on the non-error output has no corresponding output column on the error output.|  
|0xC020837B|-1071611013|DTS_E_ERRORCOLUMNHASNOOUTPUTCOLUMN|The %1 on the error output has no corresponding output column on the non-error output.|  
|0xC020837C|-1071611012|DTS_E_ERRORCOLUMNHASINCORRECTPROPERTIES|The %1 on the error output has properties that do not match the properties of its corresponding data source column.|  
|0xC020837D|-1071611011|DTS_E_ADOSRCOUTPUTCOLUMNDATATYPECANNOTBECHANGED|The data type of output columns on the %1 cannot be changed, except for DT_WSTR and DT_NTEXT columns.|  
|0xC020837F|-1071611009|DTS_E_ADOSRCDATATYPEMISMATCH|The data type of "%1" does not match the data type "%2" of the source column "%3".|  
|0xC0208380|-1071611008|DTS_E_ADOSRCCOLUMNNOTINSCHEMAROWSET|The %1 does not have a matching source column in the schema.|  
|0xC0208381|-1071611007|DTS_E_TERMLOOKUP_INVALIDREFERENCETERMTABLEORCOLUMN|The reference table/view or column used for the reference terms is invalid.|  
|0xC0208382|-1071611006|DTS_E_TERMLOOKUP_REFERENCETERMTABLEANDCOLUMNNOTSET|The reference table/view or column used for the reference terms has not been set.|  
|0xC0208383|-1071611005|DTS_E_COLUMNMAPPEDTOALREADYMAPPEDEXTERNALMETADATACOLUMN|The %1 is mapped to the external metadata column with ID %2!ld!, which is already mapped to another column.|  
|0xC0208384|-1071611004|DTS_E_TXFUZZYLOOKUP_TOOMANYPREFIXES|The SQL object name '%1' specified for property '%2' contains more than the maximum number of prefixes.  The maximum is 2.|  
|0xC0208385|-1071611003|DTS_E_MGDSRCSTATIC_OVERFLOW|The value was too large to fit in the column.|  
|0xC0208386|-1071611002|DTS_E_DATAREADERDESTREADERISCLOSED|The SSIS IDataReader is closed.|  
|0xC0208387|-1071611001|DTS_E_DATAREADERDESTREADERISATEND|The SSIS IDataReader is past the end of the result set.|  
|0xC0208388|-1071611000|DTS_E_DATAREADERDESTINVALIDCOLUMNORDINAL|The ordinal position of the column is not valid.|  
|0xC0208389|-1071610999|DTS_E_DATAREADERDESTCANNOTCONVERT|Cannot convert the %1 from data type "%2" to data type "%3".|  
|0xC020838A|-1071610998|DTS_E_DATAREADERDESTINVALIDCODEPAGE|The %1 has unsupported code page %2!d!.|  
|0xC020838B|-1071610997|DTS_E_XMLSRCEXTERNALMETADATACOLUMNNOTINSCHEMA|The %1 has no mapping to the XML schema.|  
|0xC020838D|-1071610995|DTS_E_TXTERMLOOKUP_MISMATCHED_COLUMN_METADATA|Columns with lineage IDs %1!d! and %2!d! have mismatched metadata. The input column that is mapped to an output column does not have the same metadata (datatype, precision, scale, length, or codepage).|  
|0xC020838E|-1071610994|DTS_E_DATAREADERDESTREADERTIMEOUT|The SSIS IDataReader is closed. The read timeout has expired.|  
|0xC020838F|-1071610993|DTS_E_ADOSRCINVALIDSQLCOMMAND|An error occurred executing the provided SQL command: "%1". %2|  
|0xC0208390|-1071610992|DTS_E_JOINTYPEDOESNTMATCHETI|The JoinType property specified for input column '%1' differs from the JoinType specified for the corresponding reference table column when the Match Index was initially created.  Either rebuild the Match Index with the given JoinType or change the JoinType to match the type used when the Match Index was created.|  
|0xC0208392|-1071610990|DTS_E_SQLCEDESTDATATYPENOTSUPPORTED|The data type "%1" found on column "%2" is not supported for the %3.|  
|0xC0208393|-1071610989|DTS_E_DATAREADERDESTDATATYPENOTSUPPORTED|The data type "%1" found on %2 is not supported for the %3.|  
|0xC0208394|-1071610988|DTS_E_RECORDSETDESTDATATYPENOTSUPPORTED|The data type of the %1 is not supported for the %2.|  
|0xC0208446|-1071610810|DTS_E_TXSCRIPTMIGRATIONCOULDNOTADDREFERENCE|Failed to add project reference "%1" while migrating %2. Migration might need to be completed manually.|  
|0xC0208447|-1071610809|DTS_E_TXSCRIPTMIGRATIONMULTIPLEENTRYPOINTSFOUND|Multiple entry points with the name "%1" were found during the migration of %2. Migration might need to be completed manually.|  
|0xC0208448|-1071610808|DTS_E_TXSCRIPTMIGRATIONNOENTRYPOINTFOUND|No entry point was found during the migration of %1. Migration might need to be completed manually.|  
|0xC020844B|-1071610805|DTS_E_ADODESTINSERTIONFAILURE|An exception has occurred during data insertion, the message returned from the provider is: %1|  
|0xC020844C|-1071610804|DTS_E_ADODESTCONNECTIONTYPENOTSUPPORTED|Failed to retrieve the provider invariant name from %1, it is currently not supported by ADO NET Destination component|  
|0xC020844D|-1071610803|DTS_E_ADODESTARGUMENTEXCEPTION|An argument exception has occurred while data provider tried to insert data to destination. The returned message is : %1|  
|0xC020844E|-1071610802|DTS_E_ADODESTWRONGBATCHSIZE|The BatchSize property must be a non-negative integer|  
|0xC020844F|-1071610801|DTS_E_ADODESTERRORUPDATEROW|An error has occurred while sending this row to destination data source.|  
|0xC0208450|-1071610800|DTS_E_ADODESTEXECUTEREADEREXCEPTION|Executing tSQL command throws an exception, the message is :  %1|  
|0xC0208451|-1071610799|DTS_E_ADODESTDATATYPENOTSUPPORTED|The data type "%1" found on column "%2" is not supported for the %3.|  
|0xC0208452|-1071610798|DTS_E_ADODESTFAILEDTOACQUIRECONNECTION|ADO NET Destination has failed to acquire the connection %1. The connection may have been corrupted.|  
|0xC0208453|-1071610797|DTS_E_ADODESTNOTMANAGEDCONNECTION|The specified connection %1 is not managed, please use managed connection for ADO NET destination.|  
|0xC0208454|-1071610796|DTS_E_ADODESTNOERROROUTPUT|The destination component does not have an error output. It may have been corrupted.|  
|0xC0208455|-1071610795|DTS_E_ADODESTNOLINEAGEID|The lineageID %1 associated with external column %2 does not exist at run time.|  
|0xC0208456|-1071610794|DTS_E_ADODESTEXTERNALCOLNOTEXIST|The %1 does not exist in the database. It may have been removed or renamed.|  
|0xC0208457|-1071610793|DTS_E_ADODESTGETSCHEMATABLEFAILED|Failed to get properties of external columns. The table name you entered may not exist, or you do not have SELECT permission on the table object and an alternative attempt to get column properties through connection has failed. Detailed error messages are: %1|  
|0xC0208458|-1071610792|DTS_E_ADODESTCOLUMNERRORDISPNOTSUPPORTED|Input column error disposition is not supported by ADO NET Destination component.|  
|0xC0208459|-1071610791|DTS_E_ADODESTCOLUMNTRUNDISPNOTSUPPORTED|Input column truncation disposition is not supported by ADO NET Destination component.|  
|0xC020845A|-1071610790|DTS_E_ADODESTINPUTTRUNDISPNOTSUPPORTED|Input  truncation row disposition is not supported by ADO NET Destination component.|  
|0xC020845B|-1071610789|DTS_E_ADODESTTABLENAMEERROR|The Table or View name is not expected. \n\t If you are quoting the table name, please use the prefix %1 and the suffix %2 of your selected data provider for quotation. \n\t If you are using multipart name, please use at most three parts for the table name.|  
|0xC0209001|-1071607807|DTS_E_FAILEDTOFINDCOLUMNINBUFFER|Failed to find column "%1" with lineage ID %2!d! in the buffer. The buffer manager returned error code 0x%3!8.8X!.|  
|0xC0209002|-1071607806|DTS_E_FAILEDTOGETCOLUMNINFOFROMBUFFER|Failed to get information for column "%1" (%2!d!) from the buffer. The error code returned was 0x%3!8.8X!.|  
|0xC0209011|-1071607791|DTS_E_TXAGG_ARITHMETICOVERFLOW|Arithmetic overflow encountered while aggregating "%1".|  
|0xC0209012|-1071607790|DTS_E_FAILEDTOGETCOLINFO|Failed to get information for row %1!ld!, column %2!ld! from the buffer. The error code returned was 0x%3!8.8X!.|  
|0xC0209013|-1071607789|DTS_E_FAILEDTOSETCOLINFO|Failed to set information for row %1!ld!, column %2!ld! into the buffer. The error code returned was 0x%3!8.8X!.|  
|0xC0209015|-1071607787|DTS_E_REQUIREDBUFFERISNOTAVAILBLE|A required buffer is not available.|  
|0xC0209016|-1071607786|DTS_E_FAILEDTOGETBUFFERBOUNDARYINFO|The attempt to get buffer boundary information failed with error code 0x%1!8.8X!.|  
|0xC0209017|-1071607785|DTS_E_FAILEDTOSETBUFFERENDOFROWSET|Setting the end of rowset for the buffer failed with error code 0x%1!8.8X!.|  
|0xC0209018|-1071607784|DTS_E_FAILEDTOGETDATAFORERROROUTPUTBUFFER|Failed to get data for the error output buffer.|  
|0xC0209019|-1071607783|DTS_E_FAILEDTOREMOVEROWFROMBUFFER|Removing a row from the buffer failed with error code 0x%1!8.8X!.|  
|0xC020901B|-1071607781|DTS_E_FAILEDTOSETBUFFERERRORINFO|The attempt to set buffer error information failed with error code 0x%1!8.8X!.|  
|0xC020901C|-1071607780|DTS_E_COLUMNSTATUSERROR|There was an error with %1 on %2. The column status returned was: "%3".|  
|0xC020901D|-1071607779|DTS_E_TXLOOKUP_METADATAXMLCACHEERR|Unable to cache reference metadata.|  
|0xC020901E|-1071607778|DTS_E_TXLOOKUP_ROWLOOKUPERROR|Row yielded no match during lookup.|  
|0xC020901F|-1071607777|DTS_E_INVALIDERRORDISPOSITION|The %1 has an invalid error or truncation row disposition.|  
|0xC0209022|-1071607774|DTS_E_FAILEDTODIRECTERRORROW|Directing the row to the error output failed with error code 0x%1!8.8X!.|  
|0xC0209023|-1071607773|DTS_E_FAILEDTOPREPARECOLUMNSTATUSESFORINSERT|Preparing column statuses for insert failed with error code 0x%1!8.8X!.|  
|0xC0209024|-1071607772|DTS_E_FAILEDTOFINDCOLUMNBYLINEAGEID|An attempt to find %1 with lineage ID %2!d! in the Data Flow Task buffer failed with error code 0x%3!8.8X!.|  
|0xC0209025|-1071607771|DTS_E_FAILEDTOFINDNONSPECIALERRORCOLUMN|Failed to find any non-special error column in %1.|  
|0xC0209029|-1071607767|DTS_E_INDUCEDTRANSFORMFAILUREONERROR|SSIS Error Code DTS_E_INDUCEDTRANSFORMFAILUREONERROR.  The "%1" failed because error code 0x%2!8.8X! occurred, and the error row disposition on "%3" specifies failure on error. An error occurred on the specified object of the specified component.  There may be error messages posted before this with more information about the failure.|  
|0xC020902A|-1071607766|DTS_E_INDUCEDTRANSFORMFAILUREONTRUNCATION|The "%1" failed because truncation occurred, and the truncation row disposition on "%2" specifies failure on truncation. A truncation error occurred on the specified object of the specified component.|  
|0xC020902B|-1071607765|DTS_E_TXSPLITEXPRESSIONEVALUATEDTONULL|The expression "%1" on "%2" evaluated to NULL, but the "%3" requires a Boolean results. Modify the error row disposition on the output to treat this result as False (Ignore Failure) or to redirect this row to the error output (Redirect Row).  The expression results must be Boolean for a Conditional Split.  A NULL expression result is an error.|  
|0xC020902C|-1071607764|DTS_E_TXSPLITSTATIC_EXPRESSIONEVALUATEDTONULL|The expression evaluated to NULL, but a Boolean result is required. Modify the error row disposition on the output to treat this result as False (Ignore Failure) or to redirect this row to the error output (Redirect Row). The expression results must be Boolean for a Conditional Split.  A NULL expression result is an error.|  
|0xC020902D|-1071607763|DTS_E_UTF16BIGENDIANFORMATNOTSUPPORTED|The file format of UTF-16 big endian is not supported.  Only UTF-16 little endian format is supported.|  
|0xC020902E|-1071607762|DTS_E_UTF8FORMATNOTSUPPORTEDASUNICODE|The file format of UTF-8 is not supported as Unicode.|  
|0xC020902F|-1071607761|DTS_E_DTPXMLCANTREADIDATTR|Cannot read ID attribute.|  
|0xC020903E|-1071607746|DTS_E_TXLOOKUP_INDEXCOLUMNREUSED|The cache index column %1 is referenced by more than one lookup input column.|  
|0xC020903F|-1071607745|DTS_E_TXLOOKUP_INDEXCOLUMNSMISMATCH|Lookup does not reference all cache connection manager index columns. Number of joined columns in lookup: %1!d!. Number of index columns: %2!d!.|  
|0xC0209069|-1071607703|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC020906A|-1071607702|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|The data value violated the schema constraint.|  
|0xC020906B|-1071607701|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_TRUNCATED|The data was truncated.|  
|0xC020906C|-1071607700|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the provider was unsigned.|  
|0xC020906D|-1071607699|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the provider.|  
|0xC020906E|-1071607698|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_UNAVAILABLE|No status is available.|  
|0xC020906F|-1071607697|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|The user did not have the correct permissions to write to the column.|  
|0xC0209070|-1071607696|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|The data value violated the integrity constraints for the column.|  
|0xC0209071|-1071607695|DTS_E_OLEDBSOURCEADAPTERSTATIC_UNAVAILABLE|No status is available.|  
|0xC0209072|-1071607694|DTS_E_OLEDBSOURCEADAPTERSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC0209073|-1071607693|DTS_E_OLEDBSOURCEADAPTERSTATIC_TRUNCATED|The data was truncated.|  
|0xC0209074|-1071607692|DTS_E_OLEDBSOURCEADAPTERSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the provider was unsigned.|  
|0xC0209075|-1071607691|DTS_E_OLEDBSOURCEADAPTERSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the provider.|  
|0xC0209076|-1071607690|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|The data value violated the schema constraint.|  
|0xC0209077|-1071607689|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC0209078|-1071607688|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_TRUNCATED|The data was truncated.|  
|0xC0209079|-1071607687|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the provider was unsigned.|  
|0xC020907A|-1071607686|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the provider.|  
|0xC020907B|-1071607685|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_UNAVAILABLE|No status is available.|  
|0xC020907C|-1071607684|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|The user did not have the correct permissions to write to the column.|  
|0xC020907D|-1071607683|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|The data value violates integrity constraints.|  
|0xC020907F|-1071607681|DTS_E_TXDATACONVERTSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC0209080|-1071607680|DTS_E_TXDATACONVERTSTATIC_TRUNCATED|The data was truncated.|  
|0xC0209081|-1071607679|DTS_E_TXDATACONVERTSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the provider was unsigned.|  
|0xC0209082|-1071607678|DTS_E_TXDATACONVERTSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the data conversion transform.|  
|0xC0209083|-1071607677|DTS_E_FLATFILESOURCEADAPTERSTATIC_UNAVAILABLE|No status is available.|  
|0xC0209084|-1071607676|DTS_E_FLATFILESOURCEADAPTERSTATIC_CANTCONVERTVALUE|The data value cannot be converted for reasons other than sign mismatch or data overflow.|  
|0xC0209085|-1071607675|DTS_E_FLATFILESOURCEADAPTERSTATIC_TRUNCATED|The data was truncated.|  
|0xC0209086|-1071607674|DTS_E_FLATFILESOURCEADAPTERSTATIC_SIGNMISMATCH|Conversion failed because the data value was signed and the type used by the flat file source adapter was unsigned.|  
|0xC0209087|-1071607673|DTS_E_FLATFILESOURCEADAPTERSTATIC_DATAOVERFLOW|Conversion failed because the data value overflowed the type used by the flat file source adapter.|  
|0xC020908E|-1071607666|DTS_E_TXDATACONVERTSTATIC_UNAVAILABLE|No status is available.|  
|0xC0209090|-1071607664|DTS_E_FILEOPENERR_FORREAD|Opening the file "%1" for reading failed with error code 0x%2!8.8X!.|  
|0xC0209091|-1071607663|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD|Failed to open file for reading.|  
|0xC0209092|-1071607662|DTS_E_FILEOPENERR_FORWRITE|Opening the file "%1" for writing failed with error code 0x%2!8.8X!.|  
|0xC0209093|-1071607661|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE|Failed to open file for writing.|  
|0xC0209094|-1071607660|DTS_E_TXFILEINSERTERSTATIC_INSERTERCANTREAD|Failed to read from file.|  
|0xC0209095|-1071607659|DTS_E_TXFILEEXTRACTORSTATIC_EXTRACTORCANTWRITE|Failed to write to file.|  
|0xC0209099|-1071607655|DTS_E_DTPXMLINVALIDPROPERTYARRAYTOOMANYVALUES|Too many array elements were found when parsing a property of type array. The elementCount is less than the number of array elements found.|  
|0xC020909A|-1071607654|DTS_E_DTPXMLINVALIDPROPERTYARRAYNOTENOUGHVALUES|Too few array elements were found when parsing a property of type array. The elementCount is more than the number of array elements found.|  
|0xC020909E|-1071607650|DTS_E_FILEOPENERR_FORWRITE_FILENOTFOUND|Opening the file "%1" for writing failed. The file cannot be found.|  
|0xC020909F|-1071607649|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILENOTFOUND|Opening the file for writing failed. The file cannot be found.|  
|0xC02090A0|-1071607648|DTS_E_FILEOPENERR_FORWRITE_PATHNOTFOUND|Opening the file "%1" for writing failed. The path cannot be found.|  
|0xC02090A1|-1071607647|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_PATHNOTFOUND|Opening the file for writing failed. The path cannot be found.|  
|0xC02090A2|-1071607646|DTS_E_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|Opening the file "%1" for writing failed. There are too many files open.|  
|0xC02090A3|-1071607645|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|Opening the file for writing failed. There are too many files open.|  
|0xC02090A4|-1071607644|DTS_E_FILEOPENERR_FORWRITE_ACCESSDENIED|Opening the file "%1" for writing failed. You do not have the correct permissions.|  
|0xC02090A5|-1071607643|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_ACCESSDENIED|Opening the file for writing failed. You do not have the correct permissions.|  
|0xC02090A6|-1071607642|DTS_E_FILEOPENERR_FORWRITE_FILEEXISTS|Opening the file "%1" for writing failed. The file exists and cannot be overwritten. If the AllowAppend property is FALSE and the ForceTruncate property is set to FALSE, the existence of the file will cause this failure.|  
|0xC02090A7|-1071607641|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILEEXISTS|Opening a file for writing failed. The file already exists and cannot be overwritten. If both the AllowAppend property and the ForceTruncate property are set to FALSE, the existence of the file will cause this failure.|  
|0xC02090A8|-1071607640|DTS_E_INCORRECTCUSTOMPROPERTYVALUEFOROBJECT|The value for custom property "%1" on %2 is incorrect.|  
|0xC02090A9|-1071607639|DTS_E_COLUMNSHAVEINCOMPATIBLEMETADATA|Columns "%1" and "%2" have incompatible metadata.|  
|0xC02090AD|-1071607635|DTS_E_FILEWRITEERR_DISKFULL|Opening the file "%1" for writing failed because the disk is full. There is not sufficient disk space to save this file.|  
|0xC02090AE|-1071607634|DTS_E_TXFILEEXTRACTORSTATIC_FILEWRITEERR_DISKFULL|Attempting to open the file for writing failed because the disk is full.|  
|0xC02090B9|-1071607623|DTS_E_TXAGG_SORTKEYGENFAILED|Generating a sort key failed with error 0x%1!8.8X!. The ComparisonFlags are enabled, and generating a sortkey with LCMapString failed.|  
|0xC02090BA|-1071607622|DTS_E_TXCHARMAPLCMAPFAILED|Transform failed to map string and returned error 0x%1!8.8X!. The LCMapString failed.|  
|0xC02090BB|-1071607621|DTS_E_FILEOPENERR_FORREAD_FILENOTFOUND|Opening the file "%1" for reading failed. The file was not found.|  
|0xC02090BC|-1071607620|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_FILENOTFOUND|Opening a file for reading failed. The file was not found.|  
|0xC02090BD|-1071607619|DTS_E_FILEOPENERR_FORREAD_PATHNOTFOUND|Opening the file "%1" for reading failed. The path cannot be found.|  
|0xC02090BE|-1071607618|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_PATHNOTFOUND|Opening a file for reading failed. The path was not found.|  
|0xC02090BF|-1071607617|DTS_E_FILEOPENERR_FORREAD_TOOMANYOPENFILES|Opening the file "%1" for reading failed. There are too many files open.|  
|0xC02090C0|-1071607616|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_TOOMANYOPENFILES|Opening the file for reading failed. There are too many files open.|  
|0xC02090C1|-1071607615|DTS_E_FILEOPENERR_FORREAD_ACCESSDENIED|Attempting to open the file "%1" for reading failed. Access is denied.|  
|0xC02090C2|-1071607614|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_ACCESSDENIED|Opening the file for reading failed. You do not have the correct permissions.|  
|0xC02090C3|-1071607613|DTS_E_INSERTERINVALIDBOM|The byte order mark (BOM) value for the file "%1" is 0x%2!4.4X!, but the expected value is 0x%3!4.4X!. The ExpectBOM property was set for this file, but the BOM value in the file is missing or not valid.|  
|0xC02090C4|-1071607612|DTS_E_TXFILEINSERTERSTATIC_INSERTERINVALIDBOM|The byte order mark (BOM) value for the file is not valid. The ExpectBOM property was set for this file, but the BOM value in the file is missing or not valid.|  
|0xC02090C5|-1071607611|DTS_E_NOCOMPONENTATTACHED|The %1 is not attached to a component.  It is required that a component be attached.|  
|0xC02090C9|-1071607607|DTS_E_TXLOOKUP_INVALIDMAXMEMORYPROP|The value for custom property %1 is incorrect.  It should be a number between %2!d! and %3!I64d!.|  
|0xC02090CA|-1071607606|DTS_E_TXAGG_COMPFLAGS_BADAGGREGATIONTYPE|The custom property "%1" cannot be specified for the aggregation type selected for this column. The comparison flags custom property can only be specified for group by and count distinct aggregation types.|  
|0xC02090CB|-1071607605|DTS_E_TXAGG_COMPFLAGS_BADDATATYPE|The comparison flags custom property "%1" can only be specified for columns of with datatype DT_STR or DT_WSTR.|  
|0xC02090CD|-1071607603|DTS_E_TXAGG_AGGREGATION_FAILURE|Aggregation on %1 failed with error code 0x%2!8.8X!.|  
|0xC02090CF|-1071607601|DTS_E_MAPPINGSETUPERROR|There was an error setting up the mapping. %1|  
|0xC02090D0|-1071607600|DTS_E_XMLSRCUNABLETOREADXMLDATA|The %1 was unable to read the XML data.|  
|0xC02090D1|-1071607599|DTS_E_XMLSRCUNABLETOGETXMLDATAVARIABLE|The %1 was unable to get the variable specified by the "%2" property.|  
|0xC02090D2|-1071607598|DTS_E_NODATATABLEMATCHROWID|The %1 contains a RowsetID with a value of %2 that does not reference a data table in the schema.|  
|0xC02090D6|-1071607594|DTS_E_TXAGG_BADKEYSVALUE|The property %1 must either be empty, or a number between %2!u! and %3!u!. The Keys or CountDistinctKeys property has a invalid value. The property should be a number between 0 and ULONG_MAX, inclusive, or not be set.|  
|0xC02090D7|-1071607593|DTS_E_TXAGG_TOOMANYKEYS|The aggregate component encountered too many distinct key combinations. It cannot accommodate more than %1!u! distinct key values. There are more than ULONG_MAX distinct key values in the main workspace.|  
|0xC02090D8|-1071607592|DTS_E_TXAGG_TOOMANYCOUNTDISTINCTVALUES|The aggregate component encountered too many distinct values while calculating the count distinct aggregate. It cannot accommodate more than %1!u! distinct values. There were more than ULONG_MAX distinct values while calculating the count distinct aggregation.|  
|0xC02090D9|-1071607591|DTS_E_FAILEDTOWRITETOTHEFILENAMECOLUMN|The attempt to write to the filename column failed with error code 0x%1!8.8X!.|  
|0xC02090DC|-1071607588|DTS_E_FAILEDTOFINDERRORCOLUMN|An error occurred, but the column that caused the error cannot be determined.|  
|0xC02090E3|-1071607581|DTS_E_TXLOOKUP_FAILEDUPGRADE_BAD_VERSION|Unable to upgrade lookup metadata from version %1!d! to %2!d!. The Lookup transform was unable to upgrade metadata from the existing version number in a call to PerformUpgrade().|  
|0xC02090E5|-1071607579|DTS_E_TERMEXTRACTIONORLOOKUP_NTEXTSPLITED|Failed to locate the ending boundary of a sentence.|  
|0xC02090E6|-1071607578|DTS_E_TERMEXTRACTION_EXCEED_MAXWORDNUM|The Term Extraction transformation is unable to process the input text because a sentence from the input text is too long. The sentence is segmented into several sentences.|  
|0xC02090E7|-1071607577|DTS_E_XMLSRCFAILEDTOCREATEREADER|The %1 was unable to read the XML data. %2|  
|0xC02090F0|-1071607568|DTS_E_TXLOOKUP_REINITMETADATAFAILED|The call to Lookup transform method, ReinitializeMetadata, failed.|  
|0xC02090F1|-1071607567|DTS_E_TXLOOKUP_NOJOINS|The lookup transform must contain at least one input column joined to a reference column, and none were specified. You must specify at least one join column.|  
|0xC02090F2|-1071607566|DTS_E_MANAGEDERR_BADFORMATSPECIFICATION|The message string being posted by the managed error infrastructure contains a bad format specification. This is an internal error.|  
|0xC02090F3|-1071607565|DTS_E_MANAGEDERR_UNSUPPORTEDTYPE|While formatting a message string using the managed error infrastructure, there was a variant type that does not have formatting support. This is an internal error.|  
|0xC02090F5|-1071607563|DTS_E_DATAREADERSRCUNABLETOPROCESSDATA|The %1 was unable to process the data. %2|  
|0xC02090F6|-1071607562|DTS_E_XMLSRCEMPTYPROPERTY|The property "%1" on the %2 was empty.|  
|0xC02090F7|-1071607561|DTS_E_XMLSRCINVALIDOUTPUTNAME|Attempting to create an output with the name "%1" for the XML table with the path "%2" failed because the name is invalid.|  
|0xC02090F8|-1071607560|DTS_E_MGDSRC_OVERFLOW|The value was too large to fit in the %1.|  
|0xC02090F9|-1071607559|DTS_E_DATAREADERDESTUNABLETOPROCESSDATA|The %1 was unable to process the data.|  
|0xC02090FA|-1071607558|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONTRUNCATION|The "%1" failed because truncation occurred, and the truncation row disposition on "%2"  at "%3" specifies failure on truncation. A truncation error occurred on the specified object of the specified component.|  
|0xC02090FB|-1071607557|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONERROR|The "%1" failed because error code 0x%2!8.8X! occurred, and the error row disposition on "%3" at "%4" specifies failure on error. An error occurred on the specified object of the specified component.|  
|0xC0209291|-1071607151|DTS_E_SQLCEDESTSTATIC_FAILEDTOSETVALUES|The SQLCE destination could not set the column values for the row.|  
|0xC0209292|-1071607150|DTS_E_SQLCEDESTSTATIC_FAILEDTOINSERT|The SQLCE destination could not insert the row.|  
|0xC0209293|-1071607149|DTS_E_TXFUZZYLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|Encountered OLEDB error while loading column metadata.|  
|0xC0209294|-1071607148|DTS_E_TXFUZZYLOOKUP_TOOFEWREFERENCECOLUMNS|Lookup reference metadata contains too few columns.|  
|0xC0209295|-1071607147|DTS_E_TXSCD_OLEDBERR_LOADCOLUMNMETADATA|Encountered OLEDB error while loading column metadata.|  
|0xC0209296|-1071607146|DTS_E_TXSCD_TOOFEWREFERENCECOLUMNS|Lookup reference metadata contains too few columns.|  
|0xC0209297|-1071607145|DTS_E_TXSCD_MALLOCERR_REFERENCECOLUMNINFO|Unable to allocate memory.|  
|0xC0209298|-1071607144|DTS_E_TXSCD_MALLOCERR_BUFFCOL|Unable to allocate memory.|  
|0xC0209299|-1071607143|DTS_E_TXSCD_MAINWORKSPACE_CREATEERR|Unable to create workspace buffer.|  
|0xC020929A|-1071607142|DTS_E_DTPXMLDOMCREATEERROR|Unable to instantiate XML DOM document, please verify that MSXML binaries are properly installed and registered.|  
|0xC020929B|-1071607141|DTS_E_DTPXMLDOMLOADERROR|Unable to load XML data into a local DOM for processing.|  
|0xC020929C|-1071607140|DTS_E_RSTDESTBADVARIABLETYPE|The type of the runtime variable "%1" is incorrect. The runtime variable type must be Object.|  
|0xC020929E|-1071607138|DTS_E_XMLDATAREADERMULTIPLEINLINEXMLSCHEMASNOTSUPPORTED|The XML Source Adapter was unable to process the XML data. Multiple inline schemas are not supported.|  
|0xC020929F|-1071607137|DTS_E_XMLDATAREADERANYTYPENOTSUPPORTED|The XML Source Adapter was unable to process the XML data. The content of an element can not be declared as anyType.|  
|0xC02092A0|-1071607136|DTS_E_XMLDATAREADERGROUPREFNOTSUPPORTED|The XML Source Adapter was unable to process the XML data. The content of an element can not contain a reference (ref) to a group.|  
|0xC02092A1|-1071607135|DTS_E_XMLDATAREADERMIXEDCONTENTFORCOMPLEXTYPESNOTSUPPORTED|The XML Source Adapter does not support mixed content model on Complex Types.|  
|0xC02092A2|-1071607134|DTS_E_XMLDATAREADERINLINESCHEMAFOUNDINSOURCEXML|The XML Source Adapter was unable to process the XML data. An inline schema must be the first child node in the source Xml.|  
|0xC02092A3|-1071607133|DTS_E_XMLDATAREADERNOINLINESCHEMAFOUND|The XML Source Adapter was unable to process the XML data. No inline schema was found in the source XML, but the "UseInlineSchema" property was set to true.|  
|0xC02092A4|-1071607132|DTS_E_CONNECTIONMANAGERTRANSACTEDANDRETAINEDINBULKINSERT|The component cannot use a connection manager that retains its connection in a transaction with fastload or bulk insert.|  
|0xC02092A5|-1071607131|DTS_E_OUTPUTREDIRECTINTRANSACTIONNOTALLOWED|The %1 cannot be set to redirect on error using a connection in a transaction.|  
|0xC02092A6|-1071607130|DTS_E_FOUNDORPHANEDEXTERNALMETADATACOLUMN|The %1 does not have a corresponding input or output column.|  
|0xC02092A9|-1071607127|DTS_E_RAWDESTNOINPUTCOLUMNS|There is no selected column to be written to the file.|  
|0xC02092AA|-1071607126|DTS_E_RAWDESTBLOBDATATYPE|The %1 has an invalid data type. Columns with data types DT_IMAGE, DT_TEXT and DT_NTEXT cannot be written to raw files.|  
|0xC02092AB|-1071607125|DTS_E_RAWDESTWRONGEXTERNALMETADATAUSAGE|The external metadata collection is improperly used by this component. The component should use external metadata when appending or truncating an existing file. Otherwise, the external metadata is not needed.|  
|0xC02092AC|-1071607124|DTS_E_RAWDESTMAPPEDINPUTCOLUMN|The %1 is mapped to an external metadata column with the id %2!d!. Input columns should not be mapped to external metadata columns when selected Write Option value is Create Always.|  
|0xC02092AD|-1071607123|DTS_E_RAWFILECANTOPENFORMETADATA|The file  cannot be opened for reading the metadata. If the file does not exist, and the component has already defined external metadata, you can set the "ValidateExternalMetadata" property to "false" and the file will be created at the runtime.|  
|0xC02092AE|-1071607122|DTS_E_FAILEDTOACCESSLOBCOLUMN|Failed to access LOB data from the data flow buffer for data source column "%1" with error code 0x%2!8.8X!.|  
|0xC02092AF|-1071607121|DTS_E_XMLSRCUNABLETOPROCESSXMLDATA|The %1 was unable to process the XML data. %2|  
|0xC02092B0|-1071607120|DTS_E_XMLSRCSTATIC_UNABLETOPROCESSXMLDATA|The XML Source Adapter was unable to process the XML data.|  
|0xC02092B1|-1071607119|DTS_E_RAWINVALIDACCESSMODE|The value %1!d! is not recognized as a valid access mode.|  
|0xC02092B2|-1071607118|DTS_E_INCOMPLETEDATASOURCECOLUMNFOUND|Complete metadata information for the data source column "%1" is not available.  Make sure the column is correctly defined in the data source.|  
|0xC02092B3|-1071607117|DTS_E_TXAUDIT_ONLYSTRINGLENGTHCHANGEALLOWED|Only lengths of User Name column, Package Name column, Task Name column and Machine Name column can be changed.  All other audit column datatype information is read only.|  
|0xC02092B4|-1071607116|DTS_E_ROWSETUNAVAILABLE|A rowset based on the SQL command was not returned by the OLE DB provider.|  
|0xC02092B5|-1071607115|DTS_E_COMMITFAILED|A commit failed.|  
|0xC02092B6|-1071607114|DTS_E_USEBINARYFORMATREQUIRESANSIFILE|The custom property "%1" on %2 can only be used with ANSI files.|  
|0xC02092B7|-1071607113|DTS_E_USEBINARYFORMATREQUIRESBYTES|The custom property "%1" on %2 can only be used with DT_BYTES.|  
|0xC0209302|-1071607038|DTS_E_OLEDB_NOPROVIDER_ERROR|SSIS Error Code DTS_E_OLEDB_NOPROVIDER_ERROR.  The requested OLE DB provider %2 is not registered. Error code: 0x%1!8.8X!.|  
|0xC0209303|-1071607037|DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR|SSIS Error Code DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR.  The requested OLE DB provider %2 is not registered -- perhaps no 64-bit provider is available.  Error code: 0x%1!8.8X!.|  
|0xC0209306|-1071607034|DTS_E_MULTICACHECOLMAPPINGS|The cache column, "%1", is mapped to more than one column. Remove the duplicate column mappings.|  
|0xC0209307|-1071607033|DTS_E_COLNOTMAPPEDTOCACHECOL|The %1 is not mapped to valid cache column.|  
|0xC0209308|-1071607032|DTS_E_CACHECOLDATATYPEINCOMPAT|Cannot map the input column, "%1", and the cache column, "%2", because the data types do not match.|  
|0xC0209309|-1071607031|DTS_E_INCORRECTINPUTCACHECOLCOUNT|The number of input columns does not match the number of cache columns.|  
|0xC020930A|-1071607030|DTS_E_INVALIDCACHEFILENAME|The cache file name is either not provided or is not valid. Provide a valid cache file name.|  
|0xC020930B|-1071607029|DTS_E_CACHECOLINDEXPOSMISMATCH|The index position of column, "%1", is different from index position of Cache connection manager column, "%2".|  
|0xC020930C|-1071607028|DTS_E_FAILEDTOLOADCACHE|Failed to load the cache from file, "%1".|  
|0xC020930D|-1071607027|DTS_E_TXLOOKUP_REFCOLUMNISNOTINDEX|The lookup input column %1 references non-index cache column %2.|  
|0xC020930E|-1071607026|DTS_E_FAILEDTOGETCONNECTIONSTRING|Failed to get the connection string.|  
|0xC020930F|-1071607025|DTS_E_CACHECOLDATATYPEPROPINCOMPAT|Cannot map the input column, "%1", and the cache column, "%2", because one or more data type properties do not match.|  
|0xC0209311|-1071607023|DTS_E_CACHECOLUMNOTFOUND|Cache column "%1" was not found in the cache.|  
|0xC0209312|-1071607022|DTS_E_CACHECOLUMNMAPPINGFAILED|Failed to map %1 to a cache column. The hresult is 0x%2!8.8X!.|  
|0xC0209313|-1071607021|DTS_E_CACHELOADEDFROMFILE|The %1 cannot write to the cache because the cache has been loaded from a file by %2.|  
|0xC0209314|-1071607020|DTS_E_CACHERELOADEDDIFFERENTFILES|The %1 cannot load the cache from file "%2" because the cache has already been loaded from file "%3".|  
|0xC0209316|-1071607018|DTS_E_OUTPUTNOTUSED|The output with ID %1!d! of Aggregate component is not used by any component. Please either remove it or associate it with an input of some component.|  
|0xC0209317|-1071607017|DTS_E_CACHEFILEWRITEFAILED|The %1 failed to write the cache to file "%2". The hresult is 0x%3!8.8X!.|  
|0xC0209318|-1071607016|DTS_E_XMLDATATYPECHANGED|The XML schema data type information for "%1" on  element "%2" has changed.  Please re-initialize the metadata for this component and review column mappings.|  
|0xC0209319|-1071607015|DTS_E_TXLOOKUP_UNUSEDINPUTCOLUMN|%1 not used in join or copy. Please remove the unused column from the input column list.|  
|0xC020931A|-1071607014|DTS_E_SORTSTACKOVERFLOW|The sort failed due to a stack overflow while sorting an incoming buffer.  Please reduce the DefaultBufferMaxRows property on the Data Flow Task.|  
|0xC020F42A|-1071582166|DTS_E_OLEDB_OLDPROVIDER_ERROR|Consider changing the PROVIDER in the connection string to %1 or visit https://www.microsoft.com/downloads to find and install support for %2.|  
|||DTS_E_INITTASKOBJECTFAILED|Failed to initialize the task object for task "%1!s!", type "%2!s!" due to error 0x%3!8.8X! "%4!s!".|  
|||DTS_E_GETCATMANAGERFAILED|Failed to create COM Component Categories Manager due to error 0x%1!8.8X! "%2!s!".|  
|||DTS_E_COMPONENTINITFAILED|Component %1!s! failed to initialize due to error 0x%2!8.8X! "%3!s!".|  
  
##  <a name="msgWarning"></a> Warning Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] warning messages begin with **DTS_W_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x80000036|-2147483594|DTS_W_COUNTDOWN|There are %1!lu! days left in the evaluation. When it expires, packages will not be able to be executed.|  
|0x80010015|-2147418091|DTS_W_GENERICWARNING|Warning(s) raised. There should be more specific warnings preceding this one that explain the specifics of the warning(s).|  
|0x80012010|-2147409904|DTS_W_FAILEDXMLDOCCREATION|Cannot create an XML document object instance. Verify that MSXML is installed and registered correctly.|  
|0x80012011|-2147409903|DTS_W_FAILEDCONFIGLOAD|Cannot load the XML configuration file. The XML configuration file may be malformed or not valid.|  
|0x80012012|-2147409902|DTS_W_CONFIGFILENAMEINVALID|The configuration file name "%1" is not valid. Check the configuration file name.|  
|0x80012013|-2147409901|DTS_W_CONFIGFILEINVALID|The configuration file loaded, but is not valid. The file is not formatted correctly, may be missing an element, or may be damaged.|  
|0x80012014|-2147409900|DTS_W_CONFIGFILENOTFOUND|The configuration file "%1" cannot be found. Check the directory and file name.|  
|0x80012015|-2147409899|DTS_W_CONFIGKEYNOTFOUND|Configuration registry key "%1" was not found. A configuration entry specifies a registry key that is not available. Check the registry to ensure that the key is there.|  
|0x80012016|-2147409898|DTS_W_CONFIGTYPEINVALID|The configuration type in one of the configuration entries was not valid. Valid types are listed in the DTSConfigurationType enumeration.|  
|0x80012017|-2147409897|DTS_W_CANNOTFINDOBJECT|The package path referenced an object that cannot be found: "%1". This occurs when an attempt is made to resolve a package path to an object that cannot be found.|  
|0x80012018|-2147409896|DTS_W_CONFIGFORMATINVALID_PACKAGEDELIMITER|The configuration entry, "%1", has an incorrect format because it does not begin with the package delimiter. Prepend "\package" to the package path.|  
|0x80012019|-2147409895|DTS_W_CONFIGFORMATINVALID|The configuration entry "%1" had an incorrect format. This can occur because of a missing delimiter or formatting errors, like an invalid array delimiter.|  
|0x8001201A|-2147409894|DTS_W_NOPARENTVARIABLES|Configuration from a parent variable "%1" did not occur because there was no parent variable collection.|  
|0x8001201B|-2147409893|DTS_W_CONFIGFILEFAILEDIMPORT|Failure importing configuration file: "%1".|  
|0x8001201C|-2147409892|DTS_W_PARENTVARIABLENOTFOUND|Configuration from a parent variable "%1" did not occur because there was no parent variable. Error code: 0x%2!8.8X!.|  
|0x8001201D|-2147409891|DTS_W_CONFIGFILEEMPTY|The configuration file was empty and contained no configuration entries.|  
|0x80012023|-2147409885|DTS_W_INVALIDCONFIGURATIONTYPE|The configuration type for configuration "%1" is not valid. This may occur when an attempt is made to set the type property of a configuration object to an invalid configuration type.|  
|0x80012025|-2147409883|DTS_W_REGISTRYCONFIGURATIONTYPENOTFOUND|The configuration type for the registry configuration was not found in key "%1". Add a value called ConfigType to the registry key and give it a string value of "Variable", "Property", "ConnectionManager", "LoggingProvider", or "ForEachEnumerator".|  
|0x80012026|-2147409882|DTS_W_REGISTRYCONFIGURATIONVALUENOTFOUND|The configuration value for the registry configuration was not found in key "%1". Add a value called Value to the registry key of type DWORD or String.|  
|0x80012028|-2147409880|DTS_W_PROCESSCONFIGURATIONFAILEDSET|Process configuration failed to set the destination at the package path of "%1". This occurs when attempting to set the destination property or variable fails. Check the destination property or variable.|  
|0x80012032|-2147409870|DTS_W_CONFIGUREDVALUESECTIONEMPTY|Failed to retrieve value from the .ini file. The ConfiguredValue section is either empty, or does not exist: "%1".|  
|0x80012033|-2147409869|DTS_W_CONFIGUREDTYPESECTIONEMPTY|Failed to retrieve value from the .ini file. The ConfiguredType section is either empty, or does not exist: "%1".|  
|0x80012034|-2147409868|DTS_W_PACKAGEPATHSECTIONEMPTY|Failed to retrieve value from the .ini file. The PackagePath section is either empty, or does not exist: "%1".|  
|0x80012035|-2147409867|DTS_W_CONFIGUREDVALUETYPE|Failed to retrieve value from the .ini file. The ConfiguredValueType section is either empty, or does not exist: "%1".|  
|0x80012051|-2147409839|DTS_W_SQLSERVERFAILEDIMPORT|Configuration from SQL Server was not successfully imported: "%1".|  
|0x80012052|-2147409838|DTS_W_INICONFIGURATIONPROBLEM|The .ini configuration file is not valid due to empty or missing fields.|  
|0x80012054|-2147409836|DTS_W_NORECORDSFOUNDINTABLE|Table "%1" does not have any records for configuration. This occurs when configuring from a SQL Server table that has no records for the configuration.|  
|0x80012055|-2147409835|DTS_W_DUPLICATECUSTOMEVENT|Error using same name for different custom events. The custom event "%1" was defined differently by different children of this container. There may be an error when executing the event handler.|  
|0x80012057|-2147409833|DTS_W_CONFIGREADONLYVARIABLE|The configuration attempted to change a read-only variable. The variable is at the package path "%1".|  
|0x80012058|-2147409832|DTS_W_CONFIGPROCESSCONFIGURATIONFAILED|Calling ProcessConfiguration on the package failed. The configuration attempted to change the property at the package path "%1".|  
|0x80012059|-2147409831|DTS_W_ONEORMORECONFIGLOADFAILED|Failed to load at least one of the configuration entries for the package. Check configuration entries for "%1" and previous warnings to see descriptions of which configuration failed.|  
|0x8001205A|-2147409830|DTS_W_CONFIGNODEINVALID|The configuration entry "%1" in the configuration file was not valid, or failed to configure the variable.  The name indicates which entry failed. In some cases, the name will not be available.|  
|0x80014058|-2147401640|DTS_W_FAILURENOTRESTARTABLE|This task or container has failed, but because FailPackageOnFailure property is FALSE, the package will continue. This warning is posted when the SaveCheckpoints property of the package is set to TRUE and the task or container fails.|  
|0x80017101|-2147389183|DTS_W_EMPTYPATH|The path is empty.|  
|0x80019002|-2147381246|DTS_W_MAXIMUMERRORCOUNTREACHED|SSIS Warning Code DTS_W_MAXIMUMERRORCOUNTREACHED.  The Execution method succeeded, but the number of errors raised (%1!d!) reached the maximum allowed (%2!d!); resulting in failure. This occurs when the number of errors reaches the number specified in MaximumErrorCount. Change the MaximumErrorCount or fix the errors.|  
|0x80019003|-2147381245|DTS_W_CONFIGENVVARNOTFOUND|The configuration environment variable was not found.  The environment variable was: "%1". This occurs when a package specifies an environment variable for a configuration setting but it cannot be found. Check the configurations collection in the package and verify that the specified environment variable is available and valid.|  
|0x80019316|-2147380458|DTS_W_CONNECTIONPROVIDERCHANGE|The provider name for the connection manager "%1" has been changed from "%2" to "%3".|  
|0x80019317|-2147380457|DTS_W_READEXTMAPFAILED|An exception occurred while reading the upgrade mapping files. The exception is "%1".|  
|0x80019318|-2147380456|DTS_W_DUPLICATEMAPPINGKEY|There is a duplicate mapping in file, "%1". The tag is "%2", and the key is "%3".|  
|0x80019319|-2147380455|DTS_W_IMPLICITUPGRADEMAPPING|The extension, "%1", was implicitly upgraded to "%2". Add a mapping for this extension to the UpgradeMappings directory.|  
|0x8001931A|-2147380454|DTS_W_INVALIDEXTENSIONMAPPING|A mapping in the file, "%1", is not valid. Values cannot be null or empty. The tag is "%2", the key is "%3", and the value is "%4".|  
|0x8001931C|-2147380452|DTS_W_ADOCONNECTIONDATATYPECOMPATCHANGE|The DataTypeCompatibility property of ADO type connection manager "%1" was set to 80 for backward compatibility reasons.|  
|0x8001C004|-2147368956|DTS_W_FILEENUMEMPTY|The For Each File enumerator is empty. The For Each File enumerator did not find any files that matched the file pattern, or the specified directory was empty.|  
|0x8001F02F|-2147356625|DTS_W_COULDNOTRESOLVEPACKAGEPATH|Cannot resolve a package path to an object in the package "%1". Verify that the package path is valid.|  
|0x8001F203|-2147356157|DTS_W_ITERATIONEXPRESSIONISNOTASSIGNMENT|The iteration expression is not an assignment expression: "%1". This error usually occurs when the expression in the assignment expression on the ForLoop is not an assignment expression.|  
|0x8001F204|-2147356156|DTS_W_INITIALIZATIONEXPRESSIONISNOTASSIGNMENT|The initialization expression is not an assignment expression: "%1". This error usually occurs when the expression in the iterate expressions on the ForLoop is not an assignment expression.|  
|0x8001F205|-2147356155|DTS_W_LOGPROVIDERNOTDEFINED|The executable "%1" was pasted successfully. However a log provider that was associated with the executable was not found in the collection "LogProviders".  The executable was pasted without log provider information.|  
|0x8001F300|-2147355904|DTS_W_PACKAGEUPGRADED|Succeeded in upgrading the package.|  
|0x8001F42B|-2147355605|DTS_W_LEGACYPROGID|The "%1" ProgID has been deprecated. The new ProgID for this component "%2" should be used instead.|  
|0x80020918|-2147350248|DTS_W_FTPTASK_OPERATIONFAILURE|Operation "%1" failed.|  
|0x800283A5|-2147318875|DTS_W_MSMQTASK_USE_WEAK_ENCRYPTION|The encryption algorithm "%1" uses weak encryption.|  
|0x80029164|-2147315356|DTS_W_FSTASK_OPERATIONFAILURE|Task failed to execute operation "%1".|  
|0x80029185|-2147315323|DTS_W_EXECPROCTASK_FILENOTINPATH|File/Process "%1" is not in path.|  
|0x800291C6|-2147315258|DTS_W_SENDMAILTASK_SUBJECT_MISSING|The subject is empty.|  
|0x800291C7|-2147315257|DTS_W_SENDMAILTASK_ERROR_IN_TO_LINE|The address in the "To" line is malformed. It is either missing the "\@" symbol or is not valid.|  
|0x800291C8|-2147315256|DTS_W_SENDMAILTASK_AT_MISSING_IN_FROM|The address in the "From" line is malformed. It is either missing the "\@" symbol or is not valid.|  
|0x8002927A|-2147315078|DTS_W_XMLTASK_DIFFFAILURE|The two XML documents are different.|  
|0x8002928C|-2147315060|DTS_W_XMLTASK_DTDVALIDATIONWARNING|DTD Validation will use the DTD file defined in the DOCTYPE line in the XML document. It will not use what is assigned to the property "%1".|  
|0x8002928D|-2147315059|DTS_W_XMLTASK_VALIDATIONFAILURE|Task failed to validate "%1".|  
|0x80029291|-2147315055|DTS_W_TRANSFERDBTASK_ACTIONSETTOCOPY|The transfer action value was invalid.  It is being set to copy.|  
|0x80029292|-2147315054|DTS_W_TRANSFERDBTASK_METHODSETTOONLINE|The transfer method value was invalid.  It is being set to an online transfer.|  
|0x8002F304|-2147290364|DTS_W_PROBLEMOCCURREDWITHFOLLOWINGMESSAGE|A problem occurred with the following messages: "%1".|  
|0x8002F322|-2147290334|DTS_W_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|The error message "%1" already exists at destination server.|  
|0x8002F331|-2147290319|DTS_W_JOBSTASK_JOBEXISTSATDEST|The job "%1" already exists at destination server.|  
|0x8002F332|-2147290318|DTS_W_JOBSTASK_SKIPPINGJOBEXISTSATDEST|Skipping the transfer of job "%1" since it already exists at destination.|  
|0x8002F333|-2147290317|DTS_W_JOBSTASK_OVERWRITINGJOB|Overwriting the job "%1" at destination server.|  
|0x8002F339|-2147290311|DTS_W_LOGINSTASK_ENUMVALUEINCORRECT|Persisted enumeration value of property "FailIfExists" was changed and rendered invalid. Resetting to default.|  
|0x8002F343|-2147290301|DTS_W_LOGINSTASK_OVERWRITINGLOGINATDEST|Overwriting Login "%1" at destination.|  
|0x8002F356|-2147290282|DTS_W_TRANSOBJECTSTASK_SPALREADYATDEST|Stored procedure "%1" already exists at destination.|  
|0x8002F360|-2147290272|DTS_W_TRANSOBJECTSTASK_RULEALREADYATDEST|Rule "%1" already exists at destination.|  
|0x8002F364|-2147290268|DTS_W_TRANSOBJECTSTASK_TABLEALREADYATDEST|Table "%1" already exists at destination.|  
|0x8002F368|-2147290264|DTS_W_TRANSOBJECTSTASK_VIEWALREADYATDEST|View "%1" already exists at destination.|  
|0x8002F372|-2147290254|DTS_W_TRANSOBJECTSTASK_UDFALREADYATDEST|User Defined Function "%1" already exists at destination.|  
|0x8002F376|-2147290250|DTS_W_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|Default "%1" already exists at destination.|  
|0x8002F380|-2147290240|DTS_W_TRANSOBJECTSTASK_UDDTALREADYATDEST|User Defined Data Type "%1" already exists at destination.|  
|0x8002F384|-2147290236|DTS_W_TRANSOBJECTSTASK_PFALREADYATDEST|Partition Function "%1" already exists at destination.|  
|0x8002F388|-2147290232|DTS_W_TRANSOBJECTSTASK_PSALREADYATDEST|Partition Scheme "%1" already exists at destination.|  
|0x8002F391|-2147290223|DTS_W_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|Schema "%1" already exists at destination.|  
|0x8002F396|-2147290218|DTS_W_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|SqlAssembly "%1" already exists at destination.|  
|0x8002F400|-2147290112|DTS_W_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|User Defined Aggregate "%1" already exists at destination.|  
|0x8002F404|-2147290108|DTS_W_TRANSOBJECTSTASK_TYPEALREADYATDEST|User Defined Type "%1" already exists at destination.|  
|0x8002F408|-2147290104|DTS_W_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|XmlSchemaCollection "%1" already exists at destination.|  
|0x8002F412|-2147290094|DTS_W_TRANSOBJECTSTASK_NOELEMENTSPECIFIEDTOTRANSFER|There are no elements specified to transfer.|  
|0x8002F415|-2147290091|DTS_W_TRANSOBJECTSTASK_LOGINALREADYATDEST|Login "%1" already exists at destination.|  
|0x8002F41A|-2147290086|DTS_W_TRANSOBJECTSTASK_USERALREADYATDEST|User "%1" already exists at destination.|  
|0x80047007|-2147192825|DTS_W_NOLINEAGEVALIDATION|The lineage IDs of the input columns cannot be validated because the execution trees contain cycles.|  
|0x80047034|-2147192780|DTS_W_EMPTYDATAFLOW|The DataFlow task has no components. Add components or remove the task.|  
|0x80047069|-2147192727|DTS_W_SORTEDOUTPUTHASNOSORTKEYPOSITIONS|The IsSorted property of %1 is set to TRUE, but all of its output columns' SortKeyPositions are set to zero.|  
|0x8004706F|-2147192721|DTS_W_SOURCEREMOVED|Source "%1" (%2!d!) will not be read because none of its data ever becomes visible outside the Data Flow Task.|  
|0x80047076|-2147192714|DTS_W_UNUSEDOUTPUTDATA|The output column "%1" (%2!d!) on output "%3" (%4!d!) and component "%5" (%6!d!) is not subsequently used in the Data Flow task. Removing this unused output column can increase Data Flow task performance.|  
|0x800470AE|-2147192658|DTS_W_COMPONENTREMOVED|Component "%1" (%2!d!) has been removed from the Data Flow task because its output is not used and its inputs either have no side effects or are not connected to outputs of other components. If the component is required, then the HasSideEffects property on at least one of its inputs should be set to true, or its output should be connected to something.|  
|0x800470B0|-2147192656|DTS_W_NOWORKTODO|Rows were given to a thread, but that thread has no work to do. The layout has a disconnected output. Running the pipeline with the RunInOptimizedMode property set to TRUE will be faster, and prevents this warning.|  
|0x800470C8|-2147192632|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|The external columns for %1 are out of synchronization with the data source columns. %2|  
|0x800470C9|-2147192631|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSADDITION|The column "%1" needs to be added to the external columns.|  
|0x800470CA|-2147192630|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSUPDATE|The external column "%1" needs to be updated.|  
|0x800470CB|-2147192629|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSREMOVAL|The %1 needs to be removed from the external columns.|  
|0x800470D8|-2147192616|DTS_W_EXPREVALPOTENTIALSTRINGTRUNCATION|The result string for expression "%1" may be truncated if it exceeds the maximum length of %2!d! characters. The expression could have a result value that exceeds the maximum size of a DT_WSTR.|  
|0x800470E9|-2147192599|DTS_W_COMPONENTLEAKPROCESSINPUT|A call to the ProcessInput method for input %1!d! on %2 unexpectedly kept a reference to the buffer it was passed. The refcount on that buffer was %3!d! before the call, and %4!d! after the call returned.|  
|0x800470EB|-2147192597|DTS_W_EXPREVALUNREFERENCEDINPUTCOLUMN|The "%1" on "%2" has usage type READONLY, but is not referenced by an expression. Remove the column from the list of available input columns, or reference it in an expression.|  
|0x8004801E|-2147188706|DTS_W_COULDNOTFINDCURRENTVERSION|Cannot find the "%1" value for component %2. The CurrentVersion value for the component cannot be located. This error occurs if the component has not set its registry information to contain a CurrentVersion value in the DTSInfo section. This message occurs during component development, or when the component is used in a package, if the component is not registered properly.|  
|0x80049300|-2147183872|DTS_W_BUFFERGETTEMPFILENAME|The buffer manager could not get a temporary file name.|  
|0x80049301|-2147183871|DTS_W_UNUSABLETEMPORARYPATH|The buffer manager could not create a temporary file on the path "%1". The path will not be considered for temporary storage again.|  
|0x80049304|-2147183868|DTS_W_DF_PERFCOUNTERS_DISABLED|Warning: Could not open global shared memory to communicate with performance DLL; data flow performance counters are not available.  To resolve, run this package as an administrator, or on the system's console.|  
|0x8020200F|-2145378289|DTS_W_PARTIALROWFOUNDATENDOFFILE|There is a partial row at the end of the file.|  
|0x8020202B|-2145378261|DTS_W_ENDOFFILEREACHWHILEREADINGHEADERROWS|The end of the data file was reached while reading header rows. Make sure the header row delimiter and the number of header rows to skip are correct.|  
|0x80202066|-2145378202|DTS_W_CANTRETRIEVECODEPAGEFROMOLEDBPROVIDER|Cannot retrieve the column code page info from the OLE DB provider.  If the component supports the "%1" property, the code page from that property will be used.  Change the value of the property if the current string code page values are incorrect.  If the component does not support the property, the code page from the component's locale ID will be used.|  
|0x802020F7|-2145378057|DTS_W_TXSORTSORTISTHESAME|The data is already sorted as specified so the transform can be removed.|  
|0x8020400D|-2145370099|DTS_W_NOPIPELINEDATATYPEMAPPINGAVAILABLE|The %1 references an external data type that cannot be mapped to a Data Flow task data type. The Data Flow task data type DT_WSTR will be used instead.|  
|0x802070CC|-2145357620|DTS_W_STATICTRUNCATIONINEXPRESSION|The expression "%1" will always result in a truncation of data. The expression contains a static truncation (the truncation of a fixed value).|  
|0x8020820C|-2145353204|DTS_W_UNMAPPEDINPUTCOLUMN|The input column "%1" with ID %2!d! at index %3!d! is unmapped. The lineage ID for the column is zero.|  
|0x80208305|-2145352955|DTS_W_TXFUZZYLOOKUP_DELIMITERS_DONT_MATCH|The specified delimiters do not match the delimiters used to build the pre-existing match index "%1". This error occurs when the delimiters used to tokenize fields do not match. This can have unknown effects on the matching behavior or results.|  
|0x80208308|-2145352952|DTS_W_TXFUZZYLOOKUP_MAXRESULTS_IS_ZERO|The MaxOutputMatchesPerInput property on the Fuzzy Lookup transformation is zero. No results will be produced.|  
|0x80208310|-2145352944|DTS_W_TXFUZZYLOOKUP_NO_FUZZY_JOIN_COLUMNS|There were no valid input columns with JoinType column property set to Fuzzy.  Performance on Exact joins may be improved by using the Lookup transform instead of FuzzyLookup.|  
|0x8020831C|-2145352932|DTS_W_TXFUZZYLOOKUP_TIMESTAMPCAVEAT|The reference column "%1" may be a SQL timestamp column. When the fuzzy match index is built, and a copy of the reference table is made, all reference table timestamps will reflect the current state of the table at the time of the copy. Unexpected behavior may occur if the CopyReferenceTable is set to false.|  
|0x80208321|-2145352927|DTS_W_MATCHINDEXALREADYEXISTS|A table with the name '%1' given for MatchIndexName already exists and DropExistingMatchIndex is set to FALSE.  Transform execution will fail unless this table is dropped, a different name is specified, or DropExisitingMatchIndex is set to TRUE.|  
|0x8020832B|-2145352917|DTS_W_TXFUZZYLOOKUP_JOINLENGTHMISMATCH|The length of input column '%1' is not equal to the length of the reference column '%2' that it is being matched against.|  
|0x8020832D|-2145352915|DTS_W_TXFUZZYLOOKUP_CODEPAGE_MISMATCH|The code pages of the DT_STR source column "%1" and the DT_STR dest column "%2" do not match.  This may cause unexpected results.|  
|0x8020832E|-2145352914|DTS_W_FUZZYLOOKUP_TOOMANYEXACTMATCHCOLUMNS|There are more than 16 exact match joins, so performance may not be optimal. Reduce the number of exact match joins to improve performance. SQL Server has a limit of 16 columns per index, the inverted index will be used for all lookups.|  
|0x80208350|-2145352880|DTS_W_FUZZYLOOKUP_MEMLIMITANDEXHAUSTIVESPECIFIED|The Exhaustive option requires that the entire reference be loaded into main memory.  Since a memory limit has been specified for the MaxMemoryUsage property, it is possible that the entire reference table will not fit within this bound and that the match operation will fail at runtime.|  
|0x80208351|-2145352879|DTS_W_FUZZYLOOKUP_EXACTMATCHCOLUMNSEXCEEDBYTELIMIT|The cumulative lengths of the columns specified in the exact match joins exceeds the 900 byte limit for index keys.  Fuzzy Lookup creates an index on the exact match columns to increase lookup performance and there is a possibility that creation of this index may fail and the lookup will fall back to an alternative, possibly slower, method of finding matches. If performance is a problem, try removing some exact match join columns or reduce the maximum lengths of variable length exact match columns.|  
|0x80208352|-2145352878|DTS_W_FUZZYLOOKUP_EXACTMATCHINDEXCREATIONFAILED|Failed to create an index for exact match columns. Reverting to alternative fuzzy lookup method.|  
|0x80208353|-2145352877|DTS_W_FUZZYGROUPINGINTERNALPIPELINEWARNING|The following Fuzzy Grouping internal pipeline warning occurred with warning code 0x%1!8.8X!: "%2".|  
|0x80208375|-2145352843|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTODEFAULT|No maximum length was specified for the %1 with external data type %2. The SSIS Data Flow Task data type "%3" with a length of %4!d! will be used.|  
|0x80208376|-2145352842|DTS_W_XMLSRCOUTPUTCOLUMNDATATYPEMAPPEDTOSTRING|The %1 references external data type %2, which cannot be mapped to a SSIS Data Flow Task data type.  The SSIS Data Flow Task data type DT_WSTR with a length of %3!d! will be used instead.|  
|0x80208385|-2145352827|DTS_W_NOREDIRECTWITHATTACHEDERROROUTPUTS|No rows will be sent to error output(s). Configure error or truncation dispositions to redirect rows to the error output(s), or delete data flow transformations or destinations that are attached to the error output(s).|  
|0x80208386|-2145352826|DTS_W_REDIRECTWITHNOATTACHEDERROROUTPUTS|Rows sent to the error output(s) will be lost. Add new data flow transformations or destinations to receive error rows, or reconfigure the component to stop redirecting rows to the error output(s).|  
|0x80208391|-2145352815|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTOMAXIMUM|For the %1 with external data type %2, the XML schema specified a maxLength constraint of %3!d!, which exceeds the maximum allowed column length of %4!d!. The SSIS Data Flow Task data type "%5" with a length of %6!d! will be used.|  
|0x802090E4|-2145349404|DTS_W_TXLOOKUP_DUPLICATE_KEYS|The %1 encountered duplicate reference key values when caching reference data. This error occurs in Full Cache mode only. Either remove the duplicate key values, or change the cache mode to PARTIAL or NO_CACHE.|  
|0x802092A7|-2145348953|DTS_W_POTENTIALTRUNCATIONFROMDATAINSERTION|Truncation may occur due to inserting data from data flow column "%1" with a length of %2!d! to database column "%3" with a length of %4!d!.|  
|0x802092A8|-2145348952|DTS_W_POTENTIALTRUNCATIONFROMDATARETRIEVAL|Truncation may occur due to retrieving data from database column "%1" with a length of %2!d! to data flow column "%3" with a length of %4!d!.|  
|0x802092AA|-2145348950|DTS_W_ADODESTBATCHNOTSUPPORTEDFORERRORDISPOSITION|Batch mode is not currently supported when error row disposition is used. The BatchSize property will be set to 1.|  
|0x802092AB|-2145348949|DTS_W_ADODESTNOROWSINSERTED|No rows were successfully inserted into the destination. This may be due to a data type mismatch between columns, or due to the use of a datatype that is unsupported by your ADO.NET provider. Since the error disposition for this component is not "Fail component", error messages are not shown here; set the error disposition to "Fail component" to see error messages here.|  
|0x802092AC|-2145348948|DTS_W_ADODESTPOTENTIALDATALOSS|Potential data loss may occur due to inserting data from input column "%1" with data type "%2" to external column "%3" with data type "%4". If this is intended, an alternative way to do conversion is using a Data Conversion component before ADO NET destination component.|  
|0x802092AD|-2145348947|DTS_W_ADODESTEXTERNALCOLNOTMATCHSCHEMACOL|The %1 has been out of synchronization with the database column.  The latest column has %2. Use advanced editor to refresh  available destination columns if needed.|  
|0x802092AE|-2145348946|DTS_W_ADODESTEXTERNALCOLNOTEXIST|The %1 does not exist in the database. It may have been removed or renamed. Use Advanced Editor to refresh the available destination columns if needed.|  
|0x802092AF|-2145348945|DTS_W_ADODESTNEWEXTCOL|A new column with name %1 has been added to the external database table. Use advanced editor to refresh available destination columns if needed.|  
|0x8020930C|-2145348852|DTS_W_NOMATCHOUTPUTGETSNOROWS|No rows will be sent to the no match output. Configure the transformation to redirect rows with no matching entries to the no match output, or delete the data flow transformations or destinations that are attached to the no match output.|  
|0x8020931B|-2145348837|DTS_W_ADODESTINVARIANTEXCEPTION|Exception received while enumerating ADO.Net providers. The invariant was "%1". The exception message is: "%2"|  
|0xC020822C|-1071611348|DTS_W_UNMAPPEDOUTPUTCOLUMN|The %1 has no input column mapped to it.|  
|0x930D|37645|DTS_W_EXTERNALTABLECOLSOUTOFSYNC|The table "%1" has changed. New columns might have been added to the table.|  
  
##  <a name="msgInfo"></a> Informational Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] informational messages begin with **DTS_I_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x4001100A|1073811466|DTS_I_STARTINGTRANSACTION|Starting distributed transaction for this container.|  
|0x4001100B|1073811467|DTS_I_COMMITTINGTRANSACTION|Committing distributed transaction started by this container.|  
|0x4001100C|1073811468|DTS_I_ABORTINGTRANSACTION|Aborting the current distributed transaction.|  
|0x40013501|1073820929|DTS_I_GOTMUTEXFROMWAIT|Mutex "%1" was successfully acquired.|  
|0x40013502|1073820930|DTS_I_RELEASEACQUIREDMUTEX|Mutex "%1" was successfully released.|  
|0x40013503|1073820931|DTS_I_NEWMUTEXCREATED|Mutex "%1" was successfully created.|  
|0x40015101|1073828097|DTS_I_DUMP_ON_ANY_ERR|Debug dump files will be generated for any error event.|  
|0x40015102|1073828098|DTS_I_DUMP_ON_CODES|Debug dump files will be generated for the following event codes: "%1"|  
|0x40015103|1073828099|DTS_I_START_DUMP|Event code, 0x%1!8.8X!, triggered generation of debug dump files in the folder "%2".|  
|0x40015104|1073828100|DTS_I_SSIS_INFO_DUMP|Creating SSIS information dump file "%1".|  
|0x40015106|1073828102|DTS_I_FINISH_DUMP|Debug dump files successfully created.|  
|0x40016019|1073831961|DTS_I_PACKAGEMIGRATED|The package format was migrated from version %1!d! to version %2!d!. It must be saved to retain migration changes.|  
|0x4001601A|1073831962|DTS_I_SCRIPTSMIGRATED|The scripts in the package were migrated. The package must be saved to retain migration changes.|  
|0x40016025|1073831973|DTS_I_FTPRECEIVEFILE|Receiving file "%1".|  
|0x40016026|1073831974|DTS_I_FTPSENDFILE|Sending file "%1".|  
|0x40016027|1073831975|DTS_I_FTPFILEEXISTS|File "%1" already exists.|  
|0x40016028|1073831976|DTS_I_FTPERRORLOADINGMSG|Cannot get extra error information due to an internal error.|  
|0x40016036|1073831990|DTS_I_FTPDELETEFILE|The attempt to delete file "%1" failed. This may occur when the file does not exist, the file name was spelled incorrectly, or you do not have permissions to delete the file.|  
|0x40016037|1073831991|DTS_I_CONFIGFROMREG|The package is attempting to configure from a registry entry using the registry key "%1".|  
|0x40016038|1073831992|DTS_I_CONFIGFROMENVVAR|The package is attempting to configure from the environment variable "%1".|  
|0x40016039|1073831993|DTS_I_CONFIGFROMINIFILE|The package is attempting to configure from the .ini file "%1".|  
|0x40016040|1073832000|DTS_I_CONFIGFROMSQLSERVER|The package is attempting to configure from SQL Server using the configuration string "%1".|  
|0x40016041|1073832001|DTS_I_CONFIGFROMFILE|The package is attempting to configure from the XML file "%1".|  
|0x40016042|1073832002|DTS_I_CONFIGFROMPARENTVARIABLE|The package is attempting to configure from the parent variable "%1".|  
|0x40016043|1073832003|DTS_I_ATTEMPTINGUPGRADEOFDTS|Attempting an upgrade of SSIS from version "%1" to version "%2". The package is attempting to upgrade the runtime.|  
|0x40016044|1073832004|DTS_I_ATTEMPTINGUPGRADEOFANEXTOBJ|Attempting to upgrade "%1". The package is attempting to upgrade an extensible object.|  
|0x40016045|1073832005|DTS_I_SAVECHECKPOINTSTOFILE|The package will be saving checkpoints to file "%1" during execution. The package is configured to save checkpoints.|  
|0x40016046|1073832006|DTS_I_RESTARTFROMCHECKPOINTFILE|The package restarted from checkpoint file "%1". The package was configured to restart from checkpoint.|  
|0x40016047|1073832007|DTS_I_CHECKPOINTSAVEDTOFILE|Checkpoint file "%1" was updated to record completion of this container.|  
|0x40016048|1073832008|DTS_I_CHECKPOINTFILEDELETED|Checkpoint file "%1" was deleted after successful completion of the package.|  
|0x40016049|1073832009|DTS_I_CHECKPOINTSAVINGTOFILE|Checkpoint file "%1" update starting.|  
|0x40016051|1073832017|DTS_I_CHOSENMAXEXECUTABLES|Based on the system configuration, the maximum concurrent executables are set to %1!d!.|  
|0x40016052|1073832018|DTS_I_MAXEXECUTABLES|Maximum concurrent executables are set to %1!d!.|  
|0x40016053|1073832019|DTS_I_PACKAGESTART|Beginning of package execution.|  
|0x40016054|1073832020|DTS_I_PACKAGEEND|End of package execution.|  
|0x40029161|1073910113|DTS_I_FSTASK_DIRECTORYDELETED|Directory "%1" was deleted.|  
|0x40029162|1073910114|DTS_I_FSTASK_FILEDELETED|File or directory "%1" was deleted.|  
|0x400292A8|1073910440|DTS_I_TRANSFERDBTASK_OVERWRITEDB|Overwriting the database "%1" on the destination server "%2".|  
|0x4002F304|1073935108|DTS_I_SOMETHINGHAPPENED|"%1".|  
|0x4002F323|1073935139|DTS_I_ERRMSGTASK_SKIPPINGERRORMESSAGEALREADYEXISTS|Skipping error message "%1" since it already exists on the destination server.|  
|0x4002F326|1073935142|DTS_I_ERRMSGTASK_TRANSFEREDNERRORMESSAGES|"%1" Error Messages were transferred.|  
|0x4002F351|1073935185|DTS_I_STOREDPROCSTASKS_TRANSFEREDNSPS|The task transferred "%1" Stored Procedures.|  
|0x4002F352|1073935186|DTS_I_TRANSOBJECTSTASK_TRANSFEREDNOBJECTS|Transferred "%1" objects.|  
|0x4002F358|1073935192|DTS_I_TRANSOBJECTSTASK_NOSPSTOTRANSFER|There are no Stored Procedures to transfer.|  
|0x4002F362|1073935202|DTS_I_TRANSOBJECTSTASK_NORULESTOTRANSFER|There are no Rules to transfer.|  
|0x4002F366|1073935206|DTS_I_TRANSOBJECTSTASK_NOTABLESTOTRANSFER|There are no Tables to transfer.|  
|0x4002F370|1073935216|DTS_I_TRANSOBJECTSTASK_NOVIEWSTOTRANSFER|There are no Views to transfer.|  
|0x4002F374|1073935220|DTS_I_TRANSOBJECTSTASK_NOUDFSTOTRANSFER|There are no User Defined Functions to transfer.|  
|0x4002F378|1073935224|DTS_I_TRANSOBJECTSTASK_NODEFAULTSTOTRANSFER|There are no Defaults to transfer.|  
|0x4002F382|1073935234|DTS_I_TRANSOBJECTSTASK_NOUDDTSTOTRANSFER|There are no User Defined Data Types to transfer.|  
|0x4002F386|1073935238|DTS_I_TRANSOBJECTSTASK_NOPFSTOTRANSFER|There are no Partition Functions to transfer.|  
|0x4002F390|1073935248|DTS_I_TRANSOBJECTSTASK_NOPSSTOTRANSFER|There are no Partition Schemes to transfer.|  
|0x4002F394|1073935252|DTS_I_TRANSOBJECTSTASK_NOSCHEMASTOTRANSFER|There are no Schemas to transfer.|  
|0x4002F398|1073935256|DTS_I_TRANSOBJECTSTASK_NOSQLASSEMBLIESTOTRANSFER|There are no SqlAssemblies to transfer.|  
|0x4002F402|1073935362|DTS_I_TRANSOBJECTSTASK_NOAGGREGATESTOTRANSFER|There are no User Defined Aggregates to transfer.|  
|0x4002F406|1073935366|DTS_I_TRANSOBJECTSTASK_NOTYPESTOTRANSFER|There are no User Defined Types to transfer.|  
|0x4002F410|1073935376|DTS_I_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONSTOTRANSFER|There are no XmlSchemaCollections to transfer.|  
|0x4002F418|1073935384|DTS_I_TRANSOBJECTSTASK_NOLOGINSTOTRANSFER|There are no Logins to transfer.|  
|0x4002F41D|1073935389|DTS_I_TRANSOBJECTSTASK_NOUSERSTOTRANSFER|There are no Users to transfer.|  
|0x4002F41E|1073935390|DTS_I_TRANSOBJECTSTASK_TRUNCATINGTABLE|Truncating table "%1"|  
|0x40043006|1074016262|DTS_I_EXECUTIONPHASE_PREPAREFOREXECUTE|Prepare for Execute phase is beginning.|  
|0x40043007|1074016263|DTS_I_EXECUTIONPHASE_PREEXECUTE|Pre-Execute phase is beginning.|  
|0x40043008|1074016264|DTS_I_EXECUTIONPHASE_POSTEXECUTE|Post Execute phase is beginning.|  
|0x40043009|1074016265|DTS_I_EXECUTIONPHASE_CLEANUP|Cleanup phase is beginning.|  
|0x4004300A|1074016266|DTS_I_EXECUTIONPHASE_VALIDATE|Validation phase is beginning.|  
|0x4004300B|1074016267|DTS_I_ROWS_WRITTEN|"%1" wrote %2!ld! rows.|  
|0x4004300C|1074016268|DTS_I_EXECUTIONPHASE_EXECUTE|Execute phase is beginning.|  
|0x4004800C|1074036748|DTS_I_CANTRELIEVEPRESSURE|The buffer manager detected that the system was low on virtual memory, but was unable to swap out any buffers. %1!d! buffers were considered and %2!d! were locked. Either not enough memory is available to the pipeline because not enough is installed, other processes are using it, or too many buffers are locked.|  
|0x4004800D|1074036749|DTS_I_CANTALLOCATEMEMORYPRESSURE|The buffer manager failed a memory allocation call for %3!d! bytes, but was unable to swap out any buffers to relieve memory pressure. %1!d! buffers were considered and %2!d! were locked. Either not enough memory is available to the pipeline because not enough are installed, other processes were using it, or too many buffers are locked.|  
|0x4004800E|1074036750|DTS_I_ALLOCATEDDURINGMEMORYPRESSURE|The buffer manager has allocated %1!d! bytes, even though the memory pressure has been detected and repeated attempts to swap buffers have failed.|  
|0x400490F4|1074041076|DTS_I_TXLOOKUP_CACHE_PROGRESS|%1 has cached %2!d! rows.|  
|0x400490F5|1074041077|DTS_I_TXLOOKUP_CACHE_FINAL|%1 has cached a total of %2!d! rows.|  
|0x4020206D|1075847277|DTS_I_RAWSOURCENOCOLUMNS|The raw source adapter opened a file, but the file contains no columns. The adapter will not produce data. This could indicate a damaged file, or that there are zero columns and, therefore, no data.|  
|0x402020DA|1075847386|DTS_I_OLEDBINFORMATIONALMESSAGE|An OLE DB informational message is available.|  
|0x40208327|1075872551|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_COLLATIONS_DONT_MATCH|Fuzzy match performance can be improved if the exact join FuzzyComparisonFlags on the input column "%1" are set to match with the default SQL collation for reference table column "%2".  It is also necessary that no fold flags are set in FuzzyComparisonFlagsEx.|  
|0x40208328|1075872552|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_INDEX_MISSING|Fuzzy match performance can be improved if an index is created upon the reference table across all of the specified exact match columns.|  
|0x40208387|1075872647|DTS_I_DISPSNOTREVIEWED|Error and truncation dispositions were not reviewed. Make sure this component is configured to redirect rows to error outputs, if you wish to further transform those rows.|  
|0x402090DA|1075876058|DTS_I_TXAGG_WORKSPACE_REHASH|The Aggregate transformation has encountered %1!d! key combinations. It has to re-hash data because the number of key combinations is more than expected. The component can be configured to avoid data re-hash by adjusting the Keys, KeyScale, and AutoExtendFactor properties.|  
|0x402090DB|1075876059|DTS_I_TXAGG_COUNTDISTINCT_REHASH|The Aggregate transformation has encountered %1!d! distinct values while performing a "count distinct" aggregation on "%2". The transformation will re-hash data because the number of distinct values is more than expected. The component can be configured to avoid data re-hash by adjusting the CountDistinctKeys, CountDistinctKeyScale, and AutoExtendFactor properties.|  
|0x402090DC|1075876060|DTS_I_STARTPROCESSINGFILE|The processing of file "%1" has started.|  
|0x402090DD|1075876061|DTS_I_FINISHPROCESSINGFILE|The processing of file "%1" has ended.|  
|0x402090DE|1075876062|DTS_I_TOTALDATAROWSPROCESSEDFORFILE|The total number of data rows processed for file "%1" is %2!I64d!.|  
|0x402090DF|1075876063|DTS_I_FINALCOMMITSTARTED|The final commit for the data insertion in "%1" has started.|  
|0x402090E0|1075876064|DTS_I_FINALCOMMITENDED|The final commit for the data insertion  in "%1" has ended.|  
|0x402090E1|1075876065|DTS_I_BEGINHASHINGCACHE|%1!u! rows are added to the cache. The system is processing the rows.|  
|0x402090E2|1075876066|DTS_I_SUCCEEDEDHASHINGCACHE|The %1 processed %2!u! rows in the cache. The processing time was %3 seconds. The cache used %4!I64u! bytes of memory.|  
|0x402090E3|1075876067|DTS_I_FAILEDHASHINGCACHE|The %1 failed to process the rows in the cache.  The processing time was %2 second(s).|  
|0x402090E4|1075876068|DTS_I_SUCCEEDEDPREPARINGCACHE|The %1 succeeded in preparing the cache. The preparation time was %2 seconds.|  
|0x40209314|1075876628|DTS_I_TXLOOKUP_PARTIALPERF|The %1 has performed the following operations: processed %2!I64u! rows, issued %3!I64u! database commands to the reference database, and performed %4!I64u! lookups using partial cache.|  
|0x40209315|1075876629|DTS_I_TXLOOKUP_PARTIALPERF2|The %1 has performed the following operations: processed %2!I64u! rows, issued %3!I64u! database commands to the reference database, performed %4!I64u! lookups using partial cache and %5!I64u! lookups using the cache for rows with no matching entries in the initial lookup.|  
|0x40209316|1075876630|DTS_I_CACHEFILEWRITESTARTED|The %1 is writing the cache to file "%2".|  
|0x40209317|1075876631|DTS_I_CACHEFILEWRITESUCCEEDED|The %1 has written the cache to file "%2".|  
|0x4020F42C|1075901484|DTS_I_OLEDBDESTZEROMAXCOMMITSIZE|The Maximum insert commit size property of the OLE DB destination "%1" is set to 0. This property setting can cause the running package to stop responding. For more information, see the F1 Help topic for OLE DB Destination Editor (Connection Manager Page).|  
  
##  <a name="msgGeneral"></a> General and Event Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] error messages begin with **DTS_MSG_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x1|1|DTS_MSG_CATEGORY_SERVICE_CONTROL|Incorrect function.|  
|0x2|2|DTS_MSG_CATEGORY_RUNNING_PACKAGE_MANAGEMENT|The system cannot find the file specified.|  
|0x100|256|DTS_MSG_SERVER_STARTING|Starting Microsoft SSIS Service.<br /><br /> Server version %1|  
|0x101|257|DTS_MSG_SERVER_STARTED|Microsoft SSIS Service started.<br /><br /> Server version %1|  
|0x102|258|DTS_MSG_SERVER_STOPPING|The wait operation timed out.|  
|0x103|259|DTS_MSG_SERVER_STOPPED|No more data is available.|  
|0x104|260|DTS_MSG_SERVER_START_FAILED|Microsoft SSIS Service failed to start.<br /><br /> Error: %1|  
|0x105|261|DTS_MSG_SERVER_STOP_ERROR|Error stopping Microsoft SSIS Service.<br /><br /> Error: %1|  
|0x110|272|DTS_MSG_SERVER_MISSING_CONFIG|Microsoft SSIS Service configuration file does not exist.<br /><br /> Loading with default settings.|  
|0x111|273|DTS_MSG_SERVER_BAD_CONFIG|Microsoft SSIS Service configuration file is incorrect.<br /><br /> Error reading config file: %1<br /><br /> Loading server with default settings.|  
|0x112|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|Microsoft SSIS Service:<br /><br /> Registry setting specifying configuration file does not exist.<br /><br /> Attempting to load default config file.|  
|0x150|336|DTS_MSG_SERVER_STOPPING_PACKAGE|Microsoft SSIS Service: stopping running package.<br /><br /> Package instance ID: %1<br /><br /> Package ID: %2<br /><br /> Package name: %3<br /><br /> Package description: %4<br /><br /> Package started by: %5.|  
|0x40013000|1073819648|DTS_MSG_PACKAGESTART|Package "%1" started.|  
|0x40013001|1073819649|DTS_MSG_PACKAGESUCCESS|Package "%1" finished successfully.|  
|0x40013002|1073819650|DTS_MSG_PACKAGECANCEL|Package "%1" has been cancelled.|  
|0x40013003|1073819651|DTS_MSG_PACKAGEFAILURE|Package "%1" failed.|  
|0x40013004|1073819652|DTS_MSG_CANTDELAYLOADDLL|Module %1 cannot load DLL %2 to call entry point %3 because of error %4. The product requires that DLL to run, but the DLL could not be found on the path.|  
|0x40013005|1073819653|DTS_MSG_CANTDELAYLOADDLLFUNCTION|Module %1 loaded DLL %2, but cannot find entry point %3 because of error %4. The named DLL could not be found on the path, and the product requires that DLL to run.|  
|0x40103100|1074802944|DTS_MSG_EVENTLOGENTRY|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103101|1074802945|DTS_MSG_EVENTLOGENTRY_PREEXECUTE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103102|1074802946|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103103|1074802947|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103104|1074802948|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103105|1074802949|DTS_MSG_EVENTLOGENTRY_WARNING|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103106|1074802950|DTS_MSG_EVENTLOGENTRY_ERROR|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103107|1074802951|DTS_MSG_EVENTLOGENTRY_TASKFAILED|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103108|1074802952|DTS_MSG_EVENTLOGENTRY_PROGRESS|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x40103109|1074802953|DTS_MSG_EVENTLOGENTRY_EXECSTATCHANGE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310A|1074802954|DTS_MSG_EVENTLOGENTRY_VARVALCHANGE|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310B|1074802955|DTS_MSG_EVENTLOGENTRY_CUSTOMEVENT|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310C|1074802956|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310D|1074802957|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
|0x4010310E|1074802958|DTS_MSG_EVENTLOGENTRY_INFORMATION|Event Name: %1<br /><br /> Message: %9<br /><br /> Operator: %2<br /><br /> Source Name: %3<br /><br /> Source ID: %4<br /><br /> Execution ID: %5<br /><br /> Start Time: %6<br /><br /> End Time: %7<br /><br /> Data Code: %8|  
  
##  <a name="msgSuccess"></a> Success Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] success messages begin with **DTS_S_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x40003|262147|DTS_S_NULLDATA|The value is NULL.|  
|0x40005|262149|DTS_S_TRUNCATED|The string value was truncated. The buffer received a string that was too long for the column, and the string was truncated by the buffer.|  
|0x200001|2097153|DTS_S_EXPREVALTRUNCATIONOCCURRED|A truncation occurred during evaluation of the expression. The truncation occurred during evaluation, which may include any point in an intermediate step.|  
  
##  <a name="msgPipeline"></a> Data Flow Component Error Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] error messages begin with **DTSBC_E_**, where "BC" refers to the native base class from which most Microsoft data flow components are derived.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0xC8000002|-939524094|DTSBC_E_INCORRECTEXACTNUMBEROFTOTALOUTPUTS|The total number of outputs and error outputs, %1!lu!, is incorrect. There must be exactly %2!lu!.|  
|0xC8000003|-939524093|DTSBC_E_FAILEDTOGETOUTPUTBYINDEX|Cannot retrieve output with index %1!lu!.|  
|0xC8000005|-939524091|DTSBC_E_INCORRECTEXACTNUMBEROFERROROUTPUTS|The number of error outputs, %1!lu!,  is incorrect. There must be exactly %2!lu!.|  
|0xC8000006|-939524090|DTSBC_E_INVALIDVALIDATIONSTATUSVALUE|Incorrect validation status value, "%1!lu! ".  It must be one of the values found in the DTSValidationStatus enumeration.|  
|0xC8000007|-939524089|DTSBC_E_INPUTHASNOOUTPUT|The input "%1!lu!" has no synchronous output.|  
|0xC8000008|-939524088|DTSBC_E_INPUTHASNOERROROUTPUT|The input "%1!lu!" has no synchronous error output.|  
|0xC8000009|-939524087|DTSBC_E_INVALIDHTPIVALUE|The HowToProcessInput value, %1!lu!, is not valid. It must be one of the values from the HowToProcessInput enumeration.|  
|0xC800000A|-939524086|DTSBC_E_FAILEDTOGETCOLINFO|Failed to get information for row "%1!ld!", column "%2!ld!" from the buffer.  The error code returned was 0x%3!8.8X!.|  
|0xC800000B|-939524085|DTSBC_E_FAILEDTOSETCOLINFO|Failed to set information for row "%1!ld!", column "%2!ld!" into the buffer.  The error code returned was 0x%3!8.8X!.|  
|0xC800000C|-939524084|DTSBC_E_INVALIDPROPERTY|The property "%1" is not valid.|  
|0xC800000D|-939524083|DTSBC_E_PROPERTYNOTFOUND|The property "%1" was not found.|  
|0xC8000010|-939524080|DTSBC_E_READONLYPROPERTY|Error assigning a value to the read-only property "%1".|  
|0xC8000011|-939524079|DTSBC_E_CANTINSERTOUTPUTCOLUMN|The %1 does not allow the insertion of output columns.|  
|0xC8000012|-939524078|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCH|The output columns' metadata does not match the associated input columns' metadata.  The output columns' metadata will be updated.|  
|0xC8000013|-939524077|DTSBC_E_OUTPUTCOLUMNSMISSING|There are input columns that do not have associated output columns. The output columns will be added.|  
|0xC8000014|-939524076|DTSBC_E_TOOMANYOUTPUTCOLUMNS|There are output columns that do not have associated input columns. The output columns will be removed.|  
|0xC8000015|-939524075|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCHUNMAP|The output columns' metadata does not match the associated input columns' metadata.  The input columns will be unmapped.|  
|0xC8000016|-939524074|DTSBC_E_UNMAPINPUTCOLUMNS|There are input columns that do not have associated output columns. The input columns will be unmapped.|  
|0xC8000017|-939524073|DTSBC_E_MULTIPLEINCOLSTOOUTCOL|There is an input column associated with an output column, and that output column is already associated with another input column on the same input.|  
|0xC8000018|-939524072|DTSBC_E_CANTINSERTEXTERNALMETADATACOLUMN|The %1 does not allow the insertion of external metadata columns.|  
  
  字符串文字“%1”包含非法的转义序列“\\`2!c!”。 表达式计算器中的字符串文字不支持此转义序列。-如果字符串中需要反斜杠，请使用双反斜杠符号 "\\\\"。 conceptual
helpviewer_keywords: 
  - "error numbers [Integration Services]"
  - "hresults [Integration Services]"
  - "errors [Integration Services], listed"
ms.assetid: 2c825c07-5074-42ad-90ea-0dc5a588dcf7
author: janinezhang
ms.author: janinez
---
# Integration Services Error and Message Reference

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  The following tables list predefined [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] errors, warnings, and informational messages, in ascending numerical order within each category, along with their numeric codes and symbolic names. Each of these errors is defined as a field in the <xref:Microsoft.SqlServer.Dts.Runtime.Hresults> class in the <xref:Microsoft.SqlServer.Dts.Runtime> namespace.  
  
 This list may be useful when you encounter an error code without its description. The list does not include troubleshooting information at this time.  
  
> [!IMPORTANT]  
>  Many of the error messages that you may see while working with [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] come from other components. In this topic, you will find all the errors raised by [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] components. If you do not see your error in the list, the error was raised by a component outside [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. These may include OLE DB providers, other database components such as the [!INCLUDE[ssDE](../includes/ssde-md.md)] and [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , or other services or components such as the file system, the SMTP server, Message Queuing (also known as MSMQ), and so forth. To find information about these external error messages, see the documentation specific to the component.  
  
 This list cadontains the following groups of messages:  
  
-   [Error Messages (DTS_E_*)](#msgError)  
  
-   [Warning Messages (DTS_W_*)](#msgWarning)  
  
-   [Informational Messages(DTS_I_*)](#msgInfo)  
  
-   [General and Event Messages(DTS_MSG_*)](#msgGeneral)  
  
-   [Success Messages(DTS_S_*)](#msgSuccess)  
  
-   [Data Flow Component Error Messages (DTSBC_E_*)](#msgPipeline)  
  
##  <a name="msgError"></a> Error Messages  
 The symbolic names of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] error messages begin with **DTS_E_**.  
  
|Hexadecimal code|Decimal Code|Symbolic Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x8002F347|-2147290297|DTS_E_STOREDPROCSTASK_OVERWRITINGSPATDESTINATION|Overwriting Stored Procedure "%1" at destination.|  
|0x8020837E|-2145352834|DTS_E_ADOSRCUNKNOWNTYPEMAPPEDTONTEXT|The data type "%1" found on column "%2" is not supported for the %3. This column will be converted to  DT_NTEXT.|  
|0x8020838C|-2145352820|DTS_E_XMLSRCSCHEMACOLUMNNOTINEXTERNALMETADATA|The column %1 in table %2 in the XML schema does not have a mapping in the external metadata columns.|  
|0xC0000032|-1073741774|DTS_E_NOTINITIALIZED|An internal object or variable was not initialized. This is an internal product error.  This error is returned when a variable should have a valid value but does not.|  
|0xC0000033|-1073741773|DTS_E_EXPIRED|Integration Services evaluation period has expired.|  
|0xC0000034|-1073741772|DTS_E_NEGATIVEVALUESNOTALLOWED|This property cannot be assigned a negative value. This error occurs when a negative value is assigned to a property that can only contain positive values, such as the COUNT property.|  
|0xC0000035|-1073741771|DTS_E_NEGATIVEINDEXNOTALLOWED|Indexes cannot be negative. This error occurs when a negative value is used as an index to a collection.|  
|0xC00060AB|-1073717077|DTS_E_INVALIDSSISSERVERNAME|Invalid server name "%1". SSIS service does not support multi-instance, use just server name instead of "server name\instance".|  
|0xC0008445|-1073707963|DTS_E_SCRIPTMIGRATIONFAILED64BIT|Migration for VSA scripts can not be done on 64 bit platforms due to lack of Visual Tools for Applications designer support. Run the migration under WOW64 on 64 bit platforms.|  
|0xC000931A|-1073704166|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_ERRORSINCOMMAND|The command execution generated errors.|  
|0xC000F427|-1073679321|DTS_E_SSISSTANDALONENOTINSTALLED|To run a SSIS package outside of [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] you must install %1 of Integration Services or higher.|  
|0xC0010001|-1073676287|DTS_E_VARIABLENOTFOUND|The variable cannot be found. This occurs when an attempt is made to retrieve a variable from the Variables collection on a container during execution of the package, and the variable is not there. The variable name may have changed or the variable is not being created.|  
|0xC0010003|-1073676285|DTS_E_VARIABLEREADONLY|Error trying to write to a read-only variable, "%1".|  
|0xC0010004|-1073676284|DTS_E_MANAGEDCOMPONENTSTORENOTFOUND|Unable to find the directories containing Tasks and Data Flow Task components. Check the integrity of your installation.|  
|0xC0010006|-1073676282|DTS_E_PACKAGENAMETOOLONG|Package name is too long. The limit is 128 characters. Shorten the package name.|  
|0xC0010007|-1073676281|DTS_E_PACKAGEDESCRIPTIONTOOLONG|Package description is too long. The limit is 1024 characters. Shorten the package description.|  
|0xC0010008|-1073676280|DTS_E_VERCOMMENTSTOOLONG|VersionComments property is too long. The limit is 1024 characters. Try shortening the VersionComments.|  
|0xC0010009|-1073676279|DTS_E_ELEMENTNOTFOUND|The element cannot be found in a collection. This error happens when you try to retrieve an element from a collection on a container during execution of the package and the element is not there.|  
|0xC001000A|-1073676278|DTS_E_PACKAGENOTFOUND|The specified package could not be loaded from the SQL Server database.|  
|0xC001000C|-1073676276|DTS_E_INVALIDVARIABLEVALUE|The variable value assignment is not valid. This error happens when the client or a task assigns a runtime object to a variable value.|  
|0xC001000D|-1073676275|DTS_E_RESERVEDNAMESPACE|Error assigning namespace to the variable. The namespace "System" is reserved for system use. This error happens when a component or task attempts to create a variable with a namespace of "System".|  
|0xC001000E|-1073676274|DTS_E_CONNECTIONNOTFOUND|The connection "%1" is not found. This error is thrown by Connections collection when the specific connection element is not found.|  
|0xC001000F|-1073676273|DTS_E_64BITVARIABLERECAST|The variable "%1" is a 64-bit integer variable, which is not supported on this operating system. The variable has been recast to 32-bit integer.|  
|0xC0010010|-1073676272|DTS_E_CANTCHANGEREADONLYATRUNTIME|An attempt change to a read-only attribute on variable "%1" occurred. This error happens when a read-only attribute for a variable is being changed at runtime. Read-only attributes can be changed only at design time.|  
|0xC0010011|-1073676271|DTS_E_VARIABLEINVALIDCONTAINERREF|Invalid attempt to set a variable to a container reference.  Variables are not allowed to reference containers.|  
|0xC0010013|-1073676269|DTS_E_INVALIDVARVALUE|Assigning invalid value or object to variable "%1". This error happens when a value is not appropriate for variables.|  
|0xC0010014|-1073676268|DTS_E_GENERICERROR|One or more error occurred. There should be more specific errors preceding this one that explains the details of the errors. This message is used as a return value from functions that encounter errors.|  
|0xC0010016|-1073676266|DTS_E_INVALIDARRAYVALUE|Error getting or setting an array value. The type "%1" is not allowed. This occurs when loading an array into a variable.|  
|0xC0010017|-1073676265|DTS_E_UNSUPPORTEDARRAYTYPE|Unsupported type in array. This happens when saving an array of unsupported types into a variable.|  
|0xC0010018|-1073676264|DTS_E_PERSISTENCEERROR|Error loading value "%1" from node "%2".|  
|0xC0010019|-1073676263|DTS_E_INVALIDNODE|Node "%1" is not a valid node. This happens when saving fails.|  
|0xC0010020|-1073676256|DTS_E_ERRORLOADINGTASK|Failed to load task "%1", type "%2". The contact information for this task is "%3".|  
|0xC0010021|-1073676255|DTS_E_ERRORELEMENTNOTINCOLL|Element "%1" does not exist in collection "%2".|  
|0xC0010022|-1073676254|DTS_E_MISSINGOBJECTDATA|The ObjectData element is missing in the XML block of a hosted object. This occurs when the XML parser attempts to locate the data element for an object and it cannot be found.|  
|0xC0010023|-1073676253|DTS_E_VARIABLENOTFOUNDINCOLL|The variable "%1" cannot be found. This error occurs when an attempt to retrieve a variable from a variables collection on a container during execution of the package occurs, and the variable is not there.  A variable name may have changed or the variable is not being created.|  
|0xC0010025|-1073676251|DTS_E_HASEMPTYTASKHOSTS|The package cannot execute because it contains tasks that failed to load.|  
|0xC0010026|-1073676250|DTS_E_TASKISEMPTY|The task has failed to load. The contact information for this task is "%1".|  
|0xC0010027|-1073676249|DTS_E_ERRORLOADINGTASKNOCONTACT|Error loading task "%1".|  
|0xC0010028|-1073676248|DTS_E_ERRORATLOADTASK|Error loading task. This happens when loading a task from XML fails.|  
|0xC0010200|-1073675776|DTS_E_MULTIPLECACHEWRITES|The %1 cannot write to the cache because %2 has already written to it.|  
|0xC0010201|-1073675775|DTS_E_SETCACHEFORINSERTFAILED|Failed to prepare the cache for new data.|  
|0xC0010202|-1073675774|DTS_E_SETCACHEFORFILLFAILED|Failed to mark the cache as filled with data.|  
|0xC0010203|-1073675773|DTS_E_READUNINITIALIZEDCACHE|The cache is not initialized and cannot be read by %1.|  
|0xC0010204|-1073675772|DTS_E_SETCACHEFORREADFAILED|Failed to prepare the cache for providing data.|  
|0xC0010205|-1073675771|DTS_E_READNOTFILLEDCACHE|The cache is being written to by %1, and cannot be read by %2.|  
|0xC0010206|-1073675770|DTS_E_WRITEWHILECACHEINUSE|The cache is being read from %1 and cannot be written to by %2.|  
|0xC0011001|-1073672191|DTS_E_CANTLOADFROMNODE|The runtime object cannot be loaded from the specified XML node.  This happens when trying to load a package or other object from an XML node that is not of the correct type, such as a non-SSIS XML node.|  
|0xC0011002|-1073672190|DTS_E_OPENPACKAGEFILE|Failed to open package file "%1" due to error 0x%2!8.8X! "%3".  This happens when loading a package and the file cannot be opened or loaded correctly into the XML document. This can be the result of either providing an incorrect file name was specified when calling LoadPackage or the XML file was specified and has an incorrect format.|  
|0xC0011003|-1073672189|DTS_E_LOADPACKAGEXML|Failed to load XML due to error 0x%1!8.8X! "%2". This happens when loading a package and the file cannot be opened or loaded correctly into XML document.  This can be the result of either providing an incorrect file name to the LoadPackage method or the XML file specified having an incorrect format.|  
|0xC0011004|-1073672188|DTS_E_LOADPACKAGEXMLFILE|Failed to load XML from package file "%1" due to error 0x%2!8.8X! "%3".  This happens when loading a package and the file cannot be opened or loaded correctly into an XML document. This can be the result of either providing an incorrect file name to the LoadPackage method or the XML file specified having an incorrect format.|  
|0xC0011005|-1073672187|DTS_E_OPENFILE|Failed to open package file. This happens when loading a package and the file cannot be opened or loaded correctly into an XML document. This can be the result of either providing an incorrect file name to the LoadPackage method or the XML file specified having an incorrect format.|  
|0xC0011006|-1073672186|DTS_E_UNABLETODECODEBINARYFORMAT|Unable to decode a binary format in the package.|  
|0xC0011007|-1073672185|DTS_E_FUNDAMENTALLOADINGERROR|Unable to load the package as XML because of package does not have a valid XML format. A specific XML parser error will be posted.|  
|0xC0011008|-1073672184|DTS_E_LOADFROMXML|Error loading from XML. No further detailed error information can be specified for this problem because no Events object was passed where detailed error information can be stored.|  
|0xC0011009|-1073672183|DTS_E_XMLDOMERROR|Cannot create an instance of the XML Document Object Model. MSXML may not be registered.|  
|0xC001100D|-1073672179|DTS_E_CANNOTLOADOLDPACKAGES|The package cannot be loaded. This occurs when attempting to load an older version package, or the package file refers to an invalid structured object.|  
|0xC001100E|-1073672178|DTS_E_SAVEFILE|Failed to save package file.|  
|0xC001100F|-1073672177|DTS_E_SAVEPACKAGEFILE|Failed to save package file "%1" with error 0x%2!8.8X! "%3".|  
|0xC001200D|-1073668083|DTS_E_IDTSNAMENOTSUPPORTED|The object must inherit from IDTSName100 and does not.|  
|0xC0012018|-1073668072|DTS_E_CONFIGFORMATINVALID_PACKAGEDELIMITER|The configuration entry, "%1", has an incorrect format because it does not begin with package delimiter. There was no "\package" delimiter.|  
|0xC0012019|-1073668071|DTS_E_CONFIGFORMATINVALID|The configuration entry "%1" had an incorrect format. This can occur because of a missing delimiter or formatting errors, like an invalid array delimiter.|  
|0xC001201B|-1073668069|DTS_E_CONFIGFILEFAILEDEXPORT|Failure exporting configuration file.|  
|0xC0012021|-1073668063|DTS_E_PROPERTIESCOLLECTIONREADONLY|Properties collection cannot be modified.|  
|0xC0012022|-1073668062|DTS_E_DTRXMLSAVEFAILURE|Unable to save configuration file. The file may be read only.|  
|0xC0012023|-1073668061|DTS_E_FAILPACKAGEONFAILURENA|FailPackageOnFailure property is not applicable to the package container.|  
|0xC0012024|-1073668060|DTS_E_TASKPRODUCTLEVEL|The task "%1" cannot run on installed %2 of Integration Services. It requires %3 or higher.|  
|0xC0012029|-1073668055|DTS_E_UNABLETOSAVETOFILE|Unable to save xml to "%1". The file may be read only.|  
|0xC0012037|-1073668041|DTS_E_CONFIGTYPECONVERSIONFAILED|Failed to convert a type in the configuration "%1" for the package path "%2".  This happens when a configuration value cannot be converted from a string to the appropriate destination type. Check the configuration value to ensure it can be converted to the type of the destination property or variable.|  
|0xC0012049|-1073668023|DTS_E_CONFIGFAILED|Configuration failure. This is a generic warning for all configuration types. Other warnings should precede this with more information.|  
|0xC0012050|-1073668016|DTS_E_REMOTEPACKAGEVALIDATION|Package failed validation from the ExecutePackage task. The package cannot run.|  
|0xC0013001|-1073663999|DTS_E_FAILTOCREATEMUTEX|Failed to create mutex "%1" with error 0x%2!8.8X!.|  
|0xC0013002|-1073663998|DTS_E_MUTEXOWNBYDIFFUSER|Mutex "%1" already exists and is owned by another user.|  
|0xC0013003|-1073663997|DTS_E_WAITFORMUTEXFAILED|Failed to acquire mutex "%1" with error 0x%2!8.8X!.|  
|0xC0013004|-1073663996|DTS_E_FAILTORELEASEMUTEX|Failed to release mutex "%1" with error 0x%2!8.8X!.|  
|0xC0014003|-1073659901|DTS_E_INVALIDTASKPOINTER|The wrappers task pointer is not valid. The wrapper has an invalid pointer to a task.|  
|0xC0014004|-1073659900|DTS_E_ALREADYADDED|The executable has been added to the Executables collection of another container. This occurs when a client tries to add an executable to more than one Executables collection. You need to remove the executable from the current Executables collection before attempting to add it.|  
|0xC0014005|-1073659899|DTS_E_UNKNOWNCONNECTIONMANAGERTYPE|The connection type "%1" specified for connection manager "%2" is not recognized as a valid connection manager type. This error is returned when an attempt is made to create a connection manager for an unknown connection type. Check the spelling in the connection type name.|  
|0xC0014006|-1073659898|DTS_E_COLLECTIONCOULDNTADD|An object was created but the attempt to add it to a collection failed. This can occur due to an out-of-memory condition.|  
|0xC0014007|-1073659897|DTS_E_ODBCERRORENV|There was an error creating an Open Database Connectivity (ODBC) environment.|  
|0xC0014008|-1073659896|DTS_E_ODBCERRORDBC|There was an error creating an Open Database Connectivity (ODBC) database connection.|  
|0xC0014009|-1073659895|DTS_E_ODBCERRORCONNECT|There was an error trying to establish an Open Database Connectivity (ODBC) connection with the database server.|  
|0xC001400A|-1073659894|DTS_E_CONNECTIONMANAGERQUALIFIERALREADYSET|The qualifier is already set on this instance of the connection manager. The qualifier may be set once per instance.|  
|0xC001400B|-1073659893|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSET|The qualifier has not been set on this instance of the connection manager. Setting the qualifier is required to complete initialization.|  
|0xC001400C|-1073659892|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSUPPORTED|This connection manager does not support specification of qualifiers.|  
|0xC001400D|-1073659891|DTS_E_CANNOTCLONECONNECTIONMANAGER|Connection manager "0x%1" cannot be cloned for out-of-process execution.|  
|0xC001400E|-1073659890|DTS_E_NOSQLPROFILERDLL|The log provider for SQL Server Profiler was unable to load pfclnt.dll. Please check that SQL Server Profiler is installed.|  
|0xC001400F|-1073659889|DTS_E_LOGFAILED|The SSIS logging infrastructure failed with error code 0x%1!8.8X!. This error indicates that this logging error is not attributable to a specific log provider.|  
|0xC0014010|-1073659888|DTS_E_LOGPROVIDERFAILED|The SSIS logging provider "%1" failed with error code 0x%2!8.8X! (%3).  This indicates a logging error attributable to the specified log provider.|  
|0xC0014011|-1073659887|DTS_E_SAVETOSQLSERVER_OLEDB|The SaveToSQLServer method has encountered OLE DB error code 0x%1!8.8X! (%2).  The SQL statement that was issued has failed.|  
|0xC0014012|-1073659886|DTS_E_LOADFROMSQLSERVER_OLEDB|The LoadFromSQLServer method has encountered OLE DB error code 0x%1!8.8X! (%2).  The SQL statement that was issued has failed.|  
|0xC0014013|-1073659885|DTS_E_REMOVEFROMSQLSERVER_OLEDB|The RemoveFromSQLServer method encountered OLE DB error code 0x%1!8.8X! (%2) The SQL statement that was issued has failed.|  
|0xC0014014|-1073659884|DTS_E_EXISTSONSQLSERVER_OLEDB|The ExistsOnSQLServer method has encountered OLE DB error code 0x%1!8.8X! (%2). The SQL statement issued has failed.|  
|0xC0014015|-1073659883|DTS_E_CONNECTIONSTRING|OLE DB has failed making a database connection when using the supplied connection string.|  
|0xC0014016|-1073659882|DTS_E_FROMEXECISNOTCHILD|When adding a precedence constraint, a From executable was specified that is not a child of this container.|  
|0xC0014017|-1073659881|DTS_E_TOEXECISNOTCHILD|When adding a precedence constraint, the To executable specified is not a child of this container.|  
|0xC0014018|-1073659880|DTS_E_ODBCTRANSACTIONENLIST|There was an error trying enlist an ODBC connection in a transaction. The SQLSetConnectAttr failed to set the SQL_ATTR_ENLIST_IN_DTC attribute.|  
|0xC0014019|-1073659879|DTS_E_CONNECTIONOFFLINE|The connection manager "%1" will not acquire a connection because the package OfflineMode property is TRUE. When the OfflineMode is TRUE, connections cannot be acquired.|  
|0xC001401A|-1073659878|DTS_E_BEGINTRANSACTION|The SSIS Runtime has failed to start the distributed transaction due to error 0x%1!8.8X! "%2". The DTC transaction failed to start. This could occur because the MSDTC Service is not running.|  
|0xC001401B|-1073659877|DTS_E_SETQUALIFIERDESIGNTIMEONLY|The SetQualifier method cannot be called on a connection manager during package execution. This method is used at design-time only.|  
|0xC001401C|-1073659876|DTS_E_SQLPERSISTENCEVERSION|Storing or modifying packages in SQL Server requires the SSIS runtime and database to be the same version. Storing packages in earlier versions is not supported.|  
|0xC001401D|-1073659875|DTS_E_CONNECTIONVALIDATIONFAILED|Connection "%1" failed validation.|  
|0xC001401E|-1073659874|DTS_E_INVALIDFILENAMEINCONNECTION|The file name "%1" specified in the connection was not valid.|  
|0xC001401F|-1073659873|DTS_E_MULTIPLEFILESONRETAINEDCONNECTION|Multiple file names cannot be specified on a connection when the Retain property is TRUE. Vertical bars were found on the connection string, meaning multiple file names are being specified and, in addition, the Retain property is TRUE.|  
|0xC0014020|-1073659872|DTS_E_ODBCERROR|An ODBC error %1!d! has occurred.|  
|0xC0014021|-1073659871|DTS_E_PRECEDENCECONSTRAINT|There was an error in the precedence constraint between "%1" and "%2".|  
|0xC0014022|-1073659870|DTS_E_FAILEDPOPNATIVEFEE|Failed to populate the ForEachEnumeratorInfos collection with native ForEachEnumerators with the following error code: %1.|  
|0xC0014023|-1073659869|DTS_E_GETENUMERATOR|The GetEnumerator method of the ForEach Enumerator has failed with error 0x%1!8.8X! "%2". This occurs when the ForEach Enumerator cannot enumerate.|  
|0xC0014024|-1073659868|DTS_E_CANTGETCERTDATA|The raw certificate data cannot be obtained from the supplied certificate object (error: %1). This occurs when CPackage::put_CertificateObject cannot instantiate the ManagedHelper object, when the ManagedHelper object fails, or when the ManagedHelper object returns a malformed array.|  
|0xC0014025|-1073659867|DTS_E_CANTCREATECERTCONTEXT|Failed to create certificate context (error: %1). This occurs in CPackage::put_CertificateObject or CPackage::LoadFromXML when the corresponding CryptoAPI function fails.|  
|0xC0014026|-1073659866|DTS_E_CANTOPENCERTSTORE|Opening MY certificate store failed with error "%1".This occurs in CPackage::LoadUserCertificateByName and CPackage::LoadUserCertificateByHash.|  
|0xC0014027|-1073659865|DTS_E_CANTFINDCERTBYNAME|The certificate specified by name in MY store cannot be found (error: %1). This occurs in CPackage::LoadUserCertificateByName.|  
|0xC0014028|-1073659864|DTS_E_CANTFINDCERTBYHASH|Unable to find the specified certificate by hash in "MY" store (error: %1). Occurs in CPackage::LoadUserCertificateByHash.|  
|0xC0014029|-1073659863|DTS_E_INVALIDCERTHASHFORMAT|The hash value is not a one-dimensional array of bytes (error: %1). This occurs in CPackage::LoadUserCertificateByHash.|  
|0xC001402A|-1073659862|DTS_E_CANTACCESSARRAYDATA|The data in the array cannot be accessed (error: %1). This error can occur wherever GetDataFromSafeArray is called.|  
|0xC001402B|-1073659861|DTS_E_CREATEMANAGEDHELPERFAILED|The SSIS managed helper object failed during creation with error 0x%1!8.8X! "%2". This occurs whenever CoCreateInstance CLSID_DTSManagedHelper fails.|  
|0xC001402C|-1073659860|DTS_E_OLEDBTRANSACTIONENLIST|The SSIS Runtime has failed to enlist the OLE DB connection in a distributed transaction with error 0x%1!8.8X! "%2".|  
|0xC001402D|-1073659859|DTS_E_SIGNPACKAGEFAILED|Package signing failed with error 0x%1!8.8X! "%2". This occurs when the ManagedHelper.SignDocument method fails.|  
|0xC001402E|-1073659858|DTS_E_CHECKENVELOPEFAILED|Failed to check for XML signature envelope in package XML with error 0x%1!8.8X! "%2". This occurs in CPackage::LoadFromXML.|  
|0xC001402F|-1073659857|DTS_E_GETXMLSOURCEFAILED|Failed to obtain XML source from XML DOM object with error 0x%1!8.8X! "%2". This occurs when IXMLDOMDocument::get_xml fails.|  
|0xC0014030|-1073659856|DTS_E_PACKAGEVERIFICATIONFAILED|The cryptographic signature of the package failed verification due to error 0x%1!8.8X! "%2". This occurs when the signature verification operation fails.|  
|0xC0014031|-1073659855|DTS_E_GETKEYFROMCERTFAILED|Failed to obtain cryptographic key pair associated with the specified certificate with error 0x%1!8.8X! "%2". Verify that you have the key pair for which the certificate was issued. This error usually occurs when trying to sign a document using a certificate for which the person does not have the private key.|  
|0xC0014032|-1073659854|DTS_E_INVALIDSIGNATURE|The digital signature is not valid. The contents of the package have been modified.|  
|0xC0014033|-1073659853|DTS_E_UNTRUSTEDSIGNATURE|The digital signature is valid; however the signer is not trusted and, therefore, authenticity cannot be guaranteed.|  
|0xC0014034|-1073659852|DTS_E_TRANSACTIONENLISTNOTSUPPORTED|The connection does not support enlisting in distributed transaction.|  
|0xC0014035|-1073659851|DTS_E_PACKAGEPROTECT|Failed to apply package protection with error 0x%1!8.8X! "%2". This error occurs when saving to Xml.|  
|0xC0014036|-1073659850|DTS_E_PACKAGEUNPROTECT|Failed to remove package protection with error 0x%1!8.8X! "%2". This occurs in the CPackage::LoadFromXML method.|  
|0xC0014037|-1073659849|DTS_E_PACKAGEPASSWORD|The package is encrypted with a password. The password was not specified, or is not correct.|  
|0xC0014038|-1073659848|DTS_E_DUPLICATECONSTRAINT|A precedence constraint already exists between the specified executables. More than one precedence constraint is not allowed.|  
|0xC0014039|-1073659847|DTS_E_PACKAGELOADFAILED|The package failed to load due to error 0x%1!8.8X! "%2". This occurs when CPackage::LoadFromXML fails.|  
|0xC001403A|-1073659846|DTS_E_PACKAGEOBJECTNOTENVELOPED|Failed to find package object in signed XML envelope with error 0x%1!8.8X! "%2". This occurs when signed XML does not contain a SSIS package, as expected.|  
|0xC001403B|-1073659845|DTS_E_JAGGEDEVENTINFO|The lengths of parameter names, types, and descriptions arrays are not equal. The lengths must be equal. This occurs when the lengths of the arrays are mismatched. There should be one entry per parameter in each array.|  
|0xC001403C|-1073659844|DTS_E_GETPACKAGEINFOS|An OLE DB error 0x%1!8.8X! (%2) occurred while enumerating packages. A SQL statement was issued and failed.|  
|0xC001403D|-1073659843|DTS_E_UNKNOWNLOGPROVIDERTYPE|The log provider type "%1" specified for log provider "%2" is not recognized as a valid log provider type. This error occurs when an attempt is made to create a log provider for unknown log provider type. Verify the spelling in the log provider type name.|  
|0xC001403E|-1073659842|DTS_E_UNKNOWNLOGPROVIDERTYPENOSUBS|The log provider type is not recognized as a valid log provider type. This error occurs when an attempt is made to create a log provider for unknown log provider type. Verify the spelling in the log provider type name.|  
|0xC001403F|-1073659841|DTS_E_UNKNOWNCONNECTIONMANAGERTYPENOSUBS|The connection type specified for connection manager is not a valid connection manager type. This error occurs when an attempt is made to create a connection manager for unknown connection type. Verify the spelling of the connection type name.|  
|0xC0014040|-1073659840|DTS_E_PACKAGEREMOVEFAILED|An error was encountered when trying to remove the package "%1" from SQL Server.|  
|0xC0014042|-1073659838|DTS_E_FOLDERADDFAILED|An error was encountered when trying to create a folder on SQL Server named "%1" in folder "%2".|  
|0xC0014043|-1073659837|DTS_E_CREATEFOLDERONSQLSERVER_OLEDB|The CreateFolderOnSQLServer method has encountered OLE DB error code 0x%1!8.8X! (%2) The SQL statement issued has failed.|  
|0xC0014044|-1073659836|DTS_E_FOLDERRENAMEFAILED|An error occurred when renaming folder " %1\\\\%2" to "%1\\\\%3" on SQL Server.|  
|0xC0014045|-1073659835|DTS_E_RENAMEFOLDERONSQLSERVER_OLEDB|The RenameFolderOnSQLServer method encountered OLE DB error code 0x%1!8.8X! (%2). The SQL statement issued has failed.|  
|0xC0014046|-1073659834|DTS_E_FOLDERDELETEFAILED|Error deleting SQL Server folder "%1".|  
|0xC0014047|-1073659833|DTS_E_REMOVEFOLDERFROMSQLSERVER_OLEDB|The RemoveFolderOnSQLServer method encountered OLE DB error code 0x%1!8.8X! (%2). The SQL statement issued has failed.|  
|0xC0014048|-1073659832|DTS_E_INVALIDPATHTOPACKAGE|The specified package path does not contain a package name. This occurs when the path does not contain at least one backslash or one forward slash.|  
|0xC0014049|-1073659831|DTS_E_FOLDERNOTFOUND|Cannot find folder "%1".|  
|0xC001404A|-1073659830|DTS_E_FINDFOLDERONSQLSERVER_OLEDB|While trying to find a folder on SQL an OLE DB error was encountered with error code 0x%1!8.8X! (%2).|  
|0xC001404B|-1073659829|DTS_E_OPENLOGFAILED|The SSIS logging provider has failed to open the log. Error code: 0x%1!8.8X!.|  
|0xC001404C|-1073659828|DTS_E_GETCONNECTIONINFOS|Failed to get ConnectionInfos collection with error 0x%1!8.8X! "%2". This error occurs when the call to IDTSApplication100::get_ConnectionInfos fails.|  
|0xC001404D|-1073659827|DTS_E_VARIABLEDEADLOCK|Deadlock detected while trying to lock variables. The locks cannot be acquired after 16 attempts. The locks timed out.|  
|0xC001404E|-1073659826|DTS_E_NOTDISPENSED|The Variables collection has not been returned from the VariableDispenser. An operation was attempted that is only allowed on dispensed collections.|  
|0xC001404F|-1073659825|DTS_E_VARIABLESALREADYUNLOCKED|This Variables collection has already been unlocked. The Unlock method is called only once on a dispensed Variables collection.|  
|0xC0014050|-1073659824|DTS_E_VARIABLEUNLOCKFAILED|One or more variables failed to unlock.|  
|0xC0014051|-1073659823|DTS_E_DISPENSEDREADONLY|The Variables collection was returned the from VariableDispenser and cannot be modified. Items cannot be added to or removed from dispensed collections.|  
|0xC0014052|-1073659822|DTS_E_VARIABLEALREADYONREADLIST|The variable "%1" is already on the read list. A variable may only be added once to either the read lock list or the write lock list.|  
|0xC0014053|-1073659821|DTS_E_VARIABLEALREADYONWRITELIST|The variable "%1" is already on the write list. A variable may only be added once to either the read lock list or the write lock list.|  
|0xC0014054|-1073659820|DTS_E_LOCKVARIABLEFORREAD|Failed to lock variable "%1" for read access with error 0x%2!8.8X! "%3".|  
|0xC0014055|-1073659819|DTS_E_LOCKVARIABLEFORWRITE|Failed to lock variable "%1" for read/write access with error 0x%2!8.8X! "%3".|  
|0xC0014056|-1073659818|DTS_E_CUSTOMEVENTCONFLICT|The custom event "%1" is already declared with a different parameter list. A task is trying to declare a custom event, which another task has already declared with a different parameter list.|  
|0xC0014057|-1073659817|DTS_E_EVENTHANDLERNOTALLOWED|The task providing the custom event "%1" does not allow this event to be handled in the package. The custom event was declared with AllowEventHandlers = FALSE.|  
|0xC0014059|-1073659815|DTS_E_UNSAFEVARIABLESALREADYSET|The VariableDispenser received an unsafe Variables collection. This operation cannot be repeated.|  
|0xC001405A|-1073659814|DTS_E_INVALIDPARENTPACKAGEPATH|GetPackagePath was called on the ForEachEnumerator but there was no ForEachLoop package path specified.|  
|0xC001405B|-1073659813|DTS_E_VARIABLEDEADLOCK_READ|A deadlock was detected while trying to lock variable "%1" for read access. A lock could not be acquired after 16 attempts and timed out.|  
|0xC001405C|-1073659812|DTS_E_VARIABLEDEADLOCK_READWRITE|A deadlock was detected while trying to lock variables "%1" for read/write access. A lock cannot be acquired after 16 attempts. The locks timed out.|  
|0xC001405D|-1073659811|DTS_E_VARIABLEDEADLOCK_BOTH|A deadlock was detected while trying to lock variables "%1" for read access and variables "%2" for read/write access. A lock cannot be acquired after 16 attempts. The locks timed out.|  
|0xC001405E|-1073659810|DTS_E_PACKAGEPASSWORDEMPTY|The protection level of the package requires a password, but PackagePassword property is empty.|  
|0xC001405F|-1073659809|DTS_E_DECRYPTXML_PASSWORD|Failed to decrypt an encrypted XML node because the password was not specified or not correct. Package load will attempt to continue without the encrypted information.|  
|0xC0014060|-1073659808|DTS_E_DECRYPTPACKAGE_USERKEY|Failed to decrypt a package that is encrypted with a user key. You may not be the user who encrypted this package, or you are not using the same machine that was used to save the package.|  
|0xC0014061|-1073659807|DTS_E_SERVERSTORAGEDISALLOWED|The protection level, ServerStorage, cannot be used when saving to this destination. The system could not verify that the destination supports secure storage capability.|  
|0xC0014062|-1073659806|DTS_E_LOADFROMSQLSERVER|LoadFromSQLServer method has failed.|  
|0xC0014063|-1073659805|DTS_E_SIGNATUREPOLICYVIOLATION|The package cannot be loaded because the state of the digital signature violates signature policy. Error 0x%1!8.8X! "%2"|  
|0xC0014064|-1073659804|DTS_E_SIGNATURENOTPRESENT|The package is not signed.|  
|0xC0014065|-1073659803|DTS_E_SQLPROFILERDLL_ONLY_X86|The log provider for SQL Server Profiler was unable to load pfclnt.dll because it is only supported on 32-bit systems.|  
|0xC0014100|-1073659648|DTS_E_NAMEALREADYADDED|The object cannot be added because another object with the same name already exists in the collection. Use a different name to resolve this error.|  
|0xC0014101|-1073659647|DTS_E_NAMEALREADYEXISTS|The object name cannot be changed from "%1" to "%2" because another object in the collection already uses that name. Use a different name to resolve this error.|  
|0xC0014103|-1073659645|DTS_E_FAILEDDEPENDENCIES|There was an error enumerating the package dependencies. Check other messages for more information.|  
|0xC0014104|-1073659644|DTS_E_INVALIDCHECKPOINT_TRANSACTION|The current package settings are not supported.  Please change the SaveCheckpoints property or the TransactionOption property.|  
|0xC001410E|-1073659634|DTS_E_CONNECTIONMANAGERJOINTRANSACTION|The connection manager failed to defect from the transaction.|  
|0xC0015001|-1073655807|DTS_E_BPDUPLICATE|The specified breakpoint ID already exists. This error occurs when a task calls CreateBreakpoint with the same ID multiple times. It is possible to create a breakpoint with the same ID multiple times if the task calls RemoveBreakpoint on the first creation before creating the second one.|  
|0xC0015002|-1073655806|DTS_E_BPUNKNOWNID|The specified breakpoint ID does not exist. This error occurs when a task references a breakpoint that does not exist.|  
|0xC0015004|-1073655804|DTS_E_CANTWRITETOFILE|The file, "%1", could not be opened for writing. The file could be read-only, or you do not have the correct permissions.|  
|0xC0015005|-1073655803|DTS_E_NOROWSETRETURNED|No result rowset is associated with the execution of this query. The result is not correctly specified.|  
|0xC0015105|-1073655547|DTS_E_DUMP_FAILED|Debug dump files were not generated correctly. The hresult is 0x%1!8.8X!.|  
|0xC0016001|-1073651711|DTS_E_INVALIDURL|The URL specified is not valid. This can happen when the server or proxy URL is null, or in an incorrect format. A valid URL format is in the form of https://ServerName:Port/ResourcePath or https://ServerName:Port/ResourcePath.|  
|0xC0016002|-1073651710|DTS_E_INVALIDSCHEME|The URL %1 is not valid. This can happen when a scheme other than http or https is specified, or the URL is in an incorrect format. A valid URL format is in the form of https://ServerName:Port/ResourcePath or https://ServerName:Port/ResourcePath.|  
|0xC0016003|-1073651709|DTS_E_WINHTTPCANNOTCONNECT|Connection to server %1 cannot be established. This error can occur when the server does not exist, or the proxy settings are incorrect.|  
|0xC0016004|-1073651708|DTS_E_CONNECTIONTERMINATED|The connection with the server has been reset or terminated. Try again later.|  
|0xC0016005|-1073651707|DTS_E_LOGINFAILURE|The login attempt failed for "%1". This error occurs when the login credentials provided are incorrect. Verify the login credentials.|  
|0xC0016006|-1073651706|DTS_E_INVALIDSERVERNAME|The server name specified in the URL %1 cannot be resolved.|  
|0xC0016007|-1073651705|DTS_E_PROXYAUTH|Proxy authentication failed. This error occurs when login credentials are not provided, or the credentials are incorrect.|  
|0xC0016008|-1073651704|DTS_E_SECUREFAILURE|SSL certificate response obtained from the server was not valid. Cannot process the request.|  
|0xC0016009|-1073651703|DTS_E_TIMEOUT|The request has timed out. This error can occur when the timeout specified was too short, or a connection to the server or proxy cannot be established. Ensure that the server and proxy URL are correct.|  
|0xC001600A|-1073651702|DTS_E_CLIENTAUTH|Client certificate is missing. This error occurs when the server is expecting an SSL client certificate and the user has provided an invalid certificate, or has not provided a certificate. A client certificate must be configured for this connection.|  
|0xC001600B|-1073651701|DTS_E_REDIRECTFAILURE|The specified server, URL %1, has a redirect and the redirect request failed.|  
|0xC001600C|-1073651700|DTS_E_SERVERAUTH|Server authentication failed. This error occurs when login credentials are not provided, or the credentials are incorrect.|  
|0xC001600D|-1073651699|DTS_E_WINHTTPUNKNOWNERROR|Request cannot be processed. Try again later.|  
|0xC001600E|-1073651698|DTS_E_UNKNOWNSTATUSCODE|Server returned status code - %1!u! : %2. This error occurs when the server is experiencing problems.|  
|0xC001600F|-1073651697|DTS_E_WINHTTPNOTSUPPORTED|This platform is not supported by WinHttp services.|  
|0xC0016010|-1073651696|DTS_E_INVALIDTIMEOUT|Timeout value is not valid. Timeout should be in the range of %1!d! to %2!d! (in seconds).|  
|0xC0016011|-1073651695|DTS_E_INVALIDCHUNKSIZE|The chunk size is not valid. The ChunkSize property should be in the range of %1!d! to %2!d! (in KB).|  
|0xC0016012|-1073651694|DTS_E_CERTERROR|Error processing client certificate. This error can occur when the client certificate provided was not found in the Personal Certificate Store. Verify that the client certificate is valid.|  
|0xC0016013|-1073651693|DTS_E_FORBIDDEN|Server returned error code "403 - Forbidden". This error can occur when the specified resource needs "https" access, but the certificate validity period has expired, the certificate is not valid for the use requested, or the certificate has been revoked or revocation can not be checked.|  
|0xC0016014|-1073651692|DTS_E_WINHTTPOPEN|Error initializing HTTP session with proxy "%1". This error can occur when an invalid proxy was specified. HTTP connection manager only supports CERN-type proxies.|  
|0xC0016015|-1073651691|DTS_E_OPENCERTSTORE|Error opening certificate store.|  
|0xC0016016|-1073651690|DTS_E_UNPROTECTXMLFAILED|Failed to decrypt protected XML node "%1" with error 0x%2!8.8X! "%3". You may not be authorized to access this information. This error occurs when there is a cryptographic error. Verify that the correct key is available.|  
|0xC0016017|-1073651689|DTS_E_UNPROTECTCONNECTIONSTRINGFAILED|Failed to decrypt protected connection string for server "%1" with error 0x%2!8.8X! "%3". You may not be authorized to access this information. This error occurs when there is a cryptographic error. Verify that the correct key is available.|  
|0xC0016018|-1073651688|DTS_E_NEGATIVEVERSION|The version number cannot be negative. This error occurs when the VersionMajor, VersionMinor, or VersionBuild property of the package is set to a negative value.|  
|0xC0016019|-1073651687|DTS_E_PACKAGEMIGRATED|The package has been migrated to a later version during loading. It must be reloaded to complete the process. This is an internal error code.|  
|0xC0016020|-1073651680|DTS_E_PACKAGEMIGRATIONFAILED|Package migration from version %1!d! to version %2!d! failed with error 0x%3!8.8X! "%4".|  
|0xC0016021|-1073651679|DTS_E_PACKAGEMIGRATIONMODULELOAD|Package migration module has failed to load.|  
|0xC0016022|-1073651678|DTS_E_PACKAGEMIGRATIONMODULE|Package migration module has failed.|  
|0xC0016023|-1073651677|DTS_E_CANTDETERMINEWHICHPROPTOPERSIST|Unable to persist object using default persistence. This error occurs when the default persistence is unable to determine which objects are on the hosted object.|  
|0xC0016024|-1073651676|DTS_E_CANTADDREMOVEWHENEXECUTING|Cannot add or remove an element from a package in runtime mode. This error occurs when an attempt is made to add or remove an object from a collection while the package is executing.|  
|0xC0016025|-1073651675|DTS_E_NODENOTFOUND|The "%1" node cannot be found in custom default persistence. This error occurs if the default saved XML of an extensible object was changed in a way that a saved object is no longer found, or if the extensible object itself changed.|  
|0xC0016026|-1073651674|DTS_E_COLLECTIONLOCKED|This collection cannot be modified during package validation or execution.|  
|0xC0016027|-1073651673|DTS_E_COLLOCKED|The "%1" collection cannot be modified during package validation or execution. "%2" cannot be added to the collection.|  
|0xC0016029|-1073651671|DTS_E_FTPNOTCONNECTED|Connection with the FTP server has not been established.|  
|0xC001602A|-1073651670|DTS_E_FTPERROR|An error occurred in the requested FTP operation. Detailed error description: %1.|  
|0xC001602B|-1073651669|DTS_E_FTPINVALIDRETRIES|The number of retries is not valid. The number of retries should be between %1!d! and %2!d!.|  
|0xC001602C|-1073651668|DTS_E_LOADWININET|The FTP connection manager needs the following DLL to function: %1.|  
|0xC001602D|-1073651667|DTS_E_FTPINVALIDCONNECTIONSTRING|The port specified in the connection string is not valid. The ConnectionString format is ServerName:Port. Port should be an integer value between %1!d! and %2!d!.|  
|0xC001602E|-1073651666|DTS_E_FTPCREATEFOLDER|Creating folder "%1" ... %2.|  
|0xC001602F|-1073651665|DTS_E_FTPDELETEFOLDER|Deleting folder "%1" ... %2.|  
|0xC0016030|-1073651664|DTS_E_FTPCHANGEFOLDER|Changing current directory to "%1". %2.|  
|0xC0016031|-1073651663|DTS_E_FTPFILESEMPTY|No files to transfer. This error can occur when performing a Send or Receive operation and no files are specified for the transfer.|  
|0xC0016032|-1073651662|DTS_E_FTPINVALIDLOCALPATH|Specified local path is not valid. Specify a valid local path. This can occur when the specified local path is null.|  
|0xC0016033|-1073651661|DTS_E_FTPNOFILESTODELETE|No files specified to delete.|  
|0xC0016034|-1073651660|DTS_E_WINHTTPCERTDECODE|Internal error occurred while loading the certificate. This error could occur when the certificate data is invalid.|  
|0xC0016035|-1073651659|DTS_E_WINHTTPCERTENCODE|Internal error occurred while saving the certificate data.|  
|0xC0016049|-1073651639|DTS_E_CHECKPOINTMISMATCH|Checkpoint file "%1" does not match this package. The ID of the package and the ID in the checkpoint file do not match.|  
|0xC001604A|-1073651638|DTS_E_CHECKPOINTFILEALREADYEXISTS|An existing checkpoint file is found with contents that do not appear to be for this package, so the file cannot be overwritten to start saving new checkpoints. Remove the existing checkpoint file and try again. This error occurs when a checkpoint file exists, the package is set to not use a checkpoint file, but to save checkpoints. The existing checkpoint file will not be overwritten.|  
|0xC001604B|-1073651637|DTS_E_CHECKPOINTFILELOCKED|The checkpoint file "%1" is locked by another process. This may occur if another instance of this package is currently executing.|  
|0xC001604C|-1073651636|DTS_E_OPENCHECKPOINTFILE|Checkpoint file "%1" failed to open due to error 0x%2!8.8X! "%3".|  
|0xC001604D|-1073651635|DTS_E_CREATECHECKPOINTFILE|Checkpoint file "%1" failed during creation due to error 0x%2!8.8X! "%3".|  
|0xC0016050|-1073651632|DTS_E_FTPINVALIDPORT|The FTP Port contains an invalid value. The FTP Port value should be an integer between %1!d! and %2!d!.|  
|0xC00160AA|-1073651542|DTS_E_CONNECTTOSERVERFAILED|Connect to SSIS Service on machine "%1" failed:<br /><br /> %2.|  
|0xC0017002|-1073647614|DTS_E_PROPERTYEXPRESSIONSDISABLEDONVARIABLES|The Expression property is not supported on Variable objects. Use the EvaluateAsExpression property instead.|  
|0xC0017003|-1073647613|DTS_E_PROPERTYEXPRESSIONEVAL|The expression "%1" on property "%2" cannot be evaluated. Modify the expression to be valid.|  
|0xC0017004|-1073647612|DTS_E_PROPERTYEXPRESSIONSET|The result of the expression "%1" on property "%2" cannot be written to the property. The expression was evaluated, but cannot be set on the property.|  
|0xC0017005|-1073647611|DTS_E_FORLOOPEVALEXPRESSIONINVALID|The evaluation expression for the loop is not valid. The expression needs to be modified. There should be additional error messages.|  
|0xC0017006|-1073647610|DTS_E_EXPRESSIONNOTBOOLEAN|The expression "%1" must evaluate to True or False. Change the expression to evaluate to a Boolean value.|  
|0xC0017007|-1073647609|DTS_E_FORLOOPHASNOEXPRESSION|There is no expression for the loop to evaluate. This error occurs when the expression on the For Loop is empty. Add an expression.|  
|0xC0017008|-1073647608|DTS_E_FORLOOPASSIGNEXPRESSIONINVALID|The assignment expression for the loop is not valid and needs to be modified. There should be additional error messages.|  
|0xC0017009|-1073647607|DTS_E_FORLOOPINITEXPRESSIONINVALID|The initialization expression for the loop is not valid and needs to be modified. There should be additional error messages.|  
|0xC001700A|-1073647606|DTS_E_INVALIDVERSIONNUMBER|The version number in the package is not valid. The version number cannot be greater than current version number.|  
|0xC001700C|-1073647604|DTS_E_INVALIDVERNUMCANTBENEGATIVE|The version number in the package is not valid. The version number is negative.|  
|0xC001700D|-1073647603|DTS_E_PACKAGEUPDATEDISABLED|The package has an older format version, but automatic package format upgrading is disabled.|  
|0xC001700E|-1073647602|DTS_E_EXPREVALTRUNCATIONASERROR|A truncation occurred during evaluation of the expression.|  
|0xC0019001|-1073639423|DTS_E_FAILEDSETEXECVALVARIABLE|The wrapper was unable to set the value of the variable specified in the ExecutionValueVariable property.|  
|0xC0019004|-1073639420|DTS_E_VARIABLEEXPRESSIONERROR|The expression for variable "%1" failed evaluation. There was an error in the expression.|  
|0xC0019305|-1073638651|DTS_E_UNSUPPORTEDSQLVERSION|The attempted operation is not supported with this database version.|  
|0xC001A003|-1073635325|DTS_E_TXNSPECINVALID|Transaction cannot be specified when a retained connection is used. This error occurs when Retain is set to TRUE on the connection manager, but AcquireConnection was called with a non-null transaction parameter.|  
|0xC001A004|-1073635324|DTS_E_INCOMPATIBLETRANSACTIONCONTEXT|Incompatible transaction context was specified for a retained connection. This connection has been established under a different transaction context. Retained connections can be used under exactly one transaction context.|  
|0xC001B001|-1073631231|DTS_E_NOTSUSPENDED|Resume call failed because the package is not suspended. This occurs when the client calls resume, but the package is not suspended.|  
|0xC001B002|-1073631230|DTS_E_ALREADYEXECUTING|Execute call failed because the executable is already executing. This error occurs when the client calls Execute on a container that is still executing from the last Execute call.|  
|0xC001B003|-1073631229|DTS_E_NOTEXECUTING|Suspend or Resume call failed because the executable is not executing, or is not the top-level executable. This occurs when the client calls Suspend or Resume on an executable that is not currently processing an Execute call.|  
|0xC001C002|-1073627134|DTS_E_INVALIDFILE|The file specified in the For Each File enumerator is not valid. Check that the file specified in the For Each File enumerator exists.|  
|0xC001C010|-1073627120|DTS_E_VALUEINDEXNOTINTEGER|The value index is not an integer . Mapping a For Each Variable number %1!d! to the variable "%2".|  
|0xC001C011|-1073627119|DTS_E_VALUEINDEXNEGATIVE|The value index is negative. The ForEach Variable Mapping number %1!d! to variable "%2".|  
|0xC001C012|-1073627118|DTS_E_FOREACHVARIABLEMAPPING|ForEach Variable Mapping number %1!d! to variable "%2" cannot be applied.|  
|0xC001C013|-1073627117|DTS_E_OBJECTNOTINFOREACHLOOP|Failure when adding an object to a ForEachPropertyMapping that is not a direct child of the ForEachLoop container.|  
|0xC001F001|-1073614847|DTS_E_FAILEDSYSTEMVARIABLEREMOVE|Failed to remove a system variable. This error occurs when removing a variable that is a required variable.  Required variables are variables that are created by the runtime for communicating between tasks and the runtime.|  
|0xC001F002|-1073614846|DTS_E_CHANGESYSTEMVARIABLEREADONLYFAILED|Changing the property of a variable failed because it is a system variable. System variables are read-only.|  
|0xC001F003|-1073614845|DTS_E_CHANGESYSTEMVARIABLENAMEFAILED|Changing the name of a variable failed because it is a system variable. System variables are read-only.|  
|0xC001F004|-1073614844|DTS_E_CHANGESYSTEMVARIABLENAMESPACEFAILED|Changing the namespace of a variable failed because it is a system variable. System variables are read-only.|  
|0xC001F006|-1073614842|DTS_E_EVENTHANDLERNAMEREADONLY|Changing the event handler name failed. Event handler names are read-only.|  
|0xC001F008|-1073614840|DTS_E_PATHUNKNOWN|Cannot retrieve path to object. This is a system error.|  
|0xC001F009|-1073614839|DTS_E_RUNTIMEVARIABLETYPECHANGE|The type of the value being assigned to variable "%1" differs from the current variable type. Variables may not change type during execution. Variable types are strict, except for variables of type Object.|  
|0xC001F010|-1073614832|DTS_E_INVALIDSTRING|Invalid characters in string: "%1". This occurs when a string supplied for a property value contains unprintable characters.|  
|0xC001F011|-1073614831|DTS_E_INVALIDOBJECTNAME|SSIS object name is invalid. More specific errors would have been raised explaining the exact naming problem.|  
|0xC001F021|-1073614815|DTS_E_PROPERTYREADONLY|The property "%1" is read only. This occurs when a change to a read-only property is attempted.|  
|0xC001F022|-1073614814|DTS_E_FAILEDGETTYPEINFO|The object does not support type information. This occurs when the runtime attempts to get the type information from an object to populate the Properties collection.  The object must support type information.|  
|0xC001F023|-1073614813|DTS_E_FAILEDPROPERTYGET|An error occurred while retrieving the value of property "%1". The error code is 0x%2!8.8X!.|  
|0xC001F024|-1073614812|DTS_E_FAILEDPROPERTYGET_ERRORINFO|An error occurred while retrieving the value of property "%1". The error code is 0x%2!8.8X! "%3".|  
|0xC001F025|-1073614811|DTS_E_FAILEDPROPERTYSET|An error occurred while setting the value of property "%1". The error returned is 0x%2!8.8X!.|  
|0xC001F026|-1073614810|DTS_E_FAILEDPROPERTYSET_ERRORINFO|An error occurred while setting the value of property "%1". The error returned is 0x%2!8.8X! "%3".|  
|0xC001F027|-1073614809|DTS_E_PROPERTYWRITEONLY|The property "%1" is write-only. This error occurs when trying to retrieve the value of a property through a property object, but the property is write-only.|  
|0xC001F028|-1073614808|DTS_E_NODISPATCH|The object does not implement IDispatch. This error occurs when a property object or properties collection attempts to access an IDispatch interface on an object.|  
|0xC001F029|-1073614807|DTS_E_NOCONTAININGTYPELIB|Unable to retrieve the type library of the object. This error occurs when the Properties collection attempts to retrieve the type library for an object through its IDispatch interface.|  
|0xC001F02A|-1073614806|DTS_E_INVALIDTASKMONIKER|Cannot create a task from XML for task "%1!s!", type "%2!s!" due to error 0x%3!8.8X! "%4!s!".|  
|0xC001F02C|-1073614804|DTS_E_FAILEDCREATEXMLDOCUMENT|Failed to create an XML document "%1".|  
|0xC001F02D|-1073614803|DTS_E_PMVARPROPTYPESDIFFERENT|An error occurred because there is a property mapping from a variable to a property with a different type. The property type must match the variable type.|  
|0xC001F02E|-1073614802|DTS_E_PMINVALIDPROPMAPTARGET|Attempted to set property mapping to target unsupported object type. This error occurs when passing an unsupported object type to a property mapping.|  
|0xC001F02F|-1073614801|DTS_E_COULDNOTRESOLVEPACKAGEPATH|Cannot resolve a package path to an object in the package "%1".  Verify that the package path is valid.|  
|0xC001F030|-1073614800|DTS_E_PMNODESTPROPERTY|The destination property for the property map is empty. Set the destination property name.|  
|0xC001F031|-1073614799|DTS_E_INVALIDPROPERTYMAPPINGSFOUND|The package failed to restore at least one property mapping.|  
|0xC001F032|-1073614798|DTS_E_AMBIGUOUSVARIABLENAME|The variable name is ambiguous because multiple variables with this name exist in different namespaces. Specify namespace-qualified name to prevent ambiguity.|  
|0xC001F033|-1073614797|DTS_E_DESTINATIONOBJECTPARENTLESS|The destination object in a property mapping has no parent. The destination object is not a child of any sequence container. It may have been removed from the package.|  
|0xC001F036|-1073614794|DTS_E_INVALIDPROPERTYMAPPING|The property mapping is not valid. The mapping is ignored.|  
|0xC001F038|-1073614792|DTS_E_PMFAILALERTREMOVE|Failure when alerting property mappings that a target is being removed.|  
|0xC001F03A|-1073614790|DTS_E_INVALIDFOREACHPROPERTYMAPPING|An invalid property mapping is found on the For Each Loop. This occurs when the ForEach property mapping fails to restore.|  
|0xC001F040|-1073614784|DTS_E_PMPROPERTYINVALID|A destination property was specified on a property mapping that is invalid. This occurs when a property is specified on a destination object that in not found on that object.|  
|0xC001F041|-1073614783|DTS_E_INVALIDTASKMONIKERNOPARAM|Cannot create a task from XML. This occurs when the runtime is unable to resolve the name to create a task. Verify that the name is correct.|  
|0xC001F080|-1073614720|DTS_E_COULDNOTREPLACECHECKPOINTFILE|Cannot replace the existing checkpoint file with the updated checkpoint file. The checkpoint was successfully created in a temporary file, but overwriting the existing file with the new file failed.|  
|0xC001F081|-1073614719|DTS_E_CHECKPOINTFILENOTSPECIFIED|The package is configured to always restart from a checkpoint, but checkpoint file is not specified.|  
|0xC001F082|-1073614718|DTS_E_CHECKPOINTLOADXML|The attempt to load the XML checkpoint file "%1" failed with error 0x%2!8.8X! "%3". Check that the file name specified is correct, and that the file exists.|  
|0xC001F083|-1073614717|DTS_E_LOADCHECKPOINT|The package failed during execution because the checkpoint file cannot be loaded. Further execution of the package requires a checkpoint file. This error usually occurs when the CheckpointUsage property is set to ALWAYS, which specifies that the package always restarts.|  
|0xC001F185|-1073614459|DTS_E_NOEVALEXPRESSION|The evaluation condition expression on the For Loop "%1" is empty. There must be a Boolean evaluation expression in the For Loop.|  
|0xC001F186|-1073614458|DTS_E_EXPREVALASSIGNMENTTYPEMISMATCH|The result of the assignment expression "%1" cannot be converted to a type that is compatible with the variable that it was assigned to.|  
|0xC001F187|-1073614457|DTS_E_EXPREVALASSIGNMENTTOREADONLYVARIABLE|Error using a read-only variable "%1" in an assignment expression. The expression result cannot be assigned to the variable because the variable is read only. Choose a variable that can be written to, or remove the expression from this variable.|  
|0xC001F188|-1073614456|DTS_E_EXPREVALASSIGNMENTVARIABLELOCKFORWRITEFAILED|Cannot evaluate expression "%1" because the variable "%2" does not exist or cannot be accessed for writing. The expression result cannot be assigned to the variable because the variable was not found, or could not be locked for write access.|  
|0xC001F189|-1073614455|DTS_E_EXPREVALRESULTTYPENOTSUPPORTED|The expression "%1" has a result type of "%2", which cannot be converted to a supported type.|  
|0xC001F18A|-1073614454|DTS_E_EXPREVALRESULTTYPECONVERSIONFAILED|The conversion of the result of the expression"%1" from type "%2" to a supported type failed with error code 0x%3!8.8X!. An unexpected error occurred when trying to convert the expression result to a type supported by the runtime engine, even though the type conversion is supported.|  
|0xC001F200|-1073614336|DTS_E_DTSNAME_NOTNULL|The object name is not valid. The name cannot be set to NULL.|  
|0xC001F201|-1073614335|DTS_E_DTSNAME_NOTEMPTY|The object name is not valid. The name cannot be empty.|  
|0xC001F202|-1073614334|DTS_E_DTSNAME_LEGAL|The object name "%1" is not valid. The name cannot contain any of the following characters: / \ : [ ] . =|  
|0xC001F203|-1073614333|DTS_E_DTSNAME_PRINTABLE|Object name "%1" is not valid. The name cannot contain control characters that render it unprintable.|  
|0xC001F204|-1073614332|DTS_E_DTSNAME_NOLEADWHITESP|Object name "%1" is not valid. Name cannot begin with a whitespace.|  
|0xC001F205|-1073614331|DTS_E_DTSNAME_NOTRAILWHITESP|Object name "%1" is not valid. Name cannot end with a whitespace.|  
|0xC001F206|-1073614330|DTS_E_DTSNAME_BEGINSWITHALPHA|Object name "%1" is not valid. Name must begin with an alphabetical character.|  
|0xC001F207|-1073614329|DTS_E_DTSNAME_BEGINSWITHALPHAUNDERBAR|Object name "%1" is not valid. Name must begin with an alphabetical character or underscore "_".|  
|0xC001F208|-1073614328|DTS_E_DTSNAME_ALPHADIGITUNDERBAR|Object name "%1" is not valid. Name must contain only alphanumeric characters or underscores "_".|  
|0xC001F209|-1073614327|DTS_E_DTSNAME_VALIDFILENAME|Object name "%1" is not valid. The name cannot contain any of the following characters: / \ : ? " < > &#124;|  
|0xC001F420|-1073613792|DTS_E_FAILLOADINGPROPERTY|Failed to load the value property "%1" using default persistence.|  
|0xC001F422|-1073613790|DTS_E_NODELISTENUM_INVALIDCONNMGRTYPE|Connection manager "%1" is not of type "%2"|  
|0xC001F423|-1073613789|DTS_E_NODELISTENUM_XPATHISEMPTY|"%1" is empty|  
|0xC001F424|-1073613788|DTS_E_NODELISTENUM_INVALIDDATANODE|Invalid data node in the nodelist enumerator section|  
|0xC001F425|-1073613787|DTS_E_NODELISTENUM_NOENUMERATORCREATED|No enumerator can be created|  
|0xC001F427|-1073613785|DTS_E_OPERATIONFAILCACHEINUSE|The operation failed because the cache is in use.|  
|0xC001F428|-1073613784|DTS_E_PROPERTYCANNOTBEMODIFIED|The property cannot be modified.|  
|0xC001F429|-1073613783|DTS_E_PACKAGEUPGRADEFAILED|The package upgrade has failed.|  
|0xC00220DE|-1073602338|DTS_E_TKEXECPACKAGE_UNABLETOLOADFILE|Error 0x%1!8.8X! while loading package file "%3". %2.|  
|0xC00220DF|-1073602337|DTS_E_TKEXECPACKAGE_UNSPECIFIEDPACKAGE|The package is not specified.|  
|0xC00220E0|-1073602336|DTS_E_TKEXECPACKAGE_UNSPECIFIEDCONNECTION|The connection is not specified.|  
|0xC00220E2|-1073602334|DTS_E_TKEXECPACKAGE_INCORRECTCONNECTIONMANAGERTYPE|The connection manager "%1" has an unsupported type "%2". Only "FILE" and "OLEDB" connection managers are supported.|  
|0xC00220E3|-1073602333|DTS_E_TKEXECPACKAGE_UNABLETOLOADXML|Error 0x%1!8.8X! while loading package file "%3" into an XML document. %2.|  
|0xC00220E4|-1073602332|DTS_E_TKEXECPACKAGE_UNABLETOLOAD|Error 0x%1!8.8X! while preparing to load the package. %2.|  
|0xC0024102|-1073594110|DTS_E_TASKVALIDATIONFAILED|The Validate method on the task failed, and returned error code 0x%1!8.8X! (%2). The Validate method must succeed and indicate the result using an "out" parameter.|  
|0xC0024104|-1073594108|DTS_E_TASKEXECUTEFAILED|The Execute method on the task returned error code 0x%1!8.8X! (%2). The Execute method must succeed, and indicate the result using an "out" parameter.|  
|0xC0024105|-1073594107|DTS_E_RETRIEVINGDEPENDENCIES|A failure occurred on task "%1": 0x%2!8.8X! while retrieving dependencies. The runtime was retrieving dependencies from the task's dependencies collection when the error occurred. The task may have incorrectly implemented one of the dependency interfaces.|  
|0xC0024107|-1073594105|DTS_E_TASKVALIDATIONERROR|There were errors during task validation.|  
|0xC0024108|-1073594104|DTS_E_CONNECTIONSTRINGFORMAT|The connection string format is not valid. It must consist of one or more components of the form X=Y, separated by semicolons. This error occurs when a connection string with zero components is set on database connection manager.|  
|0xC0024109|-1073594103|DTS_E_UNQUOTEDSEMICOLON|The connection string components cannot contain unquoted semicolons. If the value must contain a semicolon, enclose the entire value in quotes. This error occurs when values in the connection string contain unquoted semicolons, such as the InitialCatalog property.|  
|0xC002410A|-1073594102|DTS_E_LOGPROVIDERVALIDATIONFAILED|Validation of one or more log providers failed. The package cannot execute. The package does not execute when a log provider fails validation.|  
|0xC002410B|-1073594101|DTS_E_INVALIDVALUEINARRAY|Invalid value in array.|  
|0xC002410C|-1073594100|DTS_E_ENUMERATIONELEMENTNOTENUMERABLE|An element of the enumerator returned by the ForEach Enumerator does not implement IEnumerator, contradicting the CollectionEnumerator property of the ForEach Enumerator.|  
|0xC002410D|-1073594099|DTS_E_INVALIDENUMERATORINDEX|The enumerator failed to retrieve element at index "%1!d!".|  
|0xC0029100|-1073573632|DTS_E_AXTASK_MISSING_ENTRY_METHOD_NAME|Function not found.|  
|0xC0029101|-1073573631|DTS_E_AXTASK_EMPTY_SCRIPT|Function not found.|  
|0xC0029102|-1073573630|DTS_E_AXTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|ActiveX Script Task was initiated with a wrong XML element.|  
|0xC0029105|-1073573627|DTS_E_AXTASK_HANDLER_NOT_FOUND|Handler not found.|  
|0xC0029106|-1073573626|DTS_E_AXTASKUTIL_ENUMERATE_LANGUAGES_FAILED|An error occurred while attempting to retrieve the scripting languages installed on the system.|  
|0xC0029107|-1073573625|DTS_E_AXTASKUTIL_SCRIPTHOST_CREATE_FAILED|An error occurred while creating the ActiveX script host. Verify that you have the script host installed properly.|  
|0xC0029108|-1073573624|DTS_E_AXTASKUTIL_SCRIPTHOSTINIT_FAILED|An error occurred while trying to instantiate the script host for the chosen language. Verify that the script language you have chosen is installed on your system.|  
|0xC0029109|-1073573623|DTS_E_AXTASKUTIL_ADDVARIABLES_FAILED|An error occurred while adding the SSIS variables to the script host namespace. This might prevent the task from using SSIS variables in the script.|  
|0xC002910A|-1073573622|DTS_E_AXTASKUTIL_SCRIPT_PARSING_FAILED|A fatal error occurred while trying to parse the script text. Verify that the script engine for the chosen language is installed properly.|  
|0xC002910B|-1073573621|DTS_E_AXTASKUTIL_MSG_BAD_FUNCTION|The function name entered is not valid. Verify that a valid function name has been specified.|  
|0xC002910C|-1073573620|DTS_E_AXTASKUTIL_EXECUTION_FAILED|An error occurred while executing the script. Verify that the script engine for the selected language is installed properly.|  
|0xC002910D|-1073573619|DTS_E_AXTASKUTIL_ADDTYPELIB_FAILED|An error occurred while adding the managed type library to the script host. Verify that the DTS 2000 runtime is installed.|  
|0xC002910E|-1073573618|DTS_E_BITASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Bulk Insert Task was initiated with a wrong XML element.|  
|0xC002910F|-1073573617|DTS_E_BITASK_DATA_FILE_NOT_SPECIFIED|Data file name not specified.|  
|0xC0029110|-1073573616|DTS_E_BITASK_HANDLER_NOT_FOUND|Handler not found.|  
|0xC0029111|-1073573615|DTS_E_BITASK_CANNOT_ACQUIRE_CONNECTION|Failed to acquire the specified connection: "%1".|  
|0xC0029112|-1073573614|DTS_E_BITASK_NO_CONNECTION_MANAGER_SPECIFIED|Attempt to obtain the Connection Manager failed.|  
|0xC0029113|-1073573613|DTS_E_BITASK_INVALID_CONNECTION|The connection is not valid.|  
|0xC0029114|-1073573612|DTS_E_BITASK_NULL_CONNECTION|The connection is null.|  
|0xC0029115|-1073573611|DTS_E_BITASK_EXECUTE_FAILED|Execution failed.|  
|0xC0029116|-1073573610|DTS_E_BITASK_CANNOT_RETRIEVE_TABLES|An error occurred while retrieving the tables from the database.|  
|0xC0029117|-1073573609|DTS_E_BITASK_CANNOT_RETRIEVE_COLUMN_INFO|An error occurred while retrieving the columns of the table.|  
|0xC0029118|-1073573608|DTS_E_BITASK_ERROR_IN_DB_OPERATION|An error occurred in the database operation.|  
|0xC0029119|-1073573607|DTS_E_BITASK_INVALIDSOURCECONNECTIONNAME|The specified connection "%1" is either not valid, or points to an invalid object. To continue, specify a valid connection.|  
|0xC002911A|-1073573606|DTS_E_BITASK_INVALIDDESTCONNECTIONNAME|The destination connection specified is not valid. Supply a valid connection to continue.|  
|0xC002911B|-1073573605|DTS_E_BITASK_DESTINATION_TABLE_NOT_SPECIFIED|You must specify a table name to continue.|  
|0xC002911C|-1073573604|DTS_E_BITASK_ERROR_IN_LOAD_FROM_XML|Error occurred in LoadFromXML at the tag "%1".|  
|0xC002911D|-1073573603|DTS_E_BITASK_ERROR_IN_SAVE_TO_XML|Error occurred in SaveToXML at the tag "%1".|  
|0xC002911E|-1073573602|DTS_E_BITASKUNMANCONNECTION_INVALID_CONNECTION|The connection is not valid.|  
|0xC002911F|-1073573601|DTS_E_BITASKUNMANCONNECTION_EXECUTE_FAILED|Execution failed.|  
|0xC0029120|-1073573600|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_TABLES|Error occurred while retrieving the tables from the database.|  
|0xC0029121|-1073573599|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_COLUMN_INFO|Error occurred while retrieving the columns of the table.|  
|0xC0029122|-1073573598|DTS_E_BITASKUNMANCONNECTION_CANNOT_OPEN_FILE|Error occurred while trying to open the data file.|  
|0xC0029123|-1073573597|DTS_E_BITASKUNMANCONNECTION_OEM_CONVERSION_FAILED|Cannot convert the input OEM file to the specified format.|  
|0xC0029124|-1073573596|DTS_E_BITASKUNMANCONNECTION_ERROR_IN_DB_OPERATION|Error in database operation.|  
|0xC0029125|-1073573595|DTS_E_DTSPROCTASK_NOCONNECTIONSPECIFIED|No connection manager specified.|  
|0xC0029126|-1073573594|DTS_E_DTSPROCTASK_CONNECTIONMANAGERNOTOLAP|Connection "%1" is not an Analysis Services connection.|  
|0xC0029127|-1073573593|DTS_E_DTSPROCTASK_UNABLETOLOCATECONNECTIONMANAGER|Unable to locate connection "%1".|  
|0xC0029128|-1073573592|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEEXE|Analysis Services Execute DDL task received an invalid task data node.|  
|0xC0029129|-1073573591|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEPROC|Analysis Services Processing task received an invalid task data node.|  
|0xC002912A|-1073573590|DTS_E_DTSPROCTASK_INVALIDDDL|The DDL is not valid.|  
|0xC002912B|-1073573589|DTS_E_DTSPROCTASK_INVALIDDDLPROCESSINGCOMMANDS|The DDL found in ProcessingCommands is not valid.|  
|0xC002912C|-1073573588|DTS_E_DTSPROCTASK_CANNOTWRITEINAREADONLYVARIABLE|The Execution result cannot be saved in a read-only variable.|  
|0xC002912D|-1073573587|DTS_E_DTSPROCTASK_INVALIDVARIABLE|Variable "%1" it's not defined.|  
|0xC002912E|-1073573586|DTS_E_DTSPROCTASK_CONNECTIONNOTFOUND|Connection Manager "%1" it's not defined.|  
|0xC002912F|-1073573585|DTS_E_DTSPROCTASK_INVALIDCONNECTION|Connection Manager "%1" it's not a FILE Connection Manager.|  
|0xC0029130|-1073573584|DTS_E_DTSPROCTASK_NONEXISTENTATTRIBUTE|"%1" was not found during deserialization.|  
|0xC0029131|-1073573583|DTS_E_DTSPROCTASK_TRACEHASBEENSTOPPED|The trace has been stopped due to an exception.|  
|0xC0029132|-1073573582|DTS_E_DTSPROCTASK_DDLEXECUTIONFAILED|Execution of DDL failed.|  
|0xC0029133|-1073573581|DTS_E_DTSPROCTASK_FILEDOESNOTEXIST|There is no file associated with connection "%1".|  
|0xC0029134|-1073573580|DTS_E_DTSPROCTASK_VARIABLENOTDEFINED|Variable "%1" is not defined.|  
|0xC0029135|-1073573579|DTS_E_DTSPROCTASK_FILECONNECTIONNOTDEFINED|File connection "%1" is not defined.|  
|0xC0029136|-1073573578|DTS_E_EXEC2000PKGTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Execute DTS 2000 Package task is initiated with a wrong XML element.|  
|0xC0029137|-1073573577|DTS_E_EXEC2000PKGTASK_HANDLER_NOT_FOUND|Handler not found.|  
|0xC0029138|-1073573576|DTS_E_EXEC2000PKGTASK_PACKAGE_NAME_NOT_SPECIFIED|Package name is not specified.|  
|0xC0029139|-1073573575|DTS_E_EXEC2000PKGTASK_PACKAGE_ID_NOT_SPECIFIED|Package ID is not specified.|  
|0xC002913A|-1073573574|DTS_E_EXEC2000PKGTASK_PACKAGE_VERSIONGUID_NOT_SPECIFIED|Package version GUID is not specified.|  
|0xC002913B|-1073573573|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_SPECIFIED|SQL Server is not specified.|  
|0xC002913C|-1073573572|DTS_E_EXEC2000PKGTASK_SQL_USERNAME_NOT_SPECIFIED|SQL Server user name not specified.|  
|0xC002913D|-1073573571|DTS_E_EXEC2000PKGTASK_FILE_NAME_NOT_SPECIFIED|Storage file name not specified.|  
|0xC002913E|-1073573570|DTS_E_EXEC2000PKGTASK_DTS2000CANTBEEMPTY|The DTS 2000 package property is empty.|  
|0xC002913F|-1073573569|DTS_E_EXEC2000PKGTASK_ERROR_IN_PACKAGE_EXECUTE|An error occurred while executing the DTS 2000 package.|  
|0xC0029140|-1073573568|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_AVAILABLE_NETWORK|Cannot load the available SQL Servers from the network. Check the network connection.|  
|0xC0029141|-1073573567|DTS_E_EXEC2000PKGTASK_DATATYPE_NULL|The data type cannot be null. Please specify the correct data type to use for validating the value.|  
|0xC0029142|-1073573566|DTS_E_EXEC2000PKGTASK_NULL_VALUE|Cannot validate a null against any data type.|  
|0xC0029143|-1073573565|DTS_E_EXEC2000PKGTASK_NULL_VALUE_ARGUMENT|A required argument is null.|  
|0xC0029144|-1073573564|DTS_E_EXEC2000PKGTASK_CLS_NOT_REGISTRED_EXCEPTION|To execute the DTS 2000 Package task, start SQL Server Setup and use the Advanced button from the Components to Install page to select Legacy Components.|  
|0xC0029145|-1073573563|DTS_E_EXEC2000PKGTASK_NOT_PRIMITIVE_TYPE|"%1" is not a value type.|  
|0xC0029146|-1073573562|DTS_E_EXEC2000PKGTASK_CONVERT_FAILED|Could not convert "%1" to "%2".|  
|0xC0029147|-1073573561|DTS_E_EXEC2000PKGTASK_ERROR_IN_VALIDATE|Could not validate "%1" against "%2".|  
|0xC0029148|-1073573560|DTS_E_EXEC2000PKGTASK_ERROR_IN_LOAD_FROM_XML|Error occurred in LoadFromXML at the tag "%1".|  
|0xC0029149|-1073573559|DTS_E_EXEC2000PKGTASK_ERROR_IN_SAVE_TO_XML|Error occurred in SaveToXML at the tag "%1".|  
|0xC002914A|-1073573558|DTS_E_EXECPROCTASK_INVALIDTIMEOUT|The time-out value provided is not valid. Specify the number of seconds that the task allows the process to run. The minimum time-out is 0, which indicates that no time-out value is used and the process runs to completion or until an error occurs. The maximum time-out is 2147483 (((2^31) - 1)/1000).|  
|0xC002914B|-1073573557|DTS_E_EXECPROCTASK_CANTREDIRECTIO|Cannot redirect streams if the process can continue executing beyond the lifetime of the task.|  
|0xC002914C|-1073573556|DTS_E_EXECPROCTASK_PROCESSHASTIMEDOUT|The process timed out.|  
|0xC002914D|-1073573555|DTS_E_EXECPROCTASK_EXECUTABLENOTSPECIFIED|The executable is not specified.|  
|0xC002914E|-1073573554|DTS_E_EXECPROCTASK_STDOUTVARREADONLY|The standard out variable is read-only.|  
|0xC002914F|-1073573553|DTS_E_EXECPROCTASK_STDERRVARREADONLY|The standard error variable is read-only.|  
|0xC0029150|-1073573552|DTS_E_EXECPROCTASK_RECEIVEDINVALIDTASKDATANODE|The Execute Process task received a task data node that is not valid.|  
|0xC0029151|-1073573551|DTS_E_EXECPROCTASK_PROCESSEXITCODEEXCEEDS|In Executing "%2" "%3" at "%1", The process exit code was "%4" while the expected was "%5".|  
|0xC0029152|-1073573550|DTS_E_EXECPROCTASK_WORKINGDIRDOESNOTEXIST|The directory "%1" does not exist.|  
|0xC0029153|-1073573549|DTS_E_EXECPROCTASK_FILEDOESNOTEXIST|File/Process "%1" does not exist in directory "%2".|  
|0xC0029154|-1073573548|DTS_E_EXECPROCTASK_FILENOTINPATH|File/Process "%1" is not in path.|  
|0xC0029156|-1073573546|DTS_E_EXECPROCTASK_WORKINGDIRECTORYDOESNOTEXIST|Working Directory "%1" does not exist.|  
|0xC0029157|-1073573545|DTS_E_EXECPROCTASK_ERROREXECUTIONVALUE|The process exited with return code "%1". However, "%2" was expected.|  
|0xC0029158|-1073573544|DTS_E_FSTASK_SYNCFAILED|Synchronization object failed.|  
|0xC0029159|-1073573543|DTS_E_FSTASK_INVALIDDATA|The File System task received an invalid task data node.|  
|0xC002915A|-1073573542|DTS_E_FSTASK_DIRECTORYEXISTS|The Directory already exists.|  
|0xC002915B|-1073573541|DTS_E_FSTASK_PATHNOTVALID|"%1" is not valid on operation type "%2".|  
|0xC002915C|-1073573540|DTS_E_FSTASK_DESTINATIONNOTSET|Destination property of operation "%1" not set.|  
|0xC002915D|-1073573539|DTS_E_FSTASK_SOURCENOTSET|Source property of operation "%1" not set.|  
|0xC002915E|-1073573538|DTS_E_FSTASK_CONNECTIONTYPENOTFILE|Type of Connection "%1" is not a file.|  
|0xC002915F|-1073573537|DTS_E_FSTASK_VARIABLEDOESNTEXIST|Variable "%1" does not exist.|  
|0xC0029160|-1073573536|DTS_E_FSTASK_VARIABLENOTASTRING|Variable "%1" is not a string.|  
|0xC0029163|-1073573533|DTS_E_FSTASK_FILEDOESNOTEXIST|File or directory "%1" represented by connection "%2" does not exist.|  
|0xC0029165|-1073573531|DTS_E_FSTASK_DESTCONNUSAGETYPEINVALID|The destination file connection manager "%1" has an invalid usage type: "%2".|  
|0xC0029166|-1073573530|DTS_E_FSTASK_SRCCONNUSAGETYPEINVALID|The source file connection manager "%1" has an invalid usage type "%2".|  
|0xC0029167|-1073573529|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATION|FileSystemOperation|  
|0xC0029168|-1073573528|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATIONDESC|Provides information regarding File System operations.|  
|0xC0029169|-1073573527|DTS_E_FSTASK_TASKDISPLAYNAME|File System Task|  
|0xC002916A|-1073573526|DTS_E_FSTASK_TASKDESCRIPTION|Perform file system operations, such as copying and deleting files.|  
|0xC002916B|-1073573525|DTS_E_FTPTASK_SYNCOBJFAILED|Synchronization object failed.|  
|0xC002916C|-1073573524|DTS_E_FTPTASK_UNABLETOOBTAINFILELIST|Unable to obtain the file list.|  
|0xC002916D|-1073573523|DTS_E_FTPTASK_LOCALPATHEMPTY|The local path is empty.|  
|0xC002916E|-1073573522|DTS_E_FTPTASK_REMOTEPATHEMPTY|The remote path is empty.|  
|0xC002916F|-1073573521|DTS_E_FTPTASK_LOCALVARIBALEEMPTY|The local variable is empty.|  
|0xC0029170|-1073573520|DTS_E_FTPTASK_REMOTEVARIBALEEMPTY|The remote variable is empty.|  
|0xC0029171|-1073573519|DTS_E_FTPTASK_FTPRCVDINVLDDATANODE|The FTP task received an invalid task data node.|  
|0xC0029172|-1073573518|DTS_E_FTPTASK_CONNECTION_NAME_NULL|The connection is empty. Verify that a valid FTP connection is provided.|  
|0xC0029173|-1073573517|DTS_E_FTPTASK_CONNECTION_NOT_FTP|The connection specified is not an FTP connection. Verify that a valid FTP connection is provided.|  
|0xC0029175|-1073573515|DTS_E_FTPTASK__INITIALIZATION_WITH_NULL_XML_ELEMENT|Cannot initialize the task with a null XML element.|  
|0xC0029176|-1073573514|DTS_E_FTPTASK_SAVE_TO_NULL_XML_ELEMENT|Cannot save the task to a null XML document.|  
|0xC0029177|-1073573513|DTS_E_FTPTASK_ERROR_IN_LOAD_FROM_XML|Error occurred in LoadFromXML at the tag "%1".|  
|0xC0029178|-1073573512|DTS_E_FTPTASK_NOFILESATLOCATION|There are no files at "%1".|  
|0xC0029179|-1073573511|DTS_E_FTPTASK_LOCALVARIABLEISEMPTY|The variable "%1" is empty.|  
|0xC002917A|-1073573510|DTS_E_FTPTASK_REMOTEVARIABLEISEMPTY|The variable "%1" is empty.|  
|0xC002917B|-1073573509|DTS_E_FTPTASK_NOFILESINCONNMGR|The File "%1" doesn't contain file path(s).|  
|0xC002917C|-1073573508|DTS_E_FTPTASK_NOFILEPATHSINLOCALVAR|The variable "%1" doesn't contain file path(s).|  
|0xC002917D|-1073573507|DTS_E_FTPTASK_VARIABLENOTASTRING|Variable "%1" is not a string.|  
|0xC002917E|-1073573506|DTS_E_FTPTASK_VARIABLENOTFOUND|Variable "%1" does not exist.|  
|0xC002917F|-1073573505|DTS_E_FTPTASK_INVALIDPATHONOPERATION|Invalid path on operation "%1".|  
|0xC0029180|-1073573504|DTS_E_FTPTASK_DIRECTORYEXISTS|"%1" already exists.|  
|0xC0029182|-1073573502|DTS_E_FTPTASK_CONNECTIONTYPENOTFILE|Type of Connection "%1" is Not a file.|  
|0xC0029183|-1073573501|DTS_E_FTPTASK_FILEDOESNOTEXIST|File represented by "%1" does not exist.|  
|0xC0029184|-1073573500|DTS_E_FTPTASK_INVALIDDIRECTORY|Directory is not specified in the variable "%1".|  
|0xC0029185|-1073573499|DTS_E_FTPTASK_NOFILESFOUND|No files found in "%1".|  
|0xC0029186|-1073573498|DTS_E_FTPTASK_NODIRECTORYPATHINCONMGR|Directory is not specified in the file connection manager "%1".|  
|0xC0029187|-1073573497|DTS_E_FTPTASK_UNABLETODELETELOCALEFILE|Unable to delete local file "%1".|  
|0xC0029188|-1073573496|DTS_E_FTPTASK_UNABLETOREMOVELOCALDIRECTORY|Unable to remove local directory "%1".|  
|0xC0029189|-1073573495|DTS_E_FTPTASK_UNABLETOCREATELOCALDIRECTORY|Unable to create local directory "%1".|  
|0xC002918A|-1073573494|DTS_E_FTPTASK_UNABLETORECEIVEFILES|Unable to receive files using "%1".|  
|0xC002918B|-1073573493|DTS_E_FTPTASK_UNABLETOSENDFILES|Unable to send files using "%1".|  
|0xC002918C|-1073573492|DTS_E_FTPTASK_UNABLETOMAKEDIRREMOTE|Unable to create remote directory using "%1".|  
|0xC002918D|-1073573491|DTS_E_FTPTASK_UNABLETOREMOVEDIRREMOTE|Unable to remove remote directory using "%1".|  
|0xC002918E|-1073573490|DTS_E_FTPTASK_UNABLETODELETEREMOTEFILES|Unable to delete remote files using "%1".|  
|0xC002918F|-1073573489|DTS_E_FTPTASK_UNABLETOCONNECTTOSERVER|Unable to connect to FTP server using "%1".|  
|0xC0029190|-1073573488|DTS_E_FTPTASK_INVALIDVARIABLEVALUE|Variable "%1" doesn't start with "/".|  
|0xC0029191|-1073573487|DTS_E_FTPTASK_INVALIDREMOTEPATH|Remote path "%1" doesn't start with "/".|  
|0xC0029192|-1073573486|DTS_E_DTS_E_FTPTASK_CANNOT_ACQUIRE_CONNECTION|There was an error acquiring the FTP connection. Please check if you have specified a valid connection type "%1".|  
|0xC0029193|-1073573485|DTS_E_MSGQTASKUTIL_CERT_OPEN_STORE_FAILED|Opening the certificate store failed.|  
|0xC0029194|-1073573484|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_DISPLAY_NAME|An error occurred while retrieving the display name of the certificate.|  
|0xC0029195|-1073573483|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_ISSUER_NAME|An error occurred while retrieving the issuer name of the certificate.|  
|0xC0029196|-1073573482|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_FRIENDLY_NAME|An error occurred while retrieving the friendly name of the certificate.|  
|0xC0029197|-1073573481|DTS_E_MSMQTASK_NO_CONNECTION|The MSMQ connection name is not set.|  
|0xC0029198|-1073573480|DTS_E_MSMQTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Task was initialized with the wrong XML element.|  
|0xC0029199|-1073573479|DTS_E_MSMQTASK_DATA_FILE_NAME_EMPTY|Data file name is empty.|  
|0xC002919A|-1073573478|DTS_E_MSMQTASK_DATA_FILE_SAVE_NAME_EMPTY|The name specified for the data file to save is empty.|  
|0xC002919B|-1073573477|DTS_E_MSMQTASK_DATA_FILE_SIZE_ERROR|File size should be less than 4 MB.|  
|0xC002919C|-1073573476|DTS_E_MSMQTASK_DATA_FILE_SAVE_FAILED|Saving the data file failed.|  
|0xC002919D|-1073573475|DTS_E_MSMQTASK_STRING_COMPARE_VALUE_MISSING|String filter value is empty.|  
|0xC002919E|-1073573474|DTS_E_MSMQTASK_INVALID_QUEUE_PATH|Queue path is not valid.|  
|0xC002919F|-1073573473|DTS_E_MSMQTASK_NOT_TRANSACTIONAL|The message queue task does not support enlisting in distributed transactions.|  
|0xC00291A0|-1073573472|DTS_E_MSMQTASK_INVALID_MESSAGE_TYPE|The message type is not valid.|  
|0xC00291A1|-1073573471|DTS_E_MSMQTASK_TASK_TIMEOUT|The message queue timed out. No message has been received.|  
|0xC00291A2|-1073573470|DTS_E_MSMQTASK_INVALID_PROPERTY_VALUE|The property specified is not valid. Verify that the argument type is correct.|  
|0xC00291A3|-1073573469|DTS_E_MSMQTASK_MESSAGE_NON_AUTHENTICATED|Message is not authenticated.|  
|0xC00291A4|-1073573468|DTS_E_MSMQTASK_INVALID_ENCRYPTION_ALGO_WRAPPER|You are trying to set the value of Encryption Algorithm with an invalid object.|  
|0xC00291A5|-1073573467|DTS_E_MSMQTASK_VARIABLE_TO_RECEIVE_STRING_MSG_EMPTY|The variable to receive string message is empty.|  
|0xC00291A6|-1073573466|DTS_E_MSMQTASK_RECEIVE_VARIABLE_EMPTY|Variable to receive variable message is empty.|  
|0xC00291A7|-1073573465|DTS_E_MSMQTASK_CONNECTIONTYPENOTMSMQ|Connection "%1" is not of type MSMQ.|  
|0xC00291A8|-1073573464|DTS_E_MSMQTASK_DATAFILE_ALREADY_EXISTS|The data file "%1" already exists at the specified location. Cannot overwrite the file as the Overwrite option is set to false.|  
|0xC00291A9|-1073573463|DTS_E_MSMQTASK_STRING_MSG_TO_VARIABLE_NOT_FOUND|The specified variable "%1" to receive string message is not found in the package variable collection.|  
|0xC00291AA|-1073573462|DTS_E_MSMQTASK_CONNMNGRNULL|The connection manager "%1" is empty.|  
|0xC00291AB|-1073573461|DTS_E_MSMQTASK_CONNMNGRDOESNOTEXIST|The connection manager "%1" does not exist.|  
|0xC00291AC|-1073573460|DTS_E_SCRIPTTASK_COMPILEERRORMSG|Error "%1": "%2"\r\nLine "%3"   Column "%4" through "%5".|  
|0xC00291AD|-1073573459|DTS_E_SCRIPTTASK_COMPILEERRORMSG2|There was an error compiling the script: "%1".|  
|0xC00291AE|-1073573458|DTS_E_SCRIPTTASK_COMPILEERRORMSG3|Error "%1": "%2"\r\nLine "%3" Columns "%4"-"%5"\r\nLine Text: "%6".|  
|0xC00291AF|-1073573457|DTS_E_SCRIPTTASK_SCRIPTREPORTEDFAILURE|User script returned a failure result.|  
|0xC00291B0|-1073573456|DTS_E_SCRIPTTASK_SCRIPTFILESFAILEDTOLOAD|User script files failed to load.|  
|0xC00291B1|-1073573455|DTS_E_SCRIPTTASK_SCRIPTTHREWEXCEPTION|User script threw an exception: "%1".|  
|0xC00291B2|-1073573454|DTS_E_SCRIPTTASK_COULDNOTCREATEENTRYPOINTCLASS|Could not create an instance of entrypoint class "%1".|  
|0xC00291B3|-1073573453|DTS_E_SCRIPTTASK_LOADFROMXMLEXCEPTION|There was an exception while loading Script Task from XML: "%1".|  
|0xC00291B4|-1073573452|DTS_E_SCRIPTTASK_SOURCEITEMNOTFOUNDEXCEPTION|Source item "%1" was not found in the package.|  
|0xC00291B5|-1073573451|DTS_E_SCRIPTTASK_BINARYITEMNOTFOUNDEXCEPTION|Binary item "%1" was not found in the package.|  
|0xC00291B6|-1073573450|DTS_E_SCRIPTTASK_UNRECOGNIZEDSCRIPTLANGUAGEEXCEPTION|"%1" was not recognized as a valid script language.|  
|0xC00291B7|-1073573449|DTS_E_SCRIPTTASK_ILLEGALSCRIPTNAME|The script name is not valid. It cannot contain spaces, slashes, special characters, or begin with a number.|  
|0xC00291B8|-1073573448|DTS_E_SCRIPTTASK_INVALIDSCRIPTLANGUAGE|The script language specified is not valid.|  
|0xC00291B9|-1073573447|DTS_E_SCRIPTTASK_CANTINITNULLTASK|Cannot initialize to a null task.|  
|0xC00291BA|-1073573446|DTS_E_SCRIPTTASK_MUSTINITWITHRIGHTTASK|The Script Task user interface must initialize to an Script Task.|  
|0xC00291BB|-1073573445|DTS_E_SCRIPTTASK_WASNOTINITED|The Script Task user interface is not initialized.|  
|0xC00291BC|-1073573444|DTS_E_SCRIPTTASK_HOST_NAME_CANT_EMPTY|Name cannot be empty.|  
|0xC00291BD|-1073573443|DTS_E_SCRIPTTASK_INVALID_SCRIPT_NAME|The project name is not valid. It cannot contain spaces, slashes, special characters, or begin with a number.|  
|0xC00291BE|-1073573442|DTS_E_SCRIPTTASK_INVALID_SCRIPT_LANGUAGE|The script language specified is not valid.|  
|0xC00291BF|-1073573441|DTS_E_SCRIPTTASK_INVALID_ENTRY_POINT|Entry point not found.|  
|0xC00291C0|-1073573440|DTS_E_SCRIPTTASK_LANGUAGE_EMPTY|The script language is not specified. Verify that a valid script language is specified.|  
|0xC00291C1|-1073573439|DTS_E_SCRIPTTASK_INITIALIZATION_WITH_NULL_TASK|User interface initialization: The task is null.|  
|0xC00291C2|-1073573438|DTS_E_SCRIPTTASK_UI_INITIALIZATION_WITH_WRONG_TASK|The Script Task user interface is initialized with an incorrect task.|  
|0xC00291C3|-1073573437|DTS_E_SENDMAILTASK_RECIPIENT_EMPTY|No recipient is specified.|  
|0xC00291C4|-1073573436|DTS_E_SENDMAILTASK_SMTP_SERVER_NOT_SPECIFIED|The Simple Mail Transfer Protocol (SMTP) server is not specified. Provide a valid name or IP address of the SMTP server.|  
|0xC00291C5|-1073573435|DTS_E_SENDMAILTASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Send Mail task is initiated with an incorrect XML element.|  
|0xC00291CB|-1073573429|DTS_E_SENDMAILTASK_INVALIDATTACHMENT|Either the file "%1" does not exist or you do not have permissions to access the file.|  
|0xC00291CD|-1073573427|DTS_E_SENDMAILTASK_CHECK_VALID_SMTP_SERVER|Verify that the Simple Mail Transfer Protocol (SMTP) server specified is valid.|  
|0xC00291CE|-1073573426|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTFILE|Connection "%1" is not of type File.|  
|0xC00291CF|-1073573425|DTS_E_SENDMAILTASK_FILEDOESNOTEXIST|On operation "%1", file "%2" does not exist.|  
|0xC00291D0|-1073573424|DTS_E_SENDMAILTASK_VARIABLETYPEISNOTSTRING|Variable "%1" is not of type string.|  
|0xC00291D1|-1073573423|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTSMTP|Connection "%1" is not of type SMTP.|  
|0xC00291D2|-1073573422|DTS_E_SENDMAILTASK_CONNMNGRNULL|Connection "%1" is empty.|  
|0xC00291D3|-1073573421|DTS_E_SENDMAILTASK_NOCONNMNGR|The specified connection "%1" does not exist.|  
|0xC00291D4|-1073573420|DTS_E_SQLTASK_NOSTATEMENTSPECIFIED|No Transact-SQL statement specified.|  
|0xC00291D5|-1073573419|DTS_E_SQLTASK_NOXMLSUPPORT|The connection does not support XML result sets.|  
|0xC00291D6|-1073573418|DTS_E_SQLTASK_NOHANDLERFORCONNECTION|Cannot locate a handler for the specified connection type.|  
|0xC00291D7|-1073573417|DTS_E_SQLTASK_NOCONNECTIONMANAGER|No connection manager is specified.|  
|0xC00291D8|-1073573416|DTS_E_SQLTASK_CANNOTACQUIRECONNMANAGER|Cannot acquire a connection from the connection manager.|  
|0xC00291D9|-1073573415|DTS_E_SQLTASK_NULLPARAMETERNAME|Cannot have a null parameter name.|  
|0xC00291DA|-1073573414|DTS_E_SQLTASK_INVALIDPARAMETERNAME|The parameter name is not valid.|  
|0xC00291DB|-1073573413|DTS_E_SQLTASK_VALIDPARAMETERTYPES|Valid parameter names are of type Int or String.|  
|0xC00291DC|-1073573412|DTS_E_SQLTASK_READONLYVARIABLE|Variable "%1" cannot be used in a result binding because it is read-only.|  
|0xC00291DD|-1073573411|DTS_E_SQLTASK_INDESNOTINCOLLECTION|The index is not assigned in this collection.|  
|0xC00291DE|-1073573410|DTS_E_SQLTASK_ROVARINOUTPARAMETER|The variable "%1" cannot be used as an "out" parameter or return value in a parameter binding because it is read-only.|  
|0xC00291DF|-1073573409|DTS_E_SQLTASK_OBJECTNOTINCOLLECTION|The object does not exist in this collection.|  
|0xC00291E0|-1073573408|DTS_E_SQLTASK_UNABLETOACQUIREMANAGEDCONN|Cannot acquire a managed connection.|  
|0xC00291E1|-1073573407|DTS_E_UNABLETOPOPRESULT|Cannot populate the result columns for a single row result type. The query returned an empty result set.|  
|0xC00291E2|-1073573406|DTS_E_SQLTASK_INVALIDNUMOFRESULTBINDINGS|There is an invalid number of result bindings returned for the ResultSetType: "%1".|  
|0xC00291E3|-1073573405|DTS_E_SQLTASK_RESULTBINDTYPEFORROWSETXML|The result binding name must be set to zero for full result set and XML results.|  
|0xC00291E4|-1073573404|DTS_E_SQLTASK_INVALIDEPARAMDIRECTIONFALG|The parameter directions flag is not valid.|  
|0xC00291E5|-1073573403|DTS_E_SQLTASK_NOSQLTASKDATAINXMLFRAGMENT|The XML fragment does not contain SQL Task data.|  
|0xC00291E6|-1073573402|DTS_E_SQLTASK_MULTIPLERETURNVALUEPARAM|A parameter with type return value is not the first parameter, or there are more than one parameter of type return value.|  
|0xC00291E7|-1073573401|DTS_E_SQLTASK_CONNECTIONTYPENOTFILE|Connection "%1" is not a file connection manager.|  
|0xC00291E8|-1073573400|DTS_E_SQLTASK_FILEDOESNOTEXIST|File represented by "%1" does not exist.|  
|0xC00291E9|-1073573399|DTS_E_SQLTASK_VARIABLETYPEISNOTSTRING|Type of variable "%1" is not string.|  
|0xC00291EA|-1073573398|DTS_E_SQLTASK_VARIABLENOTFOUND|Variable "%1" does not exist or could not be locked.|  
|0xC00291EB|-1073573397|DTS_E_SQLTASK_CANNOTLOCATECONNMANAGER|Connection manager "%1" does not exist.|  
|0xC00291EC|-1073573396|DTS_E_SQLTASK_FAILEDTOACQUIRECONNECTION|Failed to acquire connection "%1". Connection may not be configured correctly or you may not have the right permissions on this connection.|  
|0xC00291ED|-1073573395|DTS_E_SQLTASK_RESULTBYNAMENOTSUPPORTED|Result binding by name "%1" is not supported for this connection type.|  
|0xC00291EE|-1073573394|DTS_E_SQLTASKCONN_ERR_NO_ROWS|A result set type of single row is specified, but no rows were returned.|  
|0xC00291EF|-1073573393|DTS_E_SQLTASKCONN_ERR_NO_DISCONNECTED_RS|No disconnected record set is available for the Transact-SQL statement.|  
|0xC00291F0|-1073573392|DTS_E_SQLTASKCONN_ERR_UNSUPPORTED_TYPE|Unsupported type.|  
|0xC00291F1|-1073573391|DTS_E_SQLTASKCONN_ERR_UNKNOWN_TYPE|Unknown type.|  
|0xC00291F2|-1073573390|DTS_E_SQLTASKCONN_ERR_PARAM_DATA_TYPE|Unsupported data type on parameter binding \\"%s\\".|  
|0xC00291F3|-1073573389|DTS_E_SQLTASKCONN_ERR_PARAM_NAME_MIX|Parameter names cannot be an mix of ordinal and named types.|  
|0xC00291F4|-1073573388|DTS_E_SQLTASKCONN_ERR_PARAM_DIR|The parameter direction on parameter binding \\"%s\\" is not valid.|  
|0xC00291F5|-1073573387|DTS_E_SQLTASKCONN_ERR_RESULT_DATA_TYPE|The data type on result set binding \\"%s\\" is not supported.|  
|0xC00291F6|-1073573386|DTS_E_SQLTASKCONN_ERR_RESULT_COL_INDEX|The result column index %d is not valid.|  
|0xC00291F7|-1073573385|DTS_E_SQLTASKCONN_ERR_UNKNOWN_RESULT_COL|Cannot find column \\"%s\\" in the result set.|  
|0xC00291F9|-1073573383|DTS_E_SQLTASKCONN_ERR_NOROWSET|No result rowset is associated with the execution of this query.|  
|0xC00291FA|-1073573382|DTS_E_SQLTASKCONN_ERR_ODBC_DISCONNECTED|Disconnected recordsets are not available from ODBC connections.|  
|0xC00291FB|-1073573381|DTS_E_SQLTASKCONN_ERR_RESULT_SET_DATA_TYPE|The data type in the result set, column %hd, is not supported.|  
|0xC00291FC|-1073573380|DTS_E_SQLTASKCONN_ERR_CANT_LOAD_XML|Cannot load XML with query result.|  
|0xC00291FD|-1073573379|DTS_E_TTGENTASK_NOCONNORVARIABLE|A connection name or variable name for the package must be specified.|  
|0xC00291FE|-1073573378|DTS_E_TTGENTASK_FAILEDCREATE|Failed to create the package.|  
|0xC00291FF|-1073573377|DTS_E_TTGENTASK_BADTABLEMETADATA|The TableMetaDataNode is not an XMLNode.|  
|0xC0029200|-1073573376|DTS_E_TTGENTASK_FAILEDCREATEPIPELINE|Failed to create the pipeline.|  
|0xC0029201|-1073573375|DTS_E_TTGENTASK_BADVARIABLETYPE|The variable is not the correct type.|  
|0xC0029202|-1073573374|DTS_E_TTGENTASK_NOTFILECONNECTION|The connection manager specified is not a FILE connection manager.|  
|0xC0029203|-1073573373|DTS_E_TTGENTASK_BADFILENAME|Invalid file name specified on the connection manager "%1".|  
|0xC0029204|-1073573372|DTS_E_WEBSERVICETASK_CONNECTION_NAME_NULL|The connection is empty. Verify that a valid HTTP connection is specified.|  
|0xC0029205|-1073573371|DTS_E_WEBSERVICETASK_CONNECTION_NOT_FOUND|The connection does not exist. Verify that a valid, existing HTTP connection is specified.|  
|0xC0029206|-1073573370|DTS_E_WEBSERVICETASK_CONNECTION_NOT_HTTP|The connection specified is not a HTTP connection. Verify that a valid HTTP connection is specified.|  
|0xC0029207|-1073573369|DTS_E_WEBSERVICETASK_SERVICE_NULL|The Web Service name is empty. Verify that a valid web service name is specified.|  
|0xC0029208|-1073573368|DTS_E_WEBSERVICETASK_METHODNAME_NULL|The web method name is empty. Verify that a valid web method is specified.|  
|0xC0029209|-1073573367|DTS_E_WEBSERVICETASK_WEBMETHODINFO_NULL|The web method is empty or may not exist. Verify that there is an existing web method to specify.|  
|0xC002920A|-1073573366|DTS_E_WEBSERVICETASK_OUTPUTLOC_NULL|The output location is empty. Verify that an existing file connection or variable is specified.|  
|0xC002920B|-1073573365|DTS_E_WEBSERVICETASK_VARIABLE_NOT_FOUND|The variable cannot be found. Verify that the variable exists in the package.|  
|0xC002920C|-1073573364|DTS_E_WEBSERVICETASK_VARIABLE_READONLY|Cannot save the result. Verify that the variable is not read-only.|  
|0xC002920D|-1073573363|DTS_E_WEBSERVICETASK_ERROR_IN_LOAD_FROM_XML|Error occurred in LoadFromXML at the tag "%1".|  
|0xC002920E|-1073573362|DTS_E_WEBSERVICETASK_ERROR_IN_SAVE_TO_XML|Error occurred in SaveToXML at the tag "%1".|  
|0xC002920F|-1073573361|DTS_E_WEBSERVICETASK_TASK_SAVE_TO_NULL_XML_ELEMENT|Cannot save the task to a null XML document.|  
|0xC0029210|-1073573360|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_NULL_XML_ELEMENT|Cannot initialize the task with a null XML element.|  
|0xC0029211|-1073573359|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|The Web Service Task is initiated with an incorrect XML element.|  
|0xC0029212|-1073573358|DTS_E_WEBSERVICETASK_UNEXPECTED_XML_ELEMENT|Unexpected XML element found.|  
|0xC0029213|-1073573357|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_CONNECTION|There was an error acquiring the HTTP connection. Verify that a valid connection type is specified.|  
|0xC0029214|-1073573356|DTS_E_WEBSERVICETASK_FILE_CONN_NOT_FOUND|Cannot save the result. Verify that there is an existing file connection.|  
|0xC0029215|-1073573355|DTS_E_WEBSERVICETASK_FILE_NOT_FOUND|Cannot save the result. Verify that the file exists.|  
|0xC0029216|-1073573354|DTS_E_WEBSERVICETASK_FILE_NULL|Cannot save the result. The file name is empty or the file is in use by another process.|  
|0xC0029217|-1073573353|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_FILE_CONNECTION|There was an error in acquiring the file connection. Verify that a valid file connection is specified.|  
|0xC0029218|-1073573352|DTS_E_WEBSERVICETASK_DATATYPE_NOT_SUPPORTED|Only Complex Types with Primitive values, Primitive Arrays, and Enumerations are supported.|  
|0xC0029219|-1073573351|DTS_E_WEBSERVICETASK_PARAMTYPE_NOT_SUPPORTED|Only Primitive, Enum, Complex, PrimitiveArray, and ComplexArray types are supported.|  
|0xC002921A|-1073573350|DTS_E_WEBSERVICETASK_WSDL_VERSION_NOT_SUPPORTED|This version of WSDL is not supported.|  
|0xC002921B|-1073573349|DTS_E_WEBSERVICETASK_WRONG_XML_ELEMENT|Initialized with an incorrect XML element.|  
|0xC002921C|-1073573348|DTS_E_WEBSERVICETASK_XML_ATTRIBUTE_NOT_FOUND|A mandatory attribute is not found.|  
|0xC002921D|-1073573347|DTS_E_WEBSERVICETASK_ENUM_NO_VALUES|The enum "%1" does not have any values. The WSDL is corrupted.|  
|0xC002921E|-1073573346|DTS_E_WEBSERVICETASK_CONNECTIONNOTFOUND|The connection cannot be found.|  
|0xC002921F|-1073573345|DTS_E_WEBSERVICETASK_CONNECTION_ALREADY_EXISTS|Connection by this name already exists.|  
|0xC0029220|-1073573344|DTS_E_WEBSERVICETASK_NULL_CONNECTION|Connection cannot be null or empty.|  
|0xC0029221|-1073573343|DTS_E_WEBSERVICETASK_NOT_HTTP_CONNECTION|The connection specified is not a HTTP connection. Verify that a valid HTTP connection is specified.|  
|0xC0029222|-1073573342|DTS_E_WEBSERVICETASK_WSDL_NOT_FOUND|The specified Uniform Resource Identifier (URI) does not contain a valid WSDL.|  
|0xC0029223|-1073573341|DTS_E_WEBSERVICETASK_ERROR_IN_DOWNLOAD|Could not read the WSDL file. The input WSDL file is not valid. The reader threw the following error: "%1".|  
|0xC0029224|-1073573340|DTS_E_WEBSERVICETASK_SERVICE_DESC_NULL|Service Description cannot be null.|  
|0xC0029225|-1073573339|DTS_E_WEBSERVICETASK_SERVICENULL|Service name cannot be null.|  
|0xC0029226|-1073573338|DTS_E_WEBSERVICETASK_WSDL_NULL|URL cannot be null.|  
|0xC0029227|-1073573337|DTS_E_WEBSERVICETASK_SERVICE_NOT_FOUND|The service is not currently available.|  
|0xC0029228|-1073573336|DTS_E_WEBSERVICETASK_SOAPPORT_NOT_FOUND|The service is not available on the SOAP port.|  
|0xC0029229|-1073573335|DTS_E_WEBSERVICETASK_SOAPBINDING_NOT_FOUND|Failed to parse the Web Services Description Language (WSDL). Cannot find the Binding that corresponds to the SOAP port.|  
|0xC002922A|-1073573334|DTS_E_WEBSERVICETASK_SOAPPORTTYPE_NOT_FOUND|Failed to parse the Web Services Description Language (WSDL). Cannot find a PortType that corresponds to the SOAP port.|  
|0xC002922B|-1073573333|DTS_E_WEBSERVICETASK_MSG_NOT_FOUND|Cannot find the message that corresponds to the method specified.|  
|0xC002922C|-1073573332|DTS_E_WEBSERVICETASK_CANNOT_GEN_PROXY|Could not generate the proxy for the given web service. The following errors were encountered while generating the proxy "%1".|  
|0xC002922D|-1073573331|DTS_E_WEBSERVICETASK_CANNOT_LOAD_PROXY|Could not load the proxy for the given web service. The exact error is as follows: "%1".|  
|0xC002922E|-1073573330|DTS_E_WEBSERVICETASK_INVALID_SERVICE|Could not find the specified service. The exact error is as follows: "%1".|  
|0xC002922F|-1073573329|DTS_E_WEBSERVICETASK_WEBMETHOD_INVOKE_FAILED|The Web Service threw the following error during method execution: "%1".|  
|0xC0029230|-1073573328|DTS_E_WEBSERVICETASK_INVOKE_ERR|Could not execute the web method. The exact error is as follows: "%1".|  
|0xC0029231|-1073573327|DTS_E_WEBSERVICETASK_METHODINFO_NULL|MethodInfo cannot be null.|  
|0xC0029232|-1073573326|DTS_E_WEBSERVICETASK_VALUE_NOT_PRIMITIVE|The specified WebMethodInfo is not correct. The ParamValue supplied does not match the ParamType. The DTSParamValue is not of type PrimitiveValue.|  
|0xC0029233|-1073573325|DTS_E_WEBSERVICETASK_VALUE_NOT_ENUM|The WebMethodInfo specified is not correct. The ParamValue supplied does not match the ParamType. The DTSParamValue found is not of type EnumValue.|  
|0xC0029234|-1073573324|DTS_E_VALUE_WEBSERVICETASK_NOT_COMPLEX|The WebMethodInfo specified is not correct. The ParamValue supplied does not match the ParamType. The DTSParamValue found is not of type ComplexValue.|  
|0xC0029235|-1073573323|DTS_E_WEBSERVICETASK_VALUE_NOT_ARRAY|The WebMethodInfo specified is not correct. The ParamValue supplied does not match the ParamType. The DTSParamValue found is not of type ArrayValue.|  
|0xC0029236|-1073573322|DTS_E_WEBSERVICETASK_TYPE_NOT_PRIMITIVE|The WebMethodInfo you have specified is wrong. "%1" is not Primitive Type.|  
|0xC0029237|-1073573321|DTS_E_WEBSERVICETASK_ARRAY_VALUE_INVALID|The format of the ArrayValue is not valid. There should be at least one element in the array.|  
|0xC0029238|-1073573320|DTS_E_WEBSERVICETASK_SELECTED_VALUE_NULL|The value of the enumeration cannot be null. Select a default value for the enumeration.|  
|0xC0029239|-1073573319|DTS_E_WEBSERVICETASK_NULL_VALUE|Cannot validate a null against any datatype.|  
|0xC002923A|-1073573318|DTS_E_WEBSERVICETASK_ENUM_VALUE_NOT_FOUND|The enumeration Value is not correct.|  
|0xC002923B|-1073573317|DTS_E_WEBSERVICETASK_PROP_NOT_EXISTS|The class specified does not contain a public property by the name "%1".|  
|0xC002923C|-1073573316|DTS_E_WEBSERVICETASK_CONVERT_FAILED|Could not convert "%1" to "%2".|  
|0xC002923D|-1073573315|DTS_E_WEBSERVICETASK_CLEANUP_FAILED|Cleanup failed. The proxy that was created for the web service may not have been deleted.|  
|0xC002923E|-1073573314|DTS_E_WEBSERVICETASK_CREATE_INSTANCE_FAILED|Could not create an object of type "%1". Please check whether the default constructor exists.|  
|0xC002923F|-1073573313|DTS_E_WEBSERVICETASK_NOT_PRIMITIVE_TYPE|"%1" is not a value type.|  
|0xC0029240|-1073573312|DTS_E_WEBSERVICETASK_ERROR_IN_VALIDATE|Could not validate "%1" against "%1".|  
|0xC0029241|-1073573311|DTS_E_WEBSERVICETASK_DATATYPE_NULL|The data type cannot be null. Specify the value of the data type to validate.|  
|0xC0029242|-1073573310|DTS_E_WEBSERVICETASK_INDEX_OUT_OF_BOUNDS|The ParamValue cannot be inserted at this position. The index specified might be lesser than zero or greater than the length.|  
|0xC0029243|-1073573309|DTS_E_WEBSERVICETASK_WRONG_WSDL|The input WSDL file is not valid.|  
|0xC0029244|-1073573308|DTS_E_WMIDRTASK_SYNCOBJECTFAILED|Synchronization object failed.|  
|0xC0029245|-1073573307|DTS_E_WMIDRTASK_MISSINGWQLQUERY|The WQL query is missing.|  
|0xC0029246|-1073573306|DTS_E_WMIDRTASK_DESTINATIONMUSTBESET|The destination must be set.|  
|0xC0029247|-1073573305|DTS_E_WMIDRTASK_MISSINGCONNECTION|No WMI connection is set.|  
|0xC0029248|-1073573304|DTS_E_WMIDRTASK_INVALIDDATANODE|WMI Data Reader Task received an invalid task data node.|  
|0xC0029249|-1073573303|DTS_E_WMIDRTASK_FAILEDVALIDATION|The task failed validation.|  
|0xC002924A|-1073573302|DTS_E_WMIDRTASK_FILEDOESNOTEXIST|File "%1" does not exist.|  
|0xC002924B|-1073573301|DTS_E_WMIDRTASK_CONNECTIONMNGRDOESNTEXIST|Connection manager "%1" does not exist.|  
|0xC002924C|-1073573300|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRINGOROBJECT|Variable "%1" is not of type string or object.|  
|0xC002924D|-1073573299|DTS_E_WMIDRTASK_CONNECTIONTYPENOTFILE|Connection "%1" is not of type "FILE".|  
|0xC002924E|-1073573298|DTS_E_WMIDRTASK_CONNECTIONTYPENOTWMI|Connection "%1" is not of type "WMI".|  
|0xC002924F|-1073573297|DTS_E_WMIDRTASK_FILEALREADYEXISTS|File "%1" already exists.|  
|0xC0029250|-1073573296|DTS_E_WMIDRTASK_CONNECTIONMANAGEREMPTY|Connection manager "%1" is empty.|  
|0xC0029251|-1073573295|DTS_E_WMIDRTASK_VARNOTOBJECT|Variable "%1" should be of type object to be assigned a data table.|  
|0xC0029252|-1073573294|DTS_E_WMIDRTASK_TASKFAILURE|Task failed due to invalid WMI query: "%1".|  
|0xC0029253|-1073573293|DTS_E_WMIDRTASK_CANTWRITETOVAR|Unable to write to variable "%1" since it set to keep its original value.|  
|0xC0029254|-1073573292|DTS_E_WMIEWTASK_SYNCOBJECTFAILED|Synchronization object failed.|  
|0xC0029255|-1073573291|DTS_E_WMIEWTASK_MISSINGWQLQUERY|The WQL query is missing.|  
|0xC0029256|-1073573290|DTS_E_WMIEWTASK_MISSINGCONNECTION|The WMI connection is missing.|  
|0xC0029257|-1073573289|DTS_E_WMIEWTASK_QUERYFAILURE|The task failed to execute the WMI query.|  
|0xC0029258|-1073573288|DTS_E_WMIEWTASK_INVALIDDATANODE|The WMI Event Watcher Task received a task data node that is not valid.|  
|0xC0029259|-1073573287|DTS_E_WMIEWTASK_CONNECTIONMNGRDOESNTEXIST|Connection manager "%1" does not exist.|  
|0xC002925A|-1073573286|DTS_E_WMIEWTASK_FILEDOESNOTEXIST|File "%1" does not exist.|  
|0xC002925B|-1073573285|DTS_E_WMIEWTASK_VARIABLETYPEISNOTSTRING|Variable "%1" is not of type string.|  
|0xC002925C|-1073573284|DTS_E_WMIEWTASK_CONNECTIONTYPENOTFILE|Connection "%1" is not of type "FILE".|  
|0xC002925D|-1073573283|DTS_E_WMIEWTASK_CONNECTIONTYPENOTWMI|Connection "%1" is not of type "WMI".|  
|0xC002925E|-1073573282|DTS_E_WMIEWTASK_FILEALREADYEXISTS|File "%1" already exists.|  
|0xC002925F|-1073573281|DTS_E_WMIEWTASK_CONNECTIONMANAGEREMPTY|Connection manager "%1" is empty.|  
|0xC0029260|-1073573280|DTS_E_WMIEWTASK_TIMEOUTOCCURRED|Timeout of "%1" second(s) occurred before event represented by "%2".|  
|0xC0029261|-1073573279|DTS_E_WMIEWTASK_ERRMESSAGE|Watching for the Wql query caused the following system exception: "%1". Check the query for errors or WMI connection for access rights/permissions.|  
|0xC0029262|-1073573278|DTS_E_XMLTASK_NODEFAULTOPERTION|The Operations specified is not defined.|  
|0xC0029263|-1073573277|DTS_E_XMLTASK_CONNECTIONTYPENOTFILE|The connection type is not File.|  
|0xC0029264|-1073573276|DTS_E_XMLTASK_CANTGETREADERFROMSOURCE|Cannot get an XmlReader from the source XML document.|  
|0xC0029265|-1073573275|DTS_E_XMLTASK_CANTGETREADERFROMDEST|Cannot get an XmlReader from the changed XML document.|  
|0xC0029266|-1073573274|DTS_E_XMLTASK_CANTGETREADERFROMDIFFGRAM|Cannot get the XDL diffgram reader from the XDL diffgram XML.|  
|0xC0029268|-1073573272|DTS_E_XMLTASK_EMPTYNODELIST|The node list is empty.|  
|0xC0029269|-1073573271|DTS_E_XMLTASK_NOELEMENTFOUND|The element was not found.|  
|0xC002926A|-1073573270|DTS_E_XMLTASK_UNDEFINEDOPERATION|The Operations specified is not defined.|  
|0xC002926B|-1073573269|DTS_E_XMLTASK_XPATHNAVERROR|Unexpected content item in XPathNavigator.|  
|0xC002926C|-1073573268|DTS_E_XMLTASK_NOSCHEMAFOUND|No schema found to enforce validation.|  
|0xC002926D|-1073573267|DTS_E_XMLTASK_VALIDATIONERROR|A validation error occurred when validating the instance document.|  
|0xC002926E|-1073573266|DTS_E_XMLTASK_SYNCOBJECTFAILED|Synchronization object failed.|  
|0xC002926F|-1073573265|DTS_E_XMLTASK_ROOTNOODESNOTMATCHED|The root nodes do not match.|  
|0xC0029270|-1073573264|DTS_E_XMLTASK_INVALIDEDITSCRIPT|The Edit Script Operation type in the final Edit Script is not valid.|  
|0xC0029271|-1073573263|DTS_E_XMLTASK_CDATANODESISSUE|CDATA nodes should be added with DiffgramAddSubtrees class.|  
|0xC0029272|-1073573262|DTS_E_XMLTASK_COMMENTSNODEISSUE|Comment nodes should be added with DiffgramAddSubtrees class.|  
|0xC0029273|-1073573261|DTS_E_XMLTASK_TEXTNODEISSUES|Text nodes should be added with DiffgramAddSubtrees class.|  
|0xC0029274|-1073573260|DTS_E_XMLTASK_WHITESPACEISSUE|Significant white space nodes should be added with DiffgramAddSubtrees class.|  
|0xC0029275|-1073573259|DTS_E_XMLTASK_DIFFENUMISSUE|Correct the OperationCost array so that it reflects the XmlDiffOperation enumeration.|  
|0xC0029276|-1073573258|DTS_E_XMLTASK_TASKISEMPTY|There are no operations in the task.|  
|0xC0029277|-1073573257|DTS_E_XMLTASK_DOCUMENTHASDATA|The document already contains data and should not be used again.|  
|0xC0029278|-1073573256|DTS_E_XMLTASK_INVALIDENODETYPE|The node type is not valid.|  
|0xC0029279|-1073573255|DTS_E_XMLTASK_INVALIDDATANODE|The XML Task received a task data node that is not valid.|  
|0xC002927B|-1073573253|DTS_E_XMLTASK_VARIABLETYPEISNOTSTRING|Variable data type is not a String.|  
|0xC002927C|-1073573252|DTS_E_XMLTASK_COULDNOTGETENCODINGFROMDOCUMENT|Cannot get encoding from XML.|  
|0xC002927D|-1073573251|DTS_E_XMLTASK_MISSINGSOURCE|Source is not specified.|  
|0xC002927E|-1073573250|DTS_E_XMLTASK_MISSINGSECONDOPERAND|Second operand is not specified.|  
|0xC002927F|-1073573249|DTS_E_XMLTASK_INVALIDPATHDESCRIPTOR|Invalid XDL diffgram. "%1" is an invalid path descriptor.|  
|0xC0029280|-1073573248|DTS_E_XMLTASK_NOMATCHINGNODE|Invalid XDL diffgram. No node matches the path descriptor "%1".|  
|0xC0029281|-1073573247|DTS_E_XMLTASK_EXPECTINGDIFFGRAMELEMENT|Invalid XDL diffgram. Expecting xd:xmldiff as a root element with namespace URI "%1".|  
|0xC0029282|-1073573246|DTS_E_XMLTASK_MISSINGSRCDOCATTRIBUTE|The XDL diffgram is not valid. The srcDocHash attribute on the xd:xmldiff element is missing.|  
|0xC0029283|-1073573245|DTS_E_XMLTASK_MISSINGOPTIONSATTRIBUTE|The XDL diffgram is not valid. The options attribute on the xd:xmldiff element is missing.|  
|0xC0029284|-1073573244|DTS_E_XMLTASK_INVALIDSRCDOCATTRIBUTE|The XDL diffgram is not valid. The srcDocHash attribute has an invalid value.|  
|0xC0029285|-1073573243|DTS_E_XMLTASK_INVALIDOPTIONSATTRIBUTE|The XDL diffgram is not valid. The options attribute has an invalid value.|  
|0xC0029286|-1073573242|DTS_E_XMLTASK_SRCDOCMISMATCH|The XDL diffgram is not applicable to this XML document. The rcDocHash value does not match.|  
|0xC0029287|-1073573241|DTS_E_XMLTASK_MORETHANONENODEMATCHED|Invalid XDL diffgram; more than one node matches the "%1" path descriptor on the xd:node or xd:change element.|  
|0xC0029288|-1073573240|DTS_E_XMLTASK_XMLDECLMISMATCH|The XDL diffgram is not applicable to this XML document. A new XML declaration cannot be added.|  
|0xC0029289|-1073573239|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODEINLIST|Internal Error. XmlDiffPathSingleNodeList can contain only one node.|  
|0xC002928A|-1073573238|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODELEFT|Internal Error. "%1" nodes left after patch, expecting 1.|  
|0xC002928B|-1073573237|DTS_E_XMLTASK_XSLTRESULTFILEISNOTXML|The File/Text Produced by the XSLT is not a valid XmlDocument, thus can not be set as result of operation: "%1".|  
|0xC002928E|-1073573234|DTS_E_XMLTASK_FILEDOESNOTEXIST|There is no file associated with connection "%1".|  
|0xC002928F|-1073573233|DTS_E_XMLTASK_XMLTEXTEMPTY|Property "%1" has no source Xml text; Xml Text is either invalid, null or empty string.|  
|0xC0029290|-1073573232|DTS_E_XMLTASK_FILEALREADYEXISTS|File "%1" already exists.|  
|0xC0029293|-1073573229|DTS_E_TRANSFERTASKS_SRCCONNECTIONREQUIRED|A source connection must be specified.|  
|0xC0029294|-1073573228|DTS_E_TRANSFERTASKS_DESTCONNECTIONREQUIRED|A destination connection must be specified.|  
|0xC0029295|-1073573227|DTS_E_TRANSFERTASKS_CONNECTIONNOTFOUND|The connection "%1" could not be found in the package.|  
|0xC0029296|-1073573226|DTS_E_TRANSFERTASKS_SERVERVERSIONNOTALLOWED|The connection "%1" specifies a SQL Server instance with a version that is not supported for transfer.  Only versions 7, 2000, and 2005 are supported.|  
|0xC0029297|-1073573225|DTS_E_TRANSFERTASKS_SRCSERVERLESSEQUALDESTSERVER|The source connection "%1" must specify a SQL Server instance with a version earlier than or the same as the destination connection "%2".|  
|0xC0029298|-1073573224|DTS_E_TRANSFERTASKS_SRCDBREQUIRED|A source database must be specified.|  
|0xC0029299|-1073573223|DTS_E_TRANSFERTASKS_SRCDBMUSTEXIST|The source database "%1" must exist on the source server.|  
|0xC002929A|-1073573222|DTS_E_TRANSFERTASKS_DESTDBREQUIRED|A destination database must be specified.|  
|0xC002929B|-1073573221|DTS_E_TRANSFERTASKS_SRCDBANDDESTDBTHESAME|The source database and the destination database can not be the same.|  
|0xC002929C|-1073573220|DTS_E_TRANSFERDBTASK_FILENAMEREQUIRED|The transfer file information %1 is missing the filename.|  
|0xC002929D|-1073573219|DTS_E_TRANSFERDBTASK_FOLDERREQUIRED|The transfer file information %1 is missing the folder part.|  
|0xC002929E|-1073573218|DTS_E_TRANSFERTASKS_NETSHAREREQUIRED|The transfer file information %1 is missing the network share part.|  
|0xC002929F|-1073573217|DTS_E_TRANSFERTASKS_FILELISTSCOUNTMISMATCH|The number of source transfer files and the number of destination transfer files must be the same.|  
|0xC00292A0|-1073573216|DTS_E_DOESNOTSUPPORTTRANSACTIONS|Enlisting in transactions is not supported.|  
|0xC00292A1|-1073573215|DTS_E_TRANSFERDBTASK_OFFLINEERROR|The following exception occurred during an offline database transfer: %1.|  
|0xC00292A2|-1073573214|DTS_E_TRANSFERDBTASK_NETSHAREDOESNOTEXIST|The network share "%1" could not be found.|  
|0xC00292A3|-1073573213|DTS_E_TRANSFERDBTASK_NETSHARENOACCESS|The network share "%1 could not be accessed.  The error is: %2.|  
|0xC00292A4|-1073573212|DTS_E_TRANSFERDBTASK_USERMUSTBEDBOORSYSADMIN|The user "%1" must be a DBO or a sysadmin for "%2" in order to perform an online database transfer.|  
|0xC00292A5|-1073573211|DTS_E_TRANSFERDBTASK_USERMUSTBESYSADMIN|The user "%1" must be a sysadmin on "%2" to perform an offline database transfer.|  
|0xC00292A6|-1073573210|DTS_E_TRANSFERDBTASK_FTCATALOGSOFFLINEYUKONONLY|Full text catalogs can only be included when performing an offline database transfer between 2 SQL Server 2005 servers.|  
|0xC00292A7|-1073573209|DTS_E_TRANSFERDBTASK_NOOVERWRITEDB|The database "%1" already exists on the destination server "%2".|  
|0xC00292A8|-1073573208|DTS_E_TRANSFERDBTASK_MUSTHAVESOURCEFILES|At least one source file must be specified.|  
|0xC00292A9|-1073573207|DTS_E_TRANSFERDBTASKS_SRCFILENOTFOUND|Could not find the file "%1" in the source database "%2".|  
|0xC00292B3|-1073573197|DTS_E_MSMQTASK_FIPS1402COMPLIANCE|The operation requested is not allowed in systems compliant with U.S. FIPS 140-2.|  
|0xC002F210|-1073548784|DTS_E_SQLTASK_ERROREXECUTINGTHEQUERY|Executing the query "%1" failed with the following error: "%2". Possible failure reasons: Problems with the query, "ResultSet" property not set correctly, parameters not set correctly, or connection not established correctly.|  
|0xC002F300|-1073548544|DTS_E_TRANSFERSPTASK_ERRORREADINGSPNAMES|Error reading stored procedure names from the xml file.|  
|0xC002F301|-1073548543|DTS_E_TRANSFERSPTASK_INVALIDDATANODE|Invalid data node for the Transfer Stored Procedure task.|  
|0xC002F302|-1073548542|DTS_E_TRANSFERTASKS_CONNECTIONTYPEISNOTSMOSERVER|Connection "%1" is not of type "SMOServer".|  
|0xC002F303|-1073548541|DTS_E_TRANSFERSPTASK_EXECUTIONFAILED|Execution failed with the following error "%1".|  
|0xC002F304|-1073548540|DTS_E_ERROROCCURREDWITHFOLLOWINGMESSAGE|An error occurred with the following error message: "%1".|  
|0xC002F305|-1073548539|DTS_E_BITASK_EXECUTION_FAILED|Bulk insert execution failed.|  
|0xC002F306|-1073548538|DTS_E_FSTASK_INVALIDDESTPATH|Invalid destination path.|  
|0xC002F307|-1073548537|DTS_E_FSTASK_CANTCREATEDIR|Can not create directory. User chose to fail the task if directory exists.|  
|0xC002F308|-1073548536|DTS_E_SQLTASK_ODBCNOSUPPORTTRANSACTION|The task has a transaction option of "Required" and connection "%1" is of type "ODBC". ODBC connections don't support transactions.|  
|0xC002F309|-1073548535|DTS_E_SQLTASK_ERRORASSIGINGVALUETOVAR|An error occurred while assigning a value to variable "%1": "%2".|  
|0xC002F30A|-1073548534|DTS_E_FSTASK_SOURCEISEMPTY|The source is empty.|  
|0xC002F30B|-1073548533|DTS_E_FSTASK_DESTINATIONISEMPTY|The destination is empty.|  
|0xC002F30C|-1073548532|DTS_E_FSTASK_FILEDIRNOTFOUND|File or directory "%1" does not exist.|  
|0xC002F30D|-1073548531|DTS_E_FSTASK_VARSRCORDESTISEMPTY|Variable "%1" is used as a source or destination and is empty.|  
|0xC002F30E|-1073548530|DTS_E_FSTASK_FILEDELETED|File or directory "%1" was deleted.|  
|0xC002F30F|-1073548529|DTS_E_FSTASK_DIRECTORYDELETED|Directory "%1" was deleted.|  
|0xC002F310|-1073548528|DTS_E_WMIDRTASK_VARIABLETYPEISNOTOBJECT|The variable "%1" should be of type object to be assigned a data table.|  
|0xC002F311|-1073548527|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRING|The variable "%1" does not have a string data type.|  
|0xC002F312|-1073548526|DTS_E_FTPTASK_CANNOTACQUIRECONNECTION|There was an error acquiring the FTP connection. Verify that a valid connection type is specified in "%1".|  
|0xC002F313|-1073548525|DTS_E_FTPTASK_CONNECTIONNOTFOUND|The FTP connection manager "%1" can not be found.|  
|0xC002F314|-1073548524|DTS_E_FTPTASK_FILEUSAGETYPEERROR|File usage type of connection "%1" should be "%2" for operation "%3".|  
|0xC002F315|-1073548523|DTS_E_TRANSFERTASKS_SOURCECANTBESAMEASDESTINATION|The source server can not be the same as the destination server.|  
|0xC002F316|-1073548522|DTS_E_ERRMSGTASK_EMPTYSOURCELIST|There are no Error Messages to transfer.|  
|0xC002F317|-1073548521|DTS_E_ERRMSGTASK_DIFFERENTMESSAGEANDLANGUAGESIZES|The lists of error messages and their corresponding languages are of different sizes.|  
|0xC002F318|-1073548520|DTS_E_ERRMSGTASK_ERRORMESSAGEOUTOFRANGE|The error message id "%1" is out of the allowed range of user defined error messages. User defined error message ids are between 50000 and 2147483647.|  
|0xC002F319|-1073548519|DTS_E_TRANSFERTASKS_NOTRANSACTIONSUPPORT|This task can not participate in a transaction.|  
|0xC002F320|-1073548512|DTS_E_ERRMSGTASK_FAILEDTOTRANSFERERRORMESSAGES|Failed to transfer some or all of the Error Messages.|  
|0xC002F321|-1073548511|DTS_E_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|The error message "%1" already exists at destination server.|  
|0xC002F324|-1073548508|DTS_E_ERRMSGTASK_ERRORMESSAGECANTBEFOUND|The error message "%1" can not be found at source server.|  
|0xC002F325|-1073548507|DTS_E_TRANSFERTASKS_EXECUTIONFAILED|Execution failed with the following error: "%1".|  
|0xC002F327|-1073548505|DTS_E_JOBSTASK_FAILEDTOTRANSFERJOBS|Failed to transfer the Job(s).|  
|0xC002F330|-1073548496|DTS_E_JOBSTASK_EMPTYSOURCELIST|There are no Jobs to transfer.|  
|0xC002F331|-1073548495|DTS_E_JOBSTASK_JOBEXISTSATDEST|The job "%1" already exists at destination server.|  
|0xC002F334|-1073548492|DTS_E_JOBSTASK_JOBCANTBEFOUND|The job "%1" can not be found at source server.|  
|0xC002F337|-1073548489|DTS_E_LOGINSTASK_EMPTYLIST|The list of "Logins" to transfer is empty.|  
|0xC002F338|-1073548488|DTS_E_LOGINSTASK_CANTGETLOGINSNAMELIST|Can not get the list of "Logins" from source server.|  
|0xC002F340|-1073548480|DTS_E_LOGINSTASK_ERRORLOGINEXISTS|Login "%1" already exists at destination server.|  
|0xC002F342|-1073548478|DTS_E_LOGINSTASK_LOGINNOTFOUND|Login "%1" does not exist at source.|  
|0xC002F344|-1073548476|DTS_E_LOGINSTASK_FAILEDTOTRANSFERLOGINS|Failed to transfer some or all of the logins.|  
|0xC002F345|-1073548475|DTS_E_STOREDPROCSTASK_FAILEDTOTRANSFERSPS|Failed to transfer the stored procedure(s). More informative error should have been raised.|  
|0xC002F346|-1073548474|DTS_E_STOREDPROCSTASK_STOREDPROCNOTFOUND|Stored Procedure "%1" is not found at the source.|  
|0xC002F349|-1073548471|DTS_E_STOREDPROCSTASK_ERRORSTOREDPROCEDUREEXISTS|Stored procedure "%1" already exists at destination server.|  
|0xC002F350|-1073548464|DTS_E_STOREDPROCSTASK_EMPTYSOURCELIST|There are no stored procedures to transfer.|  
|0xC002F353|-1073548461|DTS_E_TRANSOBJECTSTASK_FAILEDTOTRANSFEROBJECTS|Failed to transfer the object(s).|  
|0xC002F354|-1073548460|DTS_E_TRANSOBJECTSTASK_EMPTYLIST|The list of "Objects" to transfer is empty.|  
|0xC002F355|-1073548459|DTS_E_TRANSOBJECTSTASK_NOSPATSOURCE|Stored procedure "%1" does not exist at the source.|  
|0xC002F356|-1073548458|DTS_E_TRANSOBJECTSTASK_SPALREADYATDEST|Stored procedure "%1" already exists at destination.|  
|0xC002F357|-1073548457|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSPS|An error occurred while trying to get set the Stored Procedures list to transfer: "%1".|  
|0xC002F359|-1073548455|DTS_E_TRANSOBJECTSTASK_NORULEATSOURCE|Rule "%1" does not exist at the source.|  
|0xC002F360|-1073548448|DTS_E_TRANSOBJECTSTASK_RULEALREADYATDEST|Rule "%1" already exists at destination.|  
|0xC002F361|-1073548447|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGRULES|An error occurred while trying to get set the Rules list to transfer: "%1".|  
|0xC002F363|-1073548445|DTS_E_TRANSOBJECTSTASK_NOTABLEATSOURCE|Table "%1" does not exist at the source.|  
|0xC002F364|-1073548444|DTS_E_TRANSOBJECTSTASK_TABLEALREADYATDEST|Table "%1" already exists at destination.|  
|0xC002F365|-1073548443|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTABLES|An error occurred while trying to get set the Tables list to transfer: "%1".|  
|0xC002F367|-1073548441|DTS_E_TRANSOBJECTSTASK_NOVIEWATSOURCE|View "%1" does not exist at the source.|  
|0xC002F368|-1073548440|DTS_E_TRANSOBJECTSTASK_VIEWALREADYATDEST|View "%1" already exists at destination.|  
|0xC002F369|-1073548439|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGVIEWS|An error occurred while trying to get set the Views list to transfer: "%1".|  
|0xC002F371|-1073548431|DTS_E_TRANSOBJECTSTASK_NOUDFATSOURCE|User Defined Function "%1" does not exist at the source.|  
|0xC002F372|-1073548430|DTS_E_TRANSOBJECTSTASK_UDFALREADYATDEST|User Defined Function "%1" already exists at destination.|  
|0xC002F373|-1073548429|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDFS|An error occurred while trying to get set the User Defined Functions list to transfer: "%1".|  
|0xC002F375|-1073548427|DTS_E_TRANSOBJECTSTASK_NODEFAULTATSOURCE|Default "%1" does not exist at the source.|  
|0xC002F376|-1073548426|DTS_E_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|Default "%1" already exists at destination.|  
|0xC002F377|-1073548425|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGDEFAULTS|An error occurred while trying to get set the Defaults list to transfer: "%1".|  
|0xC002F379|-1073548423|DTS_E_TRANSOBJECTSTASK_NOUDDTATSOURCE|User Defined Data Type "%1" does not exist at the source.|  
|0xC002F380|-1073548416|DTS_E_TRANSOBJECTSTASK_UDDTALREADYATDEST|User Defined Data Type "%1" already exists at destination.|  
|0xC002F381|-1073548415|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDDTS|An error occurred while trying to get set the User Defined Data Types list to transfer: "%1".|  
|0xC002F383|-1073548413|DTS_E_TRANSOBJECTSTASK_NOPFATSOURCE|Partition Function "%1" does not exist at the source.|  
|0xC002F384|-1073548412|DTS_E_TRANSOBJECTSTASK_PFALREADYATDEST|Partition Function "%1" already exists at destination.|  
|0xC002F385|-1073548411|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPFS|An error occurred while trying to get set the Partition Functions list to transfer: "%1".|  
|0xC002F387|-1073548409|DTS_E_TRANSOBJECTSTASK_NOPSATSOURCE|Partition Scheme "%1" does not exist at the source.|  
|0xC002F388|-1073548408|DTS_E_TRANSOBJECTSTASK_PSALREADYATDEST|Partition Scheme "%1" already exists at destination.|  
|0xC002F389|-1073548407|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPSS|An error occurred while trying to get set the Partition Schemes list to transfer: "%1".|  
|0xC002F391|-1073548399|DTS_E_TRANSOBJECTSTASK_NOSCHEMAATSOURCE|Schema "%1" does not exist at the source.|  
|0xC002F392|-1073548398|DTS_E_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|Schema "%1" already exists at destination.|  
|0xC002F393|-1073548397|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSCHEMAS|An error occurred while trying to get set the Schemas list to transfer: "%1".|  
|0xC002F395|-1073548395|DTS_E_TRANSOBJECTSTASK_NOSQLASSEMBLYATSOURCE|SqlAssembly "%1" does not exist at the source.|  
|0xC002F396|-1073548394|DTS_E_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|SqlAssembly "%1" already exists at destination.|  
|0xC002F397|-1073548393|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSQLASSEMBLIES|An error occurred while trying to get set the SqlAssemblies list to transfer: "%1".|  
|0xC002F399|-1073548391|DTS_E_TRANSOBJECTSTASK_NOAGGREGATEATSOURCE|User Defined Aggregate "%1" does not exist at the source.|  
|0xC002F400|-1073548288|DTS_E_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|User Defined Aggregate "%1" already exists at destination.|  
|0xC002F401|-1073548287|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGAGGREGATES|An error occurred while trying to get set the User Defined Aggregates list to transfer: "%1".|  
|0xC002F403|-1073548285|DTS_E_TRANSOBJECTSTASK_NOTYPEATSOURCE|User Defined Type "%1" does not exist at the source.|  
|0xC002F404|-1073548284|DTS_E_TRANSOBJECTSTASK_TYPEALREADYATDEST|User Defined Type "%1" already exists at destination.|  
|0xC002F405|-1073548283|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTYPES|An error occurred while trying to get set the User Defined Types list to transfer: "%1".|  
|0xC002F407|-1073548281|DTS_E_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONATSOURCE|XmlSchemaCollection "%1" does not exist at the source.|  
|0xC002F408|-1073548280|DTS_E_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|XmlSchemaCollection "%1" already exists at destination.|  
|0xC002F409|-1073548279|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGXMLSCHEMACOLLECTIONS|An error occurred while trying to get set the XmlSchemaCollections list to transfer: "%1".|  
|0xC002F411|-1073548271|DTS_E_TRANSOBJECTSTASK_SUPPORTEDONYUKONONLY|Objects of type "%1" are only supported between SQL Server 2005 or newer servers.|  
|0xC002F413|-1073548269|DTS_E_LOGINSTASK_EMPTYDATABASELIST|The databases list is empty.|  
|0xC002F414|-1073548268|DTS_E_TRANSOBJECTSTASK_NOLOGINATSOURCE|Login "%1" does not exist at the source.|  
|0xC002F416|-1073548266|DTS_E_TRANSOBJECTSTASK_LOGINALREADYATDEST|Login "%1" already exists at destination.|  
|0xC002F417|-1073548265|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGLOGINS|An error occurred while trying to get set the Logins list to transfer: "%1".|  
|0xC002F419|-1073548263|DTS_E_TRANSOBJECTSTASK_NOUSERATSOURCE|User "%1" does not exist at the source.|  
|0xC002F41B|-1073548261|DTS_E_TRANSOBJECTSTASK_USERALREADYATDEST|User "%1" already exists at destination.|  
|0xC002F41C|-1073548260|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUSERS|An error occurred while trying to get set the Users list to transfer: "%1".|  
|0xC002F41F|-1073548257|DTS_E_BITASK_CANNOTRETAINCONNINTRANSACTION|The task can not have a retained connection manager in a transaction.|  
|0xC002F421|-1073548255|DTS_E_SQLTASKOUTPUTENCODINGNOTSUPPORTED|Unable to obtain XML data from SQL Server as Unicode because the provider does not support the OUTPUTENCODING property.|  
|0xC002F426|-1073548250|DTS_E_FTPTASK_FILECONNECTIONNOTFOUND|For the FTP operation "%1", the FILE connection manager "%2" can not be found.|  
|0xC002F428|-1073548248|DTS_E_TRANSOBJECTSTASK_CANNOTDROPOBJECTS|"Logins" are server level objects and can not be dropped first since the source and destination are the same server. Dropping objects first will remove the logins from the source as well.|  
|0xC002F429|-1073548247|DTS_E_SQLTASK_PARAMSIZEERROR|Parameter "%1" cannot be negative. (-1) is used for the default value.|  
|0xC0040019|-1073479655|DTS_E_UNREGISTEREDPIPELINEXML_LOAD|Data Flow objects cannot be loaded. Check if Microsoft.SqlServer.PipelineXml.dll is properly registered.|  
|0xC0040020|-1073479648|DTS_E_UNREGISTEREDPIPELINEXML_SAVE|Data Flow objects cannot be saved. Check if Microsoft.SqlServer.PipelineXml.dll is properly registered.|  
|0xC0040040|-1073479616|DTS_E_PIPELINE_SAVE|Failed to save Data Flow objects.|  
|0xC0040041|-1073479615|DTS_E_PIPELINE_LOAD|Failed to load Data Flow objects|  
|0xC0040042|-1073479614|DTS_E_SAVE_PERSTFORMAT|Failed to save Data Flow objects. The specified format is not supported.|  
|0xC0040043|-1073479613|DTS_E_LOAD_PERSTFORMAT|Failed to load Data Flow objects. The specified format is not supported.|  
|0xC0040044|-1073479612|DTS_E_SETPERSIST_PROPEVENTS|Failed to set the XML persistence events property for the Data Flow objects.|  
|0xC0040045|-1073479611|DTS_E_SETPERSIST_XMLDOM|Failed to set the persistence XML DOM property for the Data Flow objects.|  
|0xC0040046|-1073479610|DTS_E_SETPERSIST_XMLNODE|Failed to set the persistence XML ELEMENT property for the Data Flow objects.|  
|0xC0040047|-1073479609|DTS_E_SETPERSISTPROP_FAILED|Failed to set xml persistence properties for the Data Flow objects.|  
|0xC0040048|-1073479608|DTS_E_NOCUSTOMPROPCOL|Failed to get custom property collection for Data Flow components.|  
|0xC0047000|-1073451008|DTS_E_CYCLEINEXECUTIONTREE|An execution tree contains a cycle.|  
|0xC0047001|-1073451007|DTS_E_DISCONNECTEDOBJECT|The %1 object "%2" (%3!d!) is disconnected from the layout.|  
|0xC0047002|-1073451006|DTS_E_INVALIDOBJECTID|The ID for the layout object is not valid.|  
|0xC0047003|-1073451005|DTS_E_INPUTWITHOUTPATHS|A required input object is not connected to a path object.|  
|0xC0047005|-1073451003|DTS_E_INVALIDSYNCHRONOUSINPUT|%1 has an invalid synchronous input ID %2!d!.|  
|0xC0047006|-1073451002|DTS_E_INVALIDOUTPUTLINEAGEID|%1 has lineage ID %2!d!, but should have had %3!d!.|  
|0xC0047008|-1073451000|DTS_E_DUPLICATENAMESINCOLLECTION|The package contains two objects with the duplicate name of "%1" and "%2".|  
|0xC0047009|-1073450999|DTS_E_INVALIDEXCLUSIONGROUP|The "%1" and the "%2" are in the same exclusion group, but they do not have the same synchronous input.|  
|0xC004700A|-1073450998|DTS_E_DUPLICATELINEAGEIDSINCOLLECTION|Two objects in the same collection have a duplicate lineage ID of %1!d!. The objects are %2 and %3.|  
|0xC004700B|-1073450997|DTS_E_VALIDATIONFAILEDONLAYOUT|The layout failed validation.|  
|0xC004700C|-1073450996|DTS_E_VALIDATIONFAILEDONCOMPONENTS|One or more component failed validation.|  
|0xC004700D|-1073450995|DTS_E_VALIDATIONFAILED|The layout and one or more components failed validation.|  
|0xC004700E|-1073450994|DTS_E_THREADSTARTUPFAILED|The Data Flow task engine failed at startup because it cannot create one or more required threads.|  
|0xC004700F|-1073450993|DTS_E_CANTGETMUTEX|A thread failed to create a mutex at initialization.|  
|0xC0047010|-1073450992|DTS_E_CANTGETSEMAPHORE|A thread failed to create a semaphore at initialization.|  
|0xC0047011|-1073450991|DTS_E_BUFFERFAILUREDETAILS|The system reports %1!d! percent memory load. There are %2 bytes of physical memory with %3 bytes free. There are %4 bytes of virtual memory with %5 bytes free. The paging file has %6 bytes with %7 bytes free.|  
|0xC0047012|-1073450990|DTS_E_BUFFERALLOCFAILED|A buffer failed while allocating %1!d! bytes.|  
|0xC0047013|-1073450989|DTS_E_CANTCREATEBUFFERMANAGER|The Buffer Manager could not be created.|  
|0xC0047015|-1073450987|DTS_E_BUFFERBADSIZE|Buffer Type %1!d! had a size of %2!I64d! bytes.|  
|0xC0047016|-1073450986|DTS_E_DANGLINGWITHPATH|%1 is marked as dangling, but has a path attached to it.|  
|0xC0047017|-1073450985|DTS_E_INDIVIDUALVALIDATIONFAILED|%1 failed validation and returned error code 0x%2!8.8X!.|  
|0xC0047018|-1073450984|DTS_E_INDIVIDUALPOSTEXECUTEFAILED|%1 failed the post-execute phase and returned error code 0x%2!8.8X!.|  
|0xC0047019|-1073450983|DTS_E_INDIVIDUALPREPAREFAILED|%1 failed the prepare phase and returned error code 0x%2!8.8X!.|  
|0xC004701A|-1073450982|DTS_E_INDIVIDUALPREEXECUTEFAILED|%1 failed the pre-execute phase and returned error code 0x%2!8.8X!.|  
|0xC004701B|-1073450981|DTS_E_INDIVIDUALCLEANUPFAILED|%1 failed the cleanup phase and returned error code 0x%2!8.8X!.|  
|0xC004701C|-1073450980|DTS_E_INVALIDINPUTLINEAGEID|%1 has lineage ID %2!d! that was not previously used in the Data Flow task.|  
|0xC004701E|-1073450978|DTS_E_EXECUTIONTREECYCLE|Cannot connect %1 to %2 because a cycle would be created.|  
|0xC004701F|-1073450977|DTS_E_CANTCOMPARE|The data type "%1" cannot be compared. Comparison of that data type is not supported, so it cannot be sorted or used as a key.|  
|0xC0047020|-1073450976|DTS_E_REFUSEDFORSHUTDOWN|This thread has shut down and is not accepting buffers for input.|  
|0xC0047021|-1073450975|DTS_E_THREADFAILED|SSIS Error Code DTS_E_THREADFAILED.  Thread "%1" has exited with error code 0x%2!8.8X!.  There may be error messages posted before this with more information on why the thread has exited.|  
|0xC0047022|-1073450974|DTS_E_PROCESSINPUTFAILED|SSIS Error Code DTS_E_PROCESSINPUTFAILED.  The ProcessInput method on component "%1" (%2!d!) failed with error code 0x%3!8.8X! while processing input "%4" (%5!d!). The identified component returned an error from the ProcessInput method. The error is specific to the component, but the error is fatal and will cause the Data Flow task to stop running.  There may be error messages posted before this with more information about the failure.|  
|0xC0047023|-1073450973|DTS_E_CANTREALIZEVIRTUALBUFFERS|A set of virtual buffers cannot be realized.|  
|0xC0047024|-1073450972|DTS_E_PIPELINETOOCOMPLEX|The number of threads required for this pipeline is %1!d!, which is more than the system limit of %2!d!. The pipeline requires too many threads as configured. There are either too many asynchronous outputs, or EngineThreads property is set too high. Split the pipeline into multiple packages, or reduce the value of the EngineThreads property.|  
|0xC0047028|-1073450968|DTS_E_SCHEDULERCOULDNOTCOUNTSOURCES|The Data Flow engine scheduler cannot obtain a count of the sources in the layout.|  
|0xC0047029|-1073450967|DTS_E_SCHEDULERCOULDNOTCOUNTDESTINATIONS|The Data Flow engine scheduler cannot obtain a count of the destinations in the layout.|  
|0xC004702A|-1073450966|DTS_E_COMPONENTVIEWISUNAVAILABLE|The component view is unavailable. Make sure the component view has been created.|  
|0xC004702B|-1073450965|DTS_E_INCORRECTCOMPONENTVIEWID|The component view ID is incorrect. The component view may be out of synchronization. Try releasing the component view and recreating it.|  
|0xC004702C|-1073450964|DTS_E_BUFFERNOTLOCKED|This buffer is not locked and cannot be manipulated.|  
|0xC004702D|-1073450963|DTS_E_CANTBUILDBUFFERTYPE|The Data Flow task cannot allocate memory to build a buffer definition. The buffer definition had %1!d! columns.|  
|0xC004702E|-1073450962|DTS_E_CANTREGISTERBUFFERTYPE|The Data Flow task cannot register a buffer type. The type had %1!d! columns and was for execution tree %2!d!.|  
|0xC004702F|-1073450961|DTS_E_INVALIDUSESDISPOSITIONSVALUE|The UsesDispositions property cannot be changed from its initial value. This occurs when the XML is edited and the UsesDispositions value is modified. This value is set by the component when it is added to the package and is not allowed to change.|  
|0xC0047030|-1073450960|DTS_E_THREADFAILEDINITIALIZE|The Data Flow task failed to initialize a required thread and cannot begin execution. The thread previously reported a specific error.|  
|0xC0047031|-1073450959|DTS_E_THREADFAILEDCREATE|The Data Flow task failed to create a required thread and cannot begin running. The usually occurs when there is an out-of-memory state.|  
|0xC0047032|-1073450958|DTS_E_EXECUTIONTREECYCLEADDINGSYNCHRONOUSINPUT|The synchronous input of "%1" cannot be set to "%2" because a cycle would be created.|  
|0xC0047033|-1073450957|DTS_E_INVALIDCUSTOMPROPERTYNAME|A custom property named "%1" is invalid because there is a stock property with that name. A custom property cannot have the same name as a stock property on the same object.|  
|0xC0047035|-1073450955|DTS_E_BUFFERLOCKUNDERFLOW|The buffer was already unlocked.|  
|0xC0047036|-1073450954|DTS_E_INDIVIDUALCACHEINTERFACESFAILED|%1 failed initialization and returned error code 0x%2!8.8X!.|  
|0xC0047037|-1073450953|DTS_E_INDIVIDUALRELEASEINTERFACESFAILED|%1 failed during shut down and returned error code 0x%2!8.8X!. A component failed to release its interfaces.|  
|0xC0047038|-1073450952|DTS_E_PRIMEOUTPUTFAILED|SSIS Error Code DTS_E_PRIMEOUTPUTFAILED.  The PrimeOutput method on %1 returned error code 0x%2!8.8X!.  The component returned a failure code when the pipeline engine called PrimeOutput(). The meaning of the failure code is defined by the component, but the error is fatal and the pipeline stopped executing.  There may be error messages posted before this with more information about the failure.|  
|0xC0047039|-1073450951|DTS_E_THREADCANCELLED|SSIS Error Code DTS_E_THREADCANCELLED.  Thread "%1" received a shutdown signal and is terminating. The user requested a shutdown, or an error in another thread is causing the pipeline to shutdown.  There may be error messages posted before this with more information on why the thread was cancelled.|  
|0xC004703A|-1073450950|DTS_E_DISTRIBUTORCANTSETPROPERTY|Distributor for thread "%1" failed to initialize property "%2" on component "%3" because of error 0x%8.8X. The distributor could not initialize the component's property and cannot continue running.|  
|0xC004703B|-1073450949|DTS_E_CANTREGISTERVIEWBUFFERTYPE|The Data Flow task cannot register a view buffer type. The type had %1!d! columns and was for input ID %2!d!.|  
|0xC004703F|-1073450945|DTS_E_CANTCREATEEXECUTIONTREE|There is not enough memory to create an execution tree.|  
|0xC0047040|-1073450944|DTS_E_CANTINSERTINTOHASHTABLE|There is not enough memory to insert an object into the hash table.|  
|0xC0047041|-1073450943|DTS_E_OBJECTNOTINHASHTABLE|The object is not in the hash table.|  
|0xC0047043|-1073450941|DTS_E_CANTCREATECOMPONENTVIEW|Cannot create a component view because another one already exists. Only one component view can exist at a time.|  
|0xC0047046|-1073450938|DTS_E_LAYOUTCANTSETUSAGETYPE|At input "%1" (%2!d!), the virtual input column collection does not contain a virtual input column with lineage ID %3!d!.|  
|0xC0047047|-1073450937|DTS_E_WRONGOBJECTTYPE|The requested object has the incorrect object type.|  
|0xC0047048|-1073450936|DTS_E_CANTCREATESPOOLFILE|The buffer manager cannot create a temporary storage file on any path in the BufferTempStoragePath property. There is an incorrect file name or no permission or the paths have been full.|  
|0xC0047049|-1073450935|DTS_E_SEEKFAILED|The buffer manager could not seek to offset %1!d! in file "%2". The file is damaged.|  
|0xC004704A|-1073450934|DTS_E_EXTENDFAILED|The buffer manager cannot extend the file "%1" to length %2!lu! bytes.  There was insufficient disk space.|  
|0xC004704B|-1073450933|DTS_E_FILEWRITEFAILED|The buffer manager cannot write %1!d! bytes to file "%2". There was insufficient disk space or quota.|  
|0xC004704C|-1073450932|DTS_E_FILEREADFAILED|The buffer manager cannot read %1!d! bytes from file "%2". The file is damaged.|  
|0xC004704D|-1073450931|DTS_E_VIRTUALNOTSEQUENTIAL|Buffer ID %1!d! supports other virtual buffers and cannot be placed into sequential mode. IDTSBuffer100.SetSequentialMode was called on a buffer that supports virtual buffers.|  
|0xC004704E|-1073450930|DTS_E_BUFFERISREADONLY|This operation could not be performed because buffer is in read-only mode. A read-only buffer cannot be modified.|  
|0xC004704F|-1073450929|DTS_E_EXECUTIONTREECYCLESETTINGID|ID %1 cannot be set to %2!d! because a cycle would be created.|  
|0xC0047050|-1073450928|DTS_E_NOMOREBUFFERTYPES|The buffer manager ran out of memory while trying to extend the table of buffer types. This is caused by an out-of-memory condition.|  
|0xC0047051|-1073450927|DTS_E_CANTCREATENEWTYPE|The buffer manager failed to create a new buffer type.|  
|0xC0047053|-1073450925|DTS_E_SCHEDULERBADTREE|The Data Flow engine scheduler failed to retrieve the execution tree with index %1!d! from the layout. The scheduler received a count containing more execution trees than actually exist.|  
|0xC0047056|-1073450922|DTS_E_CANTCREATEPRIMEOUTPUTBUFFER|The Data Flow task failed to create a buffer to call PrimeOutput for output "%3" (%4!d!) on component "%1" (%2!d!). This error usually occurs due to an out-of-memory condition.|  
|0xC0047057|-1073450921|DTS_E_SCHEDULERTHREADMEMORY|The Data Flow engine scheduler failed to create a thread object because not enough memory is available. This is caused by an out-of-memory condition.|  
|0xC004705A|-1073450918|DTS_E_SCHEDULEROBJECT|The Data Flow engine scheduler cannot retrieve object with ID %1!d! from the layout. The Data Flow engine scheduler previously located an object that is now no longer available.|  
|0xC004705B|-1073450917|DTS_E_PREPARETREENODEFAILED|The Data Flow task failed to prepare buffers for the execution tree node beginning at output "%1" (%2!d!).|  
|0xC004705C|-1073450916|DTS_E_CANTCREATEVIRTUALBUFFER|The Data Flow task cannot create a virtual buffer to prepare for execution.|  
|0xC004705E|-1073450914|DTS_E_NOMOREIDS|The maximum ID has been reached. There are no more IDs available to assign to objects.|  
|0xC004705F|-1073450913|DTS_E_ALREADYATTACHED|The %1 is already attached and cannot be attached again.  Detach it and try again.|  
|0xC0047060|-1073450912|DTS_E_OUTPUTCOLUMNNAMECONFLICT|Column name "%1" on output "%2" cannot be used because it conflicts with a column of the same name on synchronous input "%3".|  
|0xC0047061|-1073450911|DTS_E_EOFANNOUNCEMENTFAILED|The Data Flow task cannot to create a buffer to mark the end of the rowset.|  
|0xC0047062|-1073450910|DTS_E_USERCOMPONENTEXCEPTION|A managed user component has thrown exception "%1".|  
|0xC0047063|-1073450909|DTS_E_SCHEDULERMEMORY|The Data Flow engine scheduler cannot allocate enough memory for the execution structures. The system was low on memory before execution started.|  
|0xC0047064|-1073450908|DTS_E_BUFFERNOOBJECTMEMORY|An out-of-memory condition prevented the creation of the buffer object.|  
|0xC0047065|-1073450907|DTS_E_BUFFERNOMAPMEMORY|An out-of-memory condition prevents the mapping of a buffer's lineage IDs to DTP_HCOL indexes.|  
|0xC0047066|-1073450906|DTS_E_INDIVIDUALPUTVARIABLESFAILED|The "%1!s!" cannot cache the Variables collection and returned error code 0x%2!8.8X.|  
|0xC0047067|-1073450905|DTS_E_INDIVIDUALPUTCOMPONENTMETADATAFAILED|The "%1" failed to cache the component metadata object and returned error code 0x%2!8.8X!.|  
|0xC0047068|-1073450904|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITION|"%1" has a non-zero SortKeyPosition, but its value (%2!ld!) is too large. It must be less than or equal to the number of columns.|  
|0xC004706A|-1073450902|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITIONS|The IsSorted property of %1 is set to TRUE, but the absolute values of the non-zero output column SortKeyPositions do not form a monotonically increasing sequence, starting at one.|  
|0xC004706B|-1073450901|DTS_E_INDIVIDUALVALIDATIONSTATUSFAILED|"%1" failed validation and returned validation status "%2".|  
|0xC004706C|-1073450900|DTS_E_CANTCREATECOMPONENT|Component "%1!s!" could not be created and returned error code 0x%2!8.8X! "%3!s!". Make sure that the component is registered correctly.|  
|0xC004706D|-1073450899|DTS_E_COMPONENTNOTREGISTERED|The module containing "%1" is not registered or installed correctly.|  
|0xC004706E|-1073450898|DTS_E_COMPONENTNOTFOUND|The module containing "%1" cannot be located, even though it is registered.|  
|0xC004706F|-1073450897|DTS_E_BINARYCODENOTFOUND|The script component is configured to pre-compile the script, but binary code is not found. Please visit the IDE in Script Component Editor by clicking Design Script button to cause binary code to be generated.|  
|0xC0047070|-1073450896|DTS_E_CANTCREATEBLOBFILE|The buffer manager cannot create a file to spool a long object on the directories named in the BLOBTempStoragePath property.  Either an incorrect file name was provided, or there are no permissions, or the paths have been full.|  
|0xC0047071|-1073450895|DTS_E_SYNCHRONOUSIDMISMATCH|The SynchronousInputID property on "%1" was %2!d!, and %3!d! was expected.|  
|0xC0047072|-1073450894|DTS_E_OBJECTIDNOTFOUND|No object exists with the ID %1!d!.|  
|0xC0047073|-1073450893|DTS_E_OBJECTIDLOOKUPFAILED|Unable to locate an object with ID %1!d! because of the error code 0x%2!8.8X!.|  
|0xC0047074|-1073450892|DTS_E_INVALIDCODEPAGE|The code page %1!d! specified on output column "%2" (%3!d!) is not valid. Select a different code page for output column "%2".|  
|0xC0047075|-1073450891|DTS_E_INDIVIDUALPUTEVENTINFOSFAILED|The EventInfos collection could not be cached by "%1" and returned error code 0x%2!8.8X!.|  
|0xC0047077|-1073450889|DTS_E_DUPLICATEOUTPUTCOLUMNNAMES|The name for "%1" is a duplicate.  All names must be unique.|  
|0xC0047078|-1073450888|DTS_E_NOOUTPUTCOLUMNFORINPUTCOLUMN|There is no output column associated with input column "%1" (%2!d!).|  
|0xC0047079|-1073450887|DTS_E_EXCLGRPNOSYNCINP|"%1" has a virtual buffer extending from a root source. There is an exclusion group that is not zero with a synchronous input that is zero.|  
|0xC004707A|-1073450886|DTS_E_ERROROUTCANTBEONSYNCNONEXCLUSIVEOUTPUT|"%1" cannot be an error output because error outputs cannot be placed on synchronous, non-exclusive outputs.|  
|0xC004707B|-1073450885|DTS_E_EXPREVALDIVBYZERO|A divide-by-zero error occurred. The right side operand evaluates to zero in the expression "%1".|  
|0xC004707C|-1073450884|DTS_E_EXPREVALLITERALOVERFLOW|The literal "%1" is too large to fit into type %2. The magnitude of the literal overflows the type.|  
|0xC004707D|-1073450883|DTS_E_EXPREVALBINARYOPNUMERICOVERFLOW|The result of the binary operation "%1" on data types %2 and %3 exceeds the maximum size for numeric types. The operand types could not be implicitly cast into a numeric (DT_NUMERIC) result without loss of precision or scale. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC004707E|-1073450882|DTS_E_EXPREVALBINARYOPOVERFLOW|The result of the binary operation "%1" exceeds the maximum size for result data type "%2". The magnitude of the result of the operation overflows the type of the result.|  
|0xC004707F|-1073450881|DTS_E_EXPREVALFUNCTIONOVERFLOW|The result of the function call "%1" is too large to fit in type "%2". The magnitude of the result of the function call overflows the type of the operand. An explicit cast to a larger type may be required.|  
|0xC0047080|-1073450880|DTS_E_EXPREVALBINARYTYPEMISMATCH|The data types "%1" and "%2" are incompatible for binary operator "%3". The operand types could not be implicitly cast into compatible types for the operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0047081|-1073450879|DTS_E_EXPREVALUNSUPPORTEDBINARYTYPE|The data type "%1" cannot be used with binary operator "%2". The type of one or both of the operands is not supported for the operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC0047082|-1073450878|DTS_E_EXPREVALBINARYSIGNMISMATCH|There is a sign mismatch for the bitwise binary operator "%1" in operation "%2". Both operands for this operator must be positive or negative.|  
|0xC0047083|-1073450877|DTS_E_EXPREVALBINARYOPERATIONFAILED|The binary operation "%1" failed with error code 0x%2!8.8X!. An internal error occurred, or an out-of-memory condition exists.|  
|0xC0047084|-1073450876|DTS_E_EXPREVALBINARYOPERATIONSETTYPEFAILED|Attempt to set the result type of binary operation "%1" failed with error code 0x%2!8.8X!.|  
|0xC0047085|-1073450875|DTS_E_EXPREVALSTRINGCOMPARISONFAILED|Comparing "%1" to string "%2" failed.|  
|0xC0047086|-1073450874|DTS_E_EXPREVALUNSUPPORTEDUNNARYTYPE|The data type "%1" cannot be used with unary operator "%2". This operand type is not supported for the operation. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC0047087|-1073450873|DTS_E_EXPREVALUNARYOPERATIONFAILED|The unary operation "%1" failed with error code 0x%2!8.8X!. An internal error occurred, or there is an out-of-memory condition.|  
|0xC0047088|-1073450872|DTS_E_EXPREVALUNARYOPERATIONSETTYPEFAILED|Attempt to set the result type of unary operation "%1" failed with error code 0x%2!8.8X!.|  
|0xC0047089|-1073450871|DTS_E_EXPREVALPARAMTYPEMISMATCH|The function "%1" does not support the data type "%2" for parameter number %3!d!. The type of the parameter could not be implicitly cast into a compatible type for the function. To perform this operation, the operand needs to be explicitly cast with a cast operator.|  
|0xC004708A|-1073450870|DTS_E_EXPREVALINVALIDFUNCTION|The function "%1" was not recognized. Either the function name is incorrect or does not exist.|  
|0xC004708B|-1073450869|DTS_E_EXPREVALFNSUBSTRINGINVALIDLENGTH|The length %1!d! is not valid for function "%2". The length parameter cannot be negative. Change the length parameter to zero or a positive value.|  
|0xC004708C|-1073450868|DTS_E_EXPREVALFNSUBSTRINGINVALIDSTARTINDEX|The start index %1!d! is not valid for function "%2". The start index value must be an integer greater than 0. Start index is one-based, not zero-based.|  
|0xC004708E|-1073450866|DTS_E_EXPREVALCHARMAPPINGFAILED|The function "%1" cannot perform the character mapping on string "%2".|  
|0xC004708F|-1073450865|DTS_E_EXPREVALINVALIDDATEPART|"%1" is not a valid date part for function "%2".|  
|0xC0047090|-1073450864|DTS_E_EXPREVALINVALIDNULLPARAM|Parameter number %1!d! of the function NULL with data type "%2" is not valid. The parameters of NULL() must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0047091|-1073450863|DTS_E_EXPREVALINVALIDNULLPARAMTYPE|Parameter number %1!d! of the function NULL with data type "%2" is not an integer. A parameter of NULL() must be an integer or a type that can be converted to an integer.|  
|0xC0047092|-1073450862|DTS_E_EXPREVALFUNCTIONPARAMNOTSTATIC|Parameter number %1!d! of the function "%2" is not static. This parameter must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0047093|-1073450861|DTS_E_EXPREVALINVALIDCASTPARAM|Parameter number %1!d! of the cast to data type "%2" is not valid. The parameters of cast operators must be static, and cannot contain dynamic elements such as input columns.|  
|0xC0047094|-1073450860|DTS_E_EXPREVALINVALIDCASTPARAMTYPE|Parameter number %1!d! of the cast to data type "%2" is not an integer. A parameter of a cast operator must be an integer or a type that can be converted to an integer.|  
|0xC0047095|-1073450859|DTS_E_EXPREVALINVALIDCAST|Cannot cast expression "%1" from data type "%2" to data type "%3". The requested cast is not supported.|  
|0xC0047096|-1073450858|DTS_E_EXPREVALINVALIDTOKEN|Attempt to parse the expression "%1" failed.  The token "%2" at line number "%3", character number "%4" was not recognized. The expression cannot be parsed because it contains invalid elements at the location specified.|  
|0xC0047097|-1073450857|DTS_E_EXPREVALUNEXPECTEDPARSEERROR|An error occurred when parsing the expression "%1". The expression failed to parse for an unknown reason.|  
|0xC0047098|-1073450856|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONWITHHR|Attempt to parse the expression "%1" failed and returned error code 0x%2!8.8X!. The expression cannot be parsed. It might contain invalid elements or it might not be well-formed. There may also be an out-of-memory error.|  
|0xC0047099|-1073450855|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSION|The expression "%1" is not valid and cannot be parsed. The expression may contain invalid elements or it may not be well-formed.|  
|0xC004709A|-1073450854|DTS_E_EXPREVALEXPRESSIONEMPTY|There was no expression to compute. An attempt was made to compute or get the string of an empty expression.|  
|0xC004709B|-1073450853|DTS_E_EXPREVALCOMPUTEFAILED|Attempt to compute the expression "%1" failed with error code 0x%2!8.8X!.|  
|0xC004709C|-1073450852|DTS_E_EXPREVALBUILDSTRINGFAILED|Attempt to generate a string representation of the expression failed with error code 0x%1!8.8X!. Failed when attempting to generate a displayable string that represents the expression.|  
|0xC004709D|-1073450851|DTS_E_EXPREVALCANNOTCONVERTRESULT|Cannot convert the expression result data type "%1" to the column data type "%2". The result of the expression should be written to an input/output column, but the data type of the expression cannot be converted to the data type of the column.|  
|0xC004709E|-1073450850|DTS_E_EXPREVALCONDITIONALOPINVALIDCONDITIONTYPE|The conditional expression "%1" of the conditional operator has an invalid data type of "%2". The conditional expression of the conditional operator must return a Boolean, which is type DT_BOOL.|  
|0xC004709F|-1073450849|DTS_E_EXPREVALCONDITIONALOPTYPEMISMATCH|The data types "%1" and "%2" are incompatible for the conditional operator. The operand types cannot be implicitly cast into compatible types for the conditional operation. To perform this operation, one or both operands need to be explicitly cast with a cast operator.|  
|0xC00470A0|-1073450848|DTS_E_EXPREVALCONDITIONALOPSETTYPEFAILED|Attempt to set the result type of conditional operation "%1" failed with error code 0x%2!8.8X!.|  
|0xC00470A1|-1073450847|DTS_E_BUFFERORPHANED|This buffer has been orphaned. The buffer manager has shut down, leaving an outstanding buffer and no cleanup will occur for the buffer. There is a potential for memory leaks and other problems.|  
|0xC00470A2|-1073450846|DTS_E_EXPREVALINPUTCOLUMNNAMENOTFOUND|Attempt to find the input column named "%1" failed with error code 0x%2!8.8X!. The input column specified was not found in the input column collection.|  
|0xC00470A3|-1073450845|DTS_E_EXPREVALINPUTCOLUMNIDNOTFOUND|Attempt to find the input column with lineage ID %1!d! failed with error code 0x%2!8.8X!. The input column was not found in the input column collection.|  
|0xC00470A4|-1073450844|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNNAME|The expression contains unrecognized token "%1". If "%1" is a variable, it should be expressed as "\@%1". The specified token is not valid. If the token is intended to be a variable name, it should be prefixed with the \@ symbol.|  
|0xC00470A5|-1073450843|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNID|The expression contains unrecognized token "#%1!d!".|  
|0xC00470A6|-1073450842|DTS_E_EXPREVALVARIABLENOTFOUND|The variable "%1" was not found in the Variables collection. The variable might not exist in the correct scope.|  
|0xC00470A7|-1073450841|DTS_E_EXPREVALINVALIDTOKENSTATE|Attempt to parse the expression "%1" failed. The expression might contain an invalid token, an incomplete token, or an invalid element. It might not be well-formed, or might be missing part of a required element such as a parenthesis.|  
|0xC00470A8|-1073450840|DTS_E_BLANKOUTPUTCOLUMNNAME|The name for "%1" is blank, and names cannot be blank.|  
|0xC00470A9|-1073450839|DTS_E_HASSIDEEFFECTSWITHSYNCINP|The "%1" has the HasSideEffects property set to TRUE, but "%1" is synchronous and cannot have side effects. Set the HasSideEffects property to FALSE.|  
|0xC00470AA|-1073450838|DTS_E_EXPREVALINVALIDCASTCODEPAGE|The value, %1!d!, specified for the code page parameter of the cast to data type "%2", is not valid. The code page is not installed on the machine.|  
|0xC00470AB|-1073450837|DTS_E_EXPREVALINVALIDCASTPRECISION|The value %1!d! specified for the precision parameter of the cast to data type "%2" is not valid. Precision must be in the range %3!d! to %4!d! and the precision value is out of range for the type cast.|  
|0xC00470AC|-1073450836|DTS_E_EXPREVALINVALIDCASTSCALE|The value %1!d! specified for the scale parameter of the cast to data type "%2" is not valid. The scale must be in the range %3!d! to %4!d! and the scale value is out of range for the type cast. Scale must not exceed precision and must be positive.|  
|0xC00470AD|-1073450835|DTS_E_NONSORTEDOUTPUTHASSORTKEYPOSITIONS|The IsSorted property for "%1" is false, but %2!lu! of its output columns' SortKeyPositions are non-zero.|  
|0xC00470AF|-1073450833|DTS_E_EXPREVALCONDITIONALOPCODEPAGEMISMATCH|The code pages must match for operands of conditional operation "%1" for type %2. The code page of the left operand does not match the code page of the right operand. For the conditional operator on the specified type, the code pages must be the same.|  
|0xC00470B1|-1073450831|DTS_E_REFERENCEDMETADATABADCOUNT|Input "%1" (%2!d!) references input "%3" (%4!d!), but they do not have the same number of columns. Input %5!d! has %6!d! columns, while input %7!d! has %8!d! columns.|  
|0xC00470B2|-1073450830|DTS_E_OBJECTLINEAGEIDNOTFOUND|No object exists with a lineage ID of %1!d!.|  
|0xC00470B3|-1073450829|DTS_E_FILENAMEOUTPUTCOLUMNOTFOUND|The output column for the file name cannot be found.|  
|0xC00470B4|-1073450828|DTS_E_FILENAMEOUTPUTCOLUMNINVALIDDATATYPE|The output column for the file name is not a null-terminated Unicode character string, which is data type DT_WSTR.|  
|0xC00470B5|-1073450827|DTS_E_DISTRIBUTORADDFAILED|A distributor failed to give a buffer to thread "%1" because of error 0x%2!8.8X!. The target thread is probably shutting down.|  
|0xC00470B6|-1073450826|DTS_E_LOCALENOTINSTALLED|The LocaleID %1!ld! is not installed on this system.|  
|0xC00470B7|-1073450825|DTS_E_EXPREVALILLEGALHEXESCAPEINSTRINGLITERAL|The string literal "%1" contains an illegal hexadecimal escape sequence of  "\x%2". The escape sequence is not supported in string literals in the expression evaluator. The hexadecimal escape sequences must be of the form \xhhhh where h is a valid hexadecimal digit.|  
|0xC00470B8|-1073450824|DTS_E_EXPREVALILLEGALESCAPEINSTRINGLITERAL|The string literal "%1" contains an illegal escape sequence of "\\%2!c!". The escape sequence is not supported in string literals in the expression evaluator. If a backslash is needed in the string, use a double backslash, "\\\\".|  
|0xC00470B9|-1073450823|DTS_E_NOOUTPUTCOLUMNS|“%1”不包含输出列。 异步输出必须包含输出列。|  
|0xC00470BA|-1073450822|DTS_E_LOBDATATYPENOTSUPPORTED|“%1”的长对象数据类型为 DT_TEXT、DT_NTEXT 或 DT_IMAGE，不支持该对象数据类型。|  
|0xC00470BB|-1073450821|DTS_E_OUTPUTWITHMULTIPLEERRORS|为输出 ID %1!d! 提供了多个错误输出配置， 首先提供了 %2!d! 和 %3!d!，然后又提供了 %4!d! 和 %5!d!。|  
|0xC00470BC|-1073450820|DTS_E_FAILEDDURINGOLEDBDATATYPECONVERSIONCHECK|OLE DB 访问接口在为“%1”进行数据类型转换验证时失败。|  
|0xC00470BD|-1073450819|DTS_E_BUFFERISEOR|此缓冲区表示行集的结尾，其行计数无法更改。  尝试对一个带有行集结尾标志的缓冲区调用 AddRow 或 RemoveRow。|  
|0xC00470BE|-1073450818|DTS_E_EXPREVALUNSUPPORTEDTYPE|表达式中不支持数据类型“%1”。 不支持指定的类型或该类型无效。|  
|0xC00470BF|-1073450817|DTS_E_PRIMEOUTPUTNOEOR|“%1”上的 PrimeOutput 方法返回成功消息，但是没有报告行集的结尾。 组件中存在错误。 它应该报告行结尾。 管道将关闭，以免出现意外结果。|  
|0xC00470C0|-1073450816|DTS_E_EXPREVALDATACONVERSIONOVERFLOW|从数据类型“%1”转换为数据类型“%2”时发生溢出。 源类型相对于目标类型而言太大。|  
|0xC00470C1|-1073450815|DTS_E_EXPREVALDATACONVERSIONNOTSUPPORTED|不支持从数据类型“%1”转换为数据类型“%2”。 无法将源类型转换为目标类型。|  
|0xC00470C2|-1073450814|DTS_E_EXPREVALDATACONVERSIONFAILED|尝试从数据类型 %2 转换为数据类型 %3 时出现错误代码 0x%1!8.8X! 。|  
|0xC00470C3|-1073450813|DTS_E_EXPREVALCONDITIONALOPERATIONFAILED|条件运算“%1”失败，错误代码为 0x%2!8.8X!。 发生了内部错误或内存不足错误。|  
|0xC00470C4|-1073450812|DTS_E_EXPREVALCASTFAILED|将表达式“%1”从数据类型“%2”转换为数据类型“%3”失败，错误代码为 0x%4!8.8X!。|  
|0xC00470C5|-1073450811|DTS_E_EXPREVALFUNCTIONCOMPUTEFAILED|对函数“%1”求值失败，错误代码为 0x%2!8.8X!。|  
|0xC00470C6|-1073450810|DTS_E_EXPREVALFUNCTIONCONVERTPARAMTOMEMBERFAILED|函数 NULL 中数据类型为“%2”的参数 %1!d! 转换为静态值。|  
|0xC00470C7|-1073450809|DTS_E_REDIRECTROWUNAVAILABLEWITHFASTLOADANDZEROMAXINSERTCOMMITSIZE|当启用了快速加载选项而最大插入提交大小设置为零时，不能将“%1”的错误行处理设置为重定向行。|  
|0xC00470CE|-1073450802|DTS_E_EXPREVALBINARYOPERATORCODEPAGEMISMATCH|对于“%2”类型的二元运算符“%1”的操作数，它们的代码页必须匹配。 左操作数的代码页和右操作数的代码页当前不匹配。 对于指定类型的指定二元运算符，代码页必须相同。|  
|0xC00470CF|-1073450801|DTS_E_EXPREVALVARIABLECOMPUTEFAILED|检索变量“%1”的值失败，错误代码为 0x%2!8.8X!。|  
|0xC00470D0|-1073450800|DTS_E_EXPREVALVARIABLETYPENOTSUPPORTED|表达式中不支持变量“%1”的数据类型。|  
|0xC00470D1|-1073450799|DTS_E_EXPREVALCASTCODEPAGEMISMATCH|无法将表达式“%1”从数据类型“%2”转换为数据类型“%3”，因为要转换的值的代码页(%4!d!)与请求的结果代码页(%5!d!)不匹配。 源的代码页必须与目标请求的代码页匹配。|  
|0xC00470D2|-1073450798|DTS_E_BUFFERSIZEOUTOFRANGE|默认缓冲区的大小必须介于 %1!d! 和 %2!d! 个字节的结果值。 试图将 DefaultBufferSize 属性设置为一个太小或太大的值。|  
|0xC00470D3|-1073450797|DTS_E_BUFFERMAXROWSIZEOUTOFRANGE|默认的缓冲区最大行数必须大于 %1!d! 行。 试图将 DefaultBufferMaxRows 属性设置为一个太小的值。|  
|0xC00470D4|-1073450796|DTS_E_EXTERNALCOLUMNMETADATACODEPAGEMISMATCH|%1 的代码页为 %2!d!， 应当为 %3!d!。|  
|0xC00470D5|-1073450795|DTS_E_THREADCOUNTOUTOFRANGE|无法将 %3!d! 分配给数据流任务的 EngineThreads 属性。 该值必须介于 %1!d! 和 %2!d! 之间。|  
|0xC00470D6|-1073450794|DTS_E_EXPREVALINVALIDTOKENSINGLEQUOTE|分析表达式“%1”失败。 第“%2”行的第“%3”个字符处不应有单引号。|  
|0xC00470D7|-1073450793|DTS_E_EXPREVALINVALIDTOKENSINGLEEQUAL|分析表达式“%1”失败。 第“%2”行的第“%3”个字符处不应有等号(=)。 在指定位置处可能需要一个双等号(==)。|  
|0xC00470DA|-1073450790|DTS_E_INDIVIDUALPUTREFTRACKERFAILED|组件“%1”无法缓存运行时对象引用跟踪器集合，返回的错误代码是 0x%2!8.8X!。|  
|0xC00470DB|-1073450789|DTS_E_EXPREVALAMBIGUOUSINPUTCOLUMNNAME|有多个名为“%1”的输入列。 必须以 [组件名称].[%2] 形式唯一指定所需的输入列或按沿袭 ID 引用所需的输入列。 当前在多个组件上存在指定的输入列。|  
|0xC00470DC|-1073450788|DTS_E_EXPREVALDOTTEDINPUTCOLUMNNAMENOTFOUND|查找名为“[%1].[%2]”的输入列失败，错误代码为 0x%3!8.8X!。 在输入列集合中找不到此输入列。|  
|0xC00470DD|-1073450787|DTS_E_EXPREVALAMBIGUOUSVARIABLENNAME|有多个名为“%1”的变量。 必须将所需变量唯一指定为 \@[Namespace::%2]。 多个命名空间中存在该变量。|  
|0xC00470DE|-1073450786|DTS_E_REDUCTIONFAILED|数据流引擎计划程序无法缩减管道的执行计划。 请将 OptimizedMode 属性设置为 False。|  
|0xC00470DF|-1073450785|DTS_E_EXPREVALSQRTINVALIDPARAM|函数 SQRT 无法对负值进行运算，但传递给 SQRT 函数的却是负值。|  
|0xC00470E0|-1073450784|DTS_E_EXPREVALLNINVALIDPARAM|函数 LN 无法对零或负值进行运算，但传递给 LN 函数的却是零或负值。|  
|0xC00470E1|-1073450783|DTS_E_EXPREVALLOGINVALIDPARAM|函数 LOG 无法对零或负值进行运算，但传递给 LOG 函数的却是零或负值。|  
|0xC00470E2|-1073450782|DTS_E_EXPREVALPOWERINVALIDPARAM|无法计算传递给函数 POWER 的参数，计算出的结果不确定。|  
|0xC00470E3|-1073450781|DTS_E_NOCANCELEVENT|由于出现错误 0x%1!8.8X!，运行库无法提供取消事件。|  
|0xC00470E4|-1073450780|DTS_E_CANCELRECEIVED|管道接收到一个取消请求，正在关闭。|  
|0xC00470E5|-1073450779|DTS_E_EXPREVALUNARYOPOVERFLOW|一元负运算(求反运算)“%1”的结果超出了结果数据类型“%2”的最大大小。 运算结果的大小溢出了结果类型。|  
|0xC00470E6|-1073450778|DTS_E_EXPREVALPLACEHOLDERINEXPRESSION|在表达式中找到占位符“%1”。 必须将其替换为实参或操作数。|  
|0xC00470E7|-1073450777|DTS_E_EXPREVALFNRIGHTINVALIDLENGTH|长度 %1!d! 为负数，这是无效的。 长度参数必须是正数。|  
|0xC00470E8|-1073450776|DTS_E_EXPREVALFNREPLICATEINVALIDREPEATCOUNT|重复计数 %1!d! 是负数，这对函数“%2”无效。 重复计数参数不能为负数。|  
|0xC00470EA|-1073450774|DTS_E_EXPREVALVARIABLECOULDNOTBEREAD|读取变量“%1”失败，错误代码为 0x%2!8.8X!。|  
|0xC00470EC|-1073450772|DTS_E_EXPREVALBINARYOPDTSTRNOTSUPPORTED|对于二元运算的操作数，只有输入列和转换运算才支持数据类型 DT_STR。 表达式“%1”中有一个既非输入列又非转换结果的 DT_STR 操作数，所以不能用于二元运算。 若要执行此运算，需要使用转换运算符显式转换该操作数。|  
|0xC00470ED|-1073450771|DTS_E_EXPREVALCONDITIONALOPDTSTRNOTSUPPORTED|对于条件运算符的操作数，只有输入列和转换运算才支持数据类型 DT_STR。 表达式“%1”中有一个既非输入列又非转换结果的 DT_STR 操作数，所以不能用于条件运算。 若要执行此运算，需要使用转换运算符显式转换该操作数。|  
|0xC00470EE|-1073450770|DTS_E_EXPREVALFNFINDSTRINGINVALIDOCCURRENCECOUNT|出现计数 %1!d! 对函数“%2”无效。 此参数必须大于零。|  
|0xC00470EF|-1073450769|DTS_E_INDIVIDUALPUTLOGENTRYINFOS|“%1”无法缓存 LogEntryInfos 集合，返回的错误代码为 0x%2!8.8X!。|  
|0xC00470F0|-1073450768|DTS_E_EXPREVALINVALIDDATEPARTNODE|为函数“%1”指定的日期部分参数无效。 它必须是静态字符串。  日期部分参数不能包含输入列之类的动态元素，而且必须是 DT_WSTR 类型。|  
|0xC00470F1|-1073450767|DTS_E_EXPREVALINVALIDCASTLENGTH|值 %1!d! 是负数，这是无效的。 长度必须为正数。|  
|0xC00470F2|-1073450766|DTS_E_EXPREVALINVALIDNULLCODEPAGE|值 %1!d! 为 NULL 函数中数据类型为“%2”的代码页参数指定的值 %1!d! 无效。 计算机上没有安装此代码页。|  
|0xC00470F3|-1073450765|DTS_E_EXPREVALINVALIDNULLPRECISION|值 %1!d! 为 NULL 函数中数据类型为“%2”的精度参数指定的值 %1!d! 超出了范围。 精度必须在 %3!d! 到 %4!d! 的范围内。|  
|0xC00470F4|-1073450764|DTS_E_EXPREVALINVALIDNULLSCALE|值 %1!d! 超出了范围。 小数位数必须在 %3!d! 到 %4!d! 的范围内。 小数位数不得超出精度范围，而且不能为负。|  
|0xC00470F5|-1073450763|DTS_E_EXPREVALINVALIDNULLLENGTH|值 %1!d! 为 "NULL" 函数中数据类型为 %2 的长度参数指定的值 %1!d! 是负数，这是无效的。 长度必须为正数。|  
|0xC00470F6|-1073450762|DTS_E_NEGATIVESNOTALLOWED|不能将负值赋予 %1。|  
|0xC00470F7|-1073450761|DTS_E_FASTPARSENOTALLOWED|“%2”的自定义属性“%1”不能设置为 True。  列数据类型必须是下列类型之一：DT_I1、DT_I2、DT_I4、DT_I8、DT_UI1、DT_UI2、DT_UI4、DT_UI8、DT_DBTIMESTAMP、DT_DBTIMESTAMP2、DT_DBTIMESTAMPOFFSET、DT_DATE、DT_DBDATE、DT_DBTIME、DT_DBTIME2 或 DT_FILETIME。|  
|0xC00470F8|-1073450760|DTS_E_CANNOTREATTACHPATH|不能重新附加“%1”。 请删除路径，添加一个新路径，然后再附加它。|  
|0xC00470F9|-1073450759|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALSINGULAR|函数“%1”需要 %2!d! 个参数，而不是 %3!d! 个参数。 已识别出函数名称，但参数个数无效。|  
|0xC00470FA|-1073450758|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSSINGULARPLURAL|函数“%1”需要 %2!d! 个参数，而不是 %3!d! 个参数。 已识别出函数名称，但参数个数无效。|  
|0xC00470FB|-1073450757|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALPLURAL|函数“%1”需要 %2!d! 个参数，而不是 %3!d! 个参数。 已识别出函数名称，但参数个数无效。|  
|0xC00470FC|-1073450756|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONOUTOFMEMORY|内存不足，无法分析表达式“%1”。|  
|0xC00470FD|-1073450755|DTS_E_INDIVIDUALCHECKPRODUCTLEVELFAILED|%1 无法执行其所需的产品级别检查，返回的错误代码是 0x%2!8.8X!。|  
|0xC00470FE|-1073450754|DTS_E_PRODUCTLEVELTOLOW|SSIS Error Code DTS_E_PRODUCTLEVELTOLOW.  %1 不能在安装的 Integration Services 的 %2 版本上运行。 它要求 %3 或更高版本。|  
|0xC00470FF|-1073450753|DTS_E_EXPREVALSTRINGLITERALTOOLONG|该表达式中的字符串文字超出了允许的最大长度(%1!d! 个字符）。|  
|0xC0047100|-1073450752|DTS_E_EXPREVALSTRINGVARIABLETOOLONG|变量 %1 包含的字符串超出了允许的最大长度(%2!d! 个字符）。|  
|0xC0047101|-1073450751|DTS_E_COMPONENT_NOINTERFACE|找到了 %1，但它不支持所需的 Integration Services 界面(IDTSRuntimeComponent100)。  请从组件提供商处获取该组件的更新版本。|  
|0xC0048000|-1073446912|DTS_E_CANNOTOPENREGISTRYKEY|无法打开注册表项“%1”。|  
|0xC0048001|-1073446911|DTS_E_INVALIDCOMPONENTFILENAME|无法获取 CLSID 为“%1”的组件的文件名。 请确保该组件已正确注册或提供的 CLSID 正确无误。|  
|0xC0048002|-1073446910|DTS_E_UNKNOWNCOMPONENTHASINVALIDCLSID|有一个组件的 CLSID 无效。 请确保管道中所有组件的 CLSID 都有效。|  
|0xC0048003|-1073446909|DTS_E_COMPONENTHASINVALIDCLSID|在 ID 为 %1!d! 的组件中，有一个组件的 CLSID 的列无效。|  
|0xC0048004|-1073446908|DTS_E_INVALIDINDEX|索引无效。|  
|0xC0048005|-1073446907|DTS_E_CANNOTACCESSDTSAPPLICATIONOBJECT|无法访问 Application 对象。 请确保正确安装了 SSIS。|  
|0xC0048006|-1073446906|DTS_E_ERROROCCURREDWHILERETRIEVINGFILENAME|检索组件的文件名失败，错误代码为 0x%1!8.8X!。|  
|0xC0048007|-1073446905|DTS_E_CANNOTRETRIEVEPROPERTYFORCOMPONENT|无法从 ID 为 %2!d! 的组件中检索属性“%1”。|  
|0xC0048008|-1073446904|DTS_E_DUPLICATEIDFOUND|尝试在数据流任务中多次使用 ID %1!d! 。|  
|0xC0048009|-1073446903|DTS_E_CANNOTRETRIEVEBYLINEAGE|无法从不包含列的集合中按沿袭 ID 检索项。|  
|0xC004800B|-1073446901|DTS_E_CANNOTMAPRUNTIMECONNECTIONMANAGER|在连接管理器集合中找不到 ID 为“%1”的连接管理器，错误代码为 0x%2!8.8X!。 “%3”要求连接管理器集合“%4”中存在该连接管理器。 请确保已使用该 ID 在连接管理器集合 Connections 中创建了一个连接管理器。|  
|0xC004800E|-1073446898|DTS_E_INPUTNOTKNOWN|线程“%1”为输入 %2!d! 接收到一个缓冲区，但此线程不负责该输入。 由于出现错误，数据流引擎计划程序生成了错误的执行计划。|  
|0xC004800F|-1073446897|DTS_E_GETRTINTERFACEFAILED|组件“%1”(%2!d!)无法提供 IDTSRuntimeComponent100 接口。|  
|0xC0048011|-1073446895|DTS_E_CANTGIVEAWAYBUFFER|数据流任务引擎试图复制一个缓冲区以分配另一线程，但没有成功。|  
|0xC0048012|-1073446894|DTS_E_CANTCREATEVIEWBUFFER|数据流任务引擎无法创建类型为 %1!d! 的视图缓冲区来替代类型为 %2!d! 的缓冲区 %3!d。|  
|0xC0048013|-1073446893|DTS_E_UNUSABLETEMPORARYPATH|缓冲区管理器无法在路径“%1”下创建临时文件。 临时存储区将不再考虑使用该路径。|  
|0xC0048014|-1073446892|DTS_E_DIRECTTONONERROROUTPUT|缓冲区管理器试图将一个错误行推送给未注册为错误输出的输出。 对未将 IsErrorOut 属性设置为 TRUE 的输出调用了 DirectErrorRow。|  
|0xC0048015|-1073446891|DTS_E_BUFFERISPRIVATE|对专用缓冲区调用了缓冲区方法，但专用缓冲区不支持此操作。|  
|0xC0048016|-1073446890|DTS_E_BUFFERISFLAT|专用模式缓冲区不支持此操作。|  
|0xC0048017|-1073446889|DTS_E_BUFFERISPRIMEOUTPUT|不能对传递给 PrimeOutput 的缓冲区调用此操作。 PrimeOutput 执行期间调用了缓冲区方法，但在 PrimeOutput 期间不允许进行此调用。|  
|0xC0048018|-1073446888|DTS_E_BUFFERISPROCESSINPUT|不能对传递给 ProcessInput 的缓冲区调用此操作。 ProcessInput 执行期间调用了缓冲区方法，但在 ProcessInput 期间不允许进行此调用。|  
|0xC0048019|-1073446887|DTS_E_BUFFERGETTEMPFILENAME|缓冲区管理器无法获取临时文件名。|  
|0xC004801A|-1073446886|DTS_E_REFERENCECOLUMNTOOWIDE|代码遇到的列太宽。|  
|0xC004801B|-1073446885|DTS_E_CANNOTGETRUNTIMECONNECTIONMANAGERID|无法在“%2”的连接管理器集合 Connections 中获取由“%1”指定的运行时连接管理器的 ID，错误代码为 0x%3!8.8X!。 请确保已为该组件设置了运行时连接对象的 ConnectionManager.ID 属性。|  
|0xC004801C|-1073446884|DTS_E_EMPTYRUNTIMECONNECTIONMANAGERID|“%2”的连接管理器集合 Connections 中的“%1”没有 ID 属性值。 请确保已为该组件设置了运行时连接对象的 ConnectionManagerID 属性。|  
|0xC004801D|-1073446883|DTS_E_METADATAREADONLY|执行期间无法更改元数据。|  
|0xC004801F|-1073446881|DTS_E_UPGRADEFAILED|无法将“%1”的组件元数据升级为组件的更新版本。 PerformUpgrade 方法失败。|  
|0xC0048020|-1073446880|DTS_E_COMPONENTVERSIONMISMATCH|%1 的版本与 DataFlow 的这一版本不兼容。|  
|0xC0048021|-1073446879|DTS_E_ERRORCOMPONENT|该组件不存在、未注册、不可升级或缺少所需接口。 该组件的联系信息是“%1”。|  
|0xC0048022|-1073446878|DTS_E_BUFFERISNOTPRIMEOUTPUT|对错误的缓冲区调用了该方法。 未用于组件输出的缓冲区不支持此操作。|  
|0xC0049014|-1073442796|DTS_E_EXPREVALSTATIC_COMPUTATIONFAILED|计算表达式时出错。|  
|0xC0049030|-1073442768|DTS_E_EXPREVALSTATIC_DIVBYZERO|表达式中发生被零除错误。|  
|0xC0049031|-1073442767|DTS_E_EXPREVALSTATIC_LITERALOVERFLOW|文字值太大，请求的类型中容纳不下。|  
|0xC0049032|-1073442766|DTS_E_EXPREVALSTATIC_BINARYOPNUMERICOVERFLOW|二元运算的结果对于数值类型的最大大小来说太大了。 若不降低精度或减少小数位数，就无法将操作数类型隐式转换为数值(DT_NUMERIC)结果。 若要执行此运算，需要使用转换运算符来显式转换两个操作数或其中的一个操作数。|  
|0xC0049033|-1073442765|DTS_E_EXPREVALSTATIC_BINARYOPOVERFLOW|二元运算结果的大小溢出了结果数据类型的最大大小。|  
|0xC0049034|-1073442764|DTS_E_EXPREVALSTATIC_FUNCTIONOVERFLOW|函数调用结果太大，该结果类型中容纳不下，已溢出了操作数类型。 可能需要显式转换为较大的类型。|  
|0xC0049035|-1073442763|DTS_E_EXPREVALSTATIC_BINARYTYPEMISMATCH|使用的数据类型与二元运算符不兼容。 无法将操作数类型隐式转换为与此运算兼容的类型。 若要执行此运算，需要使用转换运算符来显式转换两个操作数或其中的一个操作数。|  
|0xC0049036|-1073442762|DTS_E_EXPREVALSTATIC_UNSUPPORTEDBINARYTYPE|不支持用于某二元运算符的数据类型。 此运算不支持两个操作数或其中一个操作数的类型。 若要执行此运算，需要使用转换运算符来显式转换两个操作数或其中的一个操作数。|  
|0xC0049037|-1073442761|DTS_E_EXPREVALSTATIC_BINARYSIGNMISMATCH|位二元运算符存在符号不匹配的情况。 此运算符的操作数必须同时为正或同时为负。|  
|0xC0049038|-1073442760|DTS_E_EXPREVALSTATIC_BINARYOPERATIONFAILED|二元运算失败。 可能是内存不足，或出现内部错误。|  
|0xC0049039|-1073442759|DTS_E_EXPREVALSTATIC_BINARYOPERATIONSETTYPEFAILED|设置二元运算的结果类型失败。|  
|0xC004903A|-1073442758|DTS_E_EXPREVALSTATIC_STRINGCOMPARISONFAILED|无法比较两个字符串。|  
|0xC004903B|-1073442757|DTS_E_EXPREVALSTATIC_UNSUPPORTEDUNNARYTYPE|不支持用于某一元运算符的数据类型。 此运算不支持该操作数的类型。 若要执行此运算，需要使用转换运算符显式转换该操作数。|  
|0xC004903C|-1073442756|DTS_E_EXPREVALSTATIC_UNARYOPERATIONFAILED|一元运算失败。 可能是内存不足，或出现内部错误。|  
|0xC004903D|-1073442755|DTS_E_EXPREVALSTATIC_UNARYOPERATIONSETTYPEFAILED|设置一元运算的结果类型失败。|  
|0xC004903E|-1073442754|DTS_E_EXPREVALSTATIC_PARAMTYPEMISMATCH|某函数有一个参数属于不支持的数据类型。 无法将该参数的类型隐式转换为与此函数兼容的类型。 若要执行此运算，需要使用转换运算符显式转换该操作数。|  
|0xC004903F|-1073442753|DTS_E_EXPREVALSTATIC_INVALIDFUNCTION|表达式中出现无效的函数名称。 请确保该函数名称正确无误并且确实存在。|  
|0xC0049040|-1073442752|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDLENGTH|长度参数对函数 SUBSTRING 无效。 长度参数不能为负值。|  
|0xC0049041|-1073442751|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDSTARTINDEX|起始索引对函数 SUBSTRING 无效。 起始索引值必须是大于零的整数。 起始索引是从 1 开始的，而不是从 0 开始的。|  
|0xC0049042|-1073442750|DTS_E_EXPREVALSTATIC_INVALIDNUMBEROFPARAMS|为函数提供的参数个数不正确。 已识别出函数名称，但参数个数不正确。|  
|0xC0049043|-1073442749|DTS_E_EXPREVALSTATIC_CHARMAPPINGFAILED|字符映射函数失败。|  
|0xC0049044|-1073442748|DTS_E_EXPREVALSTATIC_INVALIDDATEPART|为日期函数指定了一个无法识别的日期部分参数。|  
|0xC0049045|-1073442747|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAM|为函数 NULL 提供的参数无效。 NULL 的参数必须是静态的，不能包含输入列之类的动态元素。|  
|0xC0049046|-1073442746|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAMTYPE|为函数 NULL 提供的参数无效。 NULL 的参数必须是整数或者可以转换为整数的类型。|  
|0xC0049047|-1073442745|DTS_E_EXPREVALSTATIC_FUNCTIONPARAMNOTSTATIC|为函数提供的参数无效。 此参数必须是静态的，不能包含输入列之类的动态元素。|  
|0xC0049048|-1073442744|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAM|为转换运算提供的参数无效。 转换运算符的参数必须是静态的，不能包含输入列之类的动态元素。|  
|0xC0049049|-1073442743|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAMTYPE|为转换运算提供的参数无效。 转换运算符的参数必须是整数或者可以转换为整数的类型。|  
|0xC004904A|-1073442742|DTS_E_EXPREVALSTATIC_INVALIDCAST|表达式包含一个不支持的类型转换。|  
|0xC004904B|-1073442741|DTS_E_EXPREVALSTATIC_INVALIDTOKEN|表达式包含一个无法识别的标记。 因为表达式中包含无效元素，所以无法对它进行分析。|  
|0xC004904C|-1073442740|DTS_E_EXPREVALSTATIC_FAILEDTOPARSEEXPRESSION|表达式无效，因而无法对它进行分析。 它可能包含无效元素，或者它的格式不正确。|  
|0xC004904D|-1073442739|DTS_E_EXPREVALSTATIC_UNARYOPOVERFLOW|一元负运算(求反运算)的结果溢出了结果数据类型的最大大小。 运算结果的大小溢出了结果类型。|  
|0xC004904E|-1073442738|DTS_E_EXPREVALSTATIC_COMPUTEFAILED|尝试计算表达式失败。|  
|0xC004904F|-1073442737|DTS_E_EXPREVALSTATIC_BUILDSTRINGFAILED|尝试生成表达式的字符串表示形式失败。|  
|0xC0049050|-1073442736|DTS_E_EXPREVALSTATIC_CANNOTCONVERTRESULT|无法将表达式结果数据类型转换为列数据类型。 应将表达式的结果写入输入/输出列，但无法将表达式的数据类型转换为列的数据类型。|  
|0xC0049051|-1073442735|DTS_E_EXPREVALSTATIC_CONDITIONALOPINVALIDCONDITIONTYPE|条件运算符的条件表达式的数据类型无效。 条件表达式的类型必须是 DT_BOOL。|  
|0xC0049052|-1073442734|DTS_E_EXPREVALSTATIC_CONDITIONALOPTYPEMISMATCH|条件运算符的操作数的数据类型不兼容。 无法将操作数类型隐式转换为与此条件运算兼容的类型。 若要执行此运算，需要使用转换运算符来显式转换两个操作数或其中的一个操作数。|  
|0xC0049053|-1073442733|DTS_E_EXPREVALSTATIC_CONDITIONALOPSETTYPEFAILED|设置条件运算的结果类型失败。|  
|0xC0049054|-1073442732|DTS_E_EXPREVALSTATIC_INPUTCOLUMNNAMENOTFOUND|在输入列集合中找不到指定的输入列。|  
|0xC0049055|-1073442731|DTS_E_EXPREVALSTATIC_INPUTCOLUMNIDNOTFOUND|尝试按沿袭 ID 查找输入列失败。 在输入列集合中找不到此输入列。|  
|0xC0049056|-1073442730|DTS_E_EXPREVALSTATIC_NOINPUTCOLUMNCOLLECTION|表达式包含一个无法识别的标记，它似乎是输入列引用，但没有可用于处理输入列的输入列集合。 未向表达式计算器提供输入列集合，但表达式中包含输入列。|  
|0xC0049057|-1073442729|DTS_E_EXPREVALSTATIC_VARIABLENOTFOUND|在集合中找不到指定的变量。 它可能不在正确的作用域内。 请确保该变量确实存在，并且其作用域正确无误。|  
|0xC0049058|-1073442728|DTS_E_EXPREVALSTATIC_INVALIDTOKENSTATE|尝试分析表达式失败。 该表达式包含一个无效或不完整的标记。 它可能包含无效元素，可能缺少某个必需元素的一部分(如右括号)，也可能格式不正确。|  
|0xC0049059|-1073442727|DTS_E_EXPREVALSTATIC_INVALIDCASTCODEPAGE|在向数据类型 DT_STR 或 DT_TEXT 转换时，为转换运算的代码页参数指定的值无效。 计算机上没有安装指定的代码页。|  
|0xC004905A|-1073442726|DTS_E_EXPREVALSTATIC_INVALIDCASTPRECISION|为转换运算的精度参数指定的值超出了类型转换的范围。|  
|0xC004905B|-1073442725|DTS_E_EXPREVALSTATIC_INVALIDCASTSCALE|为转换运算的小数位数参数指定的值超出了类型转换的范围。 小数位数不得超出精度范围，而且不能为负。|  
|0xC004905C|-1073442724|DTS_E_EXPREVALSTATIC_CONDITIONALOPCODEPAGEMISMATCH|条件运算中的代码页不匹配。 左操作数的代码页与右操作数的代码页不匹配。 对于该类型的条件运算符，代码页必须相同。|  
|0xC004905D|-1073442723|DTS_E_EXPREVALSTATIC_ILLEGALHEXESCAPEINSTRINGLITERAL|字符串文字包含非法的十六进制转义序列。 表达式计算器中的字符串文字不支持此转义序列。 十六进制转义序列的格式必须是 \xhhhh，其中 h 是有效的十六进制数字。|  
|0xC004905E|-1073442722|DTS_E_EXPREVALSTATIC_ILLEGALESCAPEINSTRINGLITERAL|字符串文字包含非法的转义序列。 表达式计算器中的字符串文字不支持此转义序列。 如果字符串中需要反斜杠，请使用双反斜杠格式 "\\\\"。|  
|0xC004905F|-1073442721|DTS_E_EXPREVALSTATIC_UNSUPPORTEDTYPE|不支持或无法识别表达式中使用的数据类型。|  
|0xC0049060|-1073442720|DTS_E_EXPREVALSTATIC_DATACONVERSIONOVERFLOW|在不同数据类型之间转换时发生溢出。 源类型太大，目标类型中容纳不下。|  
|0xC0049061|-1073442719|DTS_E_EXPREVALSTATIC_DATACONVERSIONNOTSUPPORTED|表达式包含不支持的数据类型转换。 无法将源类型转换为目标类型。|  
|0xC0049062|-1073442718|DTS_E_EXPREVALSTATIC_DATACONVERSIONFAILED|试图执行数据转换时出错。 无法将源类型转换为目标类型。|  
|0xC0049063|-1073442717|DTS_E_EXPREVALSTATIC_CONDITIONALOPERATIONFAILED|条件运算失败。|  
|0xC0049064|-1073442716|DTS_E_EXPREVALSTATIC_CASTFAILED|尝试执行类型转换时出错。|  
|0xC0049065|-1073442715|DTS_E_EXPREVALFAILEDTOCONVERTSTRCOLUMNTOWSTR|将“%1”从类型 DT_STR 转换为类型 DT_WSTR 失败，其错误代码为 0x%2!8.8X!。 在对输入列执行隐式转换时出错。|  
|0xC0049066|-1073442714|DTS_E_EXPREVALSTATIC_FAILEDTOCONVERTSTRCOLUMNTOWSTR|将输入列从类型 DT_STR 转换为类型 DT_WSTR 失败。 在对输入列执行隐式转换时出错。|  
|0xC0049067|-1073442713|DTS_E_EXPREVALSTATIC_FUNCTIONCOMPUTEFAILED|对函数求值时出错。|  
|0xC0049068|-1073442712|DTS_E_EXPREVALSTATIC_FUNCTIONCONVERTPARAMTOMEMBERFAILED|无法将函数参数转换为静态值。 此参数必须为静态参数并且不能包含动态元素(如输入列)。|  
|0xC0049088|-1073442680|DTS_E_EXPREVALSTATIC_FNRIGHTINVALIDLENGTH|长度参数对于函数 RIGHT 无效。 长度参数不能为负值。|  
|0xC0049089|-1073442679|DTS_E_EXPREVALSTATIC_FNREPLICATEINVALIDREPEATCOUNT|重复计数参数对于函数 REPLICATE 无效。 此参数不能为负。|  
|0xC0049096|-1073442666|DTS_E_EXPREVALSTATIC_BINARYOPERATORCODEPAGEMISMATCH|二元运算中的代码页不匹配。 左操作数的代码页与右操作数的代码页不匹配。 对于此二元运算，代码页必须相同。|  
|0xC0049097|-1073442665|DTS_E_EXPREVALSTATIC_VARIABLECOMPUTEFAILED|检索变量的值失败。|  
|0xC0049098|-1073442664|DTS_E_EXPREVALSTATIC_VARIABLETYPENOTSUPPORTED|此表达式所包含的变量属于不支持的数据类型。|  
|0xC004909B|-1073442661|DTS_E_EXPREVALSTATIC_CASTCODEPAGEMISMATCH|由于被转换值的代码页与请求结果的代码页不匹配，无法转换此表达式。 源的代码页必须与目标请求的代码页匹配。|  
|0xC004909C|-1073442660|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEQUOTE|此表达式包含意外的单引号。 应使用双引号。|  
|0xC004909D|-1073442659|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEEQUAL|此表达式包含意外的等号(=)。 通常在需要两个等号(==)时发生此错误。|  
|0xC00490AA|-1073442646|DTS_E_EXPREVALSTATIC_AMBIGUOUSINPUTCOLUMNNAME|指定的输入列名称不明确。  必须以 [组件名称].[列名] 形式限定列或使用沿袭 ID 引用列。 当多个组件中存在输入列时将发生此错误，此时，必须加上组件名称或使用沿袭 ID 以示区别。|  
|0xC00490AB|-1073442645|DTS_E_EXPREVALSTATIC_PLACEHOLDERINEXPRESSION|表达式中存在占位符函数参数或操作数。 应使用实参或操作数进行替换。|  
|0xC00490AC|-1073442644|DTS_E_EXPREVALSTATIC_AMBIGUOUSVARIABLENNAME|指定的变量名称不明确。 必须将所需变量限定为 \@[Namespace::Variable]。 当多个命名空间中存在该变量时将发生此错误。|  
|0xC00490D3|-1073442605|DTS_E_EXPREVALSTATIC_BINARYOPDTSTRNOTSUPPORTED|对于二元运算的操作数，只有输入列和转换运算才支持数据类型 DT_STR。 如果 DT_STR 操作数不是输入列或转换结果，则不能用于二元运算。 若要执行此运算，需要使用转换运算符显式转换该操作数。|  
|0xC00490D4|-1073442604|DTS_E_EXPREVALSTATIC_CONDITIONALOPDTSTRNOTSUPPORTED|对于条件运算符的操作数，只有输入列和转换运算才支持数据类型 DT_STR。 如果 DT_STR 操作数不是输入列或转换结果，则不能用于条件运算。 若要执行此运算，需要使用转换运算符显式转换该操作数。|  
|0xC00490D5|-1073442603|DTS_E_EXPREVALSTATIC_FNFINDSTRINGINVALIDOCCURRENCECOUNT|出现计数参数对函数 FINDSTRING 无效。 此参数必须大于零。|  
|0xC00490DD|-1073442595|DTS_E_EXPREVALSTATIC_INVALIDDATEPARTNODE|为日期函数指定的“日期部分”参数无效。 “日期部分”参数必须为静态字符串，并且不能包含动态元素(如输入列)。 这些参数必须属于类型 DT_WSTR。|  
|0xC00490DE|-1073442594|DTS_E_EXPREVALSTATIC_INVALIDCASTLENGTH|为转换运算的长度参数指定的值无效。 长度必须为正数。 但为类型转换指定的长度为负值。 请将其更改为正值。|  
|0xC00490DF|-1073442593|DTS_E_EXPREVALSTATIC_INVALIDNULLLENGTH|为 NULL 函数的长度参数指定的值无效。 长度必须为正数。 但为 NULL 函数指定的长度为负值。 请将其更改为正值。|  
|0xC00490E0|-1073442592|DTS_E_EXPREVALSTATIC_INVALIDNULLCODEPAGE|为 NULL 函数的代码页参数(数据类型为 DT_STR 或 DT_TEXT)指定的值无效。 计算机上未安装指定的代码页。 请更改指定的代码页或在计算机上安装此代码页。|  
|0xC00490E1|-1073442591|DTS_E_EXPREVALSTATIC_INVALIDNULLPRECISION|为 NULL 函数的精度参数指定的值无效。 指定的精度超出了 NULL 函数所适用的范围。|  
|0xC00490E2|-1073442590|DTS_E_EXPREVALSTATIC_INVALIDNULLSCALE|为 NULL 函数的小数位数参数指定的值无效。 指定的小数位数超出了 NULL 函数所适用的范围。 小数位数不能超过指定的精度且必须为正值。|  
|0xC00490E8|-1073442584|DTS_E_XMLSRCERRORSETTINGERROROUTPUTCOLUMNDATA|%1 试图将数据写入 %3 上的 %2，但失败。 %4|  
|0xC00490F5|-1073442571|DTS_E_TXLOOKUP_CANCEL_REQUESTED|查找转换收到了用户的取消请求。|  
|0xC00490F6|-1073442570|DTS_E_LOBLENGTHLIMITEXCEEDED|由于达到 4 GB 的限制，已停止处理字符或二进制大型对象 (LOB) 数据。|  
|0xC00490F7|-1073442569|DTS_E_CANNOTLOADCOMPONENT|无法加载托管管道组件“%1”。  异常是: %2。|  
|0xC00F9304|-1072721148|DTS_E_OLEDB_EXCEL_NOT_SUPPORTED|SSIS 错误代码 DTS_E_OLEDB_EXCEL_NOT_SUPPORTED:SSIS 的 64 位版本不支持 Excel 连接管理器，因为没有可用的 OLE DB 提供程序。|  
|0xC00F9310|-1072721136|DTS_E_CACHEBADHEADER|缓存文件损坏，或文件不是使用缓存连接管理器创建的。  请提供一个有效的缓存文件。|  
|0xC0202001|-1071636479|DTS_E_MISSINGSQLCOMMAND|SQL 命令的设置不正确。 请检查 SQLCommand 属性。|  
|0xC0202002|-1071636478|DTS_E_COMERROR|已获得 COM 错误对象信息。  源:“%1” 错误代码:0x%2!8.8X!  说明:“%3”。|  
|0xC0202003|-1071636477|DTS_E_ACQUIREDCONNECTIONUNAVAILABLE|无法访问获取的连接。|  
|0xC0202004|-1071636476|DTS_E_INCORRECTCOLUMNCOUNT|列数不正确。|  
|0xC0202005|-1071636475|DTS_E_COLUMNNOTFOUND|在数据源中找不到列“%1”。|  
|0xC0202007|-1071636473|DTS_E_OLEDBRECORD|已获得 OLE DB 记录。  源:“%1” 结果:0x%2!8.8X!  说明:“%3”。|  
|0xC0202009|-1071636471|DTS_E_OLEDBERROR|SSIS 错误代码 DTS_E_OLEDBERROR。  出现 OLE DB 错误。 错误代码:0x%1!8.8X!。|  
|0xC020200A|-1071636470|DTS_E_ALREADYCONNECTED|组件已连接。 若要连接此组件，需要先断开其连接。|  
|0xC020200B|-1071636469|DTS_E_INCORRECTSTOCKPROPERTYVALUE|属性“%1”的值不正确。|  
|0xC020200E|-1071636466|DTS_E_CANNOTOPENDATAFILE|无法打开数据文件“%1”。|  
|0xC0202010|-1071636464|DTS_E_DESTINATIONFLATFILEREQUIRED|未提供目标平面文件名。 请确保使用连接字符串配置平面文件连接管理器。 如果有多个组件使用此平面文件连接管理器，请确保连接字符串包含足够多的文件名。|  
|0xC0202011|-1071636463|DTS_E_TEXTQUALIFIERNOTFOUND|找不到列“%1”的文本限定符。|  
|0xC0202014|-1071636460|DTS_E_CANNOTCONVERTTYPES|不支持将“%1”转换为“%2”。|  
|0xC0202015|-1071636459|DTS_E_PROBLEMDETECTINGTYPECOMPATIBILITY|在验证从 %2 到 %3 的类型转换时返回错误代码 0x%1!8.8X! 。|  
|0xC0202016|-1071636458|DTS_E_CANNOTMAPINPUTCOLUMNTOOUTPUTCOLUMN|找不到“%2”所需的沿袭 ID 为“%1!d!” 的输入列。 请检查输出列的 SourceInputColumnLineageID 自定义属性。|  
|0xC0202017|-1071636457|DTS_E_INCORRECTMINIMUMNUMBEROFOUTPUTS|输出个数不正确。 至少应该有 %1!d! 个输出。|  
|0xC0202018|-1071636456|DTS_E_INCORRECTEXACTNUMBEROFOUTPUTS|输出个数不正确。 应该正好有 %1!d! 个输出。|  
|0xC0202019|-1071636455|DTS_E_STRINGCONVERSIONTOOLONG|字符串太长，无法转换。|  
|0xC020201A|-1071636454|DTS_E_INCORRECTEXACTNUMBEROFINPUTS|输入个数不正确。 应该正好有 %1!d! 个输入。|  
|0xC020201B|-1071636453|DTS_E_CANNOTHAVEZEROINPUTCOLUMNS|%1 的输入列数不能为零。|  
|0xC020201C|-1071636452|DTS_E_CANNOTHAVEINPUTS|此组件有 %1!d! 个输入。  此组件不允许有输入。|  
|0xC020201D|-1071636451|DTS_E_PROCESSINPUTCALLEDWITHINVALIDINPUTID|调用 ProcessInput 所使用的输入 ID %1!d! 无效。|  
|0xC020201F|-1071636449|DTS_E_INCORRECTCUSTOMPROPERTYTYPE|自定义属性“%1”应属于类型 %2。|  
|0xC0202020|-1071636448|DTS_E_INVALIDBUFFERTYPE|缓冲区类型无效。 请确保管道布局和所有组件都通过验证。|  
|0xC0202021|-1071636447|DTS_E_INCORRECTCUSTOMPROPERTYVALUE|自定义属性“%1”的值不正确。|  
|0xC0202022|-1071636446|DTS_E_CONNECTIONREQUIREDFORMETADATA|由于未建立连接而出错。 请求元数据时必须建立连接。 如果正在脱机工作，请取消选中“SSIS”菜单上的“脱机工作”，以启用该连接。|  
|0xC0202023|-1071636445|DTS_E_CANTCREATECUSTOMPROPERTY|无法创建自定义属性“%1”。|  
|0xC0202024|-1071636444|DTS_E_CANTGETCUSTOMPROPERTYCOLLECTION|无法检索自定义属性集合以进行初始化。|  
|0xC0202025|-1071636443|DTS_E_CANNOTCREATEACCESSOR|无法创建 OLE DB 取值函数。 请查看列元数据是否有效。|  
|0xC0202026|-1071636442|DTS_E_PRIMEOUTPUTCALLEDWITHINVALIDOUTPUTID|调用 PrimeOutput 所使用的输出 ID %1!d! 无效。|  
|0xC0202027|-1071636441|DTS_E_INCORRECTSTOCKPROPERTY|“%2”的属性“%1”的值无效。|  
|0xC0202028|-1071636440|DTS_E_CONNECTIONREQUIREDFORREAD|需要建立连接才能读取数据。|  
|0xC020202C|-1071636436|DTS_E_ERRORWHILEREADINGHEADERROWS|读取标题行时出错。|  
|0xC020202D|-1071636435|DTS_E_DUPLICATECOLUMNNAME|列名“%1”重复。|  
|0xC0202030|-1071636432|DTS_E_CANNOTGETCOLUMNNAME|无法获取 ID 为 %1!d! 的列的名称。|  
|0xC0202031|-1071636431|DTS_E_CANTDIRECTROW|无法将行定向到输出“%1”(%2!d!)。|  
|0xC020203A|-1071636422|DTS_E_CANNOTCREATEBULKINSERTHREAD|由于出现错误“%1”，无法创建大容量插入线程。|  
|0xC020203B|-1071636421|DTS_E_BULKINSERTHREADINITIALIZATIONFAILED|无法初始化 SSIS 大容量插入任务的线程。|  
|0xC020203E|-1071636418|DTS_E_BULKINSERTTHREADALREADYRUNNING|SSIS 大容量插入任务的线程已在运行。|  
|0xC020203F|-1071636417|DTS_E_BULKINSERTTHREADABNORMALCOMPLETION|SSIS 大容量插入任务的线程已因出现错误或警告而终止。|  
|0xC0202040|-1071636416|DTS_E_CANNOTGETIROWSETFASTLOAD|无法打开“%1”的 fastload 行集。 请检查数据库中是否存在此对象。|  
|0xC0202041|-1071636415|DTS_E_CONNECTREQUIREDFORMETADATAVALIDATION|由于未建立连接导致出错。 必须先建立连接才能继续验证元数据。|  
|0xC0202042|-1071636414|DTS_E_DESTINATIONTABLENAMENOTPROVIDED|未提供目标表名。|  
|0xC0202043|-1071636413|DTS_E_ICONVERTTYPEUNAVAILABLE|OLE DB 适配器使用的 OLE DB 访问接口不支持 IConvertType。 请将此适配器的 ValidateColumnMetaData 属性设置为 FALSE。|  
|0xC0202044|-1071636412|DTS_E_OLEDBPROVIDERDATATYPECONVERSIONUNSUPPORTED|OLE DB 适配器使用的 OLE DB 访问接口无法在“%3”的类型“%1”和“%2”之间进行转换。|  
|0xC0202045|-1071636411|DTS_E_VALIDATECOLUMNMETADATAFAILED|验证列元数据失败。|  
|0xC0202047|-1071636409|DTS_E_ATTEMPTINGTOINSERTINTOAROWIDCOLUMN|“%1”是行 ID 列，不能包含在数据插入操作中。|  
|0xC0202048|-1071636408|DTS_E_ATTEMPTINGTOINSERTINTOAROWVERCOLUMN|正在尝试在行版本列“%1”中插入数据。 无法在行版本列中插入数据。|  
|0xC0202049|-1071636407|DTS_E_ATTEMPTINGTOINSERTINTOAREADONLYCOLUMN|无法在只读列“%1”中插入数据。|  
|0xC020204A|-1071636406|DTS_E_UNABLETORETRIEVECOLUMNINFO|无法在数据源中检索列信息。 请确保数据库中存在目标表。|  
|0xC020204B|-1071636405|DTS_E_CANTLOCKBUFFER|无法锁定缓冲区。 系统内存不足或缓冲区管理器已达到其配额。|  
|0xC020204C|-1071636404|DTS_E_INVALIDCOMPARISONFLAGS|%1 的 ComparisonFlags 属性包含其他值为 %2!d! 的标志。|  
|0xC020204D|-1071636403|DTS_E_COLUMNMETADATAUNAVAILABLEFORVALIDATION|列元数据无法用于验证。|  
|0xC0202053|-1071636397|DTS_E_CANNOTWRITETODATAFILE|无法写入数据文件。|  
|0xC0202055|-1071636395|DTS_E_COLUMNDELIMITERNOTFOUND|找不到列“%1”的列分隔符。|  
|0xC0202058|-1071636392|DTS_E_COLUMNPARSEFAILED|无法分析数据文件中的列“%1”。|  
|0xC020205A|-1071636390|DTS_E_RAWFILENAMEREQUIRED|未正确指定文件名。  请通过以下方式指定原始文件的路径和名称: 直接在 FileName 属性中指定或在 FileNameVariable 属性中指定一个变量。|  
|0xC020205B|-1071636389|DTS_E_RAWFILECANTOPEN|无法打开文件“%1”进行写操作。 当没有文件权限或磁盘已满时会发生此错误。|  
|0xC020205C|-1071636388|DTS_E_RAWFILECANTBUFFER|无法为输出文件创建 I/O 缓冲区。 当没有文件权限或磁盘已满时会发生此错误。|  
|0xC020205D|-1071636387|DTS_E_RAWCANTWRITE|无法在文件“%2”中写入 %1!d! 个字节。 有关详细信息，请参阅前面的错误消息。|  
|0xC020205E|-1071636386|DTS_E_RAWBADHEADER|文件头中存在错误的元数据。 此文件已损坏或不是 SSIS 生成的原始数据文件。|  
|0xC020205F|-1071636385|DTS_E_RAWEXISTSCREATEONCE|由于输出文件已存在且 WriteOption 设置为 Create Once (创建一次)，导致出错。 请将 WriteOption 属性设置为 Create Always (始终创建)或删除该文件。|  
|0xC0202060|-1071636384|DTS_E_RAWCANTAPPENDTRUNCATE|由于属性设置存在冲突而出错。 AllowAppend 属性和 ForceTruncate 属性都被设置为 TRUE。 这两个属性不能同时设置为 TRUE。 请将其中一个属性设置为 FALSE。|  
|0xC0202061|-1071636383|DTS_E_RAWBADVERSION|文件的版本和标志信息错误。 此文件已损坏或不是 SSIS 生成的原始数据文件。|  
|0xC0202062|-1071636382|DTS_E_RAWVERSIONINCOMPATIBLEAPPEND|写入输出文件所使用的版本不兼容，因而无法追加。 此文件的格式较旧，已不再使用。|  
|0xC0202064|-1071636380|DTS_E_RAWMETADATAMISMATCH|由于现有文件中没有列与输入的列“%1”相匹配，因此无法追加输出文件。 旧文件在元数据中不匹配。|  
|0xC0202065|-1071636379|DTS_E_RAWMETADATACOUNTMISMATCH|由于输出文件的列数与此目标的列数不匹配，无法追加输出文件。 旧文件在元数据中不匹配。|  
|0xC0202067|-1071636377|DTS_E_ERRORRETRIEVINGCOLUMNCODEPAGE|检索列代码页信息时出错。|  
|0xC0202068|-1071636376|DTS_E_RAWCANTREAD|无法从文件“%2”读取 %1!d! 个字节时遇到意外的文件结束。 失败的原因以前应报告过。|  
|0xC0202069|-1071636375|DTS_E_RAWUNEXPECTEDEOF|从文件“%2”读取 %1!d! 个字节时遇到意外的文件结束。 由于文件格式无效，文件过早结束。|  
|0xC020206A|-1071636374|DTS_E_RAWNOLONGTYPES|无法使用列 %1。 原始适配器不支持 image、text 或 ntext 数据。|  
|0xC020206B|-1071636373|DTS_E_RAWUNEXPECTEDTYPE|适配器遇到无法识别的数据类型 %1!d!。 其原因可能是输入文件(源)损坏或缓冲区类型(目标)无效。|  
|0xC020206C|-1071636372|DTS_E_RAWSTRINGTOOLONG|字符串太长。 适配器读取的字符串长度为 %1!d! 个字节，而字符串长度不应超过 %2!d! 个字节，偏移量为 %3!d!。 这表明输入文件已损坏。 该文件显示的字符串长度超出缓冲区列的最大长度。|  
|0xC020206E|-1071636370|DTS_E_RAWSKIPFAILED|由于存在沿袭 ID 为 %3!d! 的未被引用列“%2”，原始适配器试图跳过输入文件中的 %1!d! 个字节，但出现错误。 从操作系统返回的错误以前应报告过。|  
|0xC020206F|-1071636369|DTS_E_RAWREADFAILED|由于存在沿袭 ID 为 %3!d! 的列“%2”，原始适配器试图读取输入文件中的 %1!d! 个字节，但出现错误。 从操作系统返回的错误以前应报告过。|  
|0xC0202070|-1071636368|DTS_E_RAWFILENAMEINVALID|文件名属性无效。 文件名是设备或包含无效字符。|  
|0xC0202071|-1071636367|DTS_E_BULKINSERTAPIPREPARATIONFAILED|无法准备 SSIS 大容量插入以插入数据。|  
|0xC0202072|-1071636366|DTS_E_INVALIDDATABASEOBJECTNAME|数据库对象名称“%1”无效。|  
|0xC0202073|-1071636365|DTS_E_INVALIDORDERCLAUSE|Order 子句无效。|  
|0xC0202074|-1071636364|DTS_E_RAWFILECANTOPENREAD|无法打开文件“%1”进行读操作。 当没有权限或找不到文件时会发生此错误。 其确切原因在以前的错误消息中曾报告过。|  
|0xC0202075|-1071636363|DTS_E_TIMEGENCANTCREATE|无法创建 Microsoft.AnalysisServices.TimeDimGenerator.TimeDimGenerator。|  
|0xC0202076|-1071636362|DTS_E_TIMEGENCANTCONFIGURE|无法配置 Microsoft.AnalysisServices.TimeDimGenerator。|  
|0xC0202077|-1071636361|DTS_E_TIMEGENCANTCONVERT|不支持列 %1!d! 的数据类型。|  
|0xC0202079|-1071636359|DTS_E_TIMEGENCANTREAD|从 Microsoft.AnalysisServices.TimeDimGenerator 读取失败，错误代码为 0x%1!8.8X!。|  
|0xC020207A|-1071636358|DTS_E_TIMEGENCANTREADCOLUMN|从 Microsoft.AnalysisServices.TimeDimGenerator 读取列“%2!d!” 数据失败，错误代码为 0x%2!8.8X!。|  
|0xC020207B|-1071636357|DTS_E_RSTDESTBADVARIABLENAME|为 VariableName 属性设置的变量名无效。 需要有运行时变量名才能写入。|  
|0xC020207C|-1071636356|DTS_E_RSTDESTRSTCONFIGPROBLEM|无法创建或配置 ADODB.Recordset 对象。|  
|0xC020207D|-1071636355|DTS_E_RSTDESTRSTWRITEPROBLEM|写入 ADODB.Recordset 对象时出错。|  
|0xC020207E|-1071636354|DTS_E_FILENAMEINVALID|该文件名无效。 文件名是设备或包含无效字符。|  
|0xC020207F|-1071636353|DTS_E_FILENAMEINVALIDWITHPARAM|文件名“%1”无效。 文件名是设备或包含无效字符。|  
|0xC0202080|-1071636352|DTS_E_CMDDESTNOPARAMS|无法从 SQL 命令的参数中检索目标列说明。|  
|0xC0202081|-1071636351|DTS_E_CMDDESTNOTBOUND|参数未绑定。 必须将 SQL 命令中的所有参数都绑定到输入列。|  
|0xC0202082|-1071636350|DTS_E_TXPIVOTBADUSAGE|输入列“%1”(%2!d!)的 PivotUsage 值无效。|  
|0xC0202083|-1071636349|DTS_E_TXPIVOTTOOMANYPIVOTKEYS|找到的透视键过多。 只能将一个输入列作为透视键。|  
|0xC0202084|-1071636348|DTS_E_TXPIVOTNOPIVOTKEY|找不到透视键。 必须将一个输入列作为透视键。|  
|0xC0202085|-1071636347|DTS_E_TXPIVOTINPUTALREADYMAPPED|有多个输出列(如“%1”(%2!d!))被映射到输入列“%3”(%4!d!)。|  
|0xC0202086|-1071636346|DTS_E_TXPIVOTCANTMAPPIVOTKEY|输出列“%1”(%2!d!)无法映射到 PivotKey 输入列。|  
|0xC0202087|-1071636345|DTS_E_TXPIVOTCANTMAPPINGNOTFOUND|输出列“%1”(%2!d!) 具有 SourceColumn %3!d!，后者 不是有效的输入列沿袭 ID。|  
|0xC0202088|-1071636344|DTS_E_TXPIVOTEMPTYPIVOTKEYVALUE|输出列“%1”(%2!d!)被映射到透视值输入列，但缺少 PivotKeyValue 属性值。|  
|0xC0202089|-1071636343|DTS_E_TXPIVOTDUPLICATEPIVOTKEYVALUE|输出列“%1”(%2!d!)被映射到透视值输入列，但 PivotKeyValue 属性值不唯一。|  
|0xC020208A|-1071636342|DTS_E_TXPIVOTOUTPUTNOTMAPPED|输入列“%1”(%2!d!)未映射到任何输出列。|  
|0xC020208B|-1071636341|DTS_E_TXPIVOTCANTCOMPARESETKEYS|比较设置键的值时出错。|  
|0xC020208D|-1071636339|DTS_E_TXPIVOTNOBLOB|输入列“%1”(%2!d!)不能作为设置键、透视键或透视值，因为它包含长整型数据。|  
|0xC020208E|-1071636338|DTS_E_TXPIVOTBADOUTPUTTYPE|输出类型不正确。 输出列“%1”(%2!d!)与其将被映射到的输入列必须具有相同的数据类型和元数据。|  
|0xC020208F|-1071636337|DTS_E_TXPIVOTPROCESSERROR|尝试透视源记录时出错。|  
|0xC0202090|-1071636336|DTS_E_TXPIVOTBADPIVOTKEYVALUE|透视键值“%1”无效。|  
|0xC0202091|-1071636335|DTS_E_ERRORWHILESKIPPINGDATAROWS|跳过数据行时出错。|  
|0xC0202092|-1071636334|DTS_E_ERRORWHILEREADINGDATAROWS|处理文件“%1”的数据行 %2!I64d! 时出错。|  
|0xC0202093|-1071636333|DTS_E_FAILEDTOINITIALIZEFLATFILEPARSER|初始化平面文件分析器时出错。|  
|0xC0202094|-1071636332|DTS_E_UNABLETORETRIEVECOLUMNINFOFROMFLATFILECONNECTIONMANAGER|无法从平面文件连接管理器中检索列信息。|  
|0xC0202095|-1071636331|DTS_E_FAILEDTOWRITEOUTCOLUMNNAME|无法写出列“%1”的名称。|  
|0xC0202096|-1071636330|DTS_E_INVALIDFLATFILECOLUMNTYPE|列“%1”的类型不正确。 它属于类型“%2”。 其类型只能为“%3”或“%4”。|  
|0xC0202097|-1071636329|DTS_E_DISKIOBUFFEROVERFLOW|尝试将 %1!d! 个字节的数据写入磁盘 I/O 失败。 磁盘 I/O 缓冲区的可用字节数为 %2!d! 。|  
|0xC0202098|-1071636328|DTS_E_FAILEDTOWRITEOUTHEADER|写出文件头时出错。|  
|0xC0202099|-1071636327|DTS_E_FAILEDTOGETFILESIZE|获取文件“%1”的大小时出错。|  
|0xC020209A|-1071636326|DTS_E_FAILEDTOSETFILEPOINTER|设置文件“%1”的指针时出错。|  
|0xC020209B|-1071636325|DTS_E_UNABLETOSETUPDISKIOBUFFER|设置磁盘 I/O 缓冲区时出错。|  
|0xC020209C|-1071636324|DTS_E_COLUMNDATAOVERFLOWDISKIOBUFFER|列“%1”的数据溢出磁盘 I/O 缓冲区|  
|0xC020209D|-1071636323|DTS_E_DISKIOFAILED|读取文件时发生意外磁盘 I/O 错误。|  
|0xC020209E|-1071636322|DTS_E_DISKIOTIMEDOUT|读取文件时发生磁盘 I/O 超时。|  
|0xC020209F|-1071636321|DTS_E_INPUTSNOTREADONLY|为此转换指定的输入列使用类型不能为读/写。 请将使用类型更改为只读。|  
|0xC02020A0|-1071636320|DTS_E_CANNOTCOPYORCONVERTFLATFILEDATA|无法复制或转换列“%1”的平面文件数据。|  
|0xC02020A1|-1071636319|DTS_E_FAILEDCOLUMNDATACONVERSIONSTATUS|数据转换失败。 列“%1”的数据转换返回状态值 %2!d! 和状态文本“%3”。|  
|0xC02020A2|-1071636318|DTS_E_VARIABLESCOLLECTIONUNAVAILABLE|没有 Variables 集合。|  
|0xC02020A3|-1071636317|DTS_E_TXUNPIVOTDUPLICATEPIVOTKEYVALUE|PivotKeyValue 重复。 输入列“%1”(%2!d!)被映射到透视值输出列，但其 PivotKeyValue 不唯一。|  
|0xC02020A4|-1071636316|DTS_E_TXUNPIVOTNOUNPIVOTDESTINATION|找不到逆透视目标。 必须使用 PivotKeyValue 将至少一个输入列映射到输出的 DestinationColumn。|  
|0xC02020A5|-1071636315|DTS_E_TXUNPIVOTBADKEYLIST|PivotKeyValue 无效。 如果逆透视转换有多个已逆透视的 DestinationColumn，则每个目标的 PivotKeyValues 设置必须完全匹配。|  
|0xC02020A6|-1071636314|DTS_E_TXUNPIVOTBADUNPIVOTMETADATA|UnPivot 元数据不正确。 在 UnPivot 转换中，对于所有设置了 PivotKeyValue 且指向相同 DestinationColumn 的输入列，其元数据都必须与 DestinationColumn 完全匹配。|  
|0xC02020A7|-1071636313|DTS_E_TXPIVOTBADPIVOTKEYCONVERT|无法将透视键值“%1”转换为透视键列的数据类型。|  
|0xC02020A8|-1071636312|DTS_E_TXUNPIVOTTOOMANYPIVOTKEYS|指定的透视键过多。 只能将一个输出列作为透视键。|  
|0xC02020A9|-1071636311|DTS_E_TXUNPIVOTUNMAPPEDOUTPUT|输出列“%1”(%2!d!)未由任何输入列的 DestinationColumn 属性映射。|  
|0xC02020AA|-1071636310|DTS_E_TXUNPIVOTNOPIVOT|未将任何输出列标记为 PivotKey。|  
|0xC02020AB|-1071636309|DTS_E_TXUNPIVOTNOTINPUTMAP|输入列“%1”(%2!d!)的 DestinationColumn 属性值所引用的输出列 LineageID 无效。|  
|0xC02020AC|-1071636308|DTS_E_TXUNPIVOTDUPLICATEDESTINATION|出现目标重复错误。 多个非透视输入列被映射到相同的目标输出列。|  
|0xC02020AD|-1071636307|DTS_E_TOTALINPUTCOLSCANNOTBEZERO|找不到输入列。 必须将至少一个输入列映射到输出列。|  
|0xC02020AE|-1071636306|DTS_E_TXMERGEJOINMUSTHAVESAMENUMBEROFINPUTANDOUTPUTCOLS|输入列数与输出列数不相等。 所有输入的输入列总数必须与输出列总数相等。|  
|0xC02020AF|-1071636305|DTS_E_INPUTMUSTBESORTED|未对输入进行排序。 必须对“%1”进行排序。|  
|0xC02020B0|-1071636304|DTS_E_TXMERGEJOININVALIDJOINTYPE|%1 的 JoinType 自定义属性包含的值 %2!ld! 无效。 有效值为 0 (完全联接)、1 (左联接)或 2 (内部联接)。|  
|0xC02020B1|-1071636303|DTS_E_TXMERGEJOININVALIDNUMKEYCOLS|NumKeyColumns 值无效。 在 %1 中，NumKeyColumns 自定义属性的值必须介于 1 和 %2!lu! 之间。|  
|0xC02020B2|-1071636302|DTS_E_NOKEYCOLS|找不到键列。 %1 必须至少有一个列的 SortKeyPosition 为非零。|  
|0xC02020B3|-1071636301|DTS_E_TXMERGEJOINNOTENOUGHKEYCOLS|键列不足。 %1 必须至少有 %2!ld! 个列的 SortKeyPosition 值为非零。|  
|0xC02020B4|-1071636300|DTS_E_TXMERGEJOINDATATYPEMISMATCH|数据类型不匹配。 SortKeyPosition 值为 %1!ld! 的列的数据类型 的输出列的数据类型不匹配。|  
|0xC02020B5|-1071636299|DTS_E_TXMERGEJOININVALIDSORTKEYPOS|SortKeyPosition 值为 %1!ld! 的列无效。 其值应为 %2!ld!。|  
|0xC02020B6|-1071636298|DTS_E_TXMERGEJOINSORTDIRECTIONMISMATCH|排序方向不匹配。 SortKeyPosition 值为 %1!ld! 的输出列的数据类型不匹配。|  
|0xC02020B7|-1071636297|DTS_E_TXMERGEJOINOUTPUTCOLMUSTHAVEASSOCIATEDINPUTCOL|缺少列。 %1 必须有关联的输入列。|  
|0xC02020B8|-1071636296|DTS_E_TXMERGEJOINREADONLYINPUTCOLSWITHNOOUTPUTCOL|输入列必须有输出列。 使用类型为只读的输入列没有关联的输出列。|  
|0xC02020B9|-1071636295|DTS_E_TXMERGEJOINNONSTRINGCOMPARISONFLAGSNOTZERO|比较标志不是零。 非字符串列的比较标志必须为零。|  
|0xC02020BA|-1071636294|DTS_E_TXMERGEJOINCOMPARISONFLAGSMISMATCH|SortKeyPosition 值为 %1!ld! 的列的比较标志 的输出列的数据类型不匹配。|  
|0xC02020BB|-1071636293|DTS_E_TXPIVOTBADPIVOTKEYVALUENOSTRING|无法识别透视键值。|  
|0xC02020BC|-1071636292|DTS_E_TXLINEAGEINVALIDLINEAGEITEM|沿袭项值 %1!ld! 的列无效。 其有效范围应介于 %2!ld! 和 %3!ld! 之间。|  
|0xC02020BD|-1071636291|DTS_E_CANNOTHAVEANYINPUTCOLUMNS|不允许有输入列。 输入列数必须为零。|  
|0xC02020BE|-1071636290|DTS_E_TXLINEAGEDATATYPEMISMATCH|“%1”的数据类型对于指定的沿袭项无效。|  
|0xC02020BF|-1071636289|DTS_E_TXLINEAGEINVALIDLENGTH|“%1”的长度对于指定的沿袭项无效。|  
|0xC02020C1|-1071636287|DTS_E_METADATAMISMATCHWITHOUTPUTCOLUMN|“%1”的元数据与关联的输出列的元数据不匹配。|  
|0xC02020C3|-1071636285|DTS_E_TXMERGESORTKEYPOSMISMATCH|输出列的 SortKeyPosition 值与关联的输入列的 SortKeyPosition 不匹配。|  
|0xC02020C4|-1071636284|DTS_E_ADDROWTOBUFFERFAILED|无法向数据流任务缓冲区添加行，错误代码为 0x%1!8.8X!。|  
|0xC02020C5|-1071636283|DTS_E_DATACONVERSIONFAILED|在将列“%1”(%2!d!)转换为列“%3”(%4!d!)时，数据转换失败。  转换操作返回状态值 %5!d! 和状态文本“%6”。|  
|0xC02020C6|-1071636282|DTS_E_FAILEDTOALLOCATEROWHANDLEBUFFER|无法分配行句柄缓冲区，错误代码为 0x%1!8.8X!。|  
|0xC02020C7|-1071636281|DTS_E_FAILEDTOSENDROWTOSQLSERVER|无法将行发送到 SQL Server，错误代码为 0x%1!8.8X!。|  
|0xC02020C8|-1071636280|DTS_E_FAILEDTOPREPAREBUFFERSTATUS|无法准备缓冲区状态，错误代码为 0x%1!8.8X!。|  
|0xC02020C9|-1071636279|DTS_E_FAILEDTOBUFFERROWSTARTS|无法检索缓冲区行的开头，错误代码为 0x%1!8.8X!。|  
|0xC02020CA|-1071636278|DTS_E_BULKINSERTTHREADTERMINATED|SSIS 大容量插入线程已停止运行。  无法再插入行。 请尝试增加大容量插入线程的超时值。|  
|0xC02020CB|-1071636277|DTS_E_RAWTOOMANYCOLUMNS|源文件无效。 源文件返回的列计数超过 131,072。 如果源文件不是由原始文件目标生成，通常会发生这种情况。|  
|0xC02020CC|-1071636276|DTS_E_TXUNIONALL_EXTRADANGLINGINPUT|%1 是多余的未附加输入，将被删除。|  
|0xC02020CD|-1071636275|DTS_E_TXUNIONALL_NONDANGLINGUNATTACHEDINPUT|未附加 %1 但也未将其标记为无关联。  将把其标记为无关联。|  
|0xC02020CF|-1071636273|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUE|透视键值“%1”重复。|  
|0xC02020D0|-1071636272|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUENOSTRING|透视键值重复。|  
|0xC02020D1|-1071636271|DTS_E_FAILEDTOGETCOMPONENTLOCALEID|检索组件区域设置 ID 失败。 错误代码为 0x%1!8.8X!。|  
|0xC02020D2|-1071636270|DTS_E_MISMATCHCOMPONENTCONNECTIONMANAGERLOCALEID|区域设置 ID 不匹配。 组件区域设置 ID (%1!d!)与连接管理器区域设置 ID (%2!d!)不匹配。|  
|0xC02020D3|-1071636269|DTS_E_LOCALEIDNOTSET|未设置组件区域设置 ID。 平面文件适配器需要设置平面文件连接管理器的区域设置 ID。|  
|0xC02020D4|-1071636268|DTS_E_RAWBYTESTOOLONG|二进制字段太大。 适配器试图读取长度为 %1!d! 个字节的二进制字段，而字段长度不应大于 %2!d! 个字节，偏移量为 %3!d!。 当输入文件无效时通常会出现这种情况。 文件包含的字符串太长，不符合缓冲区列的要求。|  
|0xC02020D5|-1071636267|DTS_E_TXSAMPLINGINVALIDPCT|百分比 %2!ld! 对于“%1”属性无效。 该值必须介于 0 和 100 之间。|  
|0xC02020D6|-1071636266|DTS_E_TXSAMPLINGINVALIDROWS|行数 %2!ld! 对于“%1”属性无效。 此值必须大于 0。|  
|0xC02020D7|-1071636265|DTS_E_RAWSTRINGINPUTTOOLONG|要求适配器写入的字符串长度为 %1!I64d! 个字节，而所有数据的长度必须小于 4294967295 个字节。|  
|0xC02020D9|-1071636263|DTS_E_ATLEASTONEINPUTMUSTBEMAPPEDTOOUTPUT|没有输入映射到输出。 “%1”必须至少有一个输入列映射到输出列。|  
|0xC02020DB|-1071636261|DTS_E_CANNOTCONVERTDATATYPESWITHDIFFERENTCODEPAGES|不支持从“%1”(代码页为 %2!d!) 到“%3”(代码页为 %4!d!) 的转换。|  
|0xC02020DC|-1071636260|DTS_E_COLUMNNOTMAPPEDTOEXTERNALMETADATACOLUMN|%1 的外部元数据列映射无效。  外部元数据列 ID 不能为零。|  
|0xC02020DD|-1071636259|DTS_E_COLUMNMAPPEDTONONEXISTENTEXTERNALMETADATACOLUMN|“%1”被映射到不存在的外部元数据列。|  
|0xC02020E5|-1071636251|DTS_E_UNABLETOWRITELOBDATATOBUFFER|无法为列“%1”将类型为 DT_TEXT、DT_NTEXT 或 DT_IMAGE 的长对象数据写入数据流任务缓冲区。|  
|0xC02020E8|-1071636248|DTS_E_CANNOTGETIROWSET|无法打开“%1”的行集。 请检查数据库中是否存在此对象。|  
|0xC02020E9|-1071636247|DTS_E_VARIABLEACCESSFAILED|无法访问变量“%1”，错误代码为 0x%2!8.8X!。|  
|0xC02020EA|-1071636246|DTS_E_CONNECTIONMANAGERNOTFOUND|找不到连接管理器“%1”。 组件在 Connections 集合中找不到连接管理器。|  
|0xC02020EB|-1071636245|DTS_E_VERSIONUPGRADEFAILED|无法从版本“%1”升级到版本 %2!d! 。|  
|0xC02020EC|-1071636244|DTS_E_RSTDESTBIGBLOB|输入列中的值太大，无法存储在 ADODB.Recordset 对象中。|  
|0xC02020ED|-1071636243|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|列“%1”和“%2”无法在 unicode 和非 unicode 字符串数据类型之间转换。|  
|0xC02020EE|-1071636242|DTS_E_ROWCOUNTBADVARIABLENAME|VariableName 属性指定的变量“%1”无效。 需要有效变量名才能写入。|  
|0xC02020EF|-1071636241|DTS_E_ROWCOUNTBADVARIABLETYPE|VariableName 属性指定的变量“%1”不是整数。 请将此变量类型更改为 VT_I4、VT_UI4、VT_I8 或 VT_UI8。|  
|0xC02020F0|-1071636240|DTS_E_NOCOLUMNADVANCETHROUGHFILE|未指定列，组件无法进一步处理文件。|  
|0xC02020F1|-1071636239|DTS_E_MERGEJOINSORTEDOUTPUTHASNOSORTKEYPOSITIONS|“%1”的 IsSorted 被设置为 TRUE，而所有输出列的 SortKeyPosition 都是零。 请将 IsSorted 更改为 FALSE 或至少选择一个包含非零的 SortKeyPosition 的输出列。|  
|0xC02020F2|-1071636238|DTS_E_METADATAMISMATCHWITHINPUTCOLUMN|“%1”元数据与输入列的元数据不匹配。|  
|0xC02020F3|-1071636237|DTS_E_RSTDESTBADVARIABLE|无法找到、锁定或设置指定变量的值|  
|0xC02020F4|-1071636236|DTS_E_CANTPROCESSCOLUMNTYPECODEPAGE|由于为列“%1”指定了多个代码页(%2!d! 和 %3!d!），无法处理该列。|  
|0xC02020F5|-1071636235|DTS_E_CANTINSERTCOLUMNTYPE|由于不支持类型 %2 和 %3 之间的转换，无法插入列“%1”。|  
|0xC02020F6|-1071636234|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|列“%1”无法在 unicode 和非 unicode 字符串数据类型之间转换。|  
|0xC02020F8|-1071636232|DTS_E_COULDNOTFINDINPUTBUFFERCOLUMNBYLINEAGE|%1 在其输入缓冲区中找不到 LineageID 为 %2!ld! 的列。|  
|0xC02020F9|-1071636231|DTS_E_COULDNOTGETCOLUMNINFOFORINPUTBUFFER|%1 无法从其输入缓冲区获取列 %2!lu! 的信息。|  
|0xC02020FA|-1071636230|DTS_E_COULDNOTGETCOLUMNINFOFORCOPYBUFFER|%1 无法从其复制缓冲区获取列“%2!lu!” 的信息。|  
|0xC02020FB|-1071636229|DTS_E_COULDNOTREGISTERCOPYBUFFER|%1 无法注册其复制缓冲区的类型。|  
|0xC02020FC|-1071636228|DTS_E_COULDNOTCREATECOPYBUFFER|%1 无法创建缓冲区以将数据复制到其中进行排序。|  
|0xC02020FD|-1071636227|DTS_E_DATAREADERDESTREADFAILED|DataReader 客户端无法调用 Read 或已关闭了 DataReader。|  
|0xC02020FE|-1071636226|DTS_E_NOSCHEMAINFOFOUND|SQL 命令未返回任何列信息。|  
|0xC02020FF|-1071636225|DTS_E_GETSCHEMATABLEFAILED|%1 无法为 SQL 命令检索列信息。 出现以下错误: %2|  
|0xC0202100|-1071636224|DTS_E_SOURCETABLENAMENOTPROVIDED|未提供源表名称。|  
|0xC0203110|-1071632112|DTS_E_CACHE_INVALID_INDEXPOS|缓存索引位置 %1!d! 无效。 对于非索引列，索引位置应是 0。 对于索引列，索引位置应是连续的正数。|  
|0xC0203111|-1071632111|DTS_E_CACHE_DUPLICATE_INDEXPOS|索引位置 %1!d! 是一个重复位置。 对于非索引列，索引位置应是 0。 对于索引列，索引位置应是连续的正数。|  
|0xC0203112|-1071632110|DTS_E_CACHE_TOO_FEW_INDEX_COLUMNS|至少应为缓存连接管理器指定一个索引列。 若要指定索引列，请设置缓存列的索引位置属性。|  
|0xC0203113|-1071632109|DTS_E_CACHE_INDEXPOS_NOT_CONTINUOUS|缓存索引位置必须是连续的。 对于非索引列，索引位置应是 0。 对于索引列，索引位置应是连续的正数。|  
|0xC0204000|-1071628288|DTS_E_PROPERTYNOTSUPPORTED|无法设置“%2”的属性“%1”。 指定的对象不支持要设置的属性。 请检查属性的名称、大小写和拼写。|  
|0xC0204002|-1071628286|DTS_E_CANTCHANGEPROPERTYTYPE|无法更改组件所设置的属性类型。|  
|0xC0204003|-1071628285|DTS_E_CANTADDOUTPUTID|为输出 ID %1!d! 在插入期间出错。 未创建新输出。|  
|0xC0204004|-1071628284|DTS_E_CANTDELETEOUTPUTID|无法将输出 ID %1!d! 从输出集合中删除。  此 ID 无效或者此 ID 可能是默认 ID 或错误输出。|  
|0xC0204006|-1071628282|DTS_E_FAILEDTOSETPROPERTY|无法设置“%2”的属性“%1”。|  
|0xC0204007|-1071628281|DTS_E_FAILEDTOSETOUTPUTCOLUMNTYPE|无法将类型 %1 设置为类型:“%2”，长度: %3!d!，精度: %4!d!，小数位数: %5!d!，代码页: %6!d!。|  
|0xC0204008|-1071628280|DTS_E_MORETHANONEERROROUTPUTFOUND|在组件上找到多个错误输出，只能有一个错误输出。|  
|0xC020400A|-1071628278|DTS_E_CANTSETOUTPUTCOLUMNPROPERTY|无法设置输出列的属性。|  
|0xC020400B|-1071628277|DTS_E_CANTMODIFYERROROUTPUTCOLUMNDATATYPE|出现错误“%2”，无法修改“%1”的数据类型。|  
|0xC020400E|-1071628274|DTS_E_CANONLYSETISSORTEDONSOURCE|不能将“%1”的 IsSorted 属性设置为 TRUE，因为它不是源输出。 源输出的 SynchronousInputID 值为零。|  
|0xC020400F|-1071628273|DTS_E_CANONLYSETSORTKEYONSOURCE|不能将“%1”的 SortKeyPosition 属性设置为非零值，因为“%2”不是源输出。 不能将输出列“colname”(ID)的 SortKeyPosition 属性设置为非零值，因为其输出“outputname”(ID)不是源输出。|  
|0xC0204010|-1071628272|DTS_E_CANONLYSETCOMPFLAGSONSOURCE|不能将“%1”的 ComparisonFlags 属性设置为非零值，因为“%2”不是源输出。 不能将输出列“colname”(ID)的 ComparisonFlags 属性设置为非零值，因为其输出“outputname”(ID)不是源输出。|  
|0xC0204011|-1071628271|DTS_E_NONSTRINGCOMPARISONFLAGSNOTZERO|由于“%1”不是字符串类型，所以其比较标志一定为零。 只有字符串类型列的 ComparisonFlags 才能为非零。|  
|0xC0204012|-1071628270|DTS_E_COMPFLAGSONLYONSORTCOL|不能将“%1”的 ComparisonFlags 属性设置为非零值，因为其 SortKeyPosition 被设置为零。 仅当输出列的 SortKeyPosition 也为非零值时，其 ComparisonFlags 才能为非零值。|  
|0xC0204013|-1071628269|DTS_E_READONLYSTOCKPROPERTY|此属性是只读的。|  
|0xC0204014|-1071628268|DTS_E_INVALIDDATATYPE|为 %1 设置的数据类型值(%2!ld!)无效。|  
|0xC0204015|-1071628267|DTS_E_CODEPAGEREQUIRED|“%1”要求设置代码页，但传递的值为零。|  
|0xC0204016|-1071628266|DTS_E_INVALIDSTRINGLENGTH|“%1”的长度无效。 此长度必须介于 %2!ld! 和 %3!ld! 之间。|  
|0xC0204017|-1071628265|DTS_E_INVALIDSCALE|“%1”的小数位数无效。 此小数位数必须介于 %2!ld! 和 %3!ld! 之间。|  
|0xC0204018|-1071628264|DTS_E_INVALIDPRECISION|“%1”的精度无效。 此精度必须介于 %2!ld! 和 %3!ld! 之间。|  
|0xC0204019|-1071628263|DTS_E_PROPVALUEIGNORED|为“%1”的长度、精度、小数位数或代码页设置的值为非零，而数据类型要求此值为零。|  
|0xC020401A|-1071628262|DTS_E_CANTSETOUTPUTCOLUMNDATATYPEPROPERTIES|%1 不允许设置输出列的数据类型属性。|  
|0xC020401B|-1071628261|DTS_E_INVALIDDATATYPEFORERRORCOLUMNS|“%1”包含无效的数据类型。 “%1”是一种特殊的错误列，只有 DT_I4 才是有效的数据类型。|  
|0xC020401C|-1071628260|DTS_E_NOERRORDESCFORCOMPONENT|该组件未提供错误代码说明。|  
|0xC020401D|-1071628259|DTS_E_UNRECOGNIZEDERRORCODE|指定的错误代码与此组件无关。|  
|0xC020401F|-1071628257|DTS_E_TRUNCATIONTRIGGEREDREDIRECTION|根据截断处理设置，截断导致行重定向。|  
|0xC0204020|-1071628256|DTS_E_CANTSETUSAGETYPETOREADWRITE|“%1”无法使沿袭 ID 为 %2!d! 的列可读/写，因为此列不支持该使用类型。 试图将输入列的使用类型更改为类型 UT_READWRITE，但此组件不支持该类型。|  
|0xC0204023|-1071628253|DTS_E_CANTSETUSAGETYPE|%1 禁止所请求的对沿袭 ID 为 %2!d! 的输入列的使用。|  
|0xC0204024|-1071628252|DTS_E_FAILEDTOSETUSAGETYPE|“%1”无法对沿袭 ID 为 %2!d! 的输入列执行所请求的更改。 请求失败，错误代码为 0x%3!8.8X!。 指定的错误是在尝试设置输入列的使用类型时发生的。|  
|0xC0204025|-1071628251|DTS_E_FAILEDTOSETOUTPUTCOLUMNDATATYPEPROPERTIES|无法设置“%1”的数据类型属性，错误代码为 0x%2!8.8X!。 试图设置输出列的一个或多个数据类型属性时出错。|  
|0xC0204026|-1071628250|DTS_E_UNABLETORETRIEVEMETADATA|无法检索“%1”的元数据。 请确保对象名称正确且该对象存在。|  
|0xC0204027|-1071628249|DTS_E_CANNOTMAPOUTPUTCOLUMN|无法将输出列映射到外部元数据列。|  
|0xC0204028|-1071628248|DTS_E_UNSUPPORTEDVARIABLETYPE|变量 %1 的类型必须为“%2”。|  
|0xC020402A|-1071628246|DTS_E_CANTSETEXTERNALMETADATACOLUMNDATATYPEPROPERTIES|%1 不允许设置外部元数据列数据类型属性。|  
|0xC020402B|-1071628245|DTS_E_IDNOTINPUTNOROUTPUT|ID %1!lu! 不是输入 ID，也不是输出 ID。 指定的 ID 必须是与该外部元数据集合关联的输入 ID 或输出 ID。|  
|0xC020402C|-1071628244|DTS_E_METADATACOLLECTIONNOTUSED|“%1”的外部元数据集合被标记为未用，因此无法对其执行任何操作。|  
|0xC020402D|-1071628243|DTS_E_NOBUFFERTYPEONSYNCOUTPUT|%1 属于同步输出，无法为同步输出检索该缓冲区类型。|  
|0xC0207000|-1071616000|DTS_E_INPUTCOLUMNUSAGETYPENOTREADONLY|输入列“%1”必须为只读。 此输入列的使用类型不是只读，这是不允许的。|  
|0xC0207001|-1071615999|DTS_E_MISSINGCUSTOMPROPERTY|“%1”缺少要求的属性“%2”。 此对象必须有指定的自定义属性。|  
|0xC0207002|-1071615998|DTS_E_ILLEGALCUSTOMOUTPUTPROPERTY|输出 %1 不能具有属性“%2”，但当前分配了该属性。|  
|0xC0207003|-1071615997|DTS_E_INVALIDOUTPUTEXCLUSIONGROUP|%1 必须位于排除组 %2!d! 中。 所有输出都必须属于指定的排除组。|  
|0xC0207004|-1071615996|DTS_E_PROPERTYISEMPTY|属性“%1”为空。 此属性不能为空。|  
|0xC0207005|-1071615995|DTS_E_CREATEEXPRESSIONOBJECTFAILED|无法为表达式“%1”分配内存。 创建用来存放表达式的内部对象时发生内存不足错误。|  
|0xC0207006|-1071615994|DTS_E_EXPRESSIONPARSEFAILED|无法分析表达式“%1”。 该表达式无效，要不就是内存不足。|  
|0xC0207007|-1071615993|DTS_E_EXPRESSIONCOMPUTEFAILED|无法计算表达式“%1”，错误代码为 0x%2!8.8X!。 该表达式可能存在无法在分析时检测到的错误(如被零除)，要不就是内存不足。|  
|0xC0207008|-1071615992|DTS_E_FAILEDTOCREATEEXPRESSIONARRAY|无法为表达式对象分配内存。 创建 Expression 对象指针的数组时发生内存不足错误。|  
|0xC020700A|-1071615990|DTS_E_FAILEDTOCREATEEXPRESSIONMANANGER|创建表达式管理器时 %1 失败，错误代码为 0x%2!8.8X! 。|  
|0xC020700B|-1071615989|DTS_E_SPLITEXPRESSIONNOTBOOLEAN|表达式“%1”不是布尔型表达式。 此表达式的结果类型必须为布尔型。|  
|0xC020700C|-1071615988|DTS_E_EXPRESSIONVALIDATIONFAILED|“%2”的表达式“%1”无效。|  
|0xC020700E|-1071615986|DTS_E_COLUMNNOTMATCHED|列“%1”(%2!d!)无法与任何输入文件列匹配。 在文件中找不到输出列名或输入列名。|  
|0xC020700F|-1071615985|DTS_E_SETRESULTCOLUMNFAILED|无法为 %2 的表达式“%1”设置结果列，错误代码为 0x%3!8.8X!。 无法确定接收该表达式结果的输入列或输出列或者无法将表达式结果转换为此列类型。|  
|0xC0207011|-1071615983|DTS_E_FAILEDTOGETLOCALEIDFROMPACKAGE|%1 无法从包获取区域设置 ID。|  
|0xC0207012|-1071615982|DTS_E_INCORRECTPARAMETERMAPPINGFORMAT|参数映射字符串的格式不正确。|  
|0xC0207013|-1071615981|DTS_E_NOTENOUGHPARAMETERSPROVIDED|SQL 命令需要 %1!d! 个参数，但此参数映射只有 %2!d! 个参数。|  
|0xC0207014|-1071615980|DTS_E_PARAMETERNOTFOUNDINMAPPING|SQL 命令需要名为“%1”的参数，但在此参数映射中找不到该参数。|  
|0xC0207015|-1071615979|DTS_E_DUPLICATEDATASOURCECOLUMNNAME|存在多个名为“%1”的数据源列。  数据源列名必须唯一。|  
|0xC0207016|-1071615978|DTS_E_DATASOURCECOLUMNWITHNONAMEFOUND|存在无名的数据源列。  所有数据源列都必须有名称。|  
|0xC0208001|-1071611903|DTS_E_DISCONNECTEDCOMPONENT|组件已断开与布局的连接。|  
|0xC0208002|-1071611902|DTS_E_INVALIDCOMPONENTID|布局组件的 ID 无效。|  
|0xC0208003|-1071611901|DTS_E_INVALIDINPUTCOUNT|组件的输入数无效。|  
|0xC0208004|-1071611900|DTS_E_INVALIDOUTPUTCOUNT|组件的输出数无效。|  
|0xC0208005|-1071611899|DTS_E_NOINPUTSOROUTPUTS|组件没有任何输入或输出。|  
|0xC0208007|-1071611897|DTS_E_CANTALLOCATECOLUMNINFO|内存不足，无法分配此组件操作的一组列。|  
|0xC0208008|-1071611896|DTS_E_OUTPUTCOLUMNNOTININPUT|输出列“%1”(%2!d!)引用沿袭 ID 为 %3!d! 的输入列，但找不到具有该沿袭 ID 的输入。|  
|0xC0208009|-1071611895|DTS_E_SORTNEEDSONEKEY|至少必须将一个输入列标记为排序键，但找不到任何键。|  
|0xC020800A|-1071611894|DTS_E_SORTDUPLICATEKEYWEIGHT|列“%1”(%2!d!)和列“%3”(%4!d!)已用排序键权重 %5!d! 标记。|  
|0xC020800D|-1071611891|DTS_E_CANTMODIFYINVALID|只有先修复验证问题，组件才能执行所请求的元数据更改。|  
|0xC020800E|-1071611890|DTS_E_CANTADDINPUT|无法将输入添加到输入集合。|  
|0xC020800F|-1071611889|DTS_E_CANTADDOUTPUT|无法将输出添加到输出集合。|  
|0xC0208010|-1071611888|DTS_E_CANTDELETEINPUT|无法将输入从输入集合中删除。|  
|0xC0208011|-1071611887|DTS_E_CANTDELETEOUTPUT|无法将输出从输出集合中删除。|  
|0xC0208014|-1071611884|DTS_E_CANTCHANGEUSAGETYPE|无法更改列的使用类型。|  
|0xC0208016|-1071611882|DTS_E_INVALIDUSAGETYPEFORCUSTOMPROPERTY|%1 必须可读/写才能有自定义属性“%2”。 输入列或输出列虽然有指定的自定义属性，但不可读/写。 请删除此属性或使该列可读/写。|  
|0xC0208017|-1071611881|DTS_E_READWRITECOLUMNMISSINGREQUIREDCUSTOMPROPERTY|%1 可读/写且必须有自定义属性“%2”。 请添加此属性或删除列的读/写属性。|  
|0xC0208018|-1071611880|DTS_E_CANTDELETECOLUMN|无法删除列。 组件不允许从此输入或输出中删除列。|  
|0xC0208019|-1071611879|DTS_E_CANTADDCOLUMN|组件不允许在此输入或输出中添加列。|  
|0xC020801A|-1071611878|DTS_E_CANNOTTFINDRUNTIMECONNECTIONOBJECT|找不到连接“%1”。 请确保连接管理器包含具有此名称的连接。|  
|0xC020801B|-1071611877|DTS_E_CANNOTFINDRUNTIMECONNECTIONMANAGER|找不到 ID 为“%1”的运行时连接管理器。 请确保连接管理器集合包含具有此 ID 的连接管理器。|  
|0xC020801C|-1071611876|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|SSIS 错误代码 DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER。  AcquireConnection 方法调用失败，错误代码为 0x%2!8.8X!。  可能在此之前已经发出错误消息，提供了有关 AcquireConnection 方法调用失败原因的详细信息。|  
|0xC020801D|-1071611875|DTS_E_ACQUIREDCONNECTIONISINVALID|从连接管理器“%1”获取的连接无效。|  
|0xC020801E|-1071611874|DTS_E_INCORRECTCONNECTIONMANAGERTYPE|连接管理器“%1”的类型不正确。  要求为类型“%2”。 组件可用的类型为“%3”。|  
|0xC020801F|-1071611873|DTS_E_CANNOTACQUIREMANAGEDCONNECTIONFROMCONNECTIONMANAGER|无法从运行时连接管理器获取托管连接。|  
|0xC0208020|-1071611872|DTS_E_CANTINITINPUT|无法创建输入以初始化输入集合。|  
|0xC0208021|-1071611871|DTS_E_CANTINITOUTPUT|无法创建输出以初始化输出集合。|  
|0xC0208023|-1071611869|DTS_E_EXTRACTORCANTWRITE|无法写入文件“%1”，错误代码为 0x%2!8.8X!。|  
|0xC0208024|-1071611868|DTS_E_INCORRECTCONNECTIONOBJECTTYPE|连接管理器“%1”从 AcquireConnection 方法返回的对象类型不正确。|  
|0xC0208025|-1071611867|DTS_E_INPUTCOLPROPERTYNOTFOUND|输入列“%1”(%2!d!)需要“%3”属性，但找不到此属性。 应添加缺少的属性。|  
|0xC0208026|-1071611866|DTS_E_EXTRACTORUNREFERENCED|“%1”被标记为只读，但未被任何其他列引用。 不允许存在未被引用列。|  
|0xC0208027|-1071611865|DTS_E_EXTRACTORREFERENCEDCOLUMNNOTFOUND|“%1”引用 ID 为 %2!d! 的列，但在输入中找不到该列。 引用所指向的列不存在。|  
|0xC0208028|-1071611864|DTS_E_EXTRACTORDATACOLUMNNOTBLOB|“%1”引用“%2”，但该列的类型不是 BLOB。|  
|0xC0208029|-1071611863|DTS_E_INSERTERREFERENCEDCOLUMNNOTFOUND|“%1”引用 ID 为 %2!d! 的输出列，但在输出中找不到该列。|  
|0xC020802A|-1071611862|DTS_E_INSERTERCANTREAD|无法读取文件“%1”，错误代码为 0x%2!8.8X!。|  
|0xC020802B|-1071611861|DTS_E_TXSCD_NOTYPEDCOLUMNSATINPUT|在“渐变维度”转换的输入中，必须至少有一列属于“固定”、“变化”或“历史”类型。 请确保至少有一个列为 FixedAttribute、ChangingAttribute 或 HistoricalAttribute。|  
|0xC020802C|-1071611860|DTS_E_TXSCD_INVALIDINPUTCOLUMNTYPE|“%1”的 ColumnType 属性无效。 当前值不在可接受值的范围之内。|  
|0xC020802D|-1071611859|DTS_E_TXSCD_CANNOTMAPDIFFERENTTYPES|由于彼此的数据类型不同，无法将输入列“%1”映射到外部列“%2”。 “渐变维度”转换不允许在不同类型的列之间进行映射，DT_STR 和 DT_WSTR 类型除外。|  
|0xC020802E|-1071611858|DTS_E_NTEXTDATATYPENOTSUPPORTEDWITHANSIFILES|“%1”的数据类型为 DT_NTEXT，ANSI 文件不支持此数据类型。 请改用 DT_TEXT，然后使用数据转换组件将数据转换为 DT_NTEXT。|  
|0xC020802F|-1071611857|DTS_E_TEXTDATATYPENOTSUPPORTEDWITHUNICODEFILES|“%1”的数据类型为 DT_TEXT，Unicode 文件不支持此数据类型。 请改用 DT_NTEXT，然后使用数据转换组件将数据转换为 DT_TEXT。|  
|0xC0208030|-1071611856|DTS_E_IMAGEDATATYPENOTSUPPORTED|“%1”的数据类型为不支持的 DT_IMAGE。 请改用 DT_TEXT 或 DT_NTEXT，然后使用数据转换组件将数据从 DT_IMAGE 转换为其他类型或将数据转换为 DT_IMAGE。|  
|0xC0208031|-1071611855|DTS_E_FLATFILEFORMATNOTSUPPORTED|平面文件连接管理器不支持格式“%1”。 支持的格式有: Delimited、FixedWidth、RaggedRight 和 Mixed。|  
|0xC0208032|-1071611854|DTS_E_EXTRACTORFILENAMECOLUMNNOTSTRING|“%1”应包含文件名，但它不属于 String 类型。|  
|0xC0208033|-1071611853|DTS_E_EXTRACTORCANTAPPENDTRUNCATE|由于属性设置存在冲突而出错。 “%1”的 AllowAppend 属性和 ForceTruncate 属性都被设置为 TRUE。 这两个属性不能同时设置为 TRUE。 请将其中一个属性设置为 FALSE。|  
|0xC0208034|-1071611852|DTS_E_EXTRACTORCOLUMNALREADYREFERENCED|%1 引用 ID 为 %2!d! 的列，但此列已被 %3 引用。 请将对此列的两个引用删除一个。|  
|0xC0208035|-1071611851|DTS_E_CONNECTIONMANANGERNOTASSIGNED|未给 %1 分配连接管理器。|  
|0xC0208036|-1071611850|DTS_E_INSERTERCOLUMNALREADYREFERENCED|%1 引用 ID 为 %2!d! 的输出列，但此列已被 %3 引用。|  
|0xC0208037|-1071611849|DTS_E_INSERTERCOLUMNNOTREFERENCED|“%1”未被任何输入列引用。 每个输出列必须被一个且只能被一个输入列引用。|  
|0xC0208038|-1071611848|DTS_E_INSERTERDATACOLUMNNOTBLOB|“%1”引用“%2”，但此列的类型不正确。 它必须为 DT_TEXT、DT_NTEXT 或 DT_IMAGE。 引用所指向列的类型必须为 BLOB。|  
|0xC0208039|-1071611847|DTS_E_INSERTERFILENAMECOLUMNNOTSTRING|“%1”应包含文件名，但它不是 String 类型。|  
|0xC020803A|-1071611846|DTS_E_INSERTEREXPECTBOMINVALIDTYPE|已针对 %2 将“%1”的 ExpectBOM 属性设置为 TRUE，但此列不是 NT_NTEXT 类型。 ExpectBOM 指定导入列转换需要使用字节顺序标记(BOM)。 请将 ExpectBOM 属性设置为 False 或将输出列的数据类型更改为 DT_NTEXT。|  
|0xC020803B|-1071611845|DTS_E_INSERTERINVALIDDATACOLUMNSETTYPE|数据输出列必须为 DT_TEXT、DT_NTEXT 或 DT_IMAGE。 只能将数据输出列设置为 BLOB 类型。|  
|0xC020803C|-1071611844|DTS_E_TXSCD_FIXEDATTRIBUTECHANGE|如果将 FailOnFixedAttributeChange 属性设置为 TRUE，当检测到固定的属性更改时，转换将失败。 要将行发送到“固定的属性”输出，请将 FailOnFixedAttributeChange 属性设置为 FALSE。|  
|0xC020803D|-1071611843|DTS_E_TXSCD_LOOKUPFAILURE|查找转换检索不到任何行。 当将 FailOnLookupFailure 设置为 TRUE 时，转换将失败，也就检索不到任何行。|  
|0xC020803E|-1071611842|DTS_E_TXSCD_INVALIDNUMBERSOFPARAMETERS|“渐变维度”转换的输入必须至少有一个 Key 类型的列。 请至少将一个列的类型设置为 Key。|  
|0xC020803F|-1071611841|DTS_E_TXSCD_CANNOTFINDEXTERNALCOLUMN|找不到名为“%1”的外部列。|  
|0xC0208040|-1071611840|DTS_E_TXSCD_INFFEREDINDICATORNOTBOOL|推断指示器列“%1”的类型必须为 DT_BOOL。|  
|0xC0208107|-1071611641|DTS_E_ERRORROWDISPMUSTBENOTUSED|必须将 %1 的错误行处理值设置为 RD_NotUsed。|  
|0xC0208108|-1071611640|DTS_E_TRUNCROWDISPMUSTBENOTUSED|必须将 %1 的截断行处理值设置为 RD_NotUsed。|  
|0xC0208201|-1071611391|DTS_E_TXAGG_INPUTNOTFOUNDFOROUTPUT|找不到 ID 为 %2!d! 的输出列所需的沿袭 ID 为 %1!d! 的输入列。|  
|0xC0208202|-1071611390|DTS_E_TXAGG_INVALIDOUTPUTDATATYPEFORAGGREGATE|在 ID 为 %1!d! 的输出列上指定的聚合类型的输出数据类型无效。|  
|0xC0208203|-1071611389|DTS_E_TXAGG_INVALIDINPUTDATATYPEFORAGGREGATE|用于 %2 的指定聚合的 %1 的输入数据类型无效。|  
|0xC0208204|-1071611388|DTS_E_TXAGG_INPUTOUTPUTDATATYPEMISMATCH|沿袭 ID 为 %1!d! 的输入列与 ID 为 %2!d! 的输出列的数据类型不匹配。|  
|0xC0208205|-1071611387|DTS_E_UNABLETOGETINPUTBUFFERHANDLE|无法获取输入 ID %1!d! 的输入缓冲区句柄。|  
|0xC0208206|-1071611386|DTS_E_UNABLETOGETOUTPUTBUFFERHANDLE|无法获取输出 ID %1!d! 的输出缓冲区句柄。|  
|0xC0208207|-1071611385|DTS_E_UNABLETOFINDCOLUMNHANDLEINOUTPUTBUFFER|在输出缓冲区中找不到沿袭 ID 为 %1!d! 的列。|  
|0xC0208208|-1071611384|DTS_E_UNABLETOFINDCOLUMNHANDLEININPUTBUFFER|在输出缓冲区中找不到沿袭 ID 为 %1!d! 的列。|  
|0xC0208209|-1071611383|DTS_E_CANNOTHAVEZEROOUTPUTCOLUMNS|%1 的输出列数不能为零。|  
|0xC020820A|-1071611382|DTS_E_CONNECTIONMANAGERCOLUMNCOUNTMISMATCH|平面文件连接管理器中的列数必须与平面文件适配器中的列数相同。 平面文件连接管理器的列数为 %1!d!，而平面文件适配器的列数为 %2!d!。|  
|0xC020820B|-1071611381|DTS_E_MISMATCHCONNECTIONMANAGERCOLUMN|平面文件连接管理器的索引 %2!d! 中包含列“%1”，但在平面文件适配器列集合的索引 %3!d! 中找不到此列。|  
|0xC020820D|-1071611379|DTS_E_EXTERNALMETADATACOLUMNISALREADYMAPPED|ID 为 %1!d! 的外部元数据列已被映射到 %2。|  
|0xC020820E|-1071611378|DTS_E_TXAGG_STRING_TOO_LONG|转换遇到超过 %1!u! 个字符）。|  
|0xC020820F|-1071611377|DTS_E_DERIVEDRESULT_TOO_LONG|转换遇到超过 %1!u! 个字节的结果值。|  
|0xC0208210|-1071611376|DTS_E_TXAGG_MEMALLOCERROUTPUTDESCRIPTORS|无法分配内存。|  
|0xC0208211|-1071611375|DTS_E_TXAGG_MEMALLOCERRWORKSPACEDESCRIPTORS|无法分配内存。|  
|0xC0208212|-1071611374|DTS_E_TXAGG_MEMALLOCERRSORTORDERDESCRIPTORS|无法分配内存。|  
|0xC0208213|-1071611373|DTS_E_TXAGG_MEMALLOCERRNUMERICDESCRIPTORS|无法分配内存。|  
|0xC0208214|-1071611372|DTS_E_TXAGG_MEMALLOCERRCOUNTDISTINCTDESCRIPTOR|无法分配内存。|  
|0xC0208215|-1071611371|DTS_E_TXAGG_MEMALLOCERRWORKSPACESORTORDERDESCRIPTORS|无法分配内存。|  
|0xC0208216|-1071611370|DTS_E_TXAGG_MEMALLOCERRWORKSPACENUMERICDESCRIPTORS|无法分配内存。|  
|0xC0208217|-1071611369|DTS_E_TXAGG_MEMALLOCERRWORKSPACEBUFFCOLS|无法分配内存。|  
|0xC0208218|-1071611368|DTS_E_UNREFERENCEDINPUTCOLUMN|未引用输入列“%1”。|  
|0xC0208219|-1071611367|DTS_E_CANTBUILDTHREADPOOL|排序转换无法创建包含 %1!d! 个线程的线程池。 内存不足。|  
|0xC020821A|-1071611366|DTS_E_QUEUEWORKITEMFAILED|排序转换无法将工作项排队以放入其线程池。 内存不足。|  
|0xC020821B|-1071611365|DTS_E_SORTTHREADSTOPPED|排序转换的工作线程已停止，错误代码为 0x%1!8.8X!。 对缓冲区排序时出错。|  
|0xC020821E|-1071611362|DTS_E_SORTBADTHREADCOUNT|MaxThreads 为 %1!ld!，此值应介于 1 和 %2!ld! (含)之间或为 -1，后者是默认的 CPU 数。|  
|0xC020821F|-1071611361|DTS_E_DTPXMLLOADFAILURE|无法从 XML 加载。|  
|0xC0208220|-1071611360|DTS_E_DTPXMLSAVEFAILURE|无法保存到 XML。|  
|0xC0208221|-1071611359|DTS_E_DTPXMLINT32CONVERTERR|无法将值“%1”转换为整数。|  
|0xC0208222|-1071611358|DTS_E_DTPXMLBOOLCONVERTERR|无法将值“%1”转换为布尔值。|  
|0xC0208223|-1071611357|DTS_E_DTPXMLPARSEERRORNEARID|ID 为 %1!d! 的对象附近发生加载错误。|  
|0xC0208226|-1071611354|DTS_E_DTPXMLPROPERTYTYPEERR|值“%1”对于属性“%2”无效。|  
|0xC0208228|-1071611352|DTS_E_DTPXMLSETUSAGETYPEERR|值“%1”对于属性“%2”无效。|  
|0xC0208229|-1071611351|DTS_E_DTPXMLDATATYPEERR|值“%1”对于属性“%2”无效。|  
|0xC020822A|-1071611350|DTS_E_UNMAPPEDINPUTCOLUMN|未将 %1 映射到输出列。|  
|0xC020822B|-1071611349|DTS_E_INPUTCOLUMNBADMAP|%1 包含有无效映射。  此组件上不存在 ID 为 %2!ld! 的输出列。|  
|0xC020822D|-1071611347|DTS_E_MULTIPLYMAPPEDOUTCOL|%1 被映射到的输出列已映射到此输入。|  
|0xC020822E|-1071611346|DTS_E_TXAGG_STRINGPROMOTIONFAILED|由于出现错误 0x%2!8.8X!，无法将沿袭 ID 为 %1!ld! 的输入列转换为 DT_WSTR。|  
|0xC0208230|-1071611344|DTS_E_DTPXMLIDLOOKUPERR|在包中找不到 ID 为 %1!d! 的被引用对象。|  
|0xC0208231|-1071611343|DTS_E_DTPXMLINVALIDXMLPERSISTPROPERTY|无法读取 pipelinexml 模块要求的持久性属性。 此管道未提供该属性。|  
|0xC0208232|-1071611342|DTS_E_DTPXMLPROPERTYSTATEERR|值“%1”对于属性“%2”无效。|  
|0xC0208233|-1071611341|DTS_E_CANTGETCUSTOMPROPERTY|无法检索自定义属性“%1”。|  
|0xC0208234|-1071611340|DTS_E_UNABLETOLOCATEINPUTCOLUMNID|在输入列集合中，找不到 ParameterMap 自定义属性(具有位置号为 %2!d! 的参数)中引用的、沿袭 ID 为 %1!d! 的输入列。|  
|0xC0208235|-1071611339|DTS_E_TXLOOKUP_UNABLETOLOCATEREFCOLUMN|找不到引用列“%1”。|  
|0xC0208236|-1071611338|DTS_E_TXLOOKUP_INCOMPATIBLEDATATYPES|%1 与名为“%2”的引用列的数据类型不兼容。|  
|0xC0208237|-1071611337|DTS_E_TXLOOKUP_PARAMMETADATAMISMATCH|参数化 SQL 语句生成的元数据与主 SQL 语句不匹配。|  
|0xC0208238|-1071611336|DTS_E_TXLOOKUP_INCORRECTNUMOFPARAMETERS|参数化 SQL 语句包含的参数个数不正确。 应为 %1!d!，实际为 %2!d!。|  
|0xC0208239|-1071611335|DTS_E_TXLOOKUP_INVALIDJOINTYPE|%1 包含无法联接的数据类型。|  
|0xC020823A|-1071611334|DTS_E_TXLOOKUP_INVALIDCOPYTYPE|%1 包含无法复制的数据类型。|  
|0xC020823B|-1071611333|DTS_E_INSERTERINVALIDCOLUMNDATATYPE|不支持 %1 的数据类型。 它的数据类型必须为 DT_STR 或 DT_WSTR。|  
|0xC020823C|-1071611332|DTS_E_EXTRACTORINVALIDCOLUMNDATATYPE|不支持 %1 的数据类型。 它的数据类型必须为 DT_STR、DT_WSTR、DT_TEXT、DT_NTEXT 或 DT_IMAGE。|  
|0xC020823D|-1071611331|DTS_E_TXCHARMAPINVALIDCOLUMNDATATYPE|不支持 %1 的数据类型。 它的数据类型必须为 DT_STR、DT_WSTR、DT_TEXT 或 DT_NTEXT。|  
|0xC020823E|-1071611330|DTS_E_SORTCANTCREATEEVENT|排序转换无法创建事件与其工作线程进行通信。 系统句柄不足，无法进行排序转换。|  
|0xC020823F|-1071611329|DTS_E_SORTCANTCREATETHREAD|排序转换无法创建工作线程。 内存不足，无法进行排序转换。|  
|0xC0208240|-1071611328|DTS_E_SORTCANTCOMPARE|排序转换无法将 ID 为 %2!d! 的缓冲区中的第 %1!d! 行与 ID 为 %4!d! 的缓冲区中的第 %3!d! 行进行比较。|  
|0xC0208242|-1071611326|DTS_E_TXLOOKUP_TOOFEWREFERENCECOLUMNS|查找转换引用的元数据包含的列太少。 请检查 SQLCommand 属性。 SELECT 语句必须至少返回一列。|  
|0xC0208243|-1071611325|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNINFO|无法为 ColumnInfo 结构数组分配内存。|  
|0xC0208244|-1071611324|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNPAIR|无法为 ColumnPair 结构数组分配内存。|  
|0xC0208245|-1071611323|DTS_E_TXLOOKUP_MALLOCERR_BUFFCOL|无法为 BUFFCOL 结构数组分配内存以创建主工作区。|  
|0xC0208246|-1071611322|DTS_E_TXLOOKUP_MAINWORKSPACE_CREATEERR|无法创建主工作区缓冲区。|  
|0xC0208247|-1071611321|DTS_E_TXLOOKUP_HASHTABLE_MALLOCERR|无法为哈希表分配内存。|  
|0xC0208248|-1071611320|DTS_E_TXLOOKUP_HASHNODEHEAP_CREATEERR|无法分配内存来为哈希节点创建堆。|  
|0xC0208249|-1071611319|DTS_E_TXLOOKUP_HASHNODEHEAP_MALLOCERR|无法为哈希节点堆分配内存。|  
|0xC020824A|-1071611318|DTS_E_TXLOOKUP_LRUNODEHEAP_CREATEERR|无法为 LRU 节点创建堆。 出现内存不足的情况。|  
|0xC020824B|-1071611317|DTS_E_TXLOOKUP_LRUNODEHEAP_MALLOCERR|无法为 LRU 节点堆分配内存。 出现内存不足的情况。|  
|0xC020824C|-1071611316|DTS_E_TXLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|加载列元数据时发生 OLE DB 错误。 请检查 SQLCommand 和 SqlCommandParam 属性。|  
|0xC020824D|-1071611315|DTS_E_TXLOOKUP_OLEDBERR_GETIROWSET|提取行集时发生 OLE DB 错误。 请检查 SQLCommand 和 SqlCommandParam 属性。|  
|0xC020824E|-1071611314|DTS_E_TXLOOKUP_OLEDBERR_FILLBUFFER|填充内部缓存时发生 OLE DB 错误。 请检查 SQLCommand 和 SqlCommandParam 属性。|  
|0xC020824F|-1071611313|DTS_E_TXLOOKUP_OLEDBERR_BINDPARAMETERS|绑定参数时发生 OLE DB 错误。 请检查 SQLCommand 和 SqlCommandParam 属性。|  
|0xC0208250|-1071611312|DTS_E_TXLOOKUP_OLEDBERR_CREATEBINDING|创建绑定时发生 OLE DB 错误。 请检查 SQLCommand 和 SqlCommandParam 属性。|  
|0xC0208251|-1071611311|DTS_E_TXLOOKUP_INVALID_CASE|运行时 switch 语句中出现无效事例。|  
|0xC0208252|-1071611310|DTS_E_TXLOOKUP_MAINWORKSPACE_MALLOCERR|无法给主工作区缓冲区分配内存来存放新行。 出现内存不足的情况。|  
|0xC0208253|-1071611309|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMIROWSET|提取参数化行集时发生 OLE DB 错误。 请检查 SQLCommand 和 SqlCommandParam 属性。|  
|0xC0208254|-1071611308|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMSINGLEROW|提取参数化行时发生 OLE DB 错误。 请检查 SQLCommand 和 SqlCommandParam 属性。|  
|0xC0208255|-1071611307|DTS_E_TXAGG_MAINWORKSPACE_MALLOCERR|无法给主工作区缓冲区分配内存来存放新行。 出现内存不足的情况。|  
|0xC0208256|-1071611306|DTS_E_TXAGG_MAINWORKSPACE_CREATEERR|无法创建主工作区缓冲区。|  
|0xC0208257|-1071611305|DTS_E_TXAGG_HASHTABLE_MALLOCERR|无法为哈希表分配内存。|  
|0xC0208258|-1071611304|DTS_E_TXAGG_HASHNODEHEAP_CREATEERR|无法分配内存来为哈希节点创建堆。|  
|0xC0208259|-1071611303|DTS_E_TXAGG_HASHNODEHEAP_MALLOCERR|无法为哈希节点堆分配内存。|  
|0xC020825A|-1071611302|DTS_E_TXAGG_CDNODEHEAP_CREATEERR|无法分配内存来为 CountDistinct 节点创建堆。|  
|0xC020825B|-1071611301|DTS_E_TXAGG_CDNODEHEAP_MALLOCERR|无法为 CountDistinct 节点堆分配内存。|  
|0xC020825C|-1071611300|DTS_E_TXAGG_CDCHAINHEAP_CREATEERR|无法分配内存来为 CountDistinct 链创建堆。|  
|0xC020825D|-1071611299|DTS_E_TXAGG_CDHASHTABLE_CREATEERR|无法为 CountDistinct 哈希表分配内存。|  
|0xC020825E|-1071611298|DTS_E_TXAGG_CDWORKSPACE_MALLOCERR|无法为 CountDistinct 工作区缓冲区分配内存来存放新行。|  
|0xC020825F|-1071611297|DTS_E_TXAGG_CDWORKSPACE_CREATEERR|无法创建 CountDistinct 工作区缓冲区。|  
|0xC0208260|-1071611296|DTS_E_TXAGG_CDCOLLASSEARRAY_MALLOCERR|无法为 CountDistinct Collapse 数组分配内存。|  
|0xC0208261|-1071611295|DTS_E_TXAGG_CDCHAINHEAP_MALLOCERR|无法为 CountDistinct 链分配内存。|  
|0xC0208262|-1071611294|DTS_E_TXCOPYMAP_MISMATCHED_COLUMN_METADATA|沿袭 ID 为 %1!d! 和 %2!d! 的列的元数据不匹配。 为复制映射而映射到输出列的输入列包含不同的元数据(数据类型、精度、小数位数、长度或代码页)。|  
|0xC0208263|-1071611293|DTS_E_TXCOPYMAP_INCORRECT_OUTPUT_COLUMN_MAPPING|沿袭 ID 为“%1!d!” 的输出列被错误映射到输入列。 输出列的 CopyColumnId 属性不正确。|  
|0xC0208265|-1071611291|DTS_E_CANTGETBLOBDATA|检索不到列“%1”的长整型数据。|  
|0xC0208266|-1071611290|DTS_E_CANTADDBLOBDATA|已检索到列的长整型数据，但无法将这些数据添加到数据流任务缓冲区。|  
|0xC0208267|-1071611289|DTS_E_MCASTOUTPUTCOLUMNS|输出“%1”(%2!d!)包含输出列，但多播输出未声明列。 包已损坏。|  
|0xC0208273|-1071611277|DTS_E_UNABLETOGETLOCALIZEDRESOURCE|无法加载本地化资源 ID %1!d!。 请确保 RLL 文件存在。|  
|0xC0208274|-1071611276|DTS_E_DTPXMLEVENTSCACHEERR|无法获取事件接口。 传递到数据流模块的事件接口无效，无法持续采用 XML 格式。|  
|0xC0208275|-1071611275|DTS_E_DTPXMLPATHLOADERR|在 XML 加载过程中设置路径对象时出错。|  
|0xC0208276|-1071611274|DTS_E_DTPXMLINPUTLOADERR|在 XML 加载过程中设置输入对象时出错。|  
|0xC0208277|-1071611273|DTS_E_DTPXMLOUTPUTLOADERR|在 XML 加载过程中设置输出对象时出错。|  
|0xC0208278|-1071611272|DTS_E_DTPXMLINPUTCOLUMNLOADERR|在 XML 加载过程中设置输入列对象时出错。|  
|0xC0208279|-1071611271|DTS_E_DTPXMLOUTPUTCOLUMNLOADERR|在 XML 加载过程中设置输出列对象时出错。|  
|0xC0208280|-1071611264|DTS_E_DTPXMLPROPERTYLOADERR|在 XML 加载过程中设置属性对象时出错。|  
|0xC0208281|-1071611263|DTS_E_DTPXMLCONNECTIONLOADERR|在 XML 加载过程中设置连接对象时出错。|  
|0xC0208282|-1071611262|DTS_E_FG_MISSING_OUTPUT_COLUMNS|与转换有关的特定列缺失或类型不正确。|  
|0xC0208283|-1071611261|DTS_E_FG_PREPARE_TABLES_AND_ACCESSORS|模糊分组转换无法创建要求的表和取值函数。|  
|0xC0208284|-1071611260|DTS_E_FG_COPY_INPUT|模糊分组转换无法复制输入。|  
|0xC0208285|-1071611259|DTS_E_FG_GENERATE_GROUPS|模糊分组转换无法生成组。|  
|0xC0208286|-1071611258|DTS_E_FG_LEADING_TRAILING|应用属性“%1”的设置时，模糊分组发生错误。|  
|0xC0208287|-1071611257|DTS_E_FG_PICK_CANONICAL|模糊分组转换无法选取规范的数据行以在将数据标准化时使用。|  
|0xC0208288|-1071611256|DTS_E_FG_NOBLOBS|模糊分组不支持类型为 IMAGE、TEXT 或 NTEXT 的输入列。|  
|0xC0208289|-1071611255|DTS_E_FG_FUZZY_MATCH_ON_NONSTRING|对列“%1”(%2!d!)指定了模糊匹配，而该列的数据类型不是 DT_STR 或 DT_WSTR。|  
|0xC020828A|-1071611254|DTS_E_FUZZYGROUPINGINTERNALPIPELINEERROR|发生模糊分组转换管道错误，返回错误代码 0x%1!8.8X!:“%2”。|  
|0xC020828B|-1071611253|DTS_E_CODE_PAGE_NOT_SUPPORTED|对输出列“%2”(%3!d!) 指定的代码页 %1!d!。  您首先必须通过插入数据转换将此列转换成 DT_WSTR，然后才能指定该代码页。|  
|0xC0208294|-1071611244|DTS_E_SETEODFAILED|为利用缓冲区的输出“%1”(%2!d!)设置数据结尾标志时失败。|  
|0xC0208296|-1071611242|DTS_E_CANTCLONE|无法克隆输入缓冲区。 出现内存不足的情况或存在内部错误。|  
|0xC02082F9|-1071611143|DTS_E_TXCHARMAP_CANTKATAKANAHIRAGANA|列“%1”要求同时生成平假名字符和片假名字符。|  
|0xC02082FA|-1071611142|DTS_E_TXCHARMAP_CANTSIMPLECOMPLEX|列“%1”要求同时生成简体中文字符和繁体中文字符。|  
|0xC02082FB|-1071611141|DTS_E_TXCHARMAP_CANTFULLHALF|列“%1”要求执行同时生成全角字符和半角字符的操作。|  
|0xC02082FC|-1071611140|DTS_E_TXCHARMAP_CANTCHINAJAPAN|列“%1”组合了对日语字符的操作和对中文字符的操作。|  
|0xC02082FD|-1071611139|DTS_E_TXCHARMAP_CANTCASECHINESE|列“%1”组合了对中文字符的操作和大小写操作。|  
|0xC02082FE|-1071611138|DTS_E_TXCHARMAP_CANTCASEJAPANESE|列“%1”组合了对日语字符的操作和大小写操作。|  
|0xC02082FF|-1071611137|DTS_E_TXCHARMAP_CANTBOTHCASE|列“%1”将该列同时映射为大写和小写。|  
|0xC0208300|-1071611136|DTS_E_TXCHARMAP_CANTLINGUISTIC|列“%1”将除大小写之外的标志与语言中的大小写操作组合在一起。|  
|0xC0208301|-1071611135|DTS_E_TXCHARMAP_INVALIDMAPFLAGANDDATATYPE|无法按指定方式映射列“%1”的数据类型。|  
|0xC0208302|-1071611134|DTS_E_TXFUZZYLOOKUP_UNSUPPORTED_MATCH_INDEX_VERSION|不支持预先存在的匹配索引“%2”的版本(%1)。 预期的版本应为“%3”。 如果索引元数据的版本与生成当前代码时针对的版本不匹配，将发生此错误。 请使用当前版本的代码重新生成索引，以修复此错误。|  
|0xC0208303|-1071611133|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX|表“%1”似乎不是有效的预建匹配索引。 当无法从指定的预建索引加载元数据记录时将发生此错误。|  
|0xC0208304|-1071611132|DTS_E_TXFUZZYLOOKUP_UNABLE_TO_READ_MATCH_INDEX|无法读取指定的预建匹配索引“%1”。  OLEDB 错误代码:0x%2!8.8X!。|  
|0xC0208305|-1071611131|DTS_E_TXFUZZYLOOKUP_NO_JOIN_COLUMNS|没有任何输入列具有到引用表列的有效联接。  请确保至少有一个联接是使用输入列属性 JoinToReferenceColumn 和 JoinType 定义的。|  
|0xC0208306|-1071611130|DTS_E_TXFUZZYLOOKUP_INDEX_DOES_NOT_CONTAIN_COLUMN|指定的预先存在的匹配索引“%1”不是使用模糊匹配信息为列“%2”生成的。  必须重新生成此索引以包含该信息。 当生成索引所使用的列不是模糊联接列时，将发生此错误。|  
|0xC0208307|-1071611129|DTS_E_TXFUZZYLOOKUP_IDENTIFIER_PROPERTY|为属性“%2”提供的名称“%1”不是有效的 SQL 标识符名称。 如果属性名称不符合有效 SQL 标识符名称的规范，将发生此错误。|  
|0xC0208309|-1071611127|DTS_E_TXFUZZYLOOKUP_MINSIMILARITY_INVALID|为模糊查找转换设置的 MinSimilarity 阈值属性的值必须大于等于 0.0 且小于 1.0。|  
|0xC020830A|-1071611126|DTS_E_TXFUZZYLOOKUP_INVALID_PROPERTY_VALUE|属性“%2”的值“%1”无效。|  
|0xC020830B|-1071611125|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_FUZZY_JOIN_DATATYPES|输入列“%1”与引用列“%2”之间的指定模糊查找无效，因为仅支持类型为 DT_STR 和 DT_WSTR 的字符串列之间的模糊联接。|  
|0xC020830C|-1071611124|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_EXACT_JOIN_DATATYPES|完全查找列“%1”和“%2”的数据类型不相同或不是类似的字符串类型。 支持以下类型列之间的完全联接: 数据类型相同或是 DT_STR 与 DT_WSTR 组合。|  
|0xC020830D|-1071611123|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_COPYCOLUMN_DATATYPES|复制列“%1”与“%2”的数据类型不相同或者是完全无法转换的字符串类型。 发生这种情况，是由于支持以下类型列之间从引用到输出的复制: 数据类型相同或是 DT_STR 与 DT_WSTR 组合，但不支持其他类型。|  
|0xC020830E|-1071611122|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_PASSTHRUCOLUMN_DATATYPES|传递列“%1”与“%2”的数据类型不相同。 只有具有相同数据类型的列才能作为从输入到输出的传递列。|  
|0xC020830F|-1071611121|DTS_E_TXFUZZYLOOKUP_UNABLETOLOCATEREFCOLUMN|找不到引用列“%1”。|  
|0xC0208311|-1071611119|DTS_E_TXFUZZYLOOKUP_OUTPUT_COLUMN_MUST_BE_PASSTHRU_COLUMN_OR_A_COPY_COLUMN|必须为输出列指定一个且只能指定一个 CopyColumn 或 PassThruColumn 属性。 当 CopyColumn 属性和 PassThruColumn 属性都被设置为非空值，或当 CopyColumn 属性和 PassThruColumn 属性都未被设置为非空值时，会发生此错误。|  
|0xC0208312|-1071611118|DTS_E_TXFUZZYLOOKUP_PASSTHRU_COLUMN_NOT_FOUND|在输入列集合中找不到为输出列“%3”的属性“%2”指定的源沿袭 ID“%1!d!” 。 如果在输入集内找不到在输出列上被指定为传递列的输入列 ID 时，将发生此错误。|  
|0xC0208313|-1071611117|DTS_E_TXFUZZYLOOKUP_INDEXED_COLUMN_NOT_FOUND_IN_REF_TABLE|在引用表/查询中找不到预建索引“%2”中的列“%1”。 如果在生成预先存在的匹配索引之后，引用表的架构/查询发生了更改，将出现这种情况。|  
|0xC0208314|-1071611116|DTS_E_TXFUZZYLOOKUP_TOKEN_TOO_LONG|组件遇到超过 2147483647 个字符的标记。|  
|0xC0208315|-1071611115|DTS_E_RAWMETADATAMISMATCHTYPE|无法追加输出文件。 列“%1”是按名称匹配的，而文件中列的类型为 %2，输入列的类型为 %3。 列的元数据的数据类型不匹配。|  
|0xC0208316|-1071611114|DTS_E_RAWMETADATAMISMATCHSIZE|无法追加输出文件。 列“%1”是按名称匹配的，而该文件中相应列的最大长度为 %2!d!， 输入列的最大长度为 %3!d!。 列的元数据的长度不匹配。|  
|0xC0208317|-1071611113|DTS_E_RAWMETADATAMISMATCHCODEPAGE|无法追加输出文件。 列“%1”是按名称匹配的，而文件列的代码页为 %2!d!， 输入列的代码页为 %3!d!。 指定列的元数据的代码页不匹配。|  
|0xC0208318|-1071611112|DTS_E_RAWMETADATAMISMATCHPRECISION|无法追加输出文件。 列“%1”是按名称匹配的，而文件列的精度为 %2!d!， 输入列的精度为 %3!d!。 指定列的元数据的精度不匹配。|  
|0xC0208319|-1071611111|DTS_E_RAWMETADATAMISMATCHSCALE|无法追加输出文件。 列“%1”是按名称匹配的，而文件列的小数位数为 %2!d!， 输入列的小数位数为 %3!d!。  指定列的元数据的小数位数不匹配。|  
|0xC020831A|-1071611110|DTS_E_COULD_NOT_DETERMINE_DATASOURCE_DBMSNAME|无法确定“%1”的 DBMS 名称和版本。 如果连接的 IDBProperties 未返回验证 DBMS 名称和版本所需的信息，将出现这种情况。|  
|0xC020831B|-1071611109|DTS_E_INCORRECT_SQL_SERVER_VERSION|不支持的“%1”DBMS 类型或版本。  必须建立与 Microsoft SQL Server 8.0 版或更高版本的连接。 如果连接的 IDBProperties 未返回正确的版本信息，将出现这种情况。|  
|0xC020831D|-1071611107|DTS_E_CANTDELETEERRORCOLUMNS|%1 是一种特殊的错误输出列，无法删除。|  
|0xC020831E|-1071611106|DTS_E_UNEXPECTEDCOLUMNDATATYPE|为列“%1”指定的数据类型不是所需的类型“%2”。|  
|0xC020831F|-1071611105|DTS_E_INPUTCOLUMNNOTFOUND|在输入列集合中找不到由输出列“%3”的属性“%2”引用的输入列沿袭 ID“%1”。|  
|0xC0208320|-1071611104|DTS_E_TXGROUPDUPS_INPUTCOLUMNNOTJOINED|由输出列“%3”的“%2”属性引用的输入列“%1”，必须将 ToBeCleaned 属性设置为 True，还必须有一个有效的 ExactFuzzy 属性值。|  
|0xC0208322|-1071611102|DTS_E_TXFUZZYLOOKUP_REF_TABLE_MISSING_IDENTITY_INDEX|引用表“%1”没有整数标识列的聚集索引，如果将属性“CopyRefTable”设置为 FALSE，此索引是必需的。 如果 CopyRefTable 为 False，引用表必须具有整数标识列的聚集索引。|  
|0xC0208323|-1071611101|DTS_E_TXFUZZYLOOKUP_REF_CONTAINS_NON_INTEGER_IDENT_COLUMN|引用表“%1”包含不支持的非整数类型标识列。 请使用不包含列“%2”的表视图。  出现这种错误的原因是，复制引用表时，添加了一个整数标识列，而每个表只允许有一个整数标识列。|  
|0xC0208324|-1071611100|DTS_E_TXFUZZY_MATCHCONTRIBUTION_AND_HIERARCHY_SPECIFIED|不能同时指定 MatchContribution 和层次结构信息。 由于这两个属性都是记分所使用的加权系数，因此不允许这样做。|  
|0xC0208325|-1071611099|DTS_E_TXFUZZY_HIERARCHY_INCORRECT|层次结构中表示级别的数字必须唯一。 层次结构中的有效级别值是大于或等于 1 的整数。 数字越小，列在层次结构中的级别越低。 默认值为 0，表示列不属于层次结构。 不允许出现重叠和间断。|  
|0xC0208326|-1071611098|DTS_E_TXFUZZYGROUPING_INSUFFICIENT_FUZZY_JOIN_COLUMNS|没有定义要作为模糊分组依据的列。  至少必须有一个输入列的属性是 ToBeCleaned=true 和 ExactFuzzy=2。|  
|0xC0208329|-1071611095|DTS_E_TXFUZZYLOOKUP_COLUMNINVALID|未知原因导致 ID 为“%1!d!” 的列无效。|  
|0xC020832A|-1071611094|DTS_E_TXFUZZYLOOKUP_UNSUPPORTEDDATATYPE|不支持列“%1”的数据类型。|  
|0xC020832C|-1071611092|DTS_E_TXFUZZYLOOKUP_OUTPUTLENGTHMISMATCH|输出列“%1”的长度小于其源列“%2”的长度。|  
|0xC020832F|-1071611089|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFINPUTCOLUMNS|只能有一个输入列。|  
|0xC0208330|-1071611088|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFOUTPUTCOLUMNS|只能有两个输出列。|  
|0xC0208331|-1071611087|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFINPUTCOLUMN|输入列的数据类型只能是 DT_WSTR 或 DT_NTEXT。|  
|0xC0208332|-1071611086|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFOUTPUTCOLUMN|输出列 [%1!d!] 的数据类型只能是“%2”。|  
|0xC0208333|-1071611085|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFREFERENCECOLUMN|引用列只能采用 DT_STR 或 DT_WSTR 数据类型。|  
|0xC0208334|-1071611084|DTS_E_TERMEXTRACTION_UNABLETOLOCATEREFCOLUMN|查找引用列“%1”时出错。|  
|0xC0208335|-1071611083|DTS_E_TERMEXTRACTION_INCORRECTTERMTYPE|转换的字词类型只能是 WordOnly、PhraseOnly 或 WordPhrase。|  
|0xC0208336|-1071611082|DTS_E_TERMEXTRACTION_INCORRECTFREQUENCYTHRESHOLD|“频率阈值”的值不得低于“%1!d!”。|  
|0xC0208337|-1071611081|DTS_E_TERMEXTRACTION_INCORRECTMAXLENOFTERM|“字词的最大长度”的值不得低于“%1!d!”。|  
|0xC0208338|-1071611080|DTS_E_TERMEXTRACTION_TOOFEWREFERENCECOLUMNS|字词提取引用元数据包含的列太少。|  
|0xC0208339|-1071611079|DTS_E_TERMEXTRACTION_MALLOCERR_REFERENCECOLUMNINFO|分配内存时出错。|  
|0xC020833A|-1071611078|DTS_E_TERMEXTRACTION_MAINWORKSPACE_CREATEERR|创建工作区缓冲区时出错。|  
|0xC020833B|-1071611077|DTS_E_TERMEXTRACTION_OLEDBERR_CREATEBINDING|创建绑定时出现 OLEDB 错误。|  
|0xC020833C|-1071611076|DTS_E_TERMEXTRACTION_OLEDBERR_GETIROWSET|提取行集时出现 OLEDB 错误。|  
|0xC020833D|-1071611075|DTS_E_TERMEXTRACTION_OLEDBERR_FILLBUFFER|填充内部缓存时出现 OLEDB 错误。|  
|0xC020833E|-1071611074|DTS_E_TERMEXTRACTION_PROCESSERR|在第 %1!ld! 行、第 %2!ld! 列提取字词时出错。 返回的错误代码是 0x%3!8.8X!。 从输入中删除它可解决此问题。|  
|0xC020833F|-1071611073|DTS_E_TERMEXTRACTIONORLOOKUP_PROCESSERR_DEPOSITFULL|候选字词的数目超出了其 4G 的限额。|  
|0xC0208340|-1071611072|DTS_E_TERMEXTRACTION_INVALIDOUTTERMTABLEORCOLUMN|用于排除字词的引用表、视图或列无效。|  
|0xC0208341|-1071611071|DTS_E_TXFUZZYLOOKUP_STRINGCOLUMNTOOLONG|字符串列“%1”的长度超过了 4000 个字符。  需要从 DT_STR 类型转换为 DT_WSTR，因此将发生截断。  请缩小列宽，或只使用 DT_WSTR 列类型。|  
|0xC0208342|-1071611070|DTS_E_TERMEXTRACTION_OUTTERMTABLEANDCOLUMNNOTSET|尚未设置用于排除字词的引用表、视图或列。|  
|0xC0208343|-1071611069|DTS_E_TERMLOOKUP_TOOFEWOUTPUTCOLUMNS|字词查找包含的输出列太少。|  
|0xC0208344|-1071611068|DTS_E_TERMLOOKUP_INCORRECTDATATYPEOFREFERENCECOLUMN|引用列只能采用 DT_STR 或 DT_WSTR 数据类型。|  
|0xC0208345|-1071611067|DTS_E_TERMLOOKUP_UNABLETOLOCATEREFCOLUMN|查找引用列“%1”时出错。|  
|0xC0208346|-1071611066|DTS_E_TERMLOOKUP_TOOFEWREFERENCECOLUMNS|查找引用元数据包含的列太少。|  
|0xC0208347|-1071611065|DTS_E_TERMEXTRACTIONORLOOKUP_TESTOFFSETERROR|规范字时出错。|  
|0xC0208348|-1071611064|DTS_E_TERMLOOKUP_MAINWORKSPACE_CREATEERR|创建工作区缓冲区时出错。|  
|0xC0208349|-1071611063|DTS_E_TERMLOOKUP_OLEDBERR_CREATEBINDING|创建绑定时出现 OLEDB 错误。|  
|0xC020834A|-1071611062|DTS_E_TERMLOOKUP_OLEDBERR_GETIROWSET|提取行集时出现 OLEDB 错误。|  
|0xC020834B|-1071611061|DTS_E_TERMLOOKUP_OLEDBERR_FILLBUFFER|填充内部缓存时出现 OLEDB 错误。|  
|0xC020834C|-1071611060|DTS_E_TERMLOOKUP_PROCESSERR|在第 %1!ld! 行、第 %2!ld! 列查找字词时出错。 返回的错误代码是 0x%3!8.8X!。 从输入中删除它可解决此问题。|  
|0xC020834D|-1071611059|DTS_E_TERMLOOKUP_TEXTIDINPUTCOLUMNNOTMAPPEDWITHOUTPUTCOLUMN|至少一个传递列未映射到输出列。|  
|0xC020834E|-1071611058|DTS_E_TERMLOOKUP_INCORRECTEXACTNUMBEROFTEXTCOLUMNS|应有且只应有一个输入列映射到一个引用列。|  
|0xC020834F|-1071611057|DTS_E_TERMLOOKUP_TEXTINPUTCOLUMNHAVEINCORRECTDATATYPE|映射到引用列的输入列的数据类型只能是 DT_NTXT 或 DT_WSTR。|  
|0xC0208354|-1071611052|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX_NAME|引用表名“%1”不是有效的 SQL 标识符。 当无法根据输入字符串分析表名时，就会发生此错误。 名称中可能有空格且未用引号引起。 请查看名称是否已用引号正确引起。|  
|0xC0208355|-1071611051|DTS_E_TERMEXTRACTION_TERMFILTERSTARTITERATIONERROR|字词筛选器开始其迭代时出错。|  
|0xC0208356|-1071611050|DTS_E_TERMEXTRACTION_EMPTYTERMRESULTERROR|在回收用于缓存字词的缓冲区时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC0208357|-1071611049|DTS_E_TERMEXTRACTION_STDLENGTHERROR|STL 容器中发生 std::length_error。|  
|0xC0208358|-1071611048|DTS_E_TERMLOOKUP_SAVEWORDWITHPUNCTERROR|在保存含标点符号的字时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC0208359|-1071611047|DTS_E_TERMLOOKUP_ADDREFERENCETERM|处理第 %1!ld! 个引用字词时出错。 返回的错误代码是 0x%2!8.8X!。 从您的引用表中删除该引用字词可解决此问题。|  
|0xC020835A|-1071611046|DTS_E_TERMLOOKUP_SORREFERENCETERM|对引用字词排序时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC020835B|-1071611045|DTS_E_TERMLOOKUP_COUNTTERM|统计候选字词时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC020835C|-1071611044|DTS_E_FUZZYLOOKUP_REFERENCECACHEFULL|模糊查找无法将整个引用表加载到主内存中，但如果启用了 Exhaustive 属性就必须这样做。  可能是系统内存不足，也可能是为 MaxMemoryUsage 指定的限制值不足以加载引用表。  请将 MaxMemoryUsage 设置为 0 或大幅提高其限制值。  或者，禁用 Exhaustive 属性。|  
|0xC020835D|-1071611043|DTS_E_TERMLOOKUP_INITIALIZE|初始化字词查找引擎时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC020835E|-1071611042|DTS_E_TERMLOOKUP_PROCESSSENTENCE|处理句子时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC020835F|-1071611041|DTS_E_TEXTMININGBASE_APPENDTOTEMPBUFFER|将字符串添加到内部缓冲区时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC0208360|-1071611040|DTS_E_TERMEXTRACTION_SAVEPOSTAG|保存内部缓冲区的词性标记时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC0208361|-1071611039|DTS_E_TERMEXTRACTION_COUNTTERM|统计候选字词时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC0208362|-1071611038|DTS_E_TERMEXTRACTION_INITPOSPROCESSOR|初始化词性处理器时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC0208363|-1071611037|DTS_E_TERMEXTRACTION_INITFSA|加载有限状态自动机时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC0208364|-1071611036|DTS_E_TERMEXTRACTION_INITIALIZE|初始化字词提取引擎时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC0208365|-1071611035|DTS_E_TERMEXTRACTION_PROCESSSENTENCE|在句子内处理时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC0208366|-1071611034|DTS_E_TERMEXTRACTION_INITPOSTAGVECTOR|初始化词性处理器时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC0208367|-1071611033|DTS_E_TERMEXTRACTION_SAVEPTRSTRING|将字符串添加到内部缓冲区时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC0208368|-1071611032|DTS_E_TERMEXTRACTION_ADDWORDTODECODER|将字添加到统计解码器时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC0208369|-1071611031|DTS_E_TERMEXTRACTION_DECODE|对句子进行解码时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC020836A|-1071611030|DTS_E_TERMEXTRACTION_SETEXCLUDEDTERM|设置排除字词时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC020836B|-1071611029|DTS_E_TERMEXTRACTION_PROCESSDOCUMENT|处理输入中的文档时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC020836C|-1071611028|DTS_E_TEXTMININGBASE_TESTPERIOD|在测试点是否是缩写词的一部分时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC020836D|-1071611027|DTS_E_TERMLOOKUP_ENGINEADDREFERENCETERM|设置引用字词时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC020836E|-1071611026|DTS_E_TERMLOOKUP_PROCESSDOCUMENT|处理输入中的文档时出错。 返回的错误代码是 0x%1!8.8X!。|  
|0xC020836F|-1071611025|DTS_E_INVALIDBULKINSERTPROPERTYVALUE|属性 %1 的值是 %2!d!，这是不允许的。  该值必须大于或等于 %3!d!。|  
|0xC0208370|-1071611024|DTS_E_INVALIDBULKINSERTFIRSTROWLASTROWVALUES|属性 %1 的值是 %2!d!，该值必须小于或等于属性 %4 的值 %3!d! 。|  
|0xC0208371|-1071611023|DTS_E_FUZZYLOOKUPUNABLETODELETEEXISTINGMATCHINDEX|在尝试删除名为“%1”的现有模糊匹配索引时出错。 出错的原因可能是: 该表不是由模糊查找(或此版本的模糊查找)创建的，该表已损坏，或者有其他问题。 请尝试手动删除名为“%2”的表，或为 MatchIndexName 属性另指定一个名称。|  
|0xC0208372|-1071611022|DTS_E_TERMEXTRACTION_INCORRECTSCORETYPE|该转换的“计分类型”只能是“频率”或“TFIDF”。|  
|0xC0208373|-1071611021|DTS_E_FUZZYLOOKUPREFTABLETOOBIG|指定的引用表中的行过多。 模糊查找只可用于不足 10 亿行的引用表。 请考虑缩小您的引用表。|  
|0xC0208374|-1071611020|DTS_E_FUZZYLOOKUPUNABLETODETERMINEREFERENCETABLESIZE|无法确定引用表“%1”的大小。  原因可能有: 该对象是视图，而不是表。  当 CopyReferentaceTable=false 时，模糊查找不支持视图。  请确保该表存在且 CopyReferenceTable=true。|  
|0xC0208377|-1071611017|DTS_E_XMLSRCOUTPUTCOLUMNDATATYPENOTSUPPORTED|对于 %3，不支持 %2 的 SSIS 数据流任务数据类型“%1”。|  
|0xC0208378|-1071611016|DTS_E_XMLSRCCANNOTFINDCOLUMNTOSETDATATYPE|无法给 ID 为 %1!d! 的输出列(在 ID 为 %2!d! 的输出中)设置数据类型属性。 找不到该输出或列。|  
|0xC0208379|-1071611015|DTS_E_CUSTOMPROPERTYISREADONLY|无法更改 %2 的自定义属性“%1”的值。|  
|0xC020837A|-1071611014|DTS_E_OUTPUTCOLUMNHASNOERRORCOLUMN|非错误输出中的 %1 在错误输出中没有对应的输出列。|  
|0xC020837B|-1071611013|DTS_E_ERRORCOLUMNHASNOOUTPUTCOLUMN|错误输出中的 %1 在非错误输出中没有对应的输出列。|  
|0xC020837C|-1071611012|DTS_E_ERRORCOLUMNHASINCORRECTPROPERTIES|错误输出中的 %1 的属性与其相应数据源列的属性不匹配。|  
|0xC020837D|-1071611011|DTS_E_ADOSRCOUTPUTCOLUMNDATATYPECANNOTBECHANGED|不能更改 %1 中的输出列的数据类型，DT_WSTR 和 DT_NTEXT 列除外。|  
|0xC020837F|-1071611009|DTS_E_ADOSRCDATATYPEMISMATCH|“%1”的数据类型与源列“%3”的数据类型“%2”不匹配。|  
|0xC0208380|-1071611008|DTS_E_ADOSRCCOLUMNNOTINSCHEMAROWSET|%1 在此架构中没有匹配的源列。|  
|0xC0208381|-1071611007|DTS_E_TERMLOOKUP_INVALIDREFERENCETERMTABLEORCOLUMN|用于引用字词的引用表/视图或列无效。|  
|0xC0208382|-1071611006|DTS_E_TERMLOOKUP_REFERENCETERMTABLEANDCOLUMNNOTSET|尚未设置用于引用字词的引用表/视图或列。|  
|0xC0208383|-1071611005|DTS_E_COLUMNMAPPEDTOALREADYMAPPEDEXTERNALMETADATACOLUMN|%1 被映射到 ID 为 %2!ld! 的外部元数据列，但该列已映射到另一个列。|  
|0xC0208384|-1071611004|DTS_E_TXFUZZYLOOKUP_TOOMANYPREFIXES|为属性“%2”指定的 SQL 对象名称“%1”包含的前缀超出了最大限值。  最多只能有 2 个。|  
|0xC0208385|-1071611003|DTS_E_MGDSRCSTATIC_OVERFLOW|该值太大，该列中容纳不下。|  
|0xC0208386|-1071611002|DTS_E_DATAREADERDESTREADERISCLOSED|SSIS IDataReader 已关闭。|  
|0xC0208387|-1071611001|DTS_E_DATAREADERDESTREADERISATEND|SSIS IDataReader 已到达结果集末尾。|  
|0xC0208388|-1071611000|DTS_E_DATAREADERDESTINVALIDCOLUMNORDINAL|该列的序号位置无效。|  
|0xC0208389|-1071610999|DTS_E_DATAREADERDESTCANNOTCONVERT|无法将 %1 从数据类型“%2”转换为数据类型“%3”。|  
|0xC020838A|-1071610998|DTS_E_DATAREADERDESTINVALIDCODEPAGE|%1 有不支持的代码页 %2!d!。|  
|0xC020838B|-1071610997|DTS_E_XMLSRCEXTERNALMETADATACOLUMNNOTINSCHEMA|%1 没有到 XML 架构的映射。|  
|0xC020838D|-1071610995|DTS_E_TXTERMLOOKUP_MISMATCHED_COLUMN_METADATA|沿袭 ID 为 %1!d! 和 %2!d! 的列的元数据不匹配。 映射到输出列的输入列包含不同的元数据(数据类型、精度、小数位数、长度或代码页)。|  
|0xC020838E|-1071610994|DTS_E_DATAREADERDESTREADERTIMEOUT|SSIS IDataReader 已关闭。 读取已超时。|  
|0xC020838F|-1071610993|DTS_E_ADOSRCINVALIDSQLCOMMAND|执行提供的 SQL 命令时出错:“%1”。 %2|  
|0xC0208390|-1071610992|DTS_E_JOINTYPEDOESNTMATCHETI|为输入列“%1”指定的 JoinType 属性不同于最初建立匹配索引时为对应的引用表列指定的 JoinType。  请用给定的 JoinType 重新生成匹配索引，或将 JoinType 更改为建立匹配索引时所用的类型。|  
|0xC0208392|-1071610990|DTS_E_SQLCEDESTDATATYPENOTSUPPORTED|对于 %3，不支持找到的列“%2”的数据类型“%1”。|  
|0xC0208393|-1071610989|DTS_E_DATAREADERDESTDATATYPENOTSUPPORTED|对于 %3，不支持找到的 %2 的数据类型“%1”。|  
|0xC0208394|-1071610988|DTS_E_RECORDSETDESTDATATYPENOTSUPPORTED|%2 不支持 %1 的数据类型。|  
|0xC0208446|-1071610810|DTS_E_TXSCRIPTMIGRATIONCOULDNOTADDREFERENCE|迁移 %2 时无法添加项目引用“%1”。 可能需要手动完成迁移。|  
|0xC0208447|-1071610809|DTS_E_TXSCRIPTMIGRATIONMULTIPLEENTRYPOINTSFOUND|迁移 %2 时找到多个名为“%1”的入口点。 可能需要手动完成迁移。|  
|0xC0208448|-1071610808|DTS_E_TXSCRIPTMIGRATIONNOENTRYPOINTFOUND|迁移 %1 时找不到入口点。 可能需要手动完成迁移。|  
|0xC020844B|-1071610805|DTS_E_ADODESTINSERTIONFAILURE|数据插入期间出现异常，从访问接口返回的消息为: %1|  
|0xC020844C|-1071610804|DTS_E_ADODESTCONNECTIONTYPENOTSUPPORTED|无法从 %1 检索提供程序固定名称，ADO NET 目标组件目前不支持此行为|  
|0xC020844D|-1071610803|DTS_E_ADODESTARGUMENTEXCEPTION|数据访问接口尝试将数据插入目标时出现参数异常。 返回的消息为: %1|  
|0xC020844E|-1071610802|DTS_E_ADODESTWRONGBATCHSIZE|BatchSize 属性必须为非负整数|  
|0xC020844F|-1071610801|DTS_E_ADODESTERRORUPDATEROW|将该行发送到目标数据源时出错。|  
|0xC0208450|-1071610800|DTS_E_ADODESTEXECUTEREADEREXCEPTION|执行 tSQL 命令引发了异常，消息为: %1|  
|0xC0208451|-1071610799|DTS_E_ADODESTDATATYPENOTSUPPORTED|对于 %3，不支持找到的列“%2”的数据类型“%1”。|  
|0xC0208452|-1071610798|DTS_E_ADODESTFAILEDTOACQUIRECONNECTION|ADO NET 目标未能获取连接 %1。 此连接可能已损坏。|  
|0xC0208453|-1071610797|DTS_E_ADODESTNOTMANAGEDCONNECTION|指定的连接 %1 不是托管连接，请将托管连接用于 ADO NET 目标。|  
|0xC0208454|-1071610796|DTS_E_ADODESTNOERROROUTPUT|此目标组件没有错误输出。 它可能已损坏。|  
|0xC0208455|-1071610795|DTS_E_ADODESTNOLINEAGEID|与外部列 %2 关联的 lineageID %1 在运行时不存在。|  
|0xC0208456|-1071610794|DTS_E_ADODESTEXTERNALCOLNOTEXIST|数据库中不存在 %1。 它可能已被删除或重命名。|  
|0xC0208457|-1071610793|DTS_E_ADODESTGETSCHEMATABLEFAILED|无法获取外部列的属性。 您输入的表名可能不存在，或者您没有对表对象的 SELECT 权限，并且通过连接获取列属性的替代尝试已失败。 详细错误消息为: %1|  
|0xC0208458|-1071610792|DTS_E_ADODESTCOLUMNERRORDISPNOTSUPPORTED|ADO NET 目标组件不支持输入列错误处理。|  
|0xC0208459|-1071610791|DTS_E_ADODESTCOLUMNTRUNDISPNOTSUPPORTED|ADO NET 目标组件不支持输入列截断处理。|  
|0xC020845A|-1071610790|DTS_E_ADODESTINPUTTRUNDISPNOTSUPPORTED|ADO NET 目标组件不支持输入截断行处理。|  
|0xC020845B|-1071610789|DTS_E_ADODESTTABLENAMEERROR|不应是此表或视图名称。 \n\t 如果您在引用表名，请使用您选定的数据访问接口的前缀 %1 和后缀 %2 进行引用。 \n\t 如果您要使用多部分名称，请为表名使用最多三个部分。|  
|0xC0209001|-1071607807|DTS_E_FAILEDTOFINDCOLUMNINBUFFER|在缓冲区中找不到沿袭 ID 为 %2!d! 的列“%1”。 缓冲区管理器返回了错误代码 0x%3!8.8X!。|  
|0xC0209002|-1071607806|DTS_E_FAILEDTOGETCOLUMNINFOFROMBUFFER|无法从缓冲区获取列“%1”(%2!d!)的信息。 返回的错误代码是 0x%3!8.8X!。|  
|0xC0209011|-1071607791|DTS_E_TXAGG_ARITHMETICOVERFLOW|在对“%1”执行聚合运算时出现算术溢出。|  
|0xC0209012|-1071607790|DTS_E_FAILEDTOGETCOLINFO|无法从缓冲区获取第 %1!ld! 行、第 %2!ld! 列的信息。 返回的错误代码是 0x%3!8.8X!。|  
|0xC0209013|-1071607789|DTS_E_FAILEDTOSETCOLINFO|无法将第 %1!ld! 行、第 %2!ld! 列的信息设置到缓冲区中。 返回的错误代码是 0x%3!8.8X!。|  
|0xC0209015|-1071607787|DTS_E_REQUIREDBUFFERISNOTAVAILBLE|所需的缓冲区不可用。|  
|0xC0209016|-1071607786|DTS_E_FAILEDTOGETBUFFERBOUNDARYINFO|尝试获取缓冲区边界信息的操作失败，错误代码为 0x%1!8.8X!。|  
|0xC0209017|-1071607785|DTS_E_FAILEDTOSETBUFFERENDOFROWSET|为缓冲区设置行集末尾失败，错误代码为 0x%1!8.8X!。|  
|0xC0209018|-1071607784|DTS_E_FAILEDTOGETDATAFORERROROUTPUTBUFFER|无法获取错误输出缓冲区的数据。|  
|0xC0209019|-1071607783|DTS_E_FAILEDTOREMOVEROWFROMBUFFER|从缓冲区删除行失败，错误代码为 0x%1!8.8X!。|  
|0xC020901B|-1071607781|DTS_E_FAILEDTOSETBUFFERERRORINFO|尝试设置缓冲区错误信息的操作失败，错误代码为 0x%1!8.8X!。|  
|0xC020901C|-1071607780|DTS_E_COLUMNSTATUSERROR|%2 上的 %1 出错。 返回的列状态是:“%3”。|  
|0xC020901D|-1071607779|DTS_E_TXLOOKUP_METADATAXMLCACHEERR|无法缓存引用元数据。|  
|0xC020901E|-1071607778|DTS_E_TXLOOKUP_ROWLOOKUPERROR|在查找期间行没有生成任何匹配项。|  
|0xC020901F|-1071607777|DTS_E_INVALIDERRORDISPOSITION|%1 存在无效的错误行处理设置或截断行处理设置。|  
|0xC0209022|-1071607774|DTS_E_FAILEDTODIRECTERRORROW|未能将该行定向到错误输出，错误代码为 0x%1!8.8X!。|  
|0xC0209023|-1071607773|DTS_E_FAILEDTOPREPARECOLUMNSTATUSESFORINSERT|为插入操作准备列状态失败，错误代码为 0x%1!8.8X!。|  
|0xC0209024|-1071607772|DTS_E_FAILEDTOFINDCOLUMNBYLINEAGEID|尝试在数据流任务缓冲区中查找沿袭 ID 为 %2!d! 的 %1 失败，错误代码为 0x%3!8.8X!。|  
|0xC0209025|-1071607771|DTS_E_FAILEDTOFINDNONSPECIALERRORCOLUMN|在 %1 中未能找到任何非特殊错误列。|  
|0xC0209029|-1071607767|DTS_E_INDUCEDTRANSFORMFAILUREONERROR|SSIS 错误代码 DTS_E_INDUCEDTRANSFORMFAILUREONERROR。  由于出现错误代码 0x%2!8.8X!， 而且针对“%3”的错误行处理设置指定一旦出错就失败。 在指定组件的指定对象上出现错误。  可能在此之前已经发出错误消息，提供了有关失败的详细信息。|  
|0xC020902A|-1071607766|DTS_E_INDUCEDTRANSFORMFAILUREONTRUNCATION|“%1”由于发生截断而失败，而且针对“%2”的截断行处理设置指定截断时出错。 在指定组件的指定对象上出现截断错误。|  
|0xC020902B|-1071607765|DTS_E_TXSPLITEXPRESSIONEVALUATEDTONULL|“%2”的表达式“%1”的计算结果为 NULL，但“%3”要求布尔值结果。 请修改输出的错误行处置设置，以将此结果视为 False (忽略失败)，或者将该行重定向到错误输出(重定向行)。  表达式结果必须是用于“有条件拆分”的布尔值。  NULL 表达式结果不对。|  
|0xC020902C|-1071607764|DTS_E_TXSPLITSTATIC_EXPRESSIONEVALUATEDTONULL|该表达式的计算结果为 NULL，但要求布尔值结果。 请修改输出的错误行处置设置，以将此结果视为 False (忽略失败)，或者将该行重定向到错误输出(重定向行)。 表达式结果必须是用于“有条件拆分”的布尔值。  NULL 表达式结果不对。|  
|0xC020902D|-1071607763|DTS_E_UTF16BIGENDIANFORMATNOTSUPPORTED|不支持 UTF-16 big endian 文件格式，  只支持 UTF-16 little endian 格式。|  
|0xC020902E|-1071607762|DTS_E_UTF8FORMATNOTSUPPORTEDASUNICODE|不将 UTF-8 文件格式作为 Unicode 予以支持。|  
|0xC020902F|-1071607761|DTS_E_DTPXMLCANTREADIDATTR|无法读取 ID 属性。|  
|0xC020903E|-1071607746|DTS_E_TXLOOKUP_INDEXCOLUMNREUSED|缓存索引列 %1 被多个查找输入列引用。|  
|0xC020903F|-1071607745|DTS_E_TXLOOKUP_INDEXCOLUMNSMISMATCH|查找不引用所有缓存连接管理器索引列。 查找中已联接列的数量: %1!d!。 索引列的数量: %2!d!。|  
|0xC0209069|-1071607703|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|由于除符号不匹配或数据溢出之外的其他原因，导致无法转换数据值。|  
|0xC020906A|-1071607702|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|数据值违反了架构约束。|  
|0xC020906B|-1071607701|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_TRUNCATED|数据被截断。|  
|0xC020906C|-1071607700|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SIGNMISMATCH|由于数据值带有符号而访问接口所使用的类型不带符号，导致转换失败。|  
|0xC020906D|-1071607699|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_DATAOVERFLOW|由于数据值溢出了访问接口所使用的类型，导致转换失败。|  
|0xC020906E|-1071607698|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_UNAVAILABLE|无可用状态。|  
|0xC020906F|-1071607697|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|该用户没有写入此列的正确权限。|  
|0xC0209070|-1071607696|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|数据值违反了该列的完整性约束。|  
|0xC0209071|-1071607695|DTS_E_OLEDBSOURCEADAPTERSTATIC_UNAVAILABLE|无可用状态。|  
|0xC0209072|-1071607694|DTS_E_OLEDBSOURCEADAPTERSTATIC_CANTCONVERTVALUE|由于除符号不匹配或数据溢出之外的其他原因，导致无法转换数据值。|  
|0xC0209073|-1071607693|DTS_E_OLEDBSOURCEADAPTERSTATIC_TRUNCATED|数据被截断。|  
|0xC0209074|-1071607692|DTS_E_OLEDBSOURCEADAPTERSTATIC_SIGNMISMATCH|由于数据值带有符号而访问接口所使用的类型不带符号，导致转换失败。|  
|0xC0209075|-1071607691|DTS_E_OLEDBSOURCEADAPTERSTATIC_DATAOVERFLOW|由于数据值溢出了访问接口所使用的类型，导致转换失败。|  
|0xC0209076|-1071607690|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|数据值违反了架构约束。|  
|0xC0209077|-1071607689|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|由于除符号不匹配或数据溢出之外的其他原因，导致无法转换数据值。|  
|0xC0209078|-1071607688|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_TRUNCATED|数据被截断。|  
|0xC0209079|-1071607687|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SIGNMISMATCH|由于数据值带有符号而访问接口所使用的类型不带符号，导致转换失败。|  
|0xC020907A|-1071607686|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_DATAOVERFLOW|由于数据值溢出了访问接口所使用的类型，导致转换失败。|  
|0xC020907B|-1071607685|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_UNAVAILABLE|无可用状态。|  
|0xC020907C|-1071607684|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|该用户没有写入此列的正确权限。|  
|0xC020907D|-1071607683|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|该数据值违反了完整性约束。|  
|0xC020907F|-1071607681|DTS_E_TXDATACONVERTSTATIC_CANTCONVERTVALUE|由于除符号不匹配或数据溢出之外的其他原因，导致无法转换数据值。|  
|0xC0209080|-1071607680|DTS_E_TXDATACONVERTSTATIC_TRUNCATED|数据被截断。|  
|0xC0209081|-1071607679|DTS_E_TXDATACONVERTSTATIC_SIGNMISMATCH|由于数据值带有符号而访问接口所使用的类型不带符号，导致转换失败。|  
|0xC0209082|-1071607678|DTS_E_TXDATACONVERTSTATIC_DATAOVERFLOW|由于数据值溢出了数据转换使用的类型，导致转换失败。|  
|0xC0209083|-1071607677|DTS_E_FLATFILESOURCEADAPTERSTATIC_UNAVAILABLE|无可用状态。|  
|0xC0209084|-1071607676|DTS_E_FLATFILESOURCEADAPTERSTATIC_CANTCONVERTVALUE|由于除符号不匹配或数据溢出之外的其他原因，导致无法转换数据值。|  
|0xC0209085|-1071607675|DTS_E_FLATFILESOURCEADAPTERSTATIC_TRUNCATED|数据被截断。|  
|0xC0209086|-1071607674|DTS_E_FLATFILESOURCEADAPTERSTATIC_SIGNMISMATCH|由于数据值带有符号而平面文件源适配器使用的类型不带符号，导致转换失败。|  
|0xC0209087|-1071607673|DTS_E_FLATFILESOURCEADAPTERSTATIC_DATAOVERFLOW|由于数据值溢出了平面文件源适配器使用的类型，导致转换失败。|  
|0xC020908E|-1071607666|DTS_E_TXDATACONVERTSTATIC_UNAVAILABLE|无可用状态。|  
|0xC0209090|-1071607664|DTS_E_FILEOPENERR_FORREAD|无法打开要读取的文件“%1”，错误代码为 0x%2!8.8X!。|  
|0xC0209091|-1071607663|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD|无法打开读取的文件。|  
|0xC0209092|-1071607662|DTS_E_FILEOPENERR_FORWRITE|无法打开要执行写操作的文件“%1”，错误代码为 0x%2!8.8X!。|  
|0xC0209093|-1071607661|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE|无法打开要执行写操作的文件。|  
|0xC0209094|-1071607660|DTS_E_TXFILEINSERTERSTATIC_INSERTERCANTREAD|无法读取文件。|  
|0xC0209095|-1071607659|DTS_E_TXFILEEXTRACTORSTATIC_EXTRACTORCANTWRITE|无法写入文件。|  
|0xC0209099|-1071607655|DTS_E_DTPXMLINVALIDPROPERTYARRAYTOOMANYVALUES|在对类型数组的属性进行分析时找到的数组元素过多。 elementCount 少于找到的数组元素个数。|  
|0xC020909A|-1071607654|DTS_E_DTPXMLINVALIDPROPERTYARRAYNOTENOUGHVALUES|在对类型数组的属性进行分析时找到的数组元素过少。 elementCount 多于找到的数组元素个数。|  
|0xC020909E|-1071607650|DTS_E_FILEOPENERR_FORWRITE_FILENOTFOUND|无法打开要执行写操作的文件“%1”。 找不到该文件。|  
|0xC020909F|-1071607649|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILENOTFOUND|无法打开要执行写操作的文件。 找不到该文件。|  
|0xC02090A0|-1071607648|DTS_E_FILEOPENERR_FORWRITE_PATHNOTFOUND|无法打开要执行写操作的文件“%1”。 找不到路径。|  
|0xC02090A1|-1071607647|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_PATHNOTFOUND|无法打开要执行写操作的文件。 找不到路径。|  
|0xC02090A2|-1071607646|DTS_E_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|无法打开要执行写操作的文件“%1”。 打开的文件太多。|  
|0xC02090A3|-1071607645|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|无法打开要执行写操作的文件。 打开的文件太多。|  
|0xC02090A4|-1071607644|DTS_E_FILEOPENERR_FORWRITE_ACCESSDENIED|无法打开要执行写操作的文件“%1”。 您没有适当的权限。|  
|0xC02090A5|-1071607643|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_ACCESSDENIED|无法打开要执行写操作的文件。 您没有适当的权限。|  
|0xC02090A6|-1071607642|DTS_E_FILEOPENERR_FORWRITE_FILEEXISTS|无法打开要执行写操作的文件“%1”。 该文件存在且不能被覆盖。 如果 AllowAppend 属性为 FALSE，并且 ForceTruncate 属性被设置为 FALSE，则存在该文件将会导致此失败。|  
|0xC02090A7|-1071607641|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILEEXISTS|无法打开要执行写操作的文件。 该文件已存在且不能被覆盖。 如果 AllowAppend 属性和 ForceTruncate 属性都为 FALSE，则存在该文件将会导致此错误。|  
|0xC02090A8|-1071607640|DTS_E_INCORRECTCUSTOMPROPERTYVALUEFOROBJECT|%2 的自定义属性“%1”的值不正确。|  
|0xC02090A9|-1071607639|DTS_E_COLUMNSHAVEINCOMPATIBLEMETADATA|列“%1”和“%2”的元数据不兼容。|  
|0xC02090AD|-1071607635|DTS_E_FILEWRITEERR_DISKFULL|磁盘已满，无法打开要执行写操作的文件“%1”。 磁盘空间不足，无法保存此文件。|  
|0xC02090AE|-1071607634|DTS_E_TXFILEEXTRACTORSTATIC_FILEWRITEERR_DISKFULL|磁盘已满，无法打开要执行写操作的文件。|  
|0xC02090B9|-1071607623|DTS_E_TXAGG_SORTKEYGENFAILED|未能生成排序键，错误代码为 0x%1!8.8X!。 ComparisonFlags 已启用，并且用 LCMapString 生成排序键失败。|  
|0xC02090BA|-1071607622|DTS_E_TXCHARMAPLCMAPFAILED|转换未能映射字符串，返回的错误代码为 0x%1!8.8X!。 LCMapString 失败。|  
|0xC02090BB|-1071607621|DTS_E_FILEOPENERR_FORREAD_FILENOTFOUND|无法打开要读取的文件“%1”。 找不到该文件。|  
|0xC02090BC|-1071607620|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_FILENOTFOUND|无法打开要读取的文件。 找不到该文件。|  
|0xC02090BD|-1071607619|DTS_E_FILEOPENERR_FORREAD_PATHNOTFOUND|无法打开要读取的文件“%1”。 找不到路径。|  
|0xC02090BE|-1071607618|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_PATHNOTFOUND|无法打开要读取的文件。 找不到该文件。|  
|0xC02090BF|-1071607617|DTS_E_FILEOPENERR_FORREAD_TOOMANYOPENFILES|无法打开要读取的文件“%1”。 打开的文件太多。|  
|0xC02090C0|-1071607616|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_TOOMANYOPENFILES|无法打开要读取的文件。 打开的文件太多。|  
|0xC02090C1|-1071607615|DTS_E_FILEOPENERR_FORREAD_ACCESSDENIED|无法打开要读取的文件“%1”。 拒绝访问。|  
|0xC02090C2|-1071607614|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_ACCESSDENIED|无法打开要读取的文件。 您没有适当的权限。|  
|0xC02090C3|-1071607613|DTS_E_INSERTERINVALIDBOM|文件“%1”的字节顺序标记(BOM)值是 0x%2!4.4X!，但该值应为 0x%3!4.4X!。 为此文件设置了 ExpectBOM 属性，但该文件中缺少 BOM 值或该值无效。|  
|0xC02090C4|-1071607612|DTS_E_TXFILEINSERTERSTATIC_INSERTERINVALIDBOM|该文件的字节顺序标记 (BOM) 值无效。 为此文件设置了 ExpectBOM 属性，但该文件中缺少 BOM 值或该值无效。|  
|0xC02090C5|-1071607611|DTS_E_NOCOMPONENTATTACHED|%1 未被附加到某一组件。  要求附加某一组件。|  
|0xC02090C9|-1071607607|DTS_E_TXLOOKUP_INVALIDMAXMEMORYPROP|自定义属性 %1 的值不正确，  该值应是介于 %2!d! 和 %3!I64d! 之间的数字。|  
|0xC02090CA|-1071607606|DTS_E_TXAGG_COMPFLAGS_BADAGGREGATIONTYPE|对于为此列选定的聚合类型，不能指定自定义属性“%1”。 只能为“分组依据”和“非重复计数”聚合类型指定比较标志自定义属性。|  
|0xC02090CB|-1071607605|DTS_E_TXAGG_COMPFLAGS_BADDATATYPE|只能为数据类型为 DT_STR 或 DT_WSTR 的列指定比较标志自定义属性“%1”。|  
|0xC02090CD|-1071607603|DTS_E_TXAGG_AGGREGATION_FAILURE|对 %1 执行聚合运算失败，错误代码为 0x%2!8.8X!。|  
|0xC02090CF|-1071607601|DTS_E_MAPPINGSETUPERROR|建立映射时出错。 %1|  
|0xC02090D0|-1071607600|DTS_E_XMLSRCUNABLETOREADXMLDATA|%1 无法读取 XML 数据。|  
|0xC02090D1|-1071607599|DTS_E_XMLSRCUNABLETOGETXMLDATAVARIABLE|%1 无法获取“%2”属性指定的变量。|  
|0xC02090D2|-1071607598|DTS_E_NODATATABLEMATCHROWID|%1 包含值为 %2 的 RowsetID，它没有引用架构中的数据表。|  
|0xC02090D6|-1071607594|DTS_E_TXAGG_BADKEYSVALUE|属性 %1 要么为空，要么必须是介于 %2!u! 和 %3!u! 之间的数字。 Keys 或 CountDistinctKeys 属性的值无效。 该属性应为介于 0 和 ULONG_MAX (含)之间的数值，或者不设置。|  
|0xC02090D7|-1071607593|DTS_E_TXAGG_TOOMANYKEYS|聚合组件遇到了过多的非重复键组合。 它所能容纳的非重复值不能超过 %1!u! 个。 在主工作区中的非重复键值超过 ULONG_MAX 的值。|  
|0xC02090D8|-1071607592|DTS_E_TXAGG_TOOMANYCOUNTDISTINCTVALUES|聚合组件在计算非重复计数聚合时遇到了过多的非重复值。 它所能容纳的非重复值不能超过 %1!u! 个。 在计算非重复计数聚合时遇到的非重复值超过了 ULONG_MAX 的值。|  
|0xC02090D9|-1071607591|DTS_E_FAILEDTOWRITETOTHEFILENAMECOLUMN|写入文件名列失败，错误代码为 0x%1!8.8X!。|  
|0xC02090DC|-1071607588|DTS_E_FAILEDTOFINDERRORCOLUMN|遇到错误，但无法确定导致该错误的列。|  
|0xC02090E3|-1071607581|DTS_E_TXLOOKUP_FAILEDUPGRADE_BAD_VERSION|无法将查找元数据从版本 %1!d! 升级到 %2!d!。 查找转换无法在对 PerformUpgrade() 的调用中从现有版本号升级元数据。|  
|0xC02090E5|-1071607579|DTS_E_TERMEXTRACTIONORLOOKUP_NTEXTSPLITED|找不到句子的结束边界。|  
|0xC02090E6|-1071607578|DTS_E_TERMEXTRACTION_EXCEED_MAXWORDNUM|输入文本中的某个句子太长，字词提取转换无法处理该输入文本。 请将该句子分成若干个短句。|  
|0xC02090E7|-1071607577|DTS_E_XMLSRCFAILEDTOCREATEREADER|%1 无法读取 XML 数据。 %2|  
|0xC02090F0|-1071607568|DTS_E_TXLOOKUP_REINITMETADATAFAILED|对查找转换方法 ReinitializeMetadata 的调用失败。|  
|0xC02090F1|-1071607567|DTS_E_TXLOOKUP_NOJOINS|查找转换必须包含至少一个与某一引用列联接的输入列，但未指定任何这样的列。 您必须指定至少一个联接列。|  
|0xC02090F2|-1071607566|DTS_E_MANAGEDERR_BADFORMATSPECIFICATION|托管错误基础结构发布的消息字符串包含格式有误的指定。 这是内部错误。|  
|0xC02090F3|-1071607565|DTS_E_MANAGEDERR_UNSUPPORTEDTYPE|在使用托管错误基础结构设置消息字符串的格式时，某个变量类型不支持格式设置。 这是内部错误。|  
|0xC02090F5|-1071607563|DTS_E_DATAREADERSRCUNABLETOPROCESSDATA|%1 无法处理这些数据。 %2|  
|0xC02090F6|-1071607562|DTS_E_XMLSRCEMPTYPROPERTY|%2 的属性“%1”为空。|  
|0xC02090F7|-1071607561|DTS_E_XMLSRCINVALIDOUTPUTNAME|为 XML 表创建名称为“%1”、路径为“%2”的输出失败，因为该名称无效。|  
|0xC02090F8|-1071607560|DTS_E_MGDSRC_OVERFLOW|该值太大，%1 中容纳不下。|  
|0xC02090F9|-1071607559|DTS_E_DATAREADERDESTUNABLETOPROCESSDATA|%1 无法处理这些数据。|  
|0xC02090FA|-1071607558|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONTRUNCATION|由于发生截断，且在“%3”处针对“%2”的截断行处理设置指定发生截断时失败，所以“%1”失败。 在指定组件的指定对象上出现截断错误。|  
|0xC02090FB|-1071607557|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONERROR|由于出现错误代码 0x%2!8.8X!， 且在“%4”处针对“%3”的错误行处理设置指定出错时失败，所以“%1”失败。 在指定组件的指定对象上出现错误。|  
|0xC0209291|-1071607151|DTS_E_SQLCEDESTSTATIC_FAILEDTOSETVALUES|SQLCE 目标无法为该行设置列值。|  
|0xC0209292|-1071607150|DTS_E_SQLCEDESTSTATIC_FAILEDTOINSERT|SQLCE 目标无法插入该行。|  
|0xC0209293|-1071607149|DTS_E_TXFUZZYLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|加载列的元数据时遇到 OLEDB 错误。|  
|0xC0209294|-1071607148|DTS_E_TXFUZZYLOOKUP_TOOFEWREFERENCECOLUMNS|查找引用元数据包含的列太少。|  
|0xC0209295|-1071607147|DTS_E_TXSCD_OLEDBERR_LOADCOLUMNMETADATA|加载列的元数据时遇到 OLEDB 错误。|  
|0xC0209296|-1071607146|DTS_E_TXSCD_TOOFEWREFERENCECOLUMNS|查找引用元数据包含的列太少。|  
|0xC0209297|-1071607145|DTS_E_TXSCD_MALLOCERR_REFERENCECOLUMNINFO|无法分配内存。|  
|0xC0209298|-1071607144|DTS_E_TXSCD_MALLOCERR_BUFFCOL|无法分配内存。|  
|0xC0209299|-1071607143|DTS_E_TXSCD_MAINWORKSPACE_CREATEERR|无法创建工作区缓冲区。|  
|0xC020929A|-1071607142|DTS_E_DTPXMLDOMCREATEERROR|无法实例化 XML DOM 文档，请确保 MSXML 二进制文件已正确安装并注册。|  
|0xC020929B|-1071607141|DTS_E_DTPXMLDOMLOADERROR|无法将 XML 数据加载到本地 DOM 中进行处理。|  
|0xC020929C|-1071607140|DTS_E_RSTDESTBADVARIABLETYPE|运行时变量“%1”的类型不正确。 该运行时变量的类型必须是 Object。|  
|0xC020929E|-1071607138|DTS_E_XMLDATAREADERMULTIPLEINLINEXMLSCHEMASNOTSUPPORTED|XML 源适配器无法处理 XML 数据。 不支持多个内联架构。|  
|0xC020929F|-1071607137|DTS_E_XMLDATAREADERANYTYPENOTSUPPORTED|XML 源适配器无法处理 XML 数据。 不能将元素的内容声明为 anyType。|  
|0xC02092A0|-1071607136|DTS_E_XMLDATAREADERGROUPREFNOTSUPPORTED|XML 源适配器无法处理 XML 数据。 元素的内容不能包含对组的引用(ref)。|  
|0xC02092A1|-1071607135|DTS_E_XMLDATAREADERMIXEDCONTENTFORCOMPLEXTYPESNOTSUPPORTED|XML 源适配器不支持复杂类型的混合内容模型。|  
|0xC02092A2|-1071607134|DTS_E_XMLDATAREADERINLINESCHEMAFOUNDINSOURCEXML|XML 源适配器无法处理 XML 数据。 内联架构必须是源 Xml 中的第一个子节点。|  
|0xC02092A3|-1071607133|DTS_E_XMLDATAREADERNOINLINESCHEMAFOUND|XML 源适配器无法处理 XML 数据。 在源 XML 中找不到任何内联架构，但 "UseInlineSchema" 属性却设置为 true。|  
|0xC02092A4|-1071607132|DTS_E_CONNECTIONMANAGERTRANSACTEDANDRETAINEDINBULKINSERT|该组件不能使用通过 Fastload 或大容量插入将其连接保留在某一事务中的连接管理器。|  
|0xC02092A5|-1071607131|DTS_E_OUTPUTREDIRECTINTRANSACTIONNOTALLOWED|不能将 %1 设置为使用事务中的连接在出错时重定向。|  
|0xC02092A6|-1071607130|DTS_E_FOUNDORPHANEDEXTERNALMETADATACOLUMN|%1 无相应的输入列或输出列。|  
|0xC02092A9|-1071607127|DTS_E_RAWDESTNOINPUTCOLUMNS|未选定任何要写入该文件的列。|  
|0xC02092AA|-1071607126|DTS_E_RAWDESTBLOBDATATYPE|%1 的数据类型无效。 无法将数据类型为 DT_IMAGE、DT_TEXT 和 DT_NTEXT 的列写入原始文件。|  
|0xC02092AB|-1071607125|DTS_E_RAWDESTWRONGEXTERNALMETADATAUSAGE|此组件未正确使用外部元数据集合。 它应在追加或截断现有文件时使用外部元数据， 否则，不需要使用外部元数据。|  
|0xC02092AC|-1071607124|DTS_E_RAWDESTMAPPEDINPUTCOLUMN|%1 被映射到 ID 为 %2!d! 的外部元数据列。 当 Write Option 的值为 Create Always (始终创建)时，不应将输入列映射到外部元数据列。|  
|0xC02092AD|-1071607123|DTS_E_RAWFILECANTOPENFORMETADATA|无法打开该文件来读取元数据。 如果该文件不存在，而且组件已定义了外部元数据，则可将“ValidateExternalMetadata”属性设置为“false”。这样，就会在运行时创建该文件。|  
|0xC02092AE|-1071607122|DTS_E_FAILEDTOACCESSLOBCOLUMN|从数据源列“%1”的数据流缓冲区中访问 LOB 数据失败，错误代码为 0x%2!8.8X!。|  
|0xC02092AF|-1071607121|DTS_E_XMLSRCUNABLETOPROCESSXMLDATA|%1 无法处理 XML 数据。 %2|  
|0xC02092B0|-1071607120|DTS_E_XMLSRCSTATIC_UNABLETOPROCESSXMLDATA|XML 源适配器无法处理 XML 数据。|  
|0xC02092B1|-1071607119|DTS_E_RAWINVALIDACCESSMODE|值 %1!d! 被认为是无效的访问模式。|  
|0xC02092B2|-1071607118|DTS_E_INCOMPLETEDATASOURCECOLUMNFOUND|没有数据源列“%1”的完整元数据信息。  请确保数据源中已正确定义该列。|  
|0xC02092B3|-1071607117|DTS_E_TXAUDIT_ONLYSTRINGLENGTHCHANGEALLOWED|只能更改“用户名”列、“包名称”列、“任务名称”列和“计算机名称”列的长度。  所有其他审核列数据类型信息都是只读的。|  
|0xC02092B4|-1071607116|DTS_E_ROWSETUNAVAILABLE|OLE DB 访问接口没有返回基于 SQL 命令的行集。|  
|0xC02092B5|-1071607115|DTS_E_COMMITFAILED|提交失败。|  
|0xC02092B6|-1071607114|DTS_E_USEBINARYFORMATREQUIRESANSIFILE|%2 的自定义属性“%1”只能用于 ansi 文件。|  
|0xC02092B7|-1071607113|DTS_E_USEBINARYFORMATREQUIRESBYTES|%2 的自定义属性“%1”只能用于 DT_BYTES。|  
|0xC0209302|-1071607038|DTS_E_OLEDB_NOPROVIDER_ERROR|SSIS 错误代码 DTS_E_OLEDB_NOPROVIDER_ERROR。  所请求的 OLE DB 访问接口 %2 尚未注册。 错误代码:0x%1!8.8X!。|  
|0xC0209303|-1071607037|DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR|SSIS 错误代码 DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR。  所请求的 OLE DB 访问接口 %2 尚未注册 -- 可能是由于没有可用的 64 位访问接口。  错误代码:0x%1!8.8X!。|  
|0xC0209306|-1071607034|DTS_E_MULTICACHECOLMAPPINGS|缓存列“%1”映射至多个列。 请删除重复的列映射。|  
|0xC0209307|-1071607033|DTS_E_COLNOTMAPPEDTOCACHECOL|%1 未映射到有效的缓存列。|  
|0xC0209308|-1071607032|DTS_E_CACHECOLDATATYPEINCOMPAT|由于数据类型不匹配，无法映射输入列“%1”和缓存列“%2”。|  
|0xC0209309|-1071607031|DTS_E_INCORRECTINPUTCACHECOLCOUNT|输入列的数目与缓存列的数目不匹配。|  
|0xC020930A|-1071607030|DTS_E_INVALIDCACHEFILENAME|未提供缓存文件名或缓存文件名无效。 请提供有效的缓存文件名。|  
|0xC020930B|-1071607029|DTS_E_CACHECOLINDEXPOSMISMATCH|列的索引位置“%1”与缓存连接管理器列的索引位置“%2”不同。|  
|0xC020930C|-1071607028|DTS_E_FAILEDTOLOADCACHE|无法从文件“%1”中加载缓存。|  
|0xC020930D|-1071607027|DTS_E_TXLOOKUP_REFCOLUMNISNOTINDEX|查找输入列 %1 引用非索引缓存列 %2。|  
|0xC020930E|-1071607026|DTS_E_FAILEDTOGETCONNECTIONSTRING|无法获取连接字符串。|  
|0xC020930F|-1071607025|DTS_E_CACHECOLDATATYPEPROPINCOMPAT|由于一个或多个数据类型属性不匹配，无法映射输入列“%1”和缓存列“%2”。|  
|0xC0209311|-1071607023|DTS_E_CACHECOLUMNOTFOUND|在缓存中找不到缓存列“%1”。|  
|0xC0209312|-1071607022|DTS_E_CACHECOLUMNMAPPINGFAILED|无法将 %1 映射至缓存列。 hresult 为 0x%2!8.8X!。|  
|0xC0209313|-1071607021|DTS_E_CACHELOADEDFROMFILE|由于 %2 已从文件加载了缓存，%1 无法写入缓存。|  
|0xC0209314|-1071607020|DTS_E_CACHERELOADEDDIFFERENTFILES|由于已从文件“%3”加载了缓存，%1 无法从文件“%2”加载缓存。|  
|0xC0209316|-1071607018|DTS_E_OUTPUTNOTUSED|聚合组件的 ID 为 %1!d! 的输出没有被任何组件使用。 请删除它，或者将其与某个组件的输入相关联。|  
|0xC0209317|-1071607017|DTS_E_CACHEFILEWRITEFAILED|%1 无法将缓存写到文件“%2”。 hresult 为 0x%3!8.8X!。|  
|0xC0209318|-1071607016|DTS_E_XMLDATATYPECHANGED|元素“%2”的“%1”的 XML 架构数据类型信息已更改。  请重新初始化此组件的元数据，并检查列映射。|  
|0xC0209319|-1071607015|DTS_E_TXLOOKUP_UNUSEDINPUTCOLUMN|在联接或复制中没有使用 %1。 请从输入列列表中删除未使用的列。|  
|0xC020931A|-1071607014|DTS_E_SORTSTACKOVERFLOW|由于排序传入缓冲区时堆栈溢出，排序失败。  请减小该数据流任务的 DefaultBufferMaxRows 属性。|  
|0xC020F42A|-1071582166|DTS_E_OLEDB_OLDPROVIDER_ERROR|请考虑将连接字符串中的 PROVIDER 更改为 %1，或者访问 https://www.microsoft.com/downloads 以查找并安装 %2 的支持。|  
|||DTS_E_INITTASKOBJECTFAILED|由于错误 0x%3!8.8X!“%4!s!”，无法初始化类型为“%2!s!”的 XML 创建 任务对象。|  
|||DTS_E_GETCATMANAGERFAILED|由于错误 0x%1!8.8X!“%2!s!”，无法创建 COM 组件类别管理器 。|  
|||DTS_E_COMPONENTINITFAILED|由于错误 0x%2!8.8X!“%3!s!”，组件 %1!s! 无法初始化 “%3!s!”。|  
  
##  <a name="msgWarning"></a> 警告消息  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 警告消息的符号名称以 **DTS_W_** 开头。  
  
|十六进制代码|十进制代码|符号名称|描述|  
|----------------------|------------------|-------------------|-----------------|  
|0x80000036|-2147483594|DTS_W_COUNTDOWN|评估期还剩下 %1!lu! 天。 过期后，将无法执行包。|  
|0x80010015|-2147418091|DTS_W_GENERICWARNING|出现了警告。 在此说明警告细节的警告之前，应该还有更多特定警告。|  
|0x80012010|-2147409904|DTS_W_FAILEDXMLDOCCREATION|无法创建 XML 文档对象实例。 请确保已正确安装并注册了 MSXML。|  
|0x80012011|-2147409903|DTS_W_FAILEDCONFIGLOAD|无法加载 XML 配置文件。 XML 配置文件无效或者格式可能不正确。|  
|0x80012012|-2147409902|DTS_W_CONFIGFILENAMEINVALID|配置文件名“%1”无效。 请检查此配置文件名。|  
|0x80012013|-2147409901|DTS_W_CONFIGFILEINVALID|已加载配置文件，但它是无效的。 此文件的格式不正确，可能缺少元素，或者可能已损坏。|  
|0x80012014|-2147409900|DTS_W_CONFIGFILENOTFOUND|找不到配置文件“%1”。 请检查目录和文件名。|  
|0x80012015|-2147409899|DTS_W_CONFIGKEYNOTFOUND|找不到配置注册表项“%1”。 配置条目指定的注册表项不可用。 请检查注册表以确保它包含此项。|  
|0x80012016|-2147409898|DTS_W_CONFIGTYPEINVALID|其中一个配置条目中的配置类型无效。 有效的类型在 DTSConfigurationType 枚举中列出。|  
|0x80012017|-2147409897|DTS_W_CANNOTFINDOBJECT|包路径引用了找不到的对象:“%1”。 在尝试解析找不到的对象的包路径时，会出现此情况。|  
|0x80012018|-2147409896|DTS_W_CONFIGFORMATINVALID_PACKAGEDELIMITER|配置条目“%1”的格式不正确，没有以包分隔符开头。 请将“\package”置于包路径之前。|  
|0x80012019|-2147409895|DTS_W_CONFIGFORMATINVALID|配置条目“%1”的格式不正确， 可能是缺少分隔符或格式有误，如数组分隔符无效。|  
|0x8001201A|-2147409894|DTS_W_NOPARENTVARIABLES|由于没有父变量集合，父变量“%1”中的配置没有出现。|  
|0x8001201B|-2147409893|DTS_W_CONFIGFILEFAILEDIMPORT|导入配置文件失败:“%1”。|  
|0x8001201C|-2147409892|DTS_W_PARENTVARIABLENOTFOUND|由于没有父变量，父变量“%1”中的配置没有出现。 错误代码:0x%2!8.8X!。|  
|0x8001201D|-2147409891|DTS_W_CONFIGFILEEMPTY|配置文件为空，不包含配置条目。|  
|0x80012023|-2147409885|DTS_W_INVALIDCONFIGURATIONTYPE|配置“%1”的配置类型无效。 尝试将配置对象的类型属性设置为无效的配置类型时，可能会出现此情况。|  
|0x80012025|-2147409883|DTS_W_REGISTRYCONFIGURATIONTYPENOTFOUND|在注册表项“%1”中找不到注册表配置的配置类型。 请将名为 ConfigType 的值添加到此注册表项，并赋予它一个字符串值“Variable”、“Property”、“ConnectionManager”、“LoggingProvider”或“ForEachEnumerator”。|  
|0x80012026|-2147409882|DTS_W_REGISTRYCONFIGURATIONVALUENOTFOUND|在注册表项“%1”中找不到注册表配置的配置值。 请将名为 Value 的值添加到类型为 DWORD 或 String 的注册表项中。|  
|0x80012028|-2147409880|DTS_W_PROCESSCONFIGURATIONFAILEDSET|进程配置无法在包路径“%1”处设置目标。 当设置目标属性或变量的尝试失败时，会出现这种情况。 请检查目标属性或变量。|  
|0x80012032|-2147409870|DTS_W_CONFIGUREDVALUESECTIONEMPTY|无法从 .ini 文件中检索值。 ConfiguredValue 部分为空或不存在:“%1”。|  
|0x80012033|-2147409869|DTS_W_CONFIGUREDTYPESECTIONEMPTY|无法从 .ini 文件中检索值。 ConfiguredType 部分为空或不存在:“%1”。|  
|0x80012034|-2147409868|DTS_W_PACKAGEPATHSECTIONEMPTY|无法从 .ini 文件中检索值。 PackagePath 部分为空或不存在:“%1”。|  
|0x80012035|-2147409867|DTS_W_CONFIGUREDVALUETYPE|无法从 .ini 文件中检索值。 ConfiguredValueType 部分为空或不存在:“%1”。|  
|0x80012051|-2147409839|DTS_W_SQLSERVERFAILEDIMPORT|未能从 SQL Server 成功导入配置:“%1”。|  
|0x80012052|-2147409838|DTS_W_INICONFIGURATIONPROBLEM|由于某些字段为空或缺失，.ini 配置文件无效。|  
|0x80012054|-2147409836|DTS_W_NORECORDSFOUNDINTABLE|表“%1”中没有可供配置的任何记录。 当用于配置的 SQL Server 表中没有可供配置的记录时，会出现这种情况。|  
|0x80012055|-2147409835|DTS_W_DUPLICATECUSTOMEVENT|将相同的名称用于不同的自定义事件时出错。 此容器的其他子级已给自定义事件“%1”进行了不同的定义。 执行该事件处理程序时可能会发生错误。|  
|0x80012057|-2147409833|DTS_W_CONFIGREADONLYVARIABLE|该配置试图更改某个只读变量。 该变量位于包路径“%1”处。|  
|0x80012058|-2147409832|DTS_W_CONFIGPROCESSCONFIGURATIONFAILED|对包调用 ProcessConfiguration 失败。 该配置试图更改位于包路径“%1”处的属性。|  
|0x80012059|-2147409831|DTS_W_ONEORMORECONFIGLOADFAILED|包的至少一个配置条目无法加载。 请检查“%1”的配置条目和以前的警告，查看配置失败的有关说明。|  
|0x8001205A|-2147409830|DTS_W_CONFIGNODEINVALID|配置文件中的配置条目“%1”无效，或无法配置变量。  该名称指示失败的条目。 在某些情况下，该名称将不可用。|  
|0x80014058|-2147401640|DTS_W_FAILURENOTRESTARTABLE|此任务或容器已失败，但是由于 FailPackageOnFailure 属性为 FALSE，该包将继续执行。 如果包的 SaveCheckpoints 属性设置为 TRUE，则当任务或容器失败时，会发布此警告。|  
|0x80017101|-2147389183|DTS_W_EMPTYPATH|路径为空。|  
|0x80019002|-2147381246|DTS_W_MAXIMUMERRORCOUNTREACHED|SSIS 警告代码 DTS_W_MAXIMUMERRORCOUNTREACHED。  Execution 方法已成功，但引发的错误数(%1!d!)已达到允许的最大数目(%2!d!)；结果导致失败。 当错误数达到 MaximumErrorCount 中指定的数目时将发生这种情况。 请更改 MaximumErrorCount 或纠正这些错误。|  
|0x80019003|-2147381245|DTS_W_CONFIGENVVARNOTFOUND|找不到配置环境变量。  该环境变量为:“%1”。 当包为某个配置设置指定一个无法找到的环境变量时，会出现这种情况。 请检查包中的配置集合，确保指定的环境变量存在并且有效。|  
|0x80019316|-2147380458|DTS_W_CONNECTIONPROVIDERCHANGE|连接管理器“%1”的提供程序名称已从“%2”更改为“%3”。|  
|0x80019317|-2147380457|DTS_W_READEXTMAPFAILED|读取升级映射文件时出现异常。 异常为“%1”。|  
|0x80019318|-2147380456|DTS_W_DUPLICATEMAPPINGKEY|文件“%1”中存在重复的映射。 标记为“%2”，键为“%3”。|  
|0x80019319|-2147380455|DTS_W_IMPLICITUPGRADEMAPPING|扩展插件“%1”已隐式升级到“%2”。 请将此扩展插件的映射添加到 UpgradeMappings 目录。|  
|0x8001931A|-2147380454|DTS_W_INVALIDEXTENSIONMAPPING|文件“%1”中的映射无效。 值不能为 Null 或者为空。 标记为“%2”，键为“%3”，值为“%4”。|  
|0x8001931C|-2147380452|DTS_W_ADOCONNECTIONDATATYPECOMPATCHANGE|为了向后兼容，ADO 类型连接管理器“%1”的 DataTypeCompatibility 属性设置为 80。|  
|0x8001C004|-2147368956|DTS_W_FILEENUMEMPTY|For Each 文件枚举器为空。 For Each 文件枚举器找不到与文件模式匹配的文件，或者指定的目录为空。|  
|0x8001F02F|-2147356625|DTS_W_COULDNOTRESOLVEPACKAGEPATH|无法解析包“%1”中某个对象的包路径。 请确保该包路径有效。|  
|0x8001F203|-2147356157|DTS_W_ITERATIONEXPRESSIONISNOTASSIGNMENT|迭代表达式不是赋值表达式:“%1”。 当 For 循环的赋值表达式中的表达式不是赋值表达式时，通常会出现此错误。|  
|0x8001F204|-2147356156|DTS_W_INITIALIZATIONEXPRESSIONISNOTASSIGNMENT|初始化表达式不是赋值表达式:“%1”。 当 For 循环的迭代表达式中的表达式不是赋值表达式时，通常会出现此错误。|  
|0x8001F205|-2147356155|DTS_W_LOGPROVIDERNOTDEFINED|已成功粘贴可执行文件“%1”。 但是，在集合“LogProviders”中找不到与该可执行文件关联的日志提供程序。  所以，仅粘贴了可执行文件，没有粘贴日志提供程序信息。|  
|0x8001F300|-2147355904|DTS_W_PACKAGEUPGRADED|升级包成功。|  
|0x8001F42B|-2147355605|DTS_W_LEGACYPROGID|不推荐使用“%1”ProgID。 应使用此组件的新 ProgID“%2”。|  
|0x80020918|-2147350248|DTS_W_FTPTASK_OPERATIONFAILURE|操作“%1”失败。|  
|0x800283A5|-2147318875|DTS_W_MSMQTASK_USE_WEAK_ENCRYPTION|加密算法“%1”使用弱加密。|  
|0x80029164|-2147315356|DTS_W_FSTASK_OPERATIONFAILURE|任务无法执行操作“%1”。|  
|0x80029185|-2147315323|DTS_W_EXECPROCTASK_FILENOTINPATH|文件/进程“%1”不在路径中。|  
|0x800291C6|-2147315258|DTS_W_SENDMAILTASK_SUBJECT_MISSING|主题为空。|  
|0x800291C7|-2147315257|DTS_W_SENDMAILTASK_ERROR_IN_TO_LINE|“收件人”行中的地址格式不正确。 地址中缺少“\@”符号或地址无效。|  
|0x800291C8|-2147315256|DTS_W_SENDMAILTASK_AT_MISSING_IN_FROM|“发件人”行中的地址格式不正确。 地址中缺少“\@”符号或地址无效。|  
|0x8002927A|-2147315078|DTS_W_XMLTASK_DIFFFAILURE|这两个 XML 文档不相同。|  
|0x8002928C|-2147315060|DTS_W_XMLTASK_DTDVALIDATIONWARNING|DTD 验证将使用 XML 文档中 DOCTYPE 行定义的 DTD 文件。 它将不使用赋予属性“%1”的值。|  
|0x8002928D|-2147315059|DTS_W_XMLTASK_VALIDATIONFAILURE|任务无法验证“%1”。|  
|0x80029291|-2147315055|DTS_W_TRANSFERDBTASK_ACTIONSETTOCOPY|传输操作值无效。  正将该值设置为复制。|  
|0x80029292|-2147315054|DTS_W_TRANSFERDBTASK_METHODSETTOONLINE|传输方法值无效。  正将该值设置为在线传输。|  
|0x8002F304|-2147290364|DTS_W_PROBLEMOCCURREDWITHFOLLOWINGMESSAGE|出现问题，错误消息如下:“%1”。|  
|0x8002F322|-2147290334|DTS_W_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|目标服务器上已存在错误消息“%1”。|  
|0x8002F331|-2147290319|DTS_W_JOBSTASK_JOBEXISTSATDEST|目标服务器上已存在作业“%1”。|  
|0x8002F332|-2147290318|DTS_W_JOBSTASK_SKIPPINGJOBEXISTSATDEST|由于目标中已存在作业“%1”，所以跳过对它的传输。|  
|0x8002F333|-2147290317|DTS_W_JOBSTASK_OVERWRITINGJOB|正在覆盖目标服务器上的作业“%1”。|  
|0x8002F339|-2147290311|DTS_W_LOGINSTASK_ENUMVALUEINCORRECT|属性“FailIfExists”的持久化枚举值已更改，呈现为无效。 正在重置为默认值。|  
|0x8002F343|-2147290301|DTS_W_LOGINSTASK_OVERWRITINGLOGINATDEST|正在覆盖目标中的登录名“%1”。|  
|0x8002F356|-2147290282|DTS_W_TRANSOBJECTSTASK_SPALREADYATDEST|目标中已存在存储过程“%1”。|  
|0x8002F360|-2147290272|DTS_W_TRANSOBJECTSTASK_RULEALREADYATDEST|目标中已存在规则“%1”。|  
|0x8002F364|-2147290268|DTS_W_TRANSOBJECTSTASK_TABLEALREADYATDEST|目标中已存在表“%1”。|  
|0x8002F368|-2147290264|DTS_W_TRANSOBJECTSTASK_VIEWALREADYATDEST|目标中已存在视图“%1”。|  
|0x8002F372|-2147290254|DTS_W_TRANSOBJECTSTASK_UDFALREADYATDEST|目标中已存在用户定义函数“%1”。|  
|0x8002F376|-2147290250|DTS_W_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|目标中已存在默认值“%1”。|  
|0x8002F380|-2147290240|DTS_W_TRANSOBJECTSTASK_UDDTALREADYATDEST|目标中已存在用户定义数据类型“%1”。|  
|0x8002F384|-2147290236|DTS_W_TRANSOBJECTSTASK_PFALREADYATDEST|目标中已存在分区函数“%1”。|  
|0x8002F388|-2147290232|DTS_W_TRANSOBJECTSTASK_PSALREADYATDEST|目标中已存在分区方案“%1”。|  
|0x8002F391|-2147290223|DTS_W_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|目标中已存在架构“%1”。|  
|0x8002F396|-2147290218|DTS_W_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|目标中已存在 SqlAssembly“%1”。|  
|0x8002F400|-2147290112|DTS_W_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|目标中已存在用户定义聚合“%1”。|  
|0x8002F404|-2147290108|DTS_W_TRANSOBJECTSTASK_TYPEALREADYATDEST|目标中已存在用户定义类型“%1”。|  
|0x8002F408|-2147290104|DTS_W_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|目标中已存在 XmlSchemaCollection“%1”。|  
|0x8002F412|-2147290094|DTS_W_TRANSOBJECTSTASK_NOELEMENTSPECIFIEDTOTRANSFER|没有指定要传输的元素。|  
|0x8002F415|-2147290091|DTS_W_TRANSOBJECTSTASK_LOGINALREADYATDEST|目标中已存在登录名“%1”。|  
|0x8002F41A|-2147290086|DTS_W_TRANSOBJECTSTASK_USERALREADYATDEST|目标中已存在用户“%1”。|  
|0x80047007|-2147192825|DTS_W_NOLINEAGEVALIDATION|由于执行树包含循环，无法验证输入列的沿袭 ID。|  
|0x80047034|-2147192780|DTS_W_EMPTYDATAFLOW|DataFlow 任务中没有组件。 请向任务添加组件，或者删除任务。|  
|0x80047069|-2147192727|DTS_W_SORTEDOUTPUTHASNOSORTKEYPOSITIONS|%1 的 IsSorted 属性设置为 TRUE，但其所有输出列的 SortKeyPositions 都被设置为零。|  
|0x8004706F|-2147192721|DTS_W_SOURCEREMOVED|将不读取源“%1”(%2!d!)，因为它的所有数据在数据流任务外均不可见。|  
|0x80047076|-2147192714|DTS_W_UNUSEDOUTPUTDATA|输出“%3”(%4!d!)和组件“%5”(%6!d!)的输出列“%1”(%2!d!)以后不在数据流任务中使用。 删除此不用的输出列可以提高数据流任务的性能。|  
|0x800470AE|-2147192658|DTS_W_COMPONENTREMOVED|组件的“%1”(%2!d!)输出未使用，且其输入无其他作用，或者其未连接到其他组件的输出，因此已将其从数据流任务中删除。 如果需要该组件，应至少将它的一个输入的 HasSideEffects 属性设置为 True，或者将它的输出连接到某个对象。|  
|0x800470B0|-2147192656|DTS_W_NOWORKTODO|为某个线程指定了行，但该线程没有要完成的工作。 布局有连接已断开的输出。 将 RunInOptimizedMode 属性设置为 TRUE，管道将运行得更快，并可避免出现此警告。|  
|0x800470C8|-2147192632|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|%1 的外部列与数据源列不同步。 %2|  
|0x800470C9|-2147192631|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSADDITION|需要将列“%1”添加到外部列中。|  
|0x800470CA|-2147192630|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSUPDATE|需要更新外部列“%1”。|  
|0x800470CB|-2147192629|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSREMOVAL|需要从外部列中删除 %1。|  
|0x800470D8|-2147192616|DTS_W_EXPREVALPOTENTIALSTRINGTRUNCATION|如果表达式“%1”的结果字符串超过 %2!d! 个字符）。 该表达式的结果值可能超过 DT_WSTR 的最大大小。|  
|0x800470E9|-2147192599|DTS_W_COMPONENTLEAKPROCESSINPUT|对 %2 的输入 %1!d! 调用 ProcessInput 方法时，意外地保留了对传递给该方法的缓冲区的引用。 该缓冲区的引用计数在调用前为 %3!d!， 调用返回后为 %4!d! 。|  
|0x800470EB|-2147192597|DTS_W_EXPREVALUNREFERENCEDINPUTCOLUMN|“%2”上的“%1”有 READONLY 使用类型，但是它未被表达式引用。 请从可用输入列列表中删除该列，或在某个表达式中引用该列。|  
|0x8004801E|-2147188706|DTS_W_COULDNOTFINDCURRENTVERSION|找不到组件 %2 的“%1”值。 找不到该组件的 CurrentVersion 值。 如果该组件没有设置其注册表信息，以在 DTSInfo 部分中包含 CurrentVersion 值，将出现此错误。 组件开发期间会出现此消息；或者，如果组件未正确注册，则在包中使用它时也会出现此消息。|  
|0x80049300|-2147183872|DTS_W_BUFFERGETTEMPFILENAME|缓冲区管理器无法获取临时文件名。|  
|0x80049301|-2147183871|DTS_W_UNUSABLETEMPORARYPATH|缓冲区管理器无法在路径“%1”下创建临时文件。 临时存储区将不再考虑使用该路径。|  
|0x80049304|-2147183868|DTS_W_DF_PERFCOUNTERS_DISABLED|警告：无法打开全局共享内存以与性能 DLL 通信；数据流性能计数器不可用。  若要解决此问题，请以管理员的身份或在系统控制台上运行此包。|  
|0x8020200F|-2145378289|DTS_W_PARTIALROWFOUNDATENDOFFILE|文件结尾存在不完整的行。|  
|0x8020202B|-2145378261|DTS_W_ENDOFFILEREACHWHILEREADINGHEADERROWS|在读取标题行时到达了数据文件的结尾。 请确保标题行分隔符和要跳过的标题行数是正确的。|  
|0x80202066|-2145378202|DTS_W_CANTRETRIEVECODEPAGEFROMOLEDBPROVIDER|无法从 OLE DB 访问接口检索列代码页信息。  如果该组件支持“%1”属性，将使用来自该属性的代码页。  如果当前的字符串代码页值不正确，请更改该属性的值。  如果该组件不支持该属性，将使用来自该组件的区域设置 ID 的代码页。|  
|0x802020F7|-2145378057|DTS_W_TXSORTSORTISTHESAME|数据已根据指示排序，因此转换可能被删除。|  
|0x8020400D|-2145370099|DTS_W_NOPIPELINEDATATYPEMAPPINGAVAILABLE|%1 引用了无法映射到数据流任务数据类型的外部数据类型。 将改用数据流任务数据类型 DT_WSTR。|  
|0x802070CC|-2145357620|DTS_W_STATICTRUNCATIONINEXPRESSION|表达式“%1”总是导致数据被截断。 该表达式包含一个静态截断(对固定值的截断)。|  
|0x8020820C|-2145353204|DTS_W_UNMAPPEDINPUTCOLUMN|位于索引 %3!d! 处 ID 为 %2!d! 的输入列“%1” 已被取消映射。 该列的沿袭 ID 为零。|  
|0x80208305|-2145352955|DTS_W_TXFUZZYLOOKUP_DELIMITERS_DONT_MATCH|指定的分隔符与用于生成预先存在的匹配索引“%1”的分隔符不匹配。 当用于标记字段的分隔符相互不匹配时，就会出现此错误。 这将对匹配行为或结果产生未知的影响。|  
|0x80208308|-2145352952|DTS_W_TXFUZZYLOOKUP_MAXRESULTS_IS_ZERO|模糊查找转换的 MaxOutputMatchesPerInput 属性为零。 将不生成任何结果。|  
|0x80208310|-2145352944|DTS_W_TXFUZZYLOOKUP_NO_FUZZY_JOIN_COLUMNS|没有 JoinType 列属性设置为 Fuzzy 的有效输入列。  使用查找转换而不是模糊查找可以改进完全联接的性能。|  
|0x8020831C|-2145352932|DTS_W_TXFUZZYLOOKUP_TIMESTAMPCAVEAT|引用列“%1”可以是 SQL 时间戳列。 如果生成模糊匹配索引，并且生成引用表的副本，则所有引用表时间戳都将反映生成副本时该表的当前状态。 如果 CopyReferenceTable 设置为 False，则可能发生意外行为。|  
|0x80208321|-2145352927|DTS_W_MATCHINDEXALREADYEXISTS|为 MatchIndexName 提供的名为“%1”的表已经存在，并且 DropExistingMatchIndex 设置为 FALSE。  除非删除此表，或指定其他名称，或将 DropExisitingMatchIndex 设置为 TRUE，否则转换将失败。|  
|0x8020832B|-2145352917|DTS_W_TXFUZZYLOOKUP_JOINLENGTHMISMATCH|输入列“%1”的长度与它要匹配的引用列“%2”的长度不相等。|  
|0x8020832D|-2145352915|DTS_W_TXFUZZYLOOKUP_CODEPAGE_MISMATCH|DT_STR 源列“%1”的代码页和 DT_STR 目标列“%2”的代码页不匹配。  这可能导致意外结果。|  
|0x8020832E|-2145352914|DTS_W_FUZZYLOOKUP_TOOMANYEXACTMATCHCOLUMNS|完全匹配联接多于 16 个，因此性能可能并非最佳。 请减少完全匹配联接的数目以改进性能。 SQL Server 将每个索引的列数限制为 16 个，倒排索引将用于全部查找。|  
|0x80208350|-2145352880|DTS_W_FUZZYLOOKUP_MEMLIMITANDEXHAUSTIVESPECIFIED|Exhaustive 选项要求将整个引用表加载到主内存中。  但是，由于已为 MaxMemoryUsage 属性指定了内存上限值，所以可能无法加载整个引用表，从而导致匹配操作在运行时失败。|  
|0x80208351|-2145352879|DTS_W_FUZZYLOOKUP_EXACTMATCHCOLUMNSEXCEEDBYTELIMIT|完全匹配联接中指定的列的累计长度超过了索引键 900 个字节的长度限制。  模糊查找为完全匹配列创建索引以提高查找性能，但此索引有可能无法创建，此时查找仍将使用可能速度较慢的替代方法查找匹配项。 如果性能有问题，请尝试删除一些完全匹配联接列，或减小可变长度完全匹配列的最大长度。|  
|0x80208352|-2145352878|DTS_W_FUZZYLOOKUP_EXACTMATCHINDEXCREATIONFAILED|无法为完全匹配列创建索引。 仍然使用替代的模糊查找方法。|  
|0x80208353|-2145352877|DTS_W_FUZZYGROUPINGINTERNALPIPELINEWARNING|出现警告代码为 0x%1!8.8X! 的以下模糊分组内部管道警告:“%2”。|  
|0x80208375|-2145352843|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTODEFAULT|没有为外部数据类型为 %2 的 %1 指定最大长度。 将使用长度为 %4!d! 的 SSIS 数据流任务数据类型“%3” 。|  
|0x80208376|-2145352842|DTS_W_XMLSRCOUTPUTCOLUMNDATATYPEMAPPEDTOSTRING|%1 引用了无法映射为 SSIS 数据流任务数据类型的外部数据类型 %2。  将改用长度为 %3!d! 的 SSIS 数据流任务数据类型 DT_WSTR 。|  
|0x80208385|-2145352827|DTS_W_NOREDIRECTWITHATTACHEDERROROUTPUTS|将不会向错误输出发送任何行。 请对错误处理或截断处理进行配置，使行重定向到错误输出，或删除附加到错误输出后的数据流转换或数据流目标。|  
|0x80208386|-2145352826|DTS_W_REDIRECTWITHNOATTACHEDERROROUTPUTS|发送到错误输出的行将丢失。 请添加新的数据流转换或数据流目标来接收错误输出，或对组件进行重新配置，停止将行重定向到错误输出。|  
|0x80208391|-2145352815|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTOMAXIMUM|对于外部数据类型为 %2 的 %1，XML 架构指定了值为 %3!d! 的 maxLength 约束，这超过了允许的最大列长度 %4!d!。 将使用长度为 %6!d! 的 SSIS 数据流任务数据类型“%5” 。|  
|0x802090E4|-2145349404|DTS_W_TXLOOKUP_DUPLICATE_KEYS|%1 在缓存引用数据时遇到了重复的引用键值。 此错误仅出现在 Full Cache 模式下。 请删除重复的键值，或将缓存模式更改为 PARTIAL 或 NO_CACHE。|  
|0x802092A7|-2145348953|DTS_W_POTENTIALTRUNCATIONFROMDATAINSERTION|由于将数据流中长度为 %2!d! 的列“%1”中的数据插入数据库中长度为 %4!d! 的列“%3”， 可能导致截断。|  
|0x802092A8|-2145348952|DTS_W_POTENTIALTRUNCATIONFROMDATARETRIEVAL|由于将数据库中长度为 %2!d! 的列“%1”中的数据检索到数据流中长度为 %4!d! 的列“%3”， 可能导致截断。|  
|0x802092AA|-2145348950|DTS_W_ADODESTBATCHNOTSUPPORTEDFORERRORDISPOSITION|使用错误行处理时，当前不支持批处理模式。 BatchSize 属性将设置为 1。|  
|0x802092AB|-2145348949|DTS_W_ADODESTNOROWSINSERTED|未将任何行成功地插入此目标。 这可能是因为列之间的数据类型不匹配，或者使用了您的 ADO.NET 提供程序不支持的数据类型。 由于该组件的错误处理不是“组件失败”，因此此处不会显示错误消息；将错误处理设置为“组件失败”可以在此处看到错误消息。|  
|0x802092AC|-2145348948|DTS_W_ADODESTPOTENTIALDATALOSS|如果将数据类型为“%2”的输入列“%1”中的数据插入数据类型为“%4”的外部列“%3”中，则可能会发生丢失数据的情况。 如果想要进行该插入操作，一种执行转换的替代方法是在 ADO NET 目标组件之前使用一个数据转换组件。|  
|0x802092AD|-2145348947|DTS_W_ADODESTEXTERNALCOLNOTMATCHSCHEMACOL|%1 与数据库列不同步。  最新的列具有 %2。 如果需要，请使用高级编辑器刷新可用目标列。|  
|0x802092AE|-2145348946|DTS_W_ADODESTEXTERNALCOLNOTEXIST|数据库中不存在 %1。 它可能已被删除或重命名。 如果需要，请使用高级编辑器刷新可用目标列。|  
|0x802092AF|-2145348945|DTS_W_ADODESTNEWEXTCOL|已向外部数据库表添加了一个名为 %1 的新列。 如果需要，请使用高级编辑器刷新可用目标列。|  
|0x8020930C|-2145348852|DTS_W_NOMATCHOUTPUTGETSNOROWS|将不会向无匹配输出发送任何行。 请配置转换以将没有匹配项的行重新定向至无匹配输出，或删除附加到无匹配输出的数据流转换或目标。|  
|0x8020931B|-2145348837|DTS_W_ADODESTINVARIANTEXCEPTION|枚举 ADO.Net 提供程序时收到异常。 “%1”是固定的。 异常消息为:“%2”。|  
|0xC020822C|-1071611348|DTS_W_UNMAPPEDOUTPUTCOLUMN|没有输入列映射到 %1。|  
|0x930D|37645|DTS_W_EXTERNALTABLECOLSOUTOFSYNC|表“%1”已更改。 新列可能已添加到该表。|  
  
##  <a name="msgInfo"></a> 信息性消息  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 信息性消息的符号名称以 **DTS_I_** 开头。  
  
|十六进制代码|十进制代码|符号名称|描述|  
|----------------------|------------------|-------------------|-----------------|  
|0x4001100A|1073811466|DTS_I_STARTINGTRANSACTION|正在启动此容器的分布式事务处理。|  
|0x4001100B|1073811467|DTS_I_COMMITTINGTRANSACTION|正在提交此容器启动的分布式事务处理。|  
|0x4001100C|1073811468|DTS_I_ABORTINGTRANSACTION|正在中止当前的分布式事务。|  
|0x40013501|1073820929|DTS_I_GOTMUTEXFROMWAIT|已成功获取互斥体“%1”。|  
|0x40013502|1073820930|DTS_I_RELEASEACQUIREDMUTEX|已成功释放互斥体“%1”。|  
|0x40013503|1073820931|DTS_I_NEWMUTEXCREATED|已成功创建互斥体“%1”。|  
|0x40015101|1073828097|DTS_I_DUMP_ON_ANY_ERR|将为任何错误事件生成调试转储文件。|  
|0x40015102|1073828098|DTS_I_DUMP_ON_CODES|将为以下事件代码生成调试转储文件:“%1”|  
|0x40015103|1073828099|DTS_I_START_DUMP|事件代码 0x%1!8.8X! 触发了在文件夹“%2”中生成调试转储文件。|  
|0x40015104|1073828100|DTS_I_SSIS_INFO_DUMP|正在创建 SSIS 信息转储文件“%1”。|  
|0x40015106|1073828102|DTS_I_FINISH_DUMP|已成功创建调试转储文件。|  
|0x40016019|1073831961|DTS_I_PACKAGEMIGRATED|包格式已从版本 %1!d! 迁移到版本 %2!d!。 必须保存它以保留迁移更改。|  
|0x4001601A|1073831962|DTS_I_SCRIPTSMIGRATED|已迁移包中的脚本。 必须保存包以保留迁移更改。|  
|0x40016025|1073831973|DTS_I_FTPRECEIVEFILE|正在接收文件“%1”。|  
|0x40016026|1073831974|DTS_I_FTPSENDFILE|正在发送文件“%1”。|  
|0x40016027|1073831975|DTS_I_FTPFILEEXISTS|文件“%1”已存在。|  
|0x40016028|1073831976|DTS_I_FTPERRORLOADINGMSG|由于内部错误，无法获取额外的错误信息。|  
|0x40016036|1073831990|DTS_I_FTPDELETEFILE|未能删除文件“%1”。 当文件不存在、文件名存在拼写错误或者您无权删除该文件时，都会出现这种情况。|  
|0x40016037|1073831991|DTS_I_CONFIGFROMREG|该包正尝试使用注册表项“%1”根据注册表项进行配置。|  
|0x40016038|1073831992|DTS_I_CONFIGFROMENVVAR|该包正尝试根据环境变量“%1”进行配置。|  
|0x40016039|1073831993|DTS_I_CONFIGFROMINIFILE|该包正尝试根据 .ini 文件“%1”进行配置。|  
|0x40016040|1073832000|DTS_I_CONFIGFROMSQLSERVER|该包正尝试使用配置字符串“%1”从 SQL Server 进行配置。|  
|0x40016041|1073832001|DTS_I_CONFIGFROMFILE|该包正尝试根据 XML 文件“%1”进行配置。|  
|0x40016042|1073832002|DTS_I_CONFIGFROMPARENTVARIABLE|该包正尝试根据父变量“%1”进行配置。|  
|0x40016043|1073832003|DTS_I_ATTEMPTINGUPGRADEOFDTS|正尝试将 SSIS 从版本“%1”升级到版本“%2”。 该包正尝试升级运行库。|  
|0x40016044|1073832004|DTS_I_ATTEMPTINGUPGRADEOFANEXTOBJ|正尝试升级“%1”。 该包正尝试升级可扩展对象。|  
|0x40016045|1073832005|DTS_I_SAVECHECKPOINTSTOFILE|该包将在执行期间把检查点保存到文件“%1”。 将对该包进行配置以保存检查点。|  
|0x40016046|1073832006|DTS_I_RESTARTFROMCHECKPOINTFILE|该包从检查点文件“%1”重新启动。 该包已被配置为从检查点重新启动。|  
|0x40016047|1073832007|DTS_I_CHECKPOINTSAVEDTOFILE|检查点文件“%1”已更新，以记录此容器的完成。|  
|0x40016048|1073832008|DTS_I_CHECKPOINTFILEDELETED|检查点文件“%1”已在成功完成该包后删除。|  
|0x40016049|1073832009|DTS_I_CHECKPOINTSAVINGTOFILE|正在启动检查点文件“%1”的更新。|  
|0x40016051|1073832017|DTS_I_CHOSENMAXEXECUTABLES|基于系统配置，最大并发可执行文件数目被设置为 %1!d!。|  
|0x40016052|1073832018|DTS_I_MAXEXECUTABLES|最大并发可执行文件数目被设置为 %1!d!。|  
|0x40016053|1073832019|DTS_I_PACKAGESTART|包执行开始。|  
|0x40016054|1073832020|DTS_I_PACKAGEEND|包执行结束。|  
|0x40029161|1073910113|DTS_I_FSTASK_DIRECTORYDELETED|目录“%1”已删除。|  
|0x40029162|1073910114|DTS_I_FSTASK_FILEDELETED|文件或目录“%1”已删除。|  
|0x400292A8|1073910440|DTS_I_TRANSFERDBTASK_OVERWRITEDB|正在覆盖目标服务器“%2”上的数据库“%1”。|  
|0x4002F304|1073935108|DTS_I_SOMETHINGHAPPENED|"%1".|  
|0x4002F323|1073935139|DTS_I_ERRMSGTASK_SKIPPINGERRORMESSAGEALREADYEXISTS|由于目标服务器上已存在错误消息“%1”，所以跳过它。|  
|0x4002F326|1073935142|DTS_I_ERRMSGTASK_TRANSFEREDNERRORMESSAGES|已传输“%1”条错误消息。|  
|0x4002F351|1073935185|DTS_I_STOREDPROCSTASKS_TRANSFEREDNSPS|此任务传输了“%1”个存储过程。|  
|0x4002F352|1073935186|DTS_I_TRANSOBJECTSTASK_TRANSFEREDNOBJECTS|已传输“%1”个对象。|  
|0x4002F358|1073935192|DTS_I_TRANSOBJECTSTASK_NOSPSTOTRANSFER|没有要传输的存储过程。|  
|0x4002F362|1073935202|DTS_I_TRANSOBJECTSTASK_NORULESTOTRANSFER|没有要传输的规则。|  
|0x4002F366|1073935206|DTS_I_TRANSOBJECTSTASK_NOTABLESTOTRANSFER|没有要传输的表。|  
|0x4002F370|1073935216|DTS_I_TRANSOBJECTSTASK_NOVIEWSTOTRANSFER|没有要传输的视图。|  
|0x4002F374|1073935220|DTS_I_TRANSOBJECTSTASK_NOUDFSTOTRANSFER|没有要传输的用户定义函数。|  
|0x4002F378|1073935224|DTS_I_TRANSOBJECTSTASK_NODEFAULTSTOTRANSFER|没有要传输的默认值。|  
|0x4002F382|1073935234|DTS_I_TRANSOBJECTSTASK_NOUDDTSTOTRANSFER|没有要传输的用户定义数据类型。|  
|0x4002F386|1073935238|DTS_I_TRANSOBJECTSTASK_NOPFSTOTRANSFER|没有要传输的分区函数。|  
|0x4002F390|1073935248|DTS_I_TRANSOBJECTSTASK_NOPSSTOTRANSFER|没有要传输的分区方案。|  
|0x4002F394|1073935252|DTS_I_TRANSOBJECTSTASK_NOSCHEMASTOTRANSFER|没有要传输的架构。|  
|0x4002F398|1073935256|DTS_I_TRANSOBJECTSTASK_NOSQLASSEMBLIESTOTRANSFER|没有要传输的 SqlAssemblies。|  
|0x4002F402|1073935362|DTS_I_TRANSOBJECTSTASK_NOAGGREGATESTOTRANSFER|没有要传输的用户定义聚合。|  
|0x4002F406|1073935366|DTS_I_TRANSOBJECTSTASK_NOTYPESTOTRANSFER|没有要传输的用户定义类型。|  
|0x4002F410|1073935376|DTS_I_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONSTOTRANSFER|没有要传输的 XmlSchemaCollections。|  
|0x4002F418|1073935384|DTS_I_TRANSOBJECTSTASK_NOLOGINSTOTRANSFER|没有要传输的登录名。|  
|0x4002F41D|1073935389|DTS_I_TRANSOBJECTSTASK_NOUSERSTOTRANSFER|没有要传输的用户。|  
|0x4002F41E|1073935390|DTS_I_TRANSOBJECTSTASK_TRUNCATINGTABLE|正在截断表“%1”|  
|0x40043006|1074016262|DTS_I_EXECUTIONPHASE_PREPAREFOREXECUTE|正开始执行阶段的准备工作。|  
|0x40043007|1074016263|DTS_I_EXECUTIONPHASE_PREEXECUTE|正开始执行之前阶段。|  
|0x40043008|1074016264|DTS_I_EXECUTIONPHASE_POSTEXECUTE|正开始执行之后阶段。|  
|0x40043009|1074016265|DTS_I_EXECUTIONPHASE_CLEANUP|正开始清除阶段。|  
|0x4004300A|1074016266|DTS_I_EXECUTIONPHASE_VALIDATE|正开始验证阶段。|  
|0x4004300B|1074016267|DTS_I_ROWS_WRITTEN|“%1”已写入 %2!ld! 行。|  
|0x4004300C|1074016268|DTS_I_EXECUTIONPHASE_EXECUTE|正开始执行阶段。|  
|0x4004800C|1074036748|DTS_I_CANTRELIEVEPRESSURE|缓冲区管理器检测到系统的虚拟内存不足，但无法换出任何缓冲区。 考虑了 %1!d! 个缓冲区，但锁定了 %2!d! 个缓冲区。 或者是因未安装足够的内存或其他进程正在使用内存，以致于没有足够的内存可供该管道使用；或者锁定了过多的缓冲区。|  
|0x4004800D|1074036749|DTS_I_CANTALLOCATEMEMORYPRESSURE|缓冲区管理器调用 %3!d! 个字节的内存分配量失败，但无法换出任何缓冲区来缓解内存不足的压力。 考虑了 %1!d! 个缓冲区，但锁定了 %2!d! 个缓冲区。 或者是因未安装足够的内存或其他进程正在使用内存，以致于没有足够的内存可供该管道使用；或者锁定了过多的缓冲区。|  
|0x4004800E|1074036750|DTS_I_ALLOCATEDDURINGMEMORYPRESSURE|即使已检测到内存不足并且多次尝试交换缓冲区已失败，缓冲区管理器仍分配了 %1!d! 个字节。|  
|0x400490F4|1074041076|DTS_I_TXLOOKUP_CACHE_PROGRESS|%1 已缓存了 %2!d! 行。|  
|0x400490F5|1074041077|DTS_I_TXLOOKUP_CACHE_FINAL|%1 共缓存了 %2!d! 行。|  
|0x4020206D|1075847277|DTS_I_RAWSOURCENOCOLUMNS|原始源适配器打开了一个文件，但该文件不包含任何列。 该适配器将不会生成数据。 这可能说明文件损坏，或者有许多零列，因此没有任何数据。|  
|0x402020DA|1075847386|DTS_I_OLEDBINFORMATIONALMESSAGE|存在 OLE DB 信息性消息。|  
|0x40208327|1075872551|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_COLLATIONS_DONT_MATCH|如果将输入列“%1”的完全联接 FuzzyComparisonFlags 设置为与引用表列“%2”的默认 SQL 排序规则相匹配，将改进模糊匹配的性能。  另外，FuzzyComparisonFlagsEx 中也不能设置折叠标志。|  
|0x40208328|1075872552|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_INDEX_MISSING|如果对引用表中所有指定的完全匹配列创建一个索引，将改进模糊匹配的性能。|  
|0x40208387|1075872647|DTS_I_DISPSNOTREVIEWED|未检查错误处理和截断处理。 如果您希望继续转换这些行，请确保已对该组件进行配置，将行重定向到错误输出。|  
|0x402090DA|1075876058|DTS_I_TXAGG_WORKSPACE_REHASH|聚合转换遇到了 %1!d! 个键组合。 由于键组合数目超过了预期数目，因此该转换必须重新对数据进行哈希操作。 通过调整 Keys、KeyScale 和 AutoExtendFactor 属性来配置该组件，可避免对数据重新执行哈希操作。|  
|0x402090DB|1075876059|DTS_I_TXAGG_COUNTDISTINCT_REHASH|聚合转换遇到了 %1!d! 个非重复值。 由于非重复值数目超过了预期数目，该转换将重新对数据进行哈希操作。 通过调整 CountDistinctKeys、CountDistinctKeyScale 和 AutoExtendFactor 属性来配置该组件，可避免对数据重新执行哈希操作。|  
|0x402090DC|1075876060|DTS_I_STARTPROCESSINGFILE|已开始处理文件“%1”。|  
|0x402090DD|1075876061|DTS_I_FINISHPROCESSINGFILE|文件“%1”已处理完毕。|  
|0x402090DE|1075876062|DTS_I_TOTALDATAROWSPROCESSEDFORFILE|为文件“%1”处理的数据行总数为 %2!I64d!。|  
|0x402090DF|1075876063|DTS_I_FINALCOMMITSTARTED|“%1”中的数据插入操作的最终提交已开始。|  
|0x402090E0|1075876064|DTS_I_FINALCOMMITENDED|“%1”中的数据插入操作的最终提交已结束。|  
|0x402090E1|1075876065|DTS_I_BEGINHASHINGCACHE|%1!u! 行已添加至缓存。 系统正在处理这些行。|  
|0x402090E2|1075876066|DTS_I_SUCCEEDEDHASHINGCACHE|%1 已处理缓存中的 %2!u! 行。 处理时间为 %3 秒。 缓存使用了 %4!I64u! 字节的内存。|  
|0x402090E3|1075876067|DTS_I_FAILEDHASHINGCACHE|%1 无法处理缓存中的行。  处理时间为 %2 秒。|  
|0x402090E4|1075876068|DTS_I_SUCCEEDEDPREPARINGCACHE|%1 已成功准备缓存。 准备时间为 %2 秒。|  
|0x40209314|1075876628|DTS_I_TXLOOKUP_PARTIALPERF|%1 已经执行了以下操作: 已处理 %2!I64u! 行，已对引用数据库发出 %3!I64u! 条数据库命令，并已使用部分缓存执行了 %4!I64u! 次查找。|  
|0x40209315|1075876629|DTS_I_TXLOOKUP_PARTIALPERF2|%1 已经执行了以下操作: 已处理 %2!I64u! 行，已对引用数据库发出 %3!I64u! 条数据库命令，已使用局部缓存执行了 %4!I64u! 次查找，并且使用在初次查找中无匹配项的行的缓存执行了 %5!I64u! 次查找。|  
|0x40209316|1075876630|DTS_I_CACHEFILEWRITESTARTED|%1 正在将缓存写到文件“%2”。|  
|0x40209317|1075876631|DTS_I_CACHEFILEWRITESUCCEEDED|%1 已将缓存写到文件“%2”。|  
|0x4020F42C|1075901484|DTS_I_OLEDBDESTZEROMAXCOMMITSIZE|OLE DB 目标“%1”的“最大插入提交大小”属性设置为 0。 此属性设置会导致正在运行的包停止响应。 有关详细信息，请参阅 OLE DB 目标编辑器(“连接管理器”页)的 F1 帮助主题。|  
  
##  <a name="msgGeneral"></a> 常规消息和事件消息  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 错误消息的符号名称以 **DTS_MSG_** 开头。  
  
|十六进制代码|十进制代码|符号名称|描述|  
|----------------------|------------------|-------------------|-----------------|  
|0x1|1|DTS_MSG_CATEGORY_SERVICE_CONTROL|函数不正确。|  
|0x2|2|DTS_MSG_CATEGORY_RUNNING_PACKAGE_MANAGEMENT|系统找不到指定的文件。|  
|0x100|256|DTS_MSG_SERVER_STARTING|正在启动 Microsoft SSIS 服务。<br /><br /> 服务器版本 %1|  
|0x101|257|DTS_MSG_SERVER_STARTED|Microsoft SSIS 服务已启动。<br /><br /> 服务器版本 %1|  
|0x102|258|DTS_MSG_SERVER_STOPPING|等待操作超时。|  
|0x103|259|DTS_MSG_SERVER_STOPPED|没有更多可用数据。|  
|0x104|260|DTS_MSG_SERVER_START_FAILED|Microsoft SSIS 服务启动失败。<br /><br /> 错误: %1|  
|0x105|261|DTS_MSG_SERVER_STOP_ERROR|停止 Microsoft SSIS 服务时出错。<br /><br /> 错误: %1|  
|0x110|272|DTS_MSG_SERVER_MISSING_CONFIG|Microsoft SSIS 服务配置文件不存在。<br /><br /> 正在使用默认设置加载。|  
|0x111|273|DTS_MSG_SERVER_BAD_CONFIG|Microsoft SSIS 服务配置文件不正确。<br /><br /> 读取配置文件 %1 时出错<br /><br /> 正在使用默认设置加载服务器。|  
|0x112|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|Microsoft SSIS 服务:<br /><br /> 指定配置文件的注册表设置不存在。<br /><br /> 正尝试加载默认的配置文件。|  
|0x150|336|DTS_MSG_SERVER_STOPPING_PACKAGE|Microsoft SSIS 服务: 正在停止运行中的包。<br /><br /> 包实例 ID: %1<br /><br /> 包 ID: %2<br /><br /> 包名称: %3<br /><br /> 包说明: %4<br /><br /> 包启动方: %5。|  
|0x40013000|1073819648|DTS_MSG_PACKAGESTART|包“%1”已开始。|  
|0x40013001|1073819649|DTS_MSG_PACKAGESUCCESS|包“%1”已成功完成。|  
|0x40013002|1073819650|DTS_MSG_PACKAGECANCEL|包“%1”已取消。|  
|0x40013003|1073819651|DTS_MSG_PACKAGEFAILURE|包“%1”已失败。|  
|0x40013004|1073819652|DTS_MSG_CANTDELAYLOADDLL|由于出现错误 %4，模块 %1 无法加载 DLL %2 来调用入口点 %3。 该产品要求运行该 DLL，但在路径下找不到该 DLL。|  
|0x40013005|1073819653|DTS_MSG_CANTDELAYLOADDLLFUNCTION|模块 %1 加载了 DLL %2，但由于存在错误 %4，所以找不到入口点 %3。 在路径下找不到指定的 DLL，而产品又要求运行该 DLL。|  
|0x40103100|1074802944|DTS_MSG_EVENTLOGENTRY|事件名称: %1<br /><br /> 消息: %9<br /><br /> 操作员: %2<br /><br /> 源名称: %3<br /><br /> 源 ID: %4<br /><br /> 执行 ID: %5<br /><br /> 开始时间: %6<br /><br /> 结束时间: %7<br /><br /> 数据代码: %8|  
|0x40103101|1074802945|DTS_MSG_EVENTLOGENTRY_PREEXECUTE|事件名称: %1<br /><br /> 消息: %9<br /><br /> 操作员: %2<br /><br /> 源名称: %3<br /><br /> 源 ID: %4<br /><br /> 执行 ID: %5<br /><br /> 开始时间: %6<br /><br /> 结束时间: %7<br /><br /> 数据代码: %8|  
|0x40103102|1074802946|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|事件名称: %1<br /><br /> 消息: %9<br /><br /> 操作员: %2<br /><br /> 源名称: %3<br /><br /> 源 ID: %4<br /><br /> 执行 ID: %5<br /><br /> 开始时间: %6<br /><br /> 结束时间: %7<br /><br /> 数据代码: %8|  
|0x40103103|1074802947|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|事件名称: %1<br /><br /> 消息: %9<br /><br /> 操作员: %2<br /><br /> 源名称: %3<br /><br /> 源 ID: %4<br /><br /> 执行 ID: %5<br /><br /> 开始时间: %6<br /><br /> 结束时间: %7<br /><br /> 数据代码: %8|  
|0x40103104|1074802948|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|事件名称: %1<br /><br /> 消息: %9<br /><br /> 操作员: %2<br /><br /> 源名称: %3<br /><br /> 源 ID: %4<br /><br /> 执行 ID: %5<br /><br /> 开始时间: %6<br /><br /> 结束时间: %7<br /><br /> 数据代码: %8|  
|0x40103105|1074802949|DTS_MSG_EVENTLOGENTRY_WARNING|事件名称: %1<br /><br /> 消息: %9<br /><br /> 操作员: %2<br /><br /> 源名称: %3<br /><br /> 源 ID: %4<br /><br /> 执行 ID: %5<br /><br /> 开始时间: %6<br /><br /> 结束时间: %7<br /><br /> 数据代码: %8|  
|0x40103106|1074802950|DTS_MSG_EVENTLOGENTRY_ERROR|事件名称: %1<br /><br /> 消息: %9<br /><br /> 操作员: %2<br /><br /> 源名称: %3<br /><br /> 源 ID: %4<br /><br /> 执行 ID: %5<br /><br /> 开始时间: %6<br /><br /> 结束时间: %7<br /><br /> 数据代码: %8|  
|0x40103107|1074802951|DTS_MSG_EVENTLOGENTRY_TASKFAILED|事件名称: %1<br /><br /> 消息: %9<br /><br /> 操作员: %2<br /><br /> 源名称: %3<br /><br /> 源 ID: %4<br /><br /> 执行 ID: %5<br /><br /> 开始时间: %6<br /><br /> 结束时间: %7<br /><br /> 数据代码: %8|  
|0x40103108|1074802952|DTS_MSG_EVENTLOGENTRY_PROGRESS|事件名称: %1<br /><br /> 消息: %9<br /><br /> 操作员: %2<br /><br /> 源名称: %3<br /><br /> 源 ID: %4<br /><br /> 执行 ID: %5<br /><br /> 开始时间: %6<br /><br /> 结束时间: %7<br /><br /> 数据代码: %8|  
|0x40103109|1074802953|DTS_MSG_EVENTLOGENTRY_EXECSTATCHANGE|事件名称: %1<br /><br /> 消息: %9<br /><br /> 操作员: %2<br /><br /> 源名称: %3<br /><br /> 源 ID: %4<br /><br /> 执行 ID: %5<br /><br /> 开始时间: %6<br /><br /> 结束时间: %7<br /><br /> 数据代码: %8|  
|0x4010310A|1074802954|DTS_MSG_EVENTLOGENTRY_VARVALCHANGE|事件名称: %1<br /><br /> 消息: %9<br /><br /> 操作员: %2<br /><br /> 源名称: %3<br /><br /> 源 ID: %4<br /><br /> 执行 ID: %5<br /><br /> 开始时间: %6<br /><br /> 结束时间: %7<br /><br /> 数据代码: %8|  
|0x4010310B|1074802955|DTS_MSG_EVENTLOGENTRY_CUSTOMEVENT|事件名称: %1<br /><br /> 消息: %9<br /><br /> 操作员: %2<br /><br /> 源名称: %3<br /><br /> 源 ID: %4<br /><br /> 执行 ID: %5<br /><br /> 开始时间: %6<br /><br /> 结束时间: %7<br /><br /> 数据代码: %8|  
|0x4010310C|1074802956|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|事件名称: %1<br /><br /> 消息: %9<br /><br /> 操作员: %2<br /><br /> 源名称: %3<br /><br /> 源 ID: %4<br /><br /> 执行 ID: %5<br /><br /> 开始时间: %6<br /><br /> 结束时间: %7<br /><br /> 数据代码: %8|  
|0x4010310D|1074802957|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|事件名称: %1<br /><br /> 消息: %9<br /><br /> 操作员: %2<br /><br /> 源名称: %3<br /><br /> 源 ID: %4<br /><br /> 执行 ID: %5<br /><br /> 开始时间: %6<br /><br /> 结束时间: %7<br /><br /> 数据代码: %8|  
|0x4010310E|1074802958|DTS_MSG_EVENTLOGENTRY_INFORMATION|事件名称: %1<br /><br /> 消息: %9<br /><br /> 操作员: %2<br /><br /> 源名称: %3<br /><br /> 源 ID: %4<br /><br /> 执行 ID: %5<br /><br /> 开始时间: %6<br /><br /> 结束时间: %7<br /><br /> 数据代码: %8|  
  
##  <a name="msgSuccess"></a> 成功消息  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 成功消息的符号名称以 **DTS_S_** 开头。  
  
|十六进制代码|十进制代码|符号名称|描述|  
|----------------------|------------------|-------------------|-----------------|  
|0x40003|262147|DTS_S_NULLDATA|该值为 NULL。|  
|0x40005|262149|DTS_S_TRUNCATED|该字符串值被截断。 缓冲区接收到的字符串对该列而言太长，因而已被缓冲区截断。|  
|0x200001|2097153|DTS_S_EXPREVALTRUNCATIONOCCURRED|在对表达式求值期间发生了截断。 在求值期间发生了截断，其中可能包含中间步骤中的任何点。|  
  
##  <a name="msgPipeline"></a> 数据流组件错误消息  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 错误消息的符号名称以 **DTSBC_E_** 开头，其中“BC”指的是大多数 Microsoft 数据流组件都从中派生的本机基类。  
  
|十六进制代码|十进制代码|符号名称|描述|  
|----------------------|------------------|-------------------|-----------------|  
|0xC8000002|-939524094|DTSBC_E_INCORRECTEXACTNUMBEROFTOTALOUTPUTS|输出和错误输出的总数 %1!lu! 不正确。 该值必须正好等于 %2!lu!。|  
|0xC8000003|-939524093|DTSBC_E_FAILEDTOGETOUTPUTBYINDEX|无法检索索引为 %1!lu! 的输出。|  
|0xC8000005|-939524091|DTSBC_E_INCORRECTEXACTNUMBEROFERROROUTPUTS|错误输出的数目 %1!lu! 不正确。 该值必须正好等于 %2!lu!。|  
|0xC8000006|-939524090|DTSBC_E_INVALIDVALIDATIONSTATUSVALUE|验证状态值“%1!lu!”不正确 "。  它必须是在 DTSValidationStatus 枚举中找到的值之一。|  
|0xC8000007|-939524089|DTSBC_E_INPUTHASNOOUTPUT|输入“%1!lu!” 没有同步输出。|  
|0xC8000008|-939524088|DTSBC_E_INPUTHASNOERROROUTPUT|输入“%1!lu!” 没有同步的错误输出。|  
|0xC8000009|-939524087|DTSBC_E_INVALIDHTPIVALUE|HowToProcessInput 值 %1!lu! 无效。 该值必须是 HowToProcessInput 枚举的值之一。|  
|0xC800000A|-939524086|DTSBC_E_FAILEDTOGETCOLINFO|无法从缓冲区获取行“%1!ld!”、列“%2!ld!” 列的信息。  返回的错误代码是 0x%3!8.8X!。|  
|0xC800000B|-939524085|DTSBC_E_FAILEDTOSETCOLINFO|无法将行“%1!ld!”、列“%2!ld!” 列的信息设置到缓冲区中。  返回的错误代码是 0x%3!8.8X!。|  
|0xC800000C|-939524084|DTSBC_E_INVALIDPROPERTY|属性“%1”无效。|  
|0xC800000D|-939524083|DTSBC_E_PROPERTYNOTFOUND|找不到属性“%1”。|  
|0xC8000010|-939524080|DTSBC_E_READONLYPROPERTY|向只读属性“%1”赋值时出错。|  
|0xC8000011|-939524079|DTSBC_E_CANTINSERTOUTPUTCOLUMN|%1 不允许插入输出列。|  
|0xC8000012|-939524078|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCH|输出列的元数据与关联的输入列的元数据不匹配。  将更新输出列的元数据。|  
|0xC8000013|-939524077|DTSBC_E_OUTPUTCOLUMNSMISSING|有些输入列没有关联的输出列。 将添加相应的输出列。|  
|0xC8000014|-939524076|DTSBC_E_TOOMANYOUTPUTCOLUMNS|有些输入列没有关联的输出列。 将删除这些输入列。|  
|0xC8000015|-939524075|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCHUNMAP|输出列的元数据与关联的输入列的元数据不匹配。  将取消映射这些输入列。|  
|0xC8000016|-939524074|DTSBC_E_UNMAPINPUTCOLUMNS|有些输入列没有关联的输出列。 将取消映射这些输入列。|  
|0xC8000017|-939524073|DTSBC_E_MULTIPLEINCOLSTOOUTCOL|有个输入列与一个输出列相关联，但该输出列已和同一输入中的另一输入列相关联。|  
|0xC8000018|-939524072|DTSBC_E_CANTINSERTEXTERNALMETADATACOLUMN|%1 不允许插入外部元数据列。|  
  
  

---
title: 备份 ASDatabase cmdlet |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3fabe81584debdafa73f04c1915a00f947dacad6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="backup-asdatabase-cmdlet"></a>Backup-ASDatabase cmdlet
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  将 Analysis Services 多维或表格数据库备份到 Analysis Services 备份 (.abf) 文件。  

>[!NOTE] 
>这篇文章可能包含过期的信息和示例。 有关最新的使用 Get-help cmdlet。
  
## <a name="syntax"></a>语法  
 `Backup-ASDatabase [-BackupFile] <string> [-Name] <string> [-AllowOverwrite <SwitchParameter>] [-BackupRemotePartitions <SwitchParameter>] [-ApplyCompression <SwitchParameter>] [-FilePassword <SecureString>] [-Locations <Microsoft.AnalysisServices.BackupLocation[]>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
 `Backup-ASDatabase –Database <Microsoft.AnalysisServices.Database> [-AllowOverwrite <SwitchParameter>] [-BackupRemotePartitions <SwitchParameter>] [-ApplyCompression <SwitchParameter>] [-FilePassword <SecureString>] [-Locations <Microsoft.AnalysisServices.BackupLocation[]>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 使 Analysis Services 系统管理员能够将多维或表格数据库备份到某一备份文件。 如果未指定位置，将使用在安装过程中指定的默认备份位置。  
  
 可以对您备份的文件进行加密。 使用 –FilePassword 对文件进行加密。 在以后还原文件时，您必须提供加密文件时指定的密码。  
  
 此 cmdlet 支持 –Credential 参数，该参数可在您配置 Analysis Services 实例以进行 HTTP 访问时使用。 –Credential 参数具有可提供 Windows 用户标识的 PSCredential 对象。 之后，IIS 将在连接到 Analysis Services 时模拟该用户。 此标识必须对 Analysis Services 实例具有系统管理员权限才能执行备份。  
  
## <a name="parameters"></a>Parameters  
  
### <a name="-backupfile-string"></a>-A c k e\<字符串 >  
 指定备份文件的路径和名称。 如果仅指定了文件名，而没有指定路径，将使用默认备份位置。 此参数仅与 –Name 参数一起使用。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|0|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-name-string"></a>-Name \<string>  
 指定要备份的 Analysis Services 数据库。 如果您想要以字符串的显示传入名称，则可以使用 –Database 参数或 –Name 参数指定数据库。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|1|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-allowoverwrite-switchparameter"></a>-AllowOverwrite \<SwitchParameter >  
 覆盖相同名称的备份文件。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-backupremotepartitions-switchparameter"></a>-BackupRemotePartitions \<SwitchParameter >  
 指定远程分区是否将包含在备份中。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-applycompressionswitchparameter"></a>-ApplyCompression\<SwitchParameter >  
 指定是否压缩备份文件。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-filepassword-securestring"></a>-FilePassword \<SecureString >  
 指定对备份文件加密所用的密码。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-locations-microsoftanalysisservicesbackuplocation"></a>位置\<Microsoft.AnalysisServices.BackupLocation [] >  
 指定要存储备份文件的位置。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-server-string"></a>-Server \<string>  
 指定 cmdlet 要连接和执行的 Analysis Services 实例。 如果未提供服务器名称，将连接到本地主机。 对于默认实例，仅指定服务器名称。 对于命名实例，请使用格式 servername\instancename。 对于 HTTP 连接，请使用格式 http[s]://server[:port]/virtualdirectory/msmdpump.dll。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|localhost|  
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
  
### <a name="-database-microsoftanalysisservicesdatabase"></a>-数据库\<Microsoft.AnalysisServices.Database [] >  
 指定要备份的 Analysis Services 数据库对象。 您可以使用 -Database 参数或 –Name 参数指定数据库。 如果想要传入数据库名称，则使用 –Database。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|true|  
|接受通配符？|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 此 cmdlet 支持以下常用参数：-Verbose、-Debug、-ErrorAction、-ErrorVariable、-OutBuffer 和 -OutVariable。 有关详细信息，请参阅 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## <a name="inputs-and-outputs"></a>输入和输出  
 输入类型是可以传送到 cmdlet 的对象的类型。 返回类型是 cmdlet 所返回的对象的类型。  
  
|||  
|-|-|  
|输入|Microsoft.AnalysisServices.Database<br /><br /> 您可以传送要备份的多个数据库，例如特定实例的所有数据库。|  
|输出|无。|  
  
## <a name="example-1"></a>示例 1  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default >backup-asdatabase awdb-20110930.abf “Adventure Works” -AllowOverwrite -ApplyCompression  
```  
  
 此命令将 Adventure Works 数据库备份到默认备份位置处的一个 .abf 文件。 如果在该位置存在具有相同名称的现有文件，则覆盖该文件。  
  
## <a name="example-2"></a>示例 2  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default >$AWDB = get-item “databases\Adventure Works”   
PS SQLSERVER:\SQLAS\Localhost\default >Backup-asdatabase –database:$AWDB –AllowOverwrite  
```  
  
 此命令使用 –Database，而不是 -Backupfile 和 -Name。 在您想要将数据库名称传送到 cmdlet 时使用 –Database 参数。  
  
## <a name="example-3"></a>示例 3  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default\databases >dir * | backup-asdatabase  
```  
  
 此命令备份本地服务器上的所有数据库。  
  
## <a name="example-4"></a>示例 4  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default > $pwd = read-host –AsSecureString –Prompt “Password”   
PS SQLSERVER:\SQLAS\Localhost\default > $pwd -is [System.IDisposable]   
PS SQLSERVER:\SQLAS\Localhost\default > backup-asdatabase –backupfile test.abf –name contoso_retail –filepassword:$pwd server myremoteserver  
PS SQLSERVER:\SQLAS\Localhost\default >$pwd.Dispose()  
PS SQLSERVER:\SQLAS\Localhost\default >Remove-Variable –Name pwd  
```  
  
 第 1 行和第 2 行用于提示输入将用于加密文件的密码。  
  
 第 3 行用于将远程 Analysis Services 服务器上的 Contoso_Retail 示例数据库备份到同样位于该远程服务器上的名为 test.abf 的 Analysis Services 备份文件中。 该文件将保存到默认实例的默认备份文件夹中。  
  
 第 4 行和第 5 行用于删除密码。  
  
  
  

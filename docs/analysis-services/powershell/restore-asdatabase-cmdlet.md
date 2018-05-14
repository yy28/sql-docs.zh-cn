---
title: 还原 ASDatabase cmdlet |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 867de3feef4ade78459d6e55f6fad756e18891d4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="restore-asdatabase-cmdlet"></a>Restore-ASDatabase cmdlet
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  将多维或表格数据库备份 (.abf) 文件还原到 Analysis Services 实例。  

>[!NOTE] 
>这篇文章可能包含过期的信息和示例。 有关最新的使用 Get-help cmdlet。
  
## <a name="syntax"></a>语法  
 `Restore-ASDatabase [-RestoreFile] <string> [-Name] <string> [-AllowOverwrite <SwitchParameter>] Locations <Microsoft.AnalysisServices.RestoreLocation[]>] [-Security <Microsoft.AnalysisServices.RestoreSecurity>] [-Password <System.SecureString>] [-StorageLocation <System.string>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 使 Analysis Services 系统管理员能够将多维或表格数据库从某一备份 (.abf) 文件还原到本地或远程服务器实例。 如果您正在还原的文件已加密，则可以使用 –FilePassword 提供用于对该文件进行解密的密码。  
  
 此 cmdlet 支持 –Credential 参数，该参数可在您配置 Analysis Services 实例以进行 HTTP 访问时使用。 –Credential 参数具有可提供 Windows 用户标识的 PSCredential 对象。 之后，IIS 将在连接到 Analysis Services 时模拟该用户。 此标识必须对 Analysis Services 实例具有系统管理员权限才能还原文件。  
  
## <a name="parameters"></a>Parameters  
  
### <a name="-restorefile-string"></a>-RestoreFile\<字符串 >  
 指定要还原的文件的路径和名称。 如果仅指定了文件名，而没有指定路径，将假定为默认备份位置。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|0|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-name-string"></a>-Name \<string>  
 指定要还原的 Analysis Services 数据库。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|1|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-allowoverwrite-switchparameter"></a>-AllowOverwrite \<SwitchParameter >  
 覆盖使用相同名称和位置的数据库。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-locations-microsoftanalysisservicesrestorelocation"></a>位置\<Microsoft.AnalysisServices.RestoreLocation [] >  
 指定要还原的分区的远程位置。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-security-microsoftanalysisservicesrestoresecurity"></a>安全\<Microsoft.AnalysisServices.RestoreSecurity >  
 表示用于还原操作的安全设置。 有效值为 CopyAll、SkipMembership、IgnoreSecurity。 CopyAll 将还原角色和成员身份。 SkipMembership 仅重新创建角色。 IgnoreSecurity 还原数据库，而不还原角色。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-password-securestring"></a>-密码\<SecureString >  
 指定用于还原已加密的备份文件的密码。 您必须指定最初用于加密文件的密码。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-storagelocation-string"></a>-StorageLocation\<字符串 >  
 指定数据库存储位置。 这是文件系统上数据库文件所在的位置。 如果您未在使用默认位置（该默认位置是目标实例的备份文件夹），则设置此参数。  
  
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
  
### <a name="commonparameters"></a>\<CommonParameters >  
 此 cmdlet 支持以下常用参数：-Verbose、-Debug、-ErrorAction、-ErrorVariable、-OutBuffer 和 -OutVariable。 有关详细信息，请参阅 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## <a name="inputs-and-outputs"></a>输入和输出  
 输入类型是可以传送到 cmdlet 的对象的类型。 返回类型是 cmdlet 所返回的对象的类型。  
  
|||  
|-|-|  
|输入|System.string<br /><br /> 可以将字符串值传输到 cmdlet。|  
|输出|无。|  
  
## <a name="example-1"></a>示例 1  
  
```  
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase awtest.abf testawrestoredb –security:CopyAll  
```  
  
 此命令将本地备份文件夹中的 Analysis Services 备份文件 (awtest.abf) 还原到本地 Analysis Services 默认实例。 数据库名称不必存在；在这个例子中，该数据库名称指定为还原操作的一部分。 添加 –Security:CopyAll 可以将角色和角色成员身份从备份数据库填充到新的还原的数据库。  
  
## <a name="example-2"></a>示例 2  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default > $pwd = read-host –AsSecureString –Prompt “Password”   
PS SQLSERVER:\SQLAS\Localhost\default > $pwd -is [System.IDisposable]   
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase –restorefile testdb.abf –name AWTEST2 –password:$pwd  
PS SQLSERVER:\SQLAS\Localhost\default >$pwd.Dispose()  
PS SQLSERVER:\SQLAS\Localhost\default >Remove-Variable –Name pwd  
```  
  
 第 1 和第 2 行用于提示输入已用于加密文件的密码。  
  
 第 3 行从 Analysis Services 默认实例的本地备份文件夹还原已加密的 Analysis Services 备份文件 (testdb.abf)。  
  
 第 4 行和第 5 行用于删除密码。  
  
## <a name="example-3-remote-scenario"></a>示例 3（远程应用场景）  
 本示例演示了如何从分享到 Analysis Services 远程实例的文件还原本地备份文件。 在本示例中，备份文件作为名为 **internetsales** 的数据库存储在名为 **ssas-aw-srv01**的计算机上的默认 Analysis Services 实例上。  
  
 备份文件位于网络共享上，具有公共读取访问权限。 该远程 Analysis Services 实例必须具有该文件的读取权限。 文件必须位于网络共享上（无驱动器）。  
  
 请注意，此示例不依赖于 SQLAS 提供程序。 可将 cmdlet 作为独立命令运行。  
  
```  
PS SQLSERVER:\> restore-asdatabase -restorefile "\\FileServer01\DBFiles\InternetSalesTabular.abf" -name "internetsales  
" -server "SSAS-AW-SRV01"  
```  
  
## <a name="example-4"></a>示例 4  
  
```  
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase –restorefile “\\myremoteserver\backups\testdb.abf” –name Contoso_Retail –server myremoteserver –storagelocation “\\myremoteserver\restoreDBFiles”  
```  
  
 此命令将已加密的 Analysis Services 备份文件 (testdb.abf) 还原到远程 Analysis Services 默认实例上的远程备份文件夹中。 –StorageLocation 参数用于将数据库文件放置于非默认位置，在这个例子中，将放置于名为 restoreDBfiles 的共享文件中。  
  

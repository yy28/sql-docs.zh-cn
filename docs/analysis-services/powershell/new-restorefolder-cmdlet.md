---
title: "新 RestoreFolder cmdlet |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 5938b3a9-6412-45fc-86f8-264651d01598
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 20e512bbc1ac3ba7c2a6b6604032c047f83d10cf
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="new-restorefolder-cmdlet"></a>New-RestoreFolder cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
将原始文件夹还原到新文件夹。  

>[!NOTE] 
>这篇文章可能包含过期的信息和示例。 有关最新的使用 Get-help cmdlet。
  
## <a name="syntax"></a>语法  
 `New-RestoreFolder [-OriginalFolder] <String> [-NewFolder] <String> [-AsTemplate] [-Server <String>] [-Credential <PSCredential>] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]`  
  
 `New-RestoreFolder [-Server <String>] [-Credential <PSCredential>] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]`  
  
 在 Windows PowerShell 参考中介绍了常见参数（例如–Verbose、-Debug）、错误和警告参数、-Whatif 和 –Confirm。 有关详细信息，请参阅 [about_CommonParameters](http://technet.microsoft.com/library/dd315352.aspx)。  
  
## <a name="description"></a>Description  
 New-RestoreFolder cmdlet 用于基于原始文件夹的名称创建新文件夹。  
  
## <a name="parameters"></a>Parameters  
  
### <a name="-originalfolder-string"></a>-OriginalFolder \<string>  
 获取原始文件夹位置。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|0|  
|默认值||  
|接受管道输入？|true|  
|接受通配符？|false|  
  
### <a name="-newfolder-string"></a>-NewFolder \<string>  
 设置新文件夹的位置。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|1|  
|默认值||  
|接受管道输入？|true|  
|接受通配符？|false|  
  
### <a name="-astemplate-switchparameter"></a>-AsTemplate \<SwitchParameter>  
 指定是否应在内存中创建并返回该对象。  
  
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
 对于您已经配置了 HTTP 访问的实例，此参数用于在使用 HTTP 连接到 Analysis Service 实例时传入用户名和密码。 有关详细信息，请参阅[配置 HTTP 访问 Analysis Services 上 Internet Information Services &#40; IIS &#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)为 HTTP 连接。  
  
 如果指定此参数，将使用用户名和密码连接到指定的 Analysis Server 实例。 如果未指定凭据，将使用正在运行该工具的用户的默认 Windows 帐户。  
  
 若要使用此参数，请首先使用 Get-Credential 创建一个 PSCredential 对象，以便指定用户名和密码（例如， `$Cred=Get-Credential “adventure-works\bobh”`。 然后，可以将此对象传送到 –Credential 参数 `(-Credential:$Cred`)。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|True (ByValue)|  
|接受通配符？|false|  
  
## <a name="inputs-and-outputs"></a>输入和输出  
 输入类型是可以传送到 cmdlet 的对象的类型。 返回类型是 cmdlet 所返回的对象的类型。  
  
|||  
|-|-|  
|输入||  
|输出|InclusionThresholdSetting|  
  

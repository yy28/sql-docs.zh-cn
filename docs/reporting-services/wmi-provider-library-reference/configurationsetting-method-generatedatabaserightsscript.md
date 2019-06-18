---
title: GenerateDatabaseRightsScript 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- GenerateDatabaseRightsScript (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- GenerateDatabaseRightsScript method
ms.assetid: f2e6dcc9-978f-4c2c-bafe-36c330247fd0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8714aee2b5bb33c84a1d9f11b626d3e21e06ed1f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65570971"
---
# <a name="configurationsetting-method---generatedatabaserightsscript"></a>ConfigurationSetting 方法 - GenerateDatabaseRightsScript
  生成一个 SQL 脚本，用来向用户授予运行报表服务器所需的报表服务器数据库和其他数据库的权限。 调用者需要能够连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库服务器并能够执行该脚本。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub GenerateDatabaseRightsScript(ByVal UserName As String, _  
    ByVal DatabaseName As String, ByVal IsRemote As Boolean, _  
    ByVal IsWindowsUser As Boolean, ByRef Script As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GenerateDatabaseRightsScript(string UserName, string DatabaseName, bool IsRemote, bool IsWindowsUser, out string Script,   
out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameters  
 *UserName*  
 通过此脚本授予权限时作为授予对象的用户的用户名或 Windows 安全标识符 (SID)。  
  
 *DatabaseName*  
 脚本要向用户授予访问权限的数据库名称。  
  
 *IsRemote*  
 一个布尔值，指示对于报表服务器而言数据库是否为远程数据库。  
  
 *IsWindowsUser*  
 一个布尔值，指示指定用户名是 Windows 用户还是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户。  
  
 *脚本*  
 [out] 包含所生成的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 脚本的字符串。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>Remarks  
 如果 *DatabaseName* 为空，则忽略 *IsRemote* ，并且数据库名称使用报表服务器配置文件中的值。  
  
 如果将 IsWindowsUser 设置为 true，则 UserName 的格式应为 \<domain>\\<username\>    。  
  
 如果将 *IsWindowsUser* 设置为 **true**，则生成后的脚本将向用户授予对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的登录权限，将报表服务器数据库设置为默认数据库，并向用户授予报表服务器数据库、报表服务器临时数据库、master 数据库和 MSDB 系统数据库的 **RSExec** 角色。  
  
 如果将 *IsWindowsUser* 设置为 **true**，此方法接受标准 Windows SID 作为输入。 在提供标准的 Windows SID 或服务帐户名后，它们会转换为用户名字符串。 如果数据库是本地数据库，相应帐户会正确转换为帐户的本地化表示形式。 如果数据库是远程数据库，则相应帐户会表示为该计算机的帐户。  
  
 下表显示了转换后的帐户及其远程表示形式。  
  
|被转换的帐户/SID|公用名称|远程名称|  
|---------------------------------------|-----------------|-----------------|  
|(S-1-5-18)|Local System|\<Domain>\\<ComputerName\>$|  
|.\LocalSystem|Local System|\<Domain>\\<ComputerName\>$|  
|ComputerName\LocalSystem|Local System|\<Domain>\\<ComputerName\>$|  
|LocalSystem|Local System|\<Domain>\\<ComputerName\>$|  
|(S-1-5-20)|Network Service|\<Domain>\\<ComputerName\>$|  
|NT AUTHORITY\NetworkService|Network Service|\<Domain>\\<ComputerName\>$|  
|(S-1-5-19)|Local Service|错误 - 参见下方内容。|  
|NT AUTHORITY\LocalService|Local Service|错误 - 参见下方内容。|  
  
 在 [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)]上，如果使用的是内置帐户，且报表服务器数据库是远程数据库，将返回错误。  
  
 如果指定了 **LocalService** 内置帐户，且报表服务器数据库是远程数据库，将返回错误。  
  
 如果 *IsWindowsUser* 为 true，且 *UserName* 中提供的值需要转换，则 WMI 提供程序会确定报表服务器数据库是位于同一计算机上还是远程计算机上。 为了确定该数据库是否安装在本地，WMI 提供程序会将 DatabaseServerName 属性与下面的值列表进行对比评估。 如果发现结果匹配，则数据库为本地数据库。 否则，为远程数据库。 比较时不区分大小写。  
  
|DatabaseServerName 的值|示例|  
|---------------------------------|-------------|  
|"."||  
|"(local)"||  
|"LOCAL"||  
|localhost||  
|\<Machinename>|testlab14|  
|\<MachineFQDN>|example.redmond.microsoft.com|  
|\<IPAddress>|180.012.345,678|  
  
 如果将 *IsWindowsUser* 设置为 **true**，则 WMI 提供程序会调用 LookupAccountName 以获取帐户的 SID，然后调用 LookupAccountSID 以获取要置于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 脚本中的帐户名。 这样便可确保所使用的帐户名可通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 验证。  
  
 如果将 *IsWindowsUser* 设置为 **false**，则生成的脚本将向用户授予报表服务器数据库、报表服务器临时数据库、MSDB 数据库的 **RSExec** 角色。  
  
 如果将 *IsWindowsUser* 设置为 **false**，SQL Server 用户必须在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上存在，脚本才能成功运行。  
  
 如果报表服务器没有指定的报表服务器数据库，调用 GrantRightsToDatabaseUser 将返回错误。  
  
 生成的脚本支持 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  

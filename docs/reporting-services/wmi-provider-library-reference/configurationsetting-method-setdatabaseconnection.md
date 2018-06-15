---
title: SetDatabaseConnection 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: wmi-provider-library-reference
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SetDatabaseConnection (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetDatabaseConnection method
ms.assetid: c040aa78-92b8-41e4-9ae2-eff9fcdddc5b
caps.latest.revision: 19
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7574d6acf14c44e179455bf705fc297cf5f42b84
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33031534"
---
# <a name="configurationsetting-method---setdatabaseconnection"></a>ConfigurationSetting 方法 - SetDatabaseConnection
  设置与特定报表服务器数据库的报表服务器数据库连接。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub SetDatabaseConnection(Server as String, _  
    DatabaseName as string, CredentialsType as Integer, _  
    Username as String, Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void BackupEncryptionKey(string Server,   
    string DatabaseName, Int32 CredentialsType,   
    string UserName, string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameters  
 *Server*  
 用于托管报表服务器数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称。  
  
 *DatabaseName*  
 报表服务器数据库的名称。  
  
 *CredentialsType*  
 用于连接的凭据类型。 可为以下值：  
  
-   0 - Windows  
  
-   1 – [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   2 - Windows 服务  
  
 *UserName*  
 连接报表服务器数据库时所用的帐户名。  
  
 *密码*  
 连接报表服务器数据库时所用的密码。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>Remarks  
 当 CredentialsType 参数设置为 0 (Windows) 时，必须设置 UserName 和 Password 参数。 UserName 参数的格式必须为“domain\username”，相应的值必须代表有效的 Windows 登录名。  
  
 如果将 CredentialsType 参数设置为 1 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])，则 UserName 参数传递的值必须符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名的要求。  
  
 如果将 CredentialsType 参数设置为 2（Windows 服务），则报表服务器将使用集成安全性连接到报表服务器数据库，并且忽略 UserName 和 Password 参数。 报告服务器 Web 服务将使用 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 帐户或应用程序池的帐户及 Windows 服务帐户访问报表服务器数据库。  
  
 调用后，SetDatabaseConnection 方法将加密凭据和数据库信息并将它们存储在指定报表服务器的配置文件中。  
  
 SetDatabaseConnection 方法不会检查报表服务器是否可以使用指定的数据连接到报表服务器数据库。  
  
 在第一次设置时，将根据以下处理器来设置 ConnectionPoolSize 属性：ConnectionPoolSize = #Processors * 75。  
  
 SetDatabaseConnection 方法不会向指定的帐户授予权限。 您必须为需要访问报表服务器数据库的每一帐户调用 [GenerateDatabaseRightsScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md) 方法，然后运行所生成的脚本。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  

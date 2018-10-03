---
title: DatabaseLogonType 属性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- DatabaseLogonType
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- DatabaseLogonType property
ms.assetid: 6b592582-4c35-4029-ab86-982fff47d8d6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d9d20259ec79532db2ccbb04da4f83d66f3e2abd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47608587"
---
# <a name="configurationsetting-property---databaselogontype"></a>ConfigurationSetting 属性 - DatabaseLogonType
  指定报表服务器是使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 服务帐户、Windows 用户帐户还是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名访问报表服务器数据库。 只读。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Dim DatabaseLogonType As Integer  
```  
  
```csharp  
public int DatabaseLogonType;  
```  
  
## <a name="property-values"></a>属性值  
 表示登录类型的 **integer** 对象。  
  
## <a name="example-code"></a>示例代码  
 [MSReportServer_ConfigurationSetting 类](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Remarks  
 值为：  
  
-   0 表示 Windows 登录  
  
-   1 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录  
  
-   2 表示以服务身份登录  
  
 如果指定 0 (Windows)，则必须将 [DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogonaccount.md) 属性中的值设置为相应的有效 Windows 用户帐户。  
  
 如果指定 1 (SQL Server)，请确保 [DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogonaccount.md) 的值与有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名对应。  
  
 如果指定 2（Windows 服务），则报表服务器使用 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 帐户和 Windows 服务帐户来访问报表服务器数据库。 DatabaseLogonAccount 属性被忽略。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  

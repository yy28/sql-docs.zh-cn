---
title: DatabaseLogonAccount 属性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.suite: pro-bi
ms.topic: conceptual
apiname:
- DatabaseLogonAccount
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- DatabaseLogonAccount property
ms.assetid: 55f2863f-1ac1-4519-b512-e7f11c0ea5ea
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 30aa804ea5c4622e11c711282667c35381095afe
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43264740"
---
# <a name="configurationsetting-property---databaselogonaccount"></a>ConfigurationSetting 属性 - DatabaseLogonAccount
  指定报表服务器连接到报表服务器数据库时使用的登录帐户。 只读。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Dim DatabaseLogonAccount As String  
```  
  
```csharp  
public string DatabaseLogonAccount;  
```  
  
## <a name="property-values"></a>属性值  
 表示登录帐户名的 **String** 对象。  
  
## <a name="example-code"></a>示例代码  
 [MSReportServer_ConfigurationSetting 类](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Remarks  
 此属性的有效值将因 [DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontype.md) 属性的值而异。  
  
 如果 [DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontype.md) 属性设置为 **2 (Service)**，则将忽略此属性。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  

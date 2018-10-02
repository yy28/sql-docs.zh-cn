---
title: SecureConnectionLevel 属性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SecureConnectionLevel
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SecureConnectionLevel property
ms.assetid: fd5549e7-b874-41e2-866e-2f58caf6f733
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 42beaf5446038bfaa0faf1b8e95a4eb5fc6d16b8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727895"
---
# <a name="configurationsetting-property---secureconnectionlevel"></a>ConfigurationSetting 属性 - SecureConnectionLevel
  返回 RSReportServer.config 文件中指定的安全连接级别。 只读。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Dim SecureConnectionLevel As Integer  
```  
  
```csharp  
public Integer SecureConnectionLevel;  
```  
  
## <a name="property-values"></a>属性值  
 表示安全连接级别的 **Integer** 值。 返回值表示是否配置 SSL。 值大于或等于 1 表示打开了 SSL。 值为 0 表示关闭了 SSL。  
  
## <a name="example-code"></a>示例代码  
 [MSReportServer_ConfigurationSetting 类](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Remarks

在 SQL Server 2008 R2 中，SecureConnectionLevel 是一个开关。 有关详细信息，请参阅 [ConfigurationSetting 方法 - SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md)。

## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  

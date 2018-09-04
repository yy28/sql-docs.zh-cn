---
title: ReencryptSecureInformation 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.suite: pro-bi
ms.topic: conceptual
apiname:
- ReencryptSecureInformation (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- ReencryptSecureInformation method
ms.assetid: 8a487497-c207-45b2-8c92-87c58cc68716
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5492420f484892b172de6cdefde484469b1e7054
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43278628"
---
# <a name="configurationsetting-method---reencryptsecureinformation"></a>ConfigurationSetting 方法 - ReencryptSecureInformation
  生成新的加密密钥，并使用新密钥对目录中的所有安全信息进行重新加密。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub ReencryptSecureInformation(ByRef HRESULT as Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void ReencryptSecureInformation (out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>Parameters  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
 *ExtendedErrors[]*  
 [out] 一个字符串数组，包含此调用返回的其他错误。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>Remarks  
 ReencryptSecureInformation 方法允许管理员使用新密钥替换现有加密密钥。  
  
 调用此方法时，报表服务器会生成新的加密密钥，并遍历所有加密内容以使用新的加密密钥对其进行重新加密。  
  
 传递扩展插件可以其传递设置结构存储安全信息。 调用 ReencryptSecureInformation 时，报表服务器会加载每个订阅和相应的传递扩展插件，以对关联设置中存储的信息进行重新加密。  
  
 如果此方法运行在扩展部署中的计算机上，则扩展部署中的每台计算机将都需要再次进行初始化。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  

---
title: "ReencryptSecureInformation 方法 (WMI MSReportServer_ConfigurationSetting) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- ReencryptSecureInformation (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- ReencryptSecureInformation method
ms.assetid: 8a487497-c207-45b2-8c92-87c58cc68716
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: e7b57564600c568095ec999cf1db805437f8e630
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="configurationsetting-method---reencryptsecureinformation"></a>ConfigurationSetting 方法-ReencryptSecureInformation
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
  
## <a name="remarks"></a>注释  
 ReencryptSecureInformation 方法允许管理员使用新密钥替换现有加密密钥。  
  
 调用此方法时，报表服务器会生成新的加密密钥，并遍历所有加密内容以使用新的加密密钥对其进行重新加密。  
  
 传递扩展插件可以其传递设置结构存储安全信息。 调用 ReencryptSecureInformation 时，报表服务器会加载每个订阅和相应的传递扩展插件，以对关联设置中存储的信息进行重新加密。  
  
 如果此方法运行在扩展部署中的计算机上，则扩展部署中的每台计算机将都需要再次进行初始化。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  

---
title: ReencryptSecureInformation 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- ReencryptSecureInformation (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- ReencryptSecureInformation method
ms.assetid: 8a487497-c207-45b2-8c92-87c58cc68716
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ef1a23d21e5945e15d497bab3480b48f8cf3fe6d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66098213"
---
# <a name="reencryptsecureinformation-method-wmi-msreportserverconfigurationsetting"></a>ReencryptSecureInformation 方法 (WMI MSReportServer_ConfigurationSetting)
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
  
## <a name="remarks"></a>备注  
 ReencryptSecureInformation 方法允许管理员使用新密钥替换现有加密密钥。  
  
 调用此方法时，报表服务器会生成新的加密密钥，并遍历所有加密内容以使用新的加密密钥对其进行重新加密。  
  
 传递扩展插件可以其传递设置结构存储安全信息。 调用 ReencryptSecureInformation 时，报表服务器会加载每个订阅和相应的传递扩展插件，以对关联设置中存储的信息进行重新加密。  
  
 如果此方法运行在扩展部署中的计算机上，则扩展部署中的每台计算机将都需要再次进行初始化。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  

---
description: SetSecureConnectionLevel 方法 (WMI MSReportServer_ConfigurationSetting)
title: SetSecureConnectionLevel 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SetSecureConnectionLevel (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetSecureConnectionLevel method
ms.assetid: 0fac7d5e-2670-4657-9439-331e7d93babb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b7cc099e20e27f16e1d58779bba7d76f47f5d269
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480589"
---
# <a name="configurationsetting-method---setsecureconnectionlevel"></a>ConfigurationSetting 方法 - SetSecureConnectionLevel
  设置报表服务器的安全连接级别。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub SetSecureConnectionLevel(Level as Integer, _  
    ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetSecureConnectionLevel(Int32 Level,   
    out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>参数  
 *Level*  
 表示安全连接级别的整数值。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>备注  
 调用时，报表服务器 SecureConnectionLevel 属性设置为指定的值。 值为 0 表示禁用了 TLS。 值大于或等于 1 表示启用了 TLS。  
  
-   设置该值时，将更改报表服务器配置文件中的 SecureConnectionLevel 元素，并将配置文件中的“URLRoot”  元素设置为使用 "https://"（如果指定的  级别大于或等于 1）或使用 "http://"（如果指定的  级别为 0）。  
  
 在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]中，SecureConnectionLevel 成为一个开关，默认值为 0。 对于任何通过 SetSecureConnectionLevel 方法 API 传递的大于或等于 1 的值，TLS 被视为启用，且配置属性 SecureConnectionLevel 在 rsreportserver.config 文件中进行相应的设置。 将仍允许值为 2 和 3，以便向后兼容。  
  
## <a name="requirements"></a>要求  
 **命名空间：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  

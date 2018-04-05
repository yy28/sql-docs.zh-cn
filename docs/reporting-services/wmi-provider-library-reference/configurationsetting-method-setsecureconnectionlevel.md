---
title: SetSecureConnectionLevel 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: wmi-provider-library-reference
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SetSecureConnectionLevel (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetSecureConnectionLevel method
ms.assetid: 0fac7d5e-2670-4657-9439-331e7d93babb
caps.latest.revision: 21
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3278c7f0ff788ca99fb10adcac0266545a3931d1
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
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
  
## <a name="parameters"></a>Parameters  
 *级别*  
 表示安全连接级别的整数值。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>Remarks  
 调用时，报表服务器 SecureConnectionLevel 属性设置为指定的值。 值为 0 表示关闭了 SSL。 值大于或等于 1 标识打开了 SSL。  
  
-   设置该值时，将更改报表服务器配置文件中的 SecureConnectionLevel 元素，并将配置文件中的“URLRoot”元素设置为使用 "https://"（如果指定的级别大于或等于 1）或使用 "http://"（如果指定的级别为 0）。  
  
 在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]中，SecureConnectionLevel 成为一个开关，默认值为 0。 对于任何通过 SetSecureConnectionLevel 方法 API 传递的大于或等于 1 的值，SSL 将被视为打开，并且在 rsreportserver.config 文件中相应地设置配置属性 SecureConnectionLevel。 将仍允许值为 2 和 3，以便向后兼容。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  

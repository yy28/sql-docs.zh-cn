---
title: DeleteEncryptedInformation 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
api_name:
- DeleteEncryptedInformation (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DeleteEncryptedInformation method
ms.assetid: c14ed187-bdd9-4304-88e3-72072f03c21b
caps.latest.revision: 19
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 3d3e5893460c2ce3bcd2a6575d9bdd783936c736
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138587"
---
# <a name="deleteencryptedinformation-method-wmi-msreportserverconfigurationsetting"></a>DeleteEncryptedInformation 方法 (WMI MSReportServer_ConfigurationSetting)
  从报表服务器数据库删除加密信息。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub DeleteEncryptedInformation(ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void DeleteEncryptedInformation(out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>Parameters  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
 *ExtendedErrors[]*  
 [out] 一个字符串数组，包含此调用返回的其他错误。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>Remarks  
 调用此方法后，将删除以下数据：  
  
-   加密的数据源信息，包括用户名和密码。  
  
-   使用传递扩展插件接口加密的订阅数据。  
  
-   报表服务器数据库密钥表中的所有信息。  
  
 调用此方法后，用户必须初始化使用报表服务器数据库的每台计算机。  
  
 调用 DeleteEncryptedInformation 方法不会影响报表服务器配置文件。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
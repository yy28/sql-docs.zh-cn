---
title: DatabaseLogonAccount 属性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
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
- DatabaseLogonAccount
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DatabaseLogonAccount property
ms.assetid: 55f2863f-1ac1-4519-b512-e7f11c0ea5ea
caps.latest.revision: 24
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 75a929c87f963f102535c7fbe015a4bb49e6278f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027145"
---
# <a name="databaselogonaccount-property-wmi-msreportserverconfigurationsetting"></a>DatabaseLogonAccount 属性 (WMI MSReportServer_ConfigurationSetting)
  指定报表服务器连接到报表服务器数据库时使用的登录帐户。 只读。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Dim DatabaseLogonAccount As String  
```  
  
```csharp  
public string DatabaseLogonAccount;  
```  
  
## <a name="property-values"></a>属性值  
 表示登录帐户名的 `String` 对象。  
  
## <a name="example-code"></a>示例代码  
 [MSReportServer_ConfigurationSetting 类](msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Remarks  
 此属性的有效值将因而异的值[DatabaseLogonType](configurationsetting-property-databaselogontype.md)属性。  
  
 如果忽略此属性[DatabaseLogonType](configurationsetting-property-databaselogontype.md)属性设置为`2 (Service)`。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
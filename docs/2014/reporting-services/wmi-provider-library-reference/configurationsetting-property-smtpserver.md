---
title: SMTPServer 属性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- SMTPServer
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SMTPServer property
ms.assetid: 8bcceeba-e1a0-44ef-bda1-600c6925e1db
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 43252bcc1600a0d257ac2448a716a1fbab596bfa
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59959143"
---
# <a name="smtpserver-property-wmi-msreportserverconfigurationsetting"></a>SMTPServer 属性 (WMI MSReportServer_ConfigurationSetting)
  从报表服务器配置文件中获取 SMTP 服务器属性。 只读。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Dim SMTPServer As String  
```  
  
```csharp  
public string SMTPServer;  
```  
  
## <a name="property-values"></a>属性值  
 只读 `String` 对象，包含 RSReportServer.config 文件中 `SMTPServer` 属性的值。  
  
## <a name="example-code"></a>示例代码  
 [MSReportServer_ConfigurationSetting 类](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  

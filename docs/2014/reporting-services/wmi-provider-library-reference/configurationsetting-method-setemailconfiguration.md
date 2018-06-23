---
title: SetEmailConfiguration 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
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
- SetEmailConfiguration (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetEmailConfiguration method
ms.assetid: b40a2224-2c90-4d32-892f-1fe73a0591ca
caps.latest.revision: 19
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 67d63332e69e42b3f8631d37fe24626e108dde14
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123340"
---
# <a name="setemailconfiguration-method-wmi-msreportserverconfigurationsetting"></a>SetEmailConfiguration 方法 (WMI MSReportServer_ConfigurationSetting)
  配置报表服务器用来发送电子邮件的电子邮件传递扩展插件。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub SetEmailConfiguration(ByVal SendUsingSMTPServer As Boolean, _  
    ByVal SMTPServer As String, ByVal SenderEmailAddress As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetEmailConfiguration (Boolean SendUsingSMTPServer,   
   string SMTPServer, string SenderEmailAddress,   
   out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameters  
 *SendUsingSMTPServer*  
 指示相应服务器是否将使用 SMTP 服务器发送电子邮件的布尔值。 此值仅可设置为 true。 默认值为 false。  
  
 *SMTPServer*  
 包含 SMTP 服务器的名称或 IP 地址的字符串。  
  
 *SenderEmailAddress*  
 从报表服务器发出的电子邮件的“发件人:”字段中使用的电子邮件地址。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>Remarks  
 当*SendUsingSMTPServer*参数设置为`true`、 **SendUsing**报表服务器配置文件中的条目将设置为 1。 当*SendUsingSMTPServer*设置为`false`、 **SendUsing**不配置条目。  
  
 此方法并不适合用户将报表服务器配置文件中的 **SendUsing** 条目设置为 1 以外的其他值。 若要为报表服务器配置除 SMTP 邮件以外的其他设置，必须手动编辑配置文件。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
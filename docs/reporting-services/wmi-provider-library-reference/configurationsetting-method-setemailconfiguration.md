---
title: "SetEmailConfiguration 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: wmi-provider-library-reference
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
apiname: SetEmailConfiguration (WMI MSReportServer_ConfigurationSetting Class)
apilocation: reportingservices.mof
apitype: MOFDef
helpviewer_keywords: SetEmailConfiguration method
ms.assetid: b40a2224-2c90-4d32-892f-1fe73a0591ca
caps.latest.revision: "19"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 277196f9b8817500dda3c0c7470b4950ed0ff535
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-method---setemailconfiguration"></a>ConfigurationSetting 方法 - SetEmailConfiguration
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
 如果 *SendUsingSMTPServer* 参数设置为 **true**，则报告服务器配置文件中的 **SendUsing** 条目将设置为 1。 如果 *SendUsingSMTPServer* 设置为 **false**，则不会配置 **SendUsing** 条目。  
  
 此方法并不适合用户将报表服务器配置文件中的 **SendUsing** 条目设置为 1 以外的其他值。 若要为报表服务器配置除 SMTP 邮件以外的其他设置，必须手动编辑配置文件。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  

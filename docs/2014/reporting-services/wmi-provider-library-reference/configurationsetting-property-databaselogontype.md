---
title: DatabaseLogonType 属性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
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
- DatabaseLogonType
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DatabaseLogonType property
ms.assetid: 6b592582-4c35-4029-ab86-982fff47d8d6
caps.latest.revision: 24
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 30c6961f915789c358ba8d38ad0d18e164e072cf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014233"
---
# <a name="databaselogontype-property-wmi-msreportserverconfigurationsetting"></a>DatabaseLogonType 属性 (WMI MSReportServer_ConfigurationSetting)
  指定报表服务器是使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 服务帐户、Windows 用户帐户还是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名访问报表服务器数据库。 只读。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Dim DatabaseLogonType As Integer  
```  
  
```csharp  
public int DatabaseLogonType;  
```  
  
## <a name="property-values"></a>属性值  
 表示登录类型的 `integer` 对象。  
  
## <a name="example-code"></a>示例代码  
 [MSReportServer_ConfigurationSetting 类](msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Remarks  
 值为：  
  
-   0 表示 Windows 登录  
  
-   1 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录  
  
-   2 表示以服务身份登录  
  
 如果指定 0 (Windows)，你必须设置的值[DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md)到对应的有效的 Windows 用户帐户的属性。  
  
 如果指定 1 (SQL Server)，请确保值[DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md)对应于有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名。  
  
 如果指定 2（Windows 服务），则报表服务器使用 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 帐户和 Windows 服务帐户来访问报表服务器数据库。 DatabaseLogonAccount 属性被忽略。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
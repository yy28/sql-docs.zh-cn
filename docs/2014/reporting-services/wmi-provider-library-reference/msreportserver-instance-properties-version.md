---
title: Version 属性 (WMI MSReportServer_Instance) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Version property
ms.assetid: eea6bfe9-3130-4272-b3c2-c334349a7afd
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6d88725e0392d07784be7b558dc6cd18f03e458d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48158357"
---
# <a name="version-property-wmi-msreportserverinstance"></a>Version 属性 (WMI MSReportServer_Instance)
  以格式 Major.Minor.Build.Revision 返回报表服务器的版本。 只读。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Dim Version As String  
```  
  
```csharp  
public string Version;  
```  
  
## <a name="property-value"></a>属性值  
 一个`string`，其中包含报表服务器的版本。  
  
## <a name="example-code"></a>示例代码  
 [MSReportServer_ConfigurationSetting 类](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>要求  
 **Namespace**：[!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_Instance 成员](msreportserver-instance-members.md)  
  
  

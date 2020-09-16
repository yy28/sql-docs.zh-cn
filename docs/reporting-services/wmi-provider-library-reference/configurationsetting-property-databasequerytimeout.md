---
description: DatabaseQueryTimeout 属性 (WMI MSReportServer_ConfigurationSetting)
title: DatabaseQueryTimeout 属性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- DatabaseQueryTimeout Property
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- DatabaseQueryTimeout property
ms.assetid: 96faed97-9799-4bbf-a66f-fdd532d3eace
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5772326704b5e5fd6861b6185dab75cefdf42d1d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472629"
---
# <a name="configurationsetting-property---databasequerytimeout"></a>ConfigurationSetting 属性 - DatabaseQueryTimeout
  指定必须经过多少秒后报表服务器才能假设命令失败或命令执行的时间过长。 报表服务器会根据 SQL 目录对查询进行计时，而不会根据报表的数据源计时。 读/写。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Dim DatabaseQueryTimeout As UInt32  
```  
  
```csharp  
public UInt32 DatabaseQueryTimeout;  
```  
  
## <a name="property-values"></a>属性值  
 32 位的无符号 **integer** 对象，表示允许查询运行的秒数。  
  
## <a name="example-code"></a>示例代码  
 [MSReportServer_ConfigurationSetting 类](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>要求  
 **命名空间：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  

---
title: DatabaseQueryTimeout 属性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
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
- DatabaseQueryTimeout Property
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DatabaseQueryTimeout property
ms.assetid: 96faed97-9799-4bbf-a66f-fdd532d3eace
caps.latest.revision: 35
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: bcfd675860851b62dd2868adae00c6f6f13f6357
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027384"
---
# <a name="databasequerytimeout-property-wmi-msreportserverconfigurationsetting"></a>DatabaseQueryTimeout 属性 (WMI MSReportServer_ConfigurationSetting)
  指定必须经过多少秒后报表服务器才能假设命令失败或命令执行的时间过长。 报表服务器会根据 SQL 目录对查询进行计时，而不会根据报表的数据源计时。 读/写。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Dim DatabaseQueryTimeout As UInt32  
```  
  
```csharp  
public UInt32 DatabaseQueryTimeout;  
```  
  
## <a name="property-values"></a>属性值  
 32 位无符号`integer`对象，表示允许查询运行的秒数。  
  
## <a name="example-code"></a>示例代码  
 [MSReportServer_ConfigurationSetting 类](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
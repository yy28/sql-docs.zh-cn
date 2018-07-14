---
title: ConnectionPoolSize 属性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
api_name:
- ConnectionPoolSize
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- ConnectionPoolSize property
ms.assetid: b80c8e5d-b725-4fe4-aec6-02fb18ec4434
caps.latest.revision: 17
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 86d9f0b2e863e74126101c988f0883aad77b172c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37166218"
---
# <a name="connectionpoolsize-property-wmi-msreportserverconfigurationsetting"></a>ConnectionPoolSize 属性 (WMI MSReportServer_ConfigurationSetting)
  报表服务器与承载报表服务器数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例进行通信时使用的连接池大小。 只读。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Dim ConnectionPoolSize As UInt32  
```  
  
```csharp  
public UInt32 ConnectionPoolSize;  
```  
  
## <a name="property-values"></a>属性值  
 一个只读**整数**对象返回值的`768`。  
  
## <a name="example-code"></a>示例代码  
 [MSReportServer_ConfigurationSetting 类](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  

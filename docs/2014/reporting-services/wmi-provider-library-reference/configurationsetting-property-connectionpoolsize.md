---
title: ConnectionPoolSize 属性 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
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
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 24a180fde90ff406d40a0f0c89bf82dfe5138b88
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66097864"
---
# <a name="connectionpoolsize-property-wmi-msreportserver_configurationsetting"></a>ConnectionPoolSize 属性 (WMI MSReportServer_ConfigurationSetting)
  报表服务器与承载报表服务器数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例进行通信时使用的连接池大小。 只读。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Dim ConnectionPoolSize As UInt32  
```  
  
```csharp  
public UInt32 ConnectionPoolSize;  
```  
  
## <a name="property-values"></a>属性值  
 一个只读**整数**对象，它返回值`768`。  
  
## <a name="example-code"></a>示例代码  
 [MSReportServer_ConfigurationSetting 类](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>要求  
 **命名空间：**[!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  

---
title: 在 URL 中指定设备信息设置 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], URLs
- URL access [Reporting Services], device information settings
ms.assetid: cb7f7577-c6a8-4e6f-8e60-5ec0760f29c3
caps.latest.revision: 32
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a77fe212fc4637c384a8328aa1094db91b9a8d11
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37255569"
---
# <a name="specify-device-information-settings-in-a-url"></a>在 URL 中指定设备信息设置
  设备信息设置是传递给呈现扩展插件的参数。 如果您使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 报表服务器 Web 服务的方法呈现报表，则 `DeviceInfo` XML 元素将作为输入参数传递。 子元素的`DeviceInfo`元素是特定于不同呈现扩展插件的设备信息设置。 可以通过使用 *rc:tag=value* 参数字符串在 URL 中加入设备信息设置，其中 *tag* 是所访问的设备信息设置元素的名称。 有关详细信息中的设备信息设置[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]，请参阅[设备信息设置传递给呈现扩展插件](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)。  
  
## <a name="example"></a>示例  
 以下示例通过使用图像呈现扩展插件的 *OutputFormat* 设备信息设置，将指定报表的格式设置为 JPEG（添加了换行符以增强可读性）：  
  
```  
http://servername/reportserver?/SampleReports  
/Employee Sales Summary&EmployeeID=38&rs:  
Command=Render&rs:Format=IMAGE&rc:OutputFormat=JPEG  
```  
  
## <a name="see-also"></a>请参阅  
 [URL 访问&#40;SSRS&#41;](url-access-ssrs.md)   
 [URL 访问参数引用](url-access-parameter-reference.md)  
  
  

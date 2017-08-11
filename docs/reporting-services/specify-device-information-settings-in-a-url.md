---
title: "在 URL 中指定设备信息设置 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- device information settings [Reporting Services], URLs
- URL access [Reporting Services], device information settings
ms.assetid: cb7f7577-c6a8-4e6f-8e60-5ec0760f29c3
caps.latest.revision: 32
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 09e1655e7945a459cf9d606d24cf7479ee4fc568
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="specify-device-information-settings-in-a-url"></a>在 URL 中指定设备信息设置
  设备信息设置是传递给呈现扩展插件的参数。 如果你使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 报表服务器 Web 服务的方法呈现报表，则 **DeviceInfo** XML 元素将作为输入参数传递。 **DeviceInfo** 元素的子元素特定于不同呈现扩展插件的设备信息设置。 可以通过使用 *rc:tag=value* 参数字符串在 URL 中加入设备信息设置，其中 *tag* 是所访问的设备信息设置元素的名称。 有关 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中的设备信息设置的详细信息，请参阅 [将设备信息设置传递给呈现扩展插件](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)。  
  
## <a name="example"></a>示例  
 以下示例通过使用图像呈现扩展插件的 *OutputFormat* 设备信息设置，将指定报表的格式设置为 JPEG（添加了换行符以增强可读性）：  
  
```  
http://servername/reportserver?/SampleReports  
/Employee Sales Summary&EmployeeID=38&rs:  
Command=Render&rs:Format=IMAGE&rc:OutputFormat=JPEG  
```  
  
## <a name="see-also"></a>另请参阅  
 [URL 访问 &#40;SSRS &#41;](../reporting-services/url-access-ssrs.md)   
 [URL 访问参数引用](../reporting-services/url-access-parameter-reference.md)  
  
  

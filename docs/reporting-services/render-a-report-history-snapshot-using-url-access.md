---
title: 使用 URL 访问呈现报表历史记录快照 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], report history
- history snapshots [Reporting Services]
- historical data [Reporting Services]
- snapshots [Reporting Services], URL access
- snapshots [Reporting Services], rendering report history
ms.assetid: 3f87f82d-0e61-4492-9c4b-f5238c39e8cd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2caf9def46440aa87f8b4e143cc9e3163e408ba5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580809"
---
# <a name="render-a-report-history-snapshot-using-url-access"></a>使用 URL 访问呈现报表历史记录快照
  您可以通过提供 *rs:Snapshot* 参数并将其值设置为有效的快照 ID，基于报表历史记录快照呈现报表。 参数值采用 YYYY-MM-DDTHH:MM:SS 格式，该格式基于国际标准化组织 (ISO) 8601 标准。  
  
 如果省略此参数，则报表将根据报表服务器的报表执行和缓存管理选项设置呈现。 有关报表执行的详细信息，请参阅 [设置报表处理属性](../reporting-services/report-server/set-report-processing-properties.md)。  
  
## <a name="example"></a>示例  
 下面的示例说明检索历史记录快照的 URL：  
  
```  
https://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
```  
  
## <a name="see-also"></a>另请参阅  
 [URL 访问 (SSRS)](../reporting-services/url-access-ssrs.md)   
 [URL 访问参数引用](../reporting-services/url-access-parameter-reference.md)  
  
  

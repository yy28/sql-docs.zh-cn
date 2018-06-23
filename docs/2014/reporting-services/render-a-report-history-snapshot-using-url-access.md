---
title: 使用 URL 访问呈现报表历史记录快照 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- URL access [Reporting Services], report history
- history snapshots [Reporting Services]
- historical data [Reporting Services]
- snapshots [Reporting Services], URL access
- snapshots [Reporting Services], rendering report history
ms.assetid: 3f87f82d-0e61-4492-9c4b-f5238c39e8cd
caps.latest.revision: 32
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 29ff943923807b88db27bd9c8c6a1cc8430f96a3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123345"
---
# <a name="render-a-report-history-snapshot-using-url-access"></a>使用 URL 访问呈现报表历史记录快照
  您可以通过提供 *rs:Snapshot* 参数并将其值设置为有效的快照 ID，基于报表历史记录快照呈现报表。 参数值采用 YYYY-MM-DDTHH:MM:SS 格式，该格式基于国际标准化组织 (ISO) 8601 标准。  
  
 如果省略此参数，则报表将根据报表服务器的报表执行和缓存管理选项设置呈现。 有关报表执行的详细信息，请参阅[设置报表处理属性](report-server/set-report-processing-properties.md)。  
  
## <a name="example"></a>示例  
 下面的示例说明检索历史记录快照的 URL：  
  
```  
http://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
```  
  
## <a name="see-also"></a>请参阅  
 [URL 访问&#40;SSRS&#41;](url-access-ssrs.md)   
 [URL 访问参数引用](url-access-parameter-reference.md)  
  
  
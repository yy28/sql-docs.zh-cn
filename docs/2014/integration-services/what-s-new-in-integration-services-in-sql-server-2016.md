---
title: 什么&#39;s 新 (Integration Services) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Integration Services, what's new
- what's new [Integration Services]
ms.assetid: da6999c7-e5e3-4a59-a284-1da635995af1
caps.latest.revision: 112
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c7d37fb3c1d2cd1dcafecc012fbe83e1864e50ed
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015482"
---
# <a name="what39s-new-integration-services"></a>什么&#39;s 新 (Integration Services)
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 与先前的版本并无不同。  
  
 有关其他信息[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]产品和技术，请参阅[What's New in SQL Server 2014](../sql-server/what-s-new-in-sql-server-2016.md)。  
  
 有关与相关的更改的详细信息[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]商业智能，请参阅[What's New in Analysis Services 和 Business Intelligence](../analysis-services/what-s-new-in-analysis-services.md)。  
  
##  <a name="ValidateXML"></a> XML 任务中丰富的 XML 验证输出  
 验证 XML 文档并通过启用获取丰富错误输出`ValidationDetails`XML 任务的属性。 之前`ValidationDetails`属性为可用，则由 XML 任务的 XML 验证返回仅 true 或 false 的结果，但未显示信息有关错误或其位置。 现在，设置`ValidationDetails`为 true，输出文件包含有关每个错误包括行号和位置的详细的信息。 此信息可用于了解、查找和修复 XML 文档中的错误。 有关详细信息，请参阅 [Validate XML with the XML Task](control-flow/xml-task.md)。  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 引入`ValidationDetails`中的属性[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]Service Pack 2。 此时尚未公布或记录这一新属性。 `ValidationDetails`属性也为位于[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]和 SQL Server 2016 中。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 各个版本支持的功能](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  
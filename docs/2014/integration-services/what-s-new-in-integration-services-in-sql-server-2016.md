---
title: 什么&#39;s (Integration Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, what's new
- what's new [Integration Services]
ms.assetid: da6999c7-e5e3-4a59-a284-1da635995af1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6eda4eb4f01819bd569a472df01a276c5f270f31
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766090"
---
# <a name="what39s-new-integration-services"></a>什么&#39;s (Integration Services)
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 与先前的版本并无不同。  
  
 有关其他信息[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]产品和技术，请参阅[What's New in SQL Server 2014](../sql-server/what-s-new-in-sql-server-2016.md)。  
  
 有关与相关的更改的详细信息[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]商业智能，请参阅[What's New in Analysis Services 和 Business Intelligence](../analysis-services/what-s-new-in-analysis-services.md)。  
  
##  <a name="ValidateXML"></a> XML 任务中丰富的 XML 验证输出  
 通过启用 XML 任务的 `ValidationDetails` 属性，验证 XML 文档并获取丰富的错误输出。 在可以使用 `ValidationDetails` 属性之前，XML 任务的 XML 验证仅返回 true 或 false 结果，而不包含关于错误或其位置的详细信息。 现在，当你将 `ValidationDetails` 设置为 true 时，输出文件将包含关于每个错误的详细信息，包括行号和位置。 此信息可用于了解、查找和修复 XML 文档中的错误。 有关详细信息，请参阅 [Validate XML with the XML Task](control-flow/xml-task.md)。  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 介绍了 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 2 中的 `ValidationDetails` 属性。 此时尚未公布或记录这一新属性。 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 和 SQL Server 2016 中也可使用 `ValidationDetails` 属性。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 各个版本支持的功能](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  

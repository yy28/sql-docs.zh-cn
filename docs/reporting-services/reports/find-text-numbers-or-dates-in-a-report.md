---
title: "在报表中查找文本、 数字或日期 |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- searching reports
ms.assetid: 309dffe5-00f5-404f-bb63-9e6046253ae0
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 75e9c44d9cb75cef338ff2cd684c38969aa1751f
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="find-text-numbers-or-dates-in-a-report"></a>在报表中查找文本、数字或日期
  通过键入要查找的词或短语（搜索项的最大长度为 256 个字符），可以在报表中搜索内容。 搜索一种导航技术，它在报表中查找匹配值并将焦点放在报表中包含该值的部分。  
  
 搜索不区分大小写，并且从当前选择的页或区域开始。 只有在报表中可见的内容才会包含在搜索操作中。 如果报表包含展开或折叠的区域，在搜索过程中将跳过折叠区域中的值。 只能搜索当前报表中的文本、数字或日期。 如果您使用自动生成的点击链接型报表浏览数据，则不能搜索在先前生成的报表中看到的字词，也不能使用搜索沿数据路径深入查找可能显示在报表中的字词。  
  
 输入要搜索的值时，键入您预计的显示在报表中的值。 请不要提出“这个月的平均利润是多少”等问题，除非您预计报表中存在该句中的每个词。  
  
 一次只能搜索一个词或值。 不能使用搜索运算符（例如 AND 或 OR），也不能使用符号和通配符。 不能对数据的交叉部分执行搜索（例如，搜索特定产品在特定月份的净销售额）。 对于这种分析，请通过报表生成器来创建或使用点击链接型报表。  
  
 限制访问报表数据的数据库和模型安全设置将应用于搜索操作。 如果您要在使用模型作为数据源的点击链接型报表中搜索值，并且您没有对模型部分的访问权限，由模型部分表示的数据将从搜索中排除。  
  
### <a name="to-find-data-in-a-report"></a>在报表中查找数据  
  
1.  打开该报表。  
  
2.  在报表工具栏中，输入要查找的文本、数字或日期。  
  
     如果报表工具栏不可见，则表明它已特意隐藏起来，您将不能使用它提供的功能。 报表查看器 Web 部件的属性决定了该工具栏是否可见。  
  
3.  单击 **“查找”**。  
  
4.  若要搜索随后出现的相同值，请单击 **“下一个”**。  
  
## <a name="see-also"></a>另请参阅  
 [将报表查看器 Web 部件添加到网页（SharePoint 集成模式下的 Reporting Services）](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)  
  
  

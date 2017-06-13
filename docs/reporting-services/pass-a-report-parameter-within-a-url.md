---
title: "将报表参数在 URL 内的传递 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- URL access [Reporting Services], passing parameters
- passing parameters [Reporting Services]
ms.assetid: f93a94cc-27b5-435a-aa85-69e6ec6459ad
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e3b076b74a6082e34dc9c489c0383fd6a5c3bd4f
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="pass-a-report-parameter-within-a-url"></a>在 URL 内传递报表参数
  您可以通过在报表 URL 中包含报表参数，将它们传递到报表。 这些 URL 参数不带前缀，因为它们被直接传递到报表处理引擎。  
  
> [!IMPORTANT]  
>  非常重要的一点是，URL 包括用于通过 SharePoint 和 `_vti_bin` HTTP 代理路由请求的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 代理语法。 该代理会向 HTTP 请求中添加某一上下文，该上下文是确保为 SharePoint 模式报表服务器正确执行报表所需要的。  
>   
>  如果没有包含代理语法，则需要为该参数加上 *rp:*前缀。  
  
 所有查询参数都可具有对应的报表参数。 通过传递相应报表参数将查询参数传递给报表。 有关详细信息，请参阅[在关系查询设计器中生成查询（报表生成器和 SSRS）](../reporting-services/report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md)。  
  
> [!IMPORTANT]  
>  报表参数区分大小写。  
  
> [!NOTE]  
>  报表参数区分大小写并使用以下特殊字符：  
>   
>  -   URL 字符串中的任何空格字符将根据 URL 编码标准被字符“%20”替换。  
> -   URL 的参数部分中的空格字符将被加号字符 (+) 替换。  
> -   字符串任何部分中的分号将被字符“%3A”替换。  
> -   浏览器应自动执行正确的 URL 编码。 您不必手动对任何字符进行编码。  
  
 若要设置 URL 内的报表参数，请使用以下语法：  
  
```  
  
parameter=value  
```  
  
 例如，若要指定在报表中定义的两个参数“ReportMonth”和“ReportYear”，请将以下 URL 用于本机模式报表服务器：  
  
```  
http://myrshost/ReportServer?/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2&ReportMonth=3&ReportYear=2008  
```  
  
 例如，若要指定在报表中定义的两个相同参数，请将以下 URL 用于 SharePoint 集成模式的报表服务器。 注意 `/_vti_bin`：  
  
```  
http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2.rdl&ReportMonth=3&ReportYear=2008  
```  
  
 若要为参数传递 Null 值，请使用以下语法：  
  
```  
  
parameter  
:isnull=true  
  
```  
  
 例如：  
  
```  
SalesOrderNumber:isnull=true  
```  
  
 要传递 **Boolean** 值，请使用 0 表示 False，使用 1 表示 True。 要传递 **Float** 值，请包含服务器区域设置的小数分隔符。  
  
> [!NOTE]  
>  如果报表包含的某个报表参数具有默认值，并且 **Prompt** 属性的值为 **false** （即，在报表管理器中未选择 Prompt User 属性），则无法在 URL 中为该报表参数传递值。 这向管理员提供了一个选项，以防止最终用户添加或修改某些报表参数的值。  
  
##  <a name="bkmk_examples"></a> 其他示例  
 以下 URL 示例包含空格和多个参数  
  
-   文件夹名称“SQL Server User Education Team”包含空格，因此“+”将替换每个空格。  
  
-   报表名称“team project report”包含空格，因此“+”将替换每个空格。  
  
-   传递值分别为“xgroup”和“ygroup”的两个参数“teamgrouping2”和“teamgrouping1”。  
  
```  
https://myserver/Reportserver?/SQL+Server+User+Education+Team/_ContentTeams/folder123/team+project+report&teamgrouping2=xgroup&teamgrouping1=ygroup  
```  
  
 以下 URL 示例包含一个多值参数“OrderID”。 多值参数的格式是每个值都有重复的参数名称。  
  
```  
https://myserver/Reportserver?/SQL+Server+User+Education+Team/_ContentTeams/folder123/team+project+report&teamgrouping2=xgroup&teamgrouping1=ygroup&OrderID=747&OrderID=787&OrderID=12  
```  
  
 以下 URL 示例为本机模式报表服务器传递单个参数 SellStartDate，其值为“7/1/2005”。  
  
```  
http://myserver/ReportServer/Pages/ReportViewer.aspx?%2fProduct_and_Sales_Report_AdventureWorks&SellStartDate=7/1/2005  
```  
  
## <a name="see-also"></a>另请参阅  
 [URL 访问 (SSRS)](../reporting-services/url-access-ssrs.md)   
 [URL 访问参数引用](../reporting-services/url-access-parameter-reference.md)  
  
  

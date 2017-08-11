---
title: "将语言设置为在 URL 中的报表参数 |Microsoft 文档"
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
- overriding report language settings
- report servers [Reporting Services], language settings
- languages [Reporting Services]
- URL access [Reporting Services], language overrides
- international considerations [Reporting Services]
- global considerations [Reporting Services]
ms.assetid: e1ccf22f-80d6-45bc-aae0-f5f263275092
caps.latest.revision: 29
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 815af671e5bd26445153b96f68ebcbaf0e972cf7
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="set-the-language-for-report-parameters-in-a-url"></a>设置 URL 中的报表语言参数
  *rs:ParameterLanguage* URL 访问参数可以缓解与使用浏览器语言解释区分区域性的报表参数（如日期、时间、货币和数字）相关的问题。 借助于 *rs:ParameterLanguage*，现在可以独立于浏览器解释 URL。 例如，如果报表服务器设置为区域设置“德语”，但用户正在使用设置为“英语-美国”的浏览器通过 URL 访问某个报表，则将以错误的方式解释传递到报表服务器的参数值。  
  
 请看指向某个报表的以下 URL：  
  
```  
http://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008  
```  
  
 在上述情况下，在区域性“de-de”下运行的服务器通过电子邮件订阅或超链接生成一个 URL。 超链接指示应根据德语日期/时间标准，按照开始日期 2008 年 10 月 4 日和结束日期 2008 年 10 月 11 日对报表进行参数化。 然而，通过设置为“en-us”的浏览器访问此 URL 的用户会强制服务器按照美国英语日期/时间标准将值解释为 2008 年 4 月 10 日和 2008 年 11 月 10 日。 为了解决这一问题，可以使用 *rs:ParameterLanguage* 覆盖浏览器语言以进行参数解释。  
  
```  
http://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008&rs:ParameterLanguage=de-DE  
```  
  
 除了 URL 访问参数 **rc:Parameters** 的值 **true** 和 *false*之外，您现在可以传递值 **Collapsed**。 对于某个 URL 使用 *rc:Parameters*=**Collapsed** 时，HTML 查看器的参数提示区域将折叠到视线之外，但用户仍可以进行切换。 值为 **false** 时，将从 HTML 查看器工具栏删除参数提示区域并使其无法供最终用户使用。  
  
## <a name="see-also"></a>另请参阅  
 [URL 访问 &#40;SSRS &#41;](../reporting-services/url-access-ssrs.md)   
 [URL 访问参数引用](../reporting-services/url-access-parameter-reference.md)  
  
  

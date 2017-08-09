---
title: "访问使用 URL 访问报表服务器项 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- referencing URL items for report server access
- URL access [Reporting Services], report servers
ms.assetid: a58b4ca6-129d-45e9-95c7-e9169fe5bba4
caps.latest.revision: 40
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: fa59193fcedb1d5437d8df14035fadca2b3a28f1
ms.openlocfilehash: 475435073cef3f748e26a2a71c31a55fa7e6304d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="access-report-server-items-using-url-access"></a>使用 URL 访问报表服务器项
  本主题介绍如何向访问目录项在报表中的不同类型的服务器数据基本或在 SharePoint 站点使用*rs： 命令*=*值*。 不必实际添加此参数字符串。 如果您省略此字符串，报表服务器将会计算项类型，并且自动选择适当的参数值。 但是，在 URL 中使用 rs:Command=Value 字符串可改进报表服务器的性能。  
  
 请注意下面示例中的 `_vti_bin` 代理语法。 有关使用代理语法的详细信息，请参阅 [URL Access Parameter Reference](../reporting-services/url-access-parameter-reference.md)。  
  
## <a name="access-a-report"></a>访问报表  
 若要在浏览器中查看报表，请使用 rs:Command=Render 参数。 例如：  
  
 - **本机** `http://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render`  
 - **SharePoint** `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render`  
  
> [!TIP]  
>  非常重要的一点是，URL 包括用于通过 SharePoint 和 `_vti_bin` HTTP 代理路由请求的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 代理语法。 该代理会向 HTTP 请求中添加某一上下文，该上下文是确保为 SharePoint 模式报表服务器正确执行报表所需要的。  
  
## <a name="access-a-resource"></a>访问资源  
 若要访问某一资源，请使用 rs:Command=GetResourceContents 参数。如果该资源（例如图像）与浏览器兼容，则在浏览器中打开该资源。 否则，系统会提示您打开文件或资源或将其保存到磁盘。  
  
 **本机** `http://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents`  
  
 **SharePoint** `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents`  
  
## <a name="access-a-data-source"></a>访问数据源  
 若要访问数据源，请使用 *rs:Command*=*GetDataSourceContents* 参数。 如果您的浏览器支持 XML，则当您对于该数据源是具有 **Read Contents** 权限的经过身份验证的用户时，将显示数据源定义。 例如：  
  
 **本机** `http://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 **SharePoint** `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 XML 结构可能类似于以下示例：  
  
```  
<DataSourceDefinition>  
   <Extension>SQL</Extension>  
   <ConnectString>Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security Info=False;Initial Catalog=AdventureWorks2012;Data Source=MYSERVER1;</ConnectString>  
   <CredentialRetrieval>Integrated</CredentialRetrieval>  
   <WindowsCredentials>False</WindowsCredentials>  
   <ImpersonateUser>False</ImpersonateUser>  
   <Prompt />  
   <Enabled>True</Enabled>  
</DataSourceDefinition>  
```  
  
 将根据报表服务器的 **SecureConnectionLevel** 设置返回连接字符串。 有关 **SecureConnectionLevel** 设置的详细信息，请参阅 [Using Secure Web Service Methods](../reporting-services/report-server-web-service/net-framework/using-secure-web-service-methods.md)。  
  
## <a name="access-the-contents-of-a-folder"></a>访问文件夹的内容  
 若要访问某一文件夹的内容，请使用 rs:Command=GetChildren 参数。 将返回一个一般的文件夹导航页，其中包含指向在所请求文件中包含的子文件夹、报表、数据源和资源的链接。 例如：  
  
 **本机** `http://myrshost/reportserver?/Sales&rs:Command=GetChildren`  
  
 **SharePoint** `http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/Sales&rs:Command=GetChildren`  
  
 您所看到的用户界面类似于由 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Information Server (IIS) 使用的目录浏览模式。 报表服务器的版本号（包括内部版本号）也将显示在文件夹列表之下。  
  
## <a name="see-also"></a>另请参阅  
 [URL 访问 &#40;SSRS &#41;](../reporting-services/url-access-ssrs.md)   
 [URL 访问参数引用](../reporting-services/url-access-parameter-reference.md) 


---
title: "断言中自定义程序集的权限 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- secure calls [Reporting Services]
- custom assemblies [Reporting Services], permissions
- permission sets [Reporting Services]
- asserting permissions
- permissions [Reporting Services], custom assemblies
- limited permission sets
- security configuration files [Reporting Services]
ms.assetid: 3afb9631-f15e-405e-990b-ee102828f298
caps.latest.revision: 34
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 12e12b61a6b2a2a6a58bb88dd3c4f47c2a6eab22
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="asserting-permissions-in-custom-assemblies"></a>在自定义程序集中断言权限
  默认情况下，自定义程序集代码运行并为有限**执行**权限集。 在某些情况下，您可能想要实现对您的安全系统内的受保护资源（例如文件或注册表）进行安全调用的自定义程序集。 为此，您必须执行以下操作：  
  
1.  标识代码为进行安全调用所需的确切权限。 如果此方法的一部分[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]库，应方法文档中提供了此信息。  
  
2.  修改报表服务器策略配置文件，以便向自定义程序集授予所需的权限。 有关安全策略配置文件的详细信息，请参阅[使用 Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)。  
  
3.  将所需权限断言为按其进行安全调用的方法的一部分。 这是必需的因为由报表服务器调用的自定义程序集代码是报表表达式宿主程序集，它与运行的一部分**执行**默认情况下的权限。 **执行**权限集使代码来运行，但不是能使用受保护的资源。  
  
4.  标记与自定义程序集**AllowPartiallyTrustedCallersAttribute**如果使用强名称签名。 这是必需的因为自定义程序集从属于报表表达式宿主程序集，其中，默认情况下，未被授予的报表表达式调用**FullTrust**; 因此，它是"部分受信任"的调用方。 有关详细信息，请参阅[使用具有强名称自定义程序集](../../reporting-services/custom-assemblies/using-strong-named-custom-assemblies.md)。  
  
## <a name="implementing-a-secure-call"></a>实现安全调用  
 您可以修改策略配置文件，以便向您的程序集授予特定的权限。 例如，如果您正在编写用于处理货币换算的自定义程序集，则可能需要从某一文件读取当前外币汇率。 若要检索的速率信息，你需要添加额外的安全权限， **FileIOPermission**，到你的权限设置为程序集。 您可以在策略配置文件中输入以下附加内容：  
  
```  
<PermissionSet class="NamedPermissionSet"  
   version="1"  
   Name="CurrencyRatesFilePermissionSet"  
   Description="A special permission set that grants read access to my currency rates file.">  
      <IPermission class="FileIOPermission"  
         version="1"  
         Read="C:\CurrencyRates.xml"/>  
      <IPermission class="SecurityPermission"  
         version="1"  
         Flags="Execution, Assertion"/>  
</PermissionSet>  
```  
  
 然后，添加引用该权限集的代码组：  
  
```  
<CodeGroup class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="CurrencyRatesFilePermissionSet"  
   Name="MyNewCodeGroup"  
   Description="A special code group for my custom assembly.">  
   <IMembershipCondition class="UrlMembershipCondition"  
      version="1"  
      Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\MSSQL\Reporting Services\ReportServer\bin\CurrencyConversion.dll"/>  
</CodeGroup>  
```  
  
 为使您的代码可以获取相应权限，必须在自定义程序集代码内断言该权限。 例如，如果您想要添加对某一 XML 文件 C:\CurrencyRates.xml 的只读访问，则必须向您的方法添加以下代码：  
  
```  
// C#  
FileIOPermission permission = new FileIOPermission(FileIOPermissionAccess.Read, @"C:\CurrencyRates.xml");  
try  
{  
   permission.Assert();  
   // Load the XML currency rates file  
   XmlDocument doc = new XmlDocument();  
   doc.Load(@"C:\CurrencyRates.xml");  
...  
```  
  
 还可以将断言作为方法属性添加：  
  
```  
[FileIOPermissionAttribute(SecurityAction.Assert, Read=@"C:\CurrencyRates.xml")]  
```  
  
 有关详细信息，请参阅 .NET Framework 开发人员指南中的“.NET Framework 安全性”。  
  
## <a name="see-also"></a>另请参阅  
 [与报表中使用自定义程序集](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  

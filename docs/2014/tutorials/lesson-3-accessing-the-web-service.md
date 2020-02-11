---
title: 第3课：访问 Web 服务 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c3e4c198-ab35-4548-9471-1b4e6b6e5dfd
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 09671f8880f9f7745359961d9c6c126a893d26a7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62653780"
---
# <a name="lesson-3-accessing-the-web-service"></a>第 3 课：访问 Web 服务
  将报表服务器 Web 服务的引用添加到项目中后，下一步是创建 Web 服务代理类的实例。 然后，您可以通过调用代理类中的方法来访问 Web 服务的方法。 当应用程序调用这些方法时， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 生成的代理类代码将处理应用程序与 Web 服务之间的通信。  
  
 首先，您将创建一个 Web 服务代理类的实例 <xref:ReportService2010.ReportingService2010>。 接着，您将使用代理类调用 Web 服务的 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 方法。 您将使用该调用来检索一个示例报表 Company Sales 的名称和说明。  
  
> [!NOTE]  
>  访问在具有高级服务的 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 上运行的 Web 服务时，必须将“$SQLExpress”追加到“ReportServer”路径。 例如：  
>   
>  `http://<Server Name>/reportserver$sqlexpress/reportservice2010.asmx"`  
  
### <a name="to-access-the-web-service"></a>访问 Web 服务  
  
1.  首先，您必须将命名空间添加到 Program.cs 文件（在 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 中为 Module1.vb），采用的方法是向代码文件中添加 `using`（在 `Imports` 中为 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]）指令。 如果您使用该指令，则不必完全限定命名空间中的类型。  
  
2.  为此，请在代码文件的开头添加以下代码：  
  
    ```vb  
    Imports System  
    Imports GetPropertiesSample.ReportService2010  
    ```  
  
    ```csharp  
    using System;  
    using GetPropertiesSample.ReportService2010;  
    ```  
  
3.  在代码文件中输入了命名空间指令后，请使用控制台应用程序的 Main 方法输入以下代码。 请确保在设置 Web 服务实例的 **Url** 属性时更改服务器的名称：  
  
    ```vb  
    Sub Main()  
       Dim rs As New ReportingService2010  
       rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
       rs.Url = "http://<Server Name>/reportserver/reportservice2010.asmx"  
  
       Dim name As New [Property]  
       name.Name = "Name"  
  
       Dim description As New [Property]  
       description.Name = "Description"  
  
       Dim properties(1) As [Property]  
       properties(0) = name  
       properties(1) = description  
  
       Try  
          Dim returnProperties As [Property]() = rs.GetProperties( _  
             "/AdventureWorks 2012 Sample Reports/Company Sales 2012", properties)  
  
          Dim p As [Property]  
          For Each p In returnProperties  
              Console.WriteLine((p.Name + ": " + p.Value))  
          Next p  
  
       Catch e As Exception  
          Console.WriteLine(e.Message)  
       End Try  
    End Sub  
    ```  
  
    ```csharp  
    static void Main(string[] args)  
    {  
       ReportingService2010 rs = new ReportingService2010();  
       rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
       rs.Url = "http://<Server Name>/reportserver/reportservice2010.asmx";  
  
       Property name = new Property();  
       name.Name = "Name";  
  
       Property description = new Property();  
       description.Name = "Description";  
  
       Property[] properties = new Property[2];  
       properties[0] = name;  
       properties[1] = description;  
  
       try  
       {  
          Property[] returnProperties = rs.GetProperties(  
          "/AdventureWorks 2012 Sample Reports/Company Sales 2012",properties);  
  
          foreach (Property p in returnProperties)  
          {  
             Console.WriteLine(p.Name + ": " + p.Value);  
          }  
       }  
  
       catch (Exception e)  
       {  
          Console.WriteLine(e.Message);  
       }  
    }  
    ```  
  
4.  保存解决方案。  
  
 演练示例代码使用 Web 服务的 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 方法来检索示例报表 Company Sales 2012 的属性。 <xref:ReportService2010.ReportingService2010.GetProperties%2A>方法采用两个参数：要检索其属性信息的报表的名称，以及包含要检索其值的属性名称的**属性 []** 对象的数组。 方法还返回**属性 []** 对象的数组，其中包含在 properties 参数中指定的属性的名称和值。  
  
> [!NOTE]  
>  如果为 properties 参数提供空**属性 []** 数组，则返回所有可用属性。  
  
 在前面的示例中，代码使用 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 方法返回示例报表 Company Sales 2012 的名称和说明。 然后，代码使用 `foreach` 循环将属性和值写入控制台。  
  
 有关创建和使用报表服务器 Web 服务的代理类的详细信息，请参阅 [Creating the Web Service Proxy](../reporting-services/report-server-web-service/net-framework/creating-the-web-service-proxy.md)。  
  
## <a name="see-also"></a>另请参阅  
 [第4课：运行应用程序 &#40;VB-VC&#35;&#41;](../../2014/tutorials/lesson-4-running-the-application-vb-vcsharp.md)   
 [使用 Visual Basic 或 Visual C&#35; &#40;SSRS 教程访问报表服务器 Web 服务&#41;](../../2014/tutorials/access-report-server-web-service-vb-vcsharp-ssrs-tutorial.md)  
  
  

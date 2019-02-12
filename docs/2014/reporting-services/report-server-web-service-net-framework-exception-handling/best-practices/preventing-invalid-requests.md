---
title: 防止无效请求 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- invalid requests [Reporting Services]
- exceptions [Reporting Services], invalid requests
- valid requests [Reporting Services]
ms.assetid: 4a4a2d97-4c10-43a9-8298-ef5a820ea549
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 85556b6ec616d16962214b1737fcc445b54d0801
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56019678"
---
# <a name="preventing-invalid-requests"></a>防止无效请求
  您可以通过分析应用程序流程并确保要发送到报表服务器的请求有效，防止引发某些类型的异常。 例如，在使用户能够添加或更新报表名称、数据源或其他报表服务器项的应用程序中，您应该对用户可能输入的文本进行验证。 您应该始终在将请求发送到报表服务器之前检查是否使用了保留字符。 在代码中使用条件 if 语句或其他逻辑构造可以向用户发出警报，提醒用户尚未满足将请求发送到报表服务器所需的条件。  
  
 下面是一个简化的 C# 示例，在用户尝试创建名称中包含正斜杠 (/) 字符的报表时向其提供用户友好的错误消息。  
  
```  
// C#  
private void PublishReport()  
{  
   int index;  
   string reservedChar;  
   string message;  
  
   // Check the text value of the name text box for "/",  
   // a reserved character  
   index = nameTextBox.Text.IndexOf(@"/");  
  
   if ( index != -1) // The text contains the character  
   {  
      reservedChar = nameTextBox.Text.Substring(index, 1);  
      // Build a user-friendly error message  
      message = "The name of the report cannot contain the reserved character " +  
         "\"" + reservedChar + "\". " +  
         "Please enter a valid name for the report. " +  
         "For more information about reserved characters, " +  
         "see the help documentation";  
  
      MessageBox.Show(message, "Invalid Input Error");  
   }  
   else // Publish the report  
   {  
      Byte[] definition = null;  
      Warning[] warnings = {};  
      string name = nameTextBox.Text;  
  
      FileStream stream = File.OpenRead("MyReport.rdl");  
      definition = new Byte[stream.Length];  
      stream.Read(definition, 0, (int) stream.Length);  
      stream.Close();  
      // Create report with user-defined name  
      rs.CreateCatalogItem("Report", name, "/Samples", false, definition, null, out warnings);  
      MessageBox.Show("Report: {0} created successfully", name);  
   }  
}  
```  
  
 有关在将请求发送到报表服务器前可避免的错误类型的详细信息，请参阅 [SoapException 错误表](../soapexception-class/soapexception-errors-table.md)。 有关使用 try/catch 块进一步增强前一个示例的详细信息，请参阅[使用 Try 和 Catch 块](using-try-and-catch-blocks.md)。  
  
## <a name="see-also"></a>请参阅  
 [介绍 Reporting Services 中的异常处理](../introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 类](../soapexception-class/reporting-services-soapexception-class.md)  
  
  

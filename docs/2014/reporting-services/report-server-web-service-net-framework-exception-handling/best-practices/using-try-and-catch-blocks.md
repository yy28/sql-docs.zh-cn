---
title: 使用 Try 和 Catch 块 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- exceptions [Reporting Services], try/catch blocks
- try/catch blocks [Reporting Services]
ms.assetid: a7a9ef53-e3b6-4bf7-81f3-d85615954e6f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 774894c374edf4e57d1c297f981d423a7fabd4ee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63020087"
---
# <a name="using-try-and-catch-blocks"></a>使用 Try 和 Catch 块
  在通过向代码添加条件语句以限制对于报表服务器的无效请求之后，应通过使用 try/catch 块提供适当的异常处理。 此方法从另一个层面来防止无效的请求。 如果对于报表服务器的请求包含在 try 块中，并且该请求导致报表服务器引发异常，则将在 catch 块中捕获此异常，从而防止应用程序意外终止。 一旦捕获了异常，您就可以使用该异常来指导用户以不同方式操作，或者只是以友好的方式让用户知道已发生了错误。 然后，您可以使用 finally 块来清除任何资源。 在理想情况下，应生成一个常规异常处理计划以避免不必要地重复 try/catch 块。  
  
 以下示例使用 try/catch 块以增强异常处理代码的可靠性。  
  
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
         "consult the online documentation";  
  
      MessageBox.Show(message, "Invalid Input Error");  
   }  
   else // Publish the report  
   {  
      Byte[] definition = null;  
      Warning[] warnings = {};  
      string name = nameTextBox.Text;  
  
      try  
      {  
         FileStream stream = File.OpenRead("MyReport.rdl");  
         definition = new Byte[stream.Length];  
         stream.Read(definition, 0, (int) stream.Length);  
         stream.Close();  
         // Create report with user-defined name  
         rs.CreateCatalogItem("Report", name, "/Samples", false, definition, null, out warnings);  
         MessageBox.Show("Report: {0} created successfully", name);  
      }  
  
      // Catch expected exceptions beginning with the most specific,  
      // moving to the least specific  
      catch(IOException ex)  
      {  
         MessageBox.Show(ex.Message, "File IO Exception");  
      }  
  
      catch (SoapException ex)  
      {  
         // The exception is a SOAP exception, so use  
         // the Detail property's Message element.  
         MessageBox.Show(ex.Detail["Message"].InnerXml, "SOAP Exception");   
      }  
  
      catch (Exception ex)  
      {  
         MessageBox.Show(ex.Message, "General Exception");  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [介绍 Reporting Services 中的异常处理](../introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 类](../soapexception-class/reporting-services-soapexception-class.md)  
  
  

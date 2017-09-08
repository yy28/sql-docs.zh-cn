---
title: "批处理方法 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
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
- methods [Reporting Services], batches
- BatchHeader SOAP header
- Web service [Reporting Services], methods
- Report Server Web service, batching
- batches [Reporting Services]
- XML Web service [Reporting Services], methods
- locking [Reporting Services]
- multiple Web service methods
ms.assetid: 86435534-c9fe-4b49-b88c-7fb6d21976b0
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: ff92d909aad4d6de65e74cd4382c49560cf473c1
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="batching-methods"></a>批处理方法
  通过在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中使用 SOAP 标头，您可以在单个操作中包含多个 Web 服务方法。 方法在单个数据库事务的作用域中按照调用它们的顺序运行。  
  
 回滚是使用多方法批处理操作的一个优势。 如果在运行某一批处理时对于任何方法调用出现错误，报表服务器将停止运行此批处理并回滚任何先前的操作。 当某个方法调用依赖于成功完成该批处理中的其他方法调用时，这一点很有用。  
  
 Web 服务对于多方法批处理操作不提供锁定语义。 在向服务器发送消息并且调用 Execute 命令之前，将不锁定报表服务器数据库中的行进行更新。  
  
 此外，没有并发控制来保证数据库自上次读取数据之后尚未发生变化。 如果两个客户端修改同一项，当参数仍然有效（例如，尚未重命名该项）时，最后一次更新将成功。  
  
 以下示例调用 <xref:ReportService2005.ReportingService2005.CreateFolder%2A> 方法三次，并将这些调用作为单个批处理运行。 如果对于 <xref:ReportService2005.ReportingService2005.CreateFolder%2A> 的任何调用失败，将取消整个批处理。  
  
```vb  
Imports System  
Imports System.Web.Services.Protocols  
Imports myNamespace.MyReferenceName  
  
Class Sample  
    Sub Main(args() As String)  
        Dim rs As New ReportingService2005()  
        rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
      ' Set the base Web service URL of the source server  
      rs.Url = "http://<Server Name>/reportserver/ReportService2005.asmx"  
  
        Dim bh As New BatchHeader()  
  
        bh.BatchId = service.CreateBatch()  
        rs.BatchHeaderValue = bh  
        rs.CreateFolder("New Folder1", "/", Nothing)  
        rs.CreateFolder("New Folder2", "/", Nothing)  
        rs.CreateFolder("New Folder3", "/", Nothing)  
  
        Console.WriteLine("Creating folders...")  
        rs.BatchHeaderValue = bh  
        rs.ExecuteBatch()  
        Console.WriteLine("Folders created successfully.")  
  
        rs.BatchHeaderValue = Nothing  
    End Sub  
End Class  
```  
  
```csharp  
using System;  
using System.Web.Services.Protocols;   
using myNamespace.MyReferenceName;  
  
class Sample  
{  
    static void Main(string[] args)  
    {  
        ReportingService2005 rs = new ReportingService2005();  
        rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
      // Set the base Web service URL of the source server  
      rs.Url = "http://<Server Name>/reportserver/ReportService2005.asmx"  
  
        BatchHeader bh = new BatchHeader();  
  
        bh1.BatchID = service.CreateBatch();  
        rs.BatchHeaderValue = bh;  
        rs.CreateFolder("New Folder1", "/", null);  
        rs.CreateFolder("New Folder2", "/", null);  
        rs.CreateFolder("New Folder3", "/", null);  
  
        Console.WriteLine("Creating folders...");  
        rs.BatchHeaderValue = bh1;  
        rs.ExecuteBatch();  
        Console.WriteLine("Folders created successfully.");  
  
        rs.BatchHeaderValue = null;  
    }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 <xref:ReportService2005.ReportingService2005.CancelBatch%2A>   
 <xref:ReportService2005.ReportingService2005.CreateBatch%2A>   
 [技术参考 &#40;SSRS &#41;](../../reporting-services/technical-reference-ssrs.md)   
 [使用 Reporting Services SOAP 标头](../../reporting-services/report-server-web-service-net-framework-soap-headers/using-reporting-services-soap-headers.md)  
  
  

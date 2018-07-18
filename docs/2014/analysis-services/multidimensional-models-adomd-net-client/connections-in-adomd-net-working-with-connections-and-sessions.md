---
title: 使用连接和会话在 ADOMD.NET 中 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sessions [ADOMD.NET]
- connections [ADOMD.NET]
ms.assetid: 72b43c06-f3e4-42c3-a696-4a3419c3b884
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6ef7c679aa0f295c486836763158a89a1f593ff8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37176954"
---
# <a name="working-with-connections-and-sessions-in-adomdnet"></a>使用 ADOMD.NET 中的连接和会话
  在 XML for Analysis (XMLA) 中，会话在分析数据访问期间为有状态操作提供支持。 会话为分析数据源构成命令和事务的作用域和上下文。 用于管理会话的 XMLA 元素是[BeginSession](../xmla/xml-elements-headers/beginsession-element-xmla.md)，[会话](../xmla/xml-elements-headers/session-element-xmla.md)，并[EndSession](../xmla/xml-elements-headers/endsession-element-xmla.md)。  
  
 当您开始会话、在会话过程中执行查询或检索数据，以及关闭会话时，ADOMD.NET 将使用这三个 XMLA 会话元素。  
  
## <a name="starting-a-session"></a>启动会话  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 对象的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 属性包含与 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象关联的活动会话的标识符。 通过正确使用此属性，可以有效地控制应用程序中客户端和服务器的有状态性：  
  
-   调用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 方法时，如果 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> 属性未设置为有效的会话 ID，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象将从访问接口请求新的会话 ID。 ADOMD.NET 通过将 XMLA `BeginSession` 标头发送到访问接口来启动会话。 如果 ADOMD.NET 成功开始会话，ADOMD.NET 会将 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 属性的值设置为新创建的会话的会话 ID。  
  
-   调用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 方法时，如果 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> 属性设置为有效的会话 ID，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象将尝试连接到指定会话。  
  
 如果 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象无法连接到指定会话，或如果访问接口不支持会话，则引发异常。  
  
> [!NOTE]  
>  ADOMD.NET 创建会话后，可将多个 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象连接到单个活动会话，也可以断开单个 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象与该会话的连接，并将该对象重新连接到另一会话。  
  
## <a name="working-in-a-session"></a>在会话中工作  
 在 ADOMD.NET 将 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象连接到有效会话后，ADOMD.NET 将向访问接口发送 XMLA `Session` 标头，以及应用程序对数据或元数据的每个请求。 每个请求都将会话 ID 设置为 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 属性的值。  
  
 会话 ID 不保证会话保持有效。 如果会话过期（例如，会话超时或者连接中断），访问接口可以选择结束和回滚该会话的操作。 如果发生此情况，从 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 对象的所有后续方法调用都将引发异常。 因为只有当下一个请求发送到访问接口而不是会话过期时才引发异常，所以应用程序必须能够随时处理这些异常，才能够从访问接口检索数据或元数据。  
  
## <a name="closing-a-session"></a>关闭会话  
 如果<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A>无需指定的值调用方法*endSession*参数，或者如果*endSession*参数设置为 True，这两个连接到该会话和会话与关联<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>对象已关闭。 为了关闭会话，ADOMD.NET 将向访问接口发送 XMLA `EndSession` 标头，且将会话 ID 设置为 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 属性的值。  
  
 如果<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A>与调用方法*endSession*参数设置为 False，与关联的会话<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>对象保持活动状态，但与会话连接已关闭。  
  
## <a name="example-of-managing-a-session"></a>管理会话的示例  
 下面的示例演示如何打开连接、创建会话以及关闭连接，同时保持会话在 ADOMD.NET 中处于打开状态：  
  
```vb  
Public Function CreateSession(ByVal connectionString As String) As String  
    Dim strSessionID As String = ""  
    Dim objConnection As New AdomdConnection  
  
    Try  
        ' First, try to connect to the specified data source.  
        ' If the connection string is not valid, or if the specified  
        ' provider does not support sessions, an exception is thrown.  
        objConnection.ConnectionString = connectionString  
        objConnection.Open()  
  
        ' Now that the connection is open, retrieve the new  
        ' active session ID.  
        strSessionID = objConnection.SessionID  
        ' Close the connection, but leave the session open.  
        objConnection.Close(False)  
        Return strSessionID  
  
    Finally  
        objConnection = Nothing  
    End Try  
End Function  
```  
  
```csharp  
static string CreateSession(string connectionString)  
{  
    string strSessionID = "";  
    AdomdConnection objConnection = new AdomdConnection();  
    try  
    {  
        /*First, try to connect to the specified data source.  
          If the connection string is not valid, or if the specified  
          provider does not support sessions, an exception is thrown. */  
        objConnection.ConnectionString = connectionString;  
        objConnection.Open();  
  
        // Now that the connection is open, retrieve the new  
        // active session ID.  
        strSessionID = objConnection.SessionID;  
        // Close the connection, but leave the session open.  
        objConnection.Close(false);  
        return strSessionID;  
    }  
    finally  
    {  
        objConnection = null;  
    }  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [在 ADOMD.NET 中建立连接](connections-in-adomd-net.md)  
  
  

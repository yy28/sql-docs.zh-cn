---
title: 处理 SMO 事件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- events [SMO]
- SQL Server Management Objects, events
- SMO [SQL Server], events
- events [SMO], about events
ms.assetid: b4f120dd-ba78-46ff-99c5-e47effac8544
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e74a05e025f474737130f1faeb61f2647d8e69bd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37212987"
---
# <a name="handling-smo-events"></a>处理 SMO 事件
  某些服务器事件类型可以通过使用事件处理程序和 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 对象来进行订阅。  
  
 当服务器上发生某些操作时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理对象 (SMO) 中的许多实例类可以触发事件。  
  
 通过设置事件处理程序并订阅相关事件，可以以编程方式对这些事件进行处理。 这种事件处理只是暂时性的，因为当 SMO 客户端程序退出时会删除所有的订阅。  
  
## <a name="connectioncontext-event-handling"></a>ConnectionContext 事件处理  
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 对象支持若干种事件类型。 事件属性必须设置为相应事件处理程序的实例，且必须将事件处理程序对象定义为用于处理事件的受保护函数。  
  
## <a name="event-subscription"></a>事件订阅  
 您可以通过以下方法处理事件：编写事件处理程序类，创建该类的实例，将事件处理程序分配给父对象，然后订阅事件。  
  
 必须编写事件处理程序类才能处理事件。 事件处理程序类可以包含多个事件处理程序函数，且只有在安装事件处理程序类后才能处理事件。 事件处理程序函数接收来自事件有关的信息*ServerEventNotificatificationArgs*参数可用于报告有关事件的信息。  
  
 中列出的数据库和服务器可以处理的事件类型<xref:Microsoft.SqlServer.Management.Smo.DatabaseEventSet>类和<xref:Microsoft.SqlServer.Management.Smo.ServerEventSet>类。  
  
## <a name="example"></a>示例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="registering-event-handlers-and-subscribing-to-event-handling-in-visual-basic"></a>在 Visual Basic 中注册事件处理程序并订阅事件处理  
 此代码示例演示如何设置事件处理程序以及如何订阅数据库事件。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBEvents1](SMO How to#SMO_VBEvents1)]  -->  
  
## <a name="registering-event-handlers-and-subscribing-to-event-handling-in-visual-c"></a>在 Visual C# 中注册事件处理程序并订阅事件处理  
 此代码示例演示如何设置事件处理程序以及如何订阅数据库事件。  
  
```  
//Create an event handler subroutine that runs when a table is created.   
private void MyCreateEventHandler(object sender, ServerEventArgs e)   
{   
Console.WriteLine("A table has just been added to the AdventureWorks2012 database.");   
}   
//Create an event handler subroutine that runs when a table is deleted.   
private void MyDropEventHandler(object sender, ServerEventArgs e)   
{   
Console.WriteLine("A table has just been dropped from the AdventureWorks2012 database.");   
}   
public void Main()   
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Create a database event set that contains the CreateTable event only.   
DatabaseEventSet databaseCreateEventSet = new DatabaseEventSet();   
databaseCreateEventSet.CreateTable = true;   
//Create a server event handler and set it to the first event handler subroutine.   
ServerEventHandler serverCreateEventHandler;   
serverCreateEventHandler = new ServerEventHandler(MyCreateEventHandler);   
//Subscribe to the first server event handler when a CreateTable event occurs.   
db.Events.SubscribeToEvents(databaseCreateEventSet, serverCreateEventHandler);   
    //Create a database event set that contains the DropTable event only.   
DatabaseEventSet databaseDropEventSet = new DatabaseEventSet();   
databaseDropEventSet.DropTable = true;   
//Create a server event handler and set it to the second event handler subroutine.   
ServerEventHandler serverDropEventHandler;   
serverDropEventHandler = new ServerEventHandler(MyDropEventHandler);   
//Subscribe to the second server event handler when a DropTable event occurs.   
db.Events.SubscribeToEvents(databaseDropEventSet, serverDropEventHandler);   
//Start event handling.   
db.Events.StartEvents();   
//Create a table on the database.   
Table tb;   
tb = new Table(db, "Test_Table");   
Column mycol1;   
mycol1 = new Column(tb, "Name", DataType.NChar(50));   
mycol1.Collation = "Latin1_General_CI_AS";   
mycol1.Nullable = true;   
tb.Columns.Add(mycol1);   
tb.Create();   
//Remove the table.   
tb.Drop();   
//Wait until the events have occured.   
int x;   
int y;   
for (x = 1; x <= 1000000000; x++) {   
    y = x * 2;   
}   
//Stop event handling.   
db.Events.StopEvents();   
}  
```  
  
  

---
title: "ADO 事件实例化： ADO 和 WFC |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9ee4be21-657b-407a-afa4-0b27a6b096ce
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ffe0911f2845e7ff7e41cf41fcc4f267f7c0ad66
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="ado-event-instantiation-ado-and-wfc"></a>ADO 事件实例化： ADO 和 WFC
ADO 的 Windows 基础类 (ADO/WFC) 的 ADO 事件模型上构建，并提供简化的应用程序的编程接口。 一般情况下，ADO/WFC 截获 ADO 事件，将在事件参数合并到单个事件类，，然后调用事件处理程序。  
  
### <a name="to-use-ado-events-in-adowfc"></a>若要在 ADO/WFC 中使用 ADO 事件  
  
1.  定义你自己的事件处理程序来处理事件。 例如，如果你想要处理**ConnectComplete**中的事件**ConnectionEvent**系列，你可以使用此代码：  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    {  
        System.out.println("onConnectComplete:" + e);  
    }  
    ```  
  
2.  定义用于表示事件处理程序的处理程序的对象。 处理程序对象应为数据类型的**ConnectEventHandler**类型的事件**ConnectionEvent**，或数据类型**RecordsetEventHandler**类型的事件**RecordsetEvent**。 例如，代码的以下你**ConnectComplete**事件处理程序：  
  
    ```  
    ConnectionEventHandler handler =   
        new ConnectionEventHandler(this, "onConnectComplete");  
    ```  
  
     第一个参数**ConnectionEventHandler**构造函数是对包含事件处理程序在第二个参数名为的类的引用。  
  
3.  将事件处理程序添加到指定用于处理特定类型的事件的处理程序的列表。 使用带名称的方法，如**加载项***EventName*(*处理程序*)。  
  
4.  ADO/WFC 内部实现所有 ADO 事件处理程序。 因此，事件引起**连接**或**记录集**操作截获 ADO/WFC 事件处理程序。  
  
     ADO/WFC 事件处理程序将 ADO **ConnectionEvent** ADO/WFC 实例中的参数**ConnectionEvent**类或 ADO **RecordsetEvent**中的参数实例的 ADO/WFC **RecordsetEvent**类。 这些 ADO/WFC 类合并 ADO 事件参数;也就是说，每个 ADO/WFC 类包含所有 ADO 中每个唯一参数的一个数据成员**ConnectionEvent**或**RecordsetEvent**方法。  
  
5.  ADO/WFC 然后调用事件处理程序与 ADO/WFC 事件对象。 例如，你**onConnectComplete**处理程序的签名如下：  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    ```  
  
     第一个参数是发送事件的对象的类型 ([连接](../../../ado/reference/ado-api/connection-object-ado.md)或[记录集](../../../ado/reference/ado-api/recordset-object-ado.md))，而第二个参数是在 ADO/WFC 事件对象 (**ConnectionEvent**或**RecordsetEvent**)。  
  
     事件处理程序的签名是比 ADO 事件简单得多。 但是，你仍必须了解要知道的参数将适用的事件以及如何响应的 ADO 事件模型。  
  
6.  从事件处理程序返回到 ADO 事件 ADO/WFC 处理程序。 ADO/WFC 相关 ADO/WFC 事件数据成员复制回 ADO 事件参数，并返回 ADO 事件处理程序。  
  
7.  如果你已完成处理，从 ADO/WFC 事件处理程序的列表中删除您的处理程序。 使用带名称的方法，如**removeOn***EventName*(*处理程序*)。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO-WFC 语法索引](../../../ado/reference/ado-api/ado-wfc-syntax-index.md)   
 [事件参数](../../../ado/guide/data/event-parameters.md)   
 [事件处理程序是如何协同工作](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [事件类型](../../../ado/guide/data/types-of-events.md)

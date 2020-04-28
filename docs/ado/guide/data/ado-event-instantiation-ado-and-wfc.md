---
title: ADO 事件实例化： ADO 和 WFC |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 9ee4be21-657b-407a-afa4-0b27a6b096ce
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7dbbbf92c751093d2a7333b7ac1f76888d41d345
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "70212338"
---
# <a name="ado-event-instantiation-ado-and-wfc"></a>ADO 事件实例化：ADO 和 WFC
Windows 基础类（ADO/WFC）的 ADO 构建于 ADO 事件模型上，并提供简化的应用程序编程接口。 通常情况下，ADO/WFC 会截获 ADO 事件，将事件参数合并为单个事件类，然后调用事件处理程序。  
  
### <a name="to-use-ado-events-in-adowfc"></a>在 ADO/WFC 中使用 ADO 事件  
  
1.  定义自己的事件处理程序以处理事件。 例如，如果要处理**ConnectionEvent**系列中的**ConnectComplete**事件，可以使用以下代码：  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    {  
        System.out.println("onConnectComplete:" + e);  
    }  
    ```  
  
2.  定义用于表示事件处理程序的处理程序对象。 对于**ConnectionEvent**类型的事件，处理程序对象应为数据类型**ConnectEventHandler** ，对于**RecordsetEvent**类型的事件，则为数据类型**RecordsetEventHandler** 。 例如，为**ConnectComplete**事件处理程序编写以下代码：  
  
    ```  
    ConnectionEventHandler handler =   
        new ConnectionEventHandler(this, "onConnectComplete");  
    ```  
  
     **ConnectionEventHandler**构造函数的第一个参数是对类的引用，该类包含第二个参数中命名的事件处理程序。  
  
3.  将事件处理程序添加到指定用于处理特定事件类型的处理程序列表。 使用带有名称的方法，如**加载**项_事件_（*处理程序*）。  
  
4.  ADO/WFC 在内部实现所有 ADO 事件处理程序。 因此，由**连接**或**记录集**操作导致的事件被 ADO/WFC 事件处理程序截获。  
  
     ADO/WFC 事件处理程序在 ado/WFC **ConnectionEvent**类的实例中传递 ado **ConnectionEvent**参数，或在 ado/wfc **RecordsetEvent**类的实例中传递 ado **RecordsetEvent**参数。 这些 ADO/WFC 类合并了 ADO 事件参数;也就是说，每个 ADO/WFC 类对于所有 ADO **ConnectionEvent**或**RecordsetEvent**方法中的每个唯一参数都包含一个数据成员。  
  
5.  ADO/WFC 随后将调用事件处理程序和 ADO/WFC 事件对象。 例如， **onConnectComplete**处理程序的签名如下所示：  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    ```  
  
     第一个参数是发送事件的对象的类型（[连接](../../../ado/reference/ado-api/connection-object-ado.md)或[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)），第二个参数是 ADO/WFC 事件对象（**ConnectionEvent**或**RecordsetEvent**）。  
  
     事件处理程序的签名比 ADO 事件简单。 但是，您仍然必须了解 ADO 事件模型，才能了解哪些参数适用于事件以及如何做出响应。  
  
6.  从事件处理程序返回到 ADO 事件的 ADO/WFC 处理程序。 ADO/WFC 将相关的 ADO/WFC 事件数据成员复制回 ADO 事件参数，然后 ADO 事件处理程序返回。  
  
7.  完成处理后，从 ADO/WFC 事件处理程序列表中删除处理程序。 使用带有名称的方法，如**removeOn**_事件_名称（*处理程序*）。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO-WFC 语法索引](../../../ado/reference/ado-api/ado-wfc-syntax-index.md)   
 [事件参数](../../../ado/guide/data/event-parameters.md)   
 [事件处理程序如何协同工作](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [事件类型](../../../ado/guide/data/types-of-events.md)

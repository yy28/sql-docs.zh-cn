---
title: "断开连接，并重新连接记录集 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Recordset object [ADO], disconnecting and reconnecting
ms.assetid: c5134af7-81d6-4de4-9fd1-cfe29973545e
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a6ddbc392ae0bd0c378a4d08cd2c76f3119d8332
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>断开连接，并重新连接记录集
在 ADO 中找到的最强大功能之一是从数据源打开客户端记录集，然后断开与数据源连接的记录集的功能。 一旦已断开记录集，可以关闭与数据源的连接，从而释放使用对其进行维护的服务器上的资源。 你可以继续查看和编辑中记录集的数据，当它断开连接时和稍后重新连接到数据源并在批处理模式下发送更新。  
  
 要断开连接的记录集，使用 adUseClient，光标所在的位置打开它，然后设置 ActiveConnection 属性等于执行任何操作。 （c + + 用户应将 ActiveConnection 设置为 NULL，以断开连接。）  
  
 我们将使用断开连接的记录集更高版本在本部分中时，我们讨论记录集持久性进行寻址方案中，我们需要客户端计算机未连接到网络时在记录集中可用的应用程序具有的数据。  
  
## <a name="see-also"></a>另请参阅  
 [批处理模式](../../../ado/guide/data/batch-mode.md)


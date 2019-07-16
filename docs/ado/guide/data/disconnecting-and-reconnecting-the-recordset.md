---
title: 断开连接并重新连接记录集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset object [ADO], disconnecting and reconnecting
ms.assetid: c5134af7-81d6-4de4-9fd1-cfe29973545e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9829ddfd7e625941c97bd3b2027c328a1fba93d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925515"
---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>断开连接并重新连接记录集
在 ADO 中找到的最强大功能之一是从数据源打开客户端的记录集，然后断开与数据源连接记录集的能力。 一旦已断开连接记录集，可以关闭到数据源的连接，从而释放用于对其进行维护的服务器上的资源。 可以继续查看和编辑记录集中的数据，它断开连接时和更高版本重新连接到数据源并在批处理模式下发送更新。  
  
 若要断开连接记录集，请使用 adUseClient，光标所在的位置将其打开，并将 ActiveConnection 属性设置为 Nothing。 (C++用户应将设置为 NULL，以断开连接的 ActiveConnection。)  
  
 我们将使用未连接记录集更高版本在本部分介绍使用记录集暂留来解决方案中，我们需要客户端计算机未连接到网络时在记录集中的应用程序可以具有的数据。  
  
## <a name="see-also"></a>请参阅  
 [批处理模式](../../../ado/guide/data/batch-mode.md)

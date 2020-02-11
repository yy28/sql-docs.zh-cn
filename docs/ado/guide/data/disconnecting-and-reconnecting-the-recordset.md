---
title: 断开和重新连接记录集 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925515"
---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>断开连接并重新连接记录集
ADO 中最强大的功能之一是能够从数据源打开客户端记录集，然后将记录集与数据源断开连接。 断开记录集的连接后，可以关闭与数据源的连接，从而释放用于维护该数据源的服务器上的资源。 当记录集中的数据断开连接，然后重新连接到数据源并在批处理模式下发送更新时，可以继续查看和编辑该记录集中的数据。  
  
 若要断开记录集的连接，请使用光标位置 adUseClient 打开它，然后将 ActiveConnection 属性设置为 "无"。 （C + + 用户应将 ActiveConnection 设置为 NULL 以断开连接。）  
  
 我们将在本部分的后面部分介绍如何使用断开连接的记录集来解决这样一种情况：当客户端计算机未连接到网络时，我们需要将记录集中的数据提供给应用程序。  
  
## <a name="see-also"></a>另请参阅  
 [批处理模式](../../../ado/guide/data/batch-mode.md)

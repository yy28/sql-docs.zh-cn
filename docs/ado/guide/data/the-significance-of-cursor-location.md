---
title: 光标位置的重要性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- server-side cursors [ADO]
- cursors [ADO], client-side
- client-side cursors [ADO]
- cursors [ADO], server-side
ms.assetid: 70ef5b1c-0459-41a1-b796-031f61a29a8a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d25153a3c84340ad6feea43aa969ef52d358fe4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47717715"
---
# <a name="the-significance-of-cursor-location"></a>游标位置的重要性
每个游标使用临时资源来保存其数据。 这些资源可以是内存、 磁盘分页文件、 临时磁盘文件或甚至临时存储在数据库中。 游标被称为*客户端*游标时这些资源都位于客户端计算机上。 游标被称为*服务器端*游标时这些资源位于服务器上。  
  
## <a name="client-side-cursors"></a>客户端游标  
 在 ADO 中，调用的客户端游标通过使用**adUseClient CursorLocationEnum。** 与非键集客户端游标，服务器将发送整个结果集在网络上客户端计算机。 客户端计算机提供和管理所需的游标和结果集的临时资源。 客户端应用程序可以浏览整个结果集以确定所需的行。  
  
 如果它们包含过多的行，静态和由键集驱动的客户端游标可能会在工作站上放置大量负载。 虽然都能够构建有数千行的游标的游标库，用于提取此类大的行集的应用程序可能会很差。 有例外情况，当然。 对于某些应用程序，大的客户端游标可能是完全适合，性能可能不会出现问题。  
  
 客户端游标的一个明显的好处是快速响应。 结果集已下载到客户端计算机后，浏览的所有行都都非常快。 你的应用程序是通常更具可伸缩性与客户端游标，因为游标的资源要求放置在每个单独的客户端，而不是服务器上。  
  
## <a name="server-side-cursors"></a>服务器端游标  
 在 ADO 中，对于服务器端游标通过使用调用**adUseServer CursorLocationEnum。** 与服务器端游标，服务器将管理结果集使用提供的服务器计算机资源。 服务器端游标通过网络返回请求的数据。 此类型的游标有时可以提供更好的性能比客户端游标，尤其是在情况下，过多的网络流量时出现问题。  
  
 但是，务必要指出的是，服务器端游标，至少暂时-对于每个活动的客户端占用宝贵的服务器资源。 你必须相应地规划以确保你的服务器硬件能够管理所有的活动客户端请求的服务器端游标。 此外，服务器端游标可能因为它提供了只有单个行访问较慢，不没有可用的任何批处理游标。  
  
 服务器端游标是插入、 更新或删除记录时很有用。 对于服务器端游标，可以在同一连接上有多个活动语句。

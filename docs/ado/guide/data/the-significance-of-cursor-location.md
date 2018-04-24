---
title: 光标位置的重要性 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- server-side cursors [ADO]
- cursors [ADO], client-side
- client-side cursors [ADO]
- cursors [ADO], server-side
ms.assetid: 70ef5b1c-0459-41a1-b796-031f61a29a8a
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bb82081d69a03cd7ab9b7a42cf5ed7fead811657
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="the-significance-of-cursor-location"></a>光标位置的重要性
每个游标使用临时资源来保存其数据。 这些资源可以是内存、 磁盘页面文件、 临时磁盘文件或甚至临时存储在数据库中。 游标被称为*客户端*光标时这些资源都位于客户端计算机上。 游标被称为*服务器端*时这些资源位于服务器上的光标。  
  
## <a name="client-side-cursors"></a>客户端游标  
 在 ADO，对于客户端游标通过使用调用**adUseClient CursorLocationEnum。** 与非键集客户端游标，服务器发送到客户端计算机在网络设置整个结果。 客户端计算机提供，并管理通过游标和结果集所需的临时资源。 客户端应用程序可以浏览整个结果集以确定所需的行。  
  
 如果它们包括行过多，静态和键集驱动的客户端游标可能将大量负载放置在工作站上。 所有游标库时生成与数千个行的游标的支持，设计用于提取此类大的行集的应用程序可能会都很差。 有例外情况，这是当然的。 对于某些应用程序，可能完全适合大型的客户端游标和性能可能不会出现问题。  
  
 客户端游标的一个明显的好处是快速响应。 结果集已下载到客户端计算机后，浏览访问的行是非常快。 你的应用程序是通常与客户端游标可缩放的因为光标的资源要求放置在每个单独的客户端，而不在服务器上。  
  
## <a name="server-side-cursors"></a>服务器端游标  
 在 ADO，对于服务器端游标通过使用调用**adUseServer CursorLocationEnum。** 与服务器端游标，服务器将管理使用提供的服务器计算机的资源的结果集中。 服务器端游标通过网络返回请求的数据。 此类型的游标有时可以提供更好的性能比客户端游标，尤其是在其中过多的网络流量是问题的情况下。  
  
 但是，务必点的服务器端游标已-至少暂时-对于每个活动的客户端消耗宝贵的服务器资源。 你必须相应地规划以确保你的服务器硬件能够管理的所有服务器端游标的活动客户端请求。 此外，服务器端游标可能会很慢因为它提供仅单个行的访问权限-不没有可用的任何批处理光标。  
  
 服务器端游标时都很有用插入、 更新或删除记录。 使用服务器端游标时，你可以对相同的连接的多个活动语句。

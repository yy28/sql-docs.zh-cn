---
title: 标准数据库访问体系结构 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a9d41800-9068-4b76-895a-32b2853692dd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 99e0a0eee2636a04d182076bb580b1ccf8069921
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="standard-database-access-architectures"></a>标准数据库访问体系结构
在查看一节中所述的数据库访问组件，事实证明该这两个孩子-编程接口和数据流式传输协议 — 非常适合进行标准化。 其他两个组件-IPC 机制和网络协议 — 不仅驻留在太低级别，但两个类型都高度依赖于网络和操作系统。 没有第三个方法也-网关-为标准化提供可能的匹配项。  
  
 本部分包含以下主题。  
  
-   [标准编程接口](../../odbc/reference/standard-programming-interface.md)  
  
-   [标准数据流协议](../../odbc/reference/standard-data-stream-protocol.md)  
  
-   [标准网关](../../odbc/reference/standard-gateway.md)

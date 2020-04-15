---
title: 标准数据库访问体系结构 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a9d41800-9068-4b76-895a-32b2853692dd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6e78202eff69e6b30dc1e97d80f464dad75bb201
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280030"
---
# <a name="standard-database-access-architectures"></a>标准数据库访问体系结构
在查看上一节中描述的数据库访问组件时，发现其中两个组件（编程接口和数据流协议）是标准化的良好候选者。 其他两个组件 - IPC 机制和网络协议 - 不仅驻留在太低的水平，但它们都高度依赖于网络和操作系统。 还有第三种方法 - 网关 - 为标准化提供了可能性。  
  
 本部分包含以下主题。  
  
-   [标准编程接口](../../odbc/reference/standard-programming-interface.md)  
  
-   [标准数据流协议](../../odbc/reference/standard-data-stream-protocol.md)  
  
-   [标准网关](../../odbc/reference/standard-gateway.md)

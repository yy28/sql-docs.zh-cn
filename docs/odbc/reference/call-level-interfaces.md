---
title: 呼叫级接口 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], CLI
- CLI [ODBC], using CLI
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], CLI
- call-level interface [ODBC], using call-level interface
ms.assetid: 42257bb6-0bf1-4533-a4ef-4a6dd2aecb18
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4288a278f745d533c92d3d45892753ef1a74c2b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306538"
---
# <a name="call-level-interfaces"></a>调用级别接口
将 SQL 语句发送到 DBMS 的最后一种技术是通过调用级接口 （CLI）。 调用级接口提供可由应用程序调用的 DBMS 函数库。 因此，调用级接口不是试图将 SQL 与其他编程语言混合，而是类似于大多数程序员习惯使用的常规库，如 C 中的字符串、I/O 或数学库。 请注意，支持嵌入式 SQL 的 DBMS 已经具有调用级接口，该调用由预编译器生成。 但是，这些呼叫没有记录，如有更改，恕不另行通知。  
  
 调用级接口通常用于客户端/服务器体系结构，其中应用程序（客户端）驻留在一台计算机上，DBMS（服务器）驻留在另一台计算机上。 应用程序在本地系统上调用 CLI 函数，这些调用通过网络发送到 DBMS 进行处理。  
  
 调用级接口类似于动态 SQL，因为 SQL 语句在运行时传递给 DBMS 进行处理，但它不同于整个嵌入式 SQL，因为没有嵌入 SQL 语句，也不需要预编译。  
  
 使用呼叫级接口通常涉及以下步骤：  
  
1.  应用程序调用 CLI 函数以连接到 DBMS。  
  
2.  应用程序生成 SQL 语句并将其放在缓冲区中。 然后，它调用一个或多个 CLI 函数将语句发送到 DBMS 以进行准备和执行。  
  
3.  如果语句是 SELECT 语句，则应用程序调用 CLI 函数以在应用程序缓冲区中返回结果。 通常，此函数一次返回一行或一列数据。  
  
4.  应用程序调用 CLI 函数以断开与 DBMS 的连接。

---
title: 调用级接口 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], CLI
- CLI [ODBC], using CLI
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], CLI
- call-level interface [ODBC], using call-level interface
ms.assetid: 42257bb6-0bf1-4533-a4ef-4a6dd2aecb18
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6094e97d73dc11ec4c6507b6d5018353e2e345e2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32907472"
---
# <a name="call-level-interfaces"></a>调用级接口
将 SQL 语句发送到 DBMS 的最后一个方法是通过调用级界面 (CLI)。 调用级接口提供的应用程序可以调用它的 DBMS 函数的库。 因此，而不是尝试与另一种编程语言的混合 SQL，则调用级接口是类似于大多数程序员来说已经习惯于使用，如字符串、 I/O 或在 c。 请注意该 Dbms 支持嵌入式的 SQL 的数学库例程库已调用级接口，对其调用都由预编译器。 但是，这些调用是未记录和使用者，恕不另行通知。  
  
 调用级接口通常用在客户端/服务器体系结构，在其中应用程序 （客户端） 位于一台计算机上，DBMS （服务器） 驻留在另一台计算机上。 在应用程序在本地系统上，调用 CLI 函数和这些调用会跨网络发送到 DBMS 以进行处理。  
  
 调用级接口非常相似动态 sql，SQL 语句被传送到 DBMS，以处理在运行时，但它不同于嵌入式 SQL 作为一个整体： 有没有嵌入的 SQL 语句并且没有预编译器是必需的。  
  
 使用调用级接口通常涉及以下步骤：  
  
1.  应用程序调用一个 CLI 函数来连接到 DBMS。  
  
2.  应用程序生成的 SQL 语句，并将其放在缓冲区中。 然后，它将调用一个或多个要将声明发送到为准备和执行 DBMS 的 CLI 函数。  
  
3.  如果语句是 SELECT 语句，应用程序将调用一个 CLI 函数来在应用程序缓冲区中返回结果。 通常情况下，此函数返回一行或一列数据一次。  
  
4.  应用程序调用一个 CLI 函数来断开 DBMS。

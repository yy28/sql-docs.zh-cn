---
title: 调用级接口 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6c37084ad91a931c4479ecf826c5cb554765412
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135665"
---
# <a name="call-level-interfaces"></a>调用级别接口
向 DBMS 发送 SQL 语句的最后一种方法是通过调用级别接口（CLI）。 调用级别接口提供可由应用程序调用的 DBMS 函数库。 因此，调用级别接口并不是尝试将 SQL 与另一种编程语言混合使用，而是类似于大多数程序员习惯使用的例程库，如 C 中的字符串、i/o 或数学库。请注意，支持嵌入的 SQL 的 Dbms 已经具有调用级别接口，即对预编译器生成的调用。 但是，这些调用未记录，如有更改，恕不另行通知。  
  
 调用级别接口通常用于客户端/服务器体系结构，在该体系结构中，应用程序（客户端）驻留在一台计算机上，DBMS （服务器）驻留在另一台计算机上。 应用程序在本地系统上调用 CLI 函数，这些调用通过网络发送到 DBMS 进行处理。  
  
 调用级别接口类似于动态 SQL，因为 SQL 语句在运行时会传递给 DBMS 以进行处理，但它不同于嵌入的 SQL 作为一个整体，因为没有嵌入的 SQL 语句，也不需要预编译器。  
  
 使用调用级别接口通常涉及以下步骤：  
  
1.  应用程序调用 CLI 函数连接到 DBMS。  
  
2.  应用程序将生成一个 SQL 语句，并将其放入缓冲区。 然后，它调用一个或多个 CLI 函数将语句发送到 DBMS，以便进行准备和执行。  
  
3.  如果语句是 SELECT 语句，则应用程序将调用 CLI 函数以返回应用程序缓冲区中的结果。 通常，此函数一次返回一行或一列数据。  
  
4.  应用程序调用 CLI 函数以便与 DBMS 断开连接。

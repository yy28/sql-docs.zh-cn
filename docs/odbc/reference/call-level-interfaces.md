---
title: 调用级别接口 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 99ec2d9a1995502a4bfd96dad02157ccc6574f6c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735003"
---
# <a name="call-level-interfaces"></a>调用级别接口
将 SQL 语句发送到 DBMS 的最终方法是通过调用级别接口 (CLI)。 调用级别接口提供了可以在应用程序调用的 DBMS 函数库。 因此，而不是尝试与另一种编程语言混合 SQL，则调用级别接口是类似于大多数编程人员所习惯使用，如字符串、 I/O 或 c。 请注意该 Dbms 支持的嵌入式的 SQL 中的数学库的日常库已调用级别接口，通过使用预编译器生成的调用。 但是，这些调用是未记录以及可能会有所更改，恕不另行通知。  
  
 调用级别接口通常用在客户端/服务器体系结构，在其中应用程序 （客户端） 驻留在一台计算机上，DBMS （服务器） 驻留在另一台计算机上。 在应用程序在本地系统上调用 CLI 函数和这些调用通过网络发送到 DBMS 进行处理。  
  
 调用级别接口相当于动态 SQL，SQL 语句被传送到 DBMS，以处理在运行时，但它不同于嵌入式 SQL 作为一个整体，没有嵌入的 SQL 语句，并且不使用预编译器需要。  
  
 使用调用级别接口通常涉及以下步骤：  
  
1.  应用程序调用一个 CLI 函数来连接到 DBMS。  
  
2.  应用程序生成的 SQL 语句，并将其放入一个缓冲区。 然后，它将调用一个或多个 CLI 函数以将语句发送到的准备和执行 DBMS。  
  
3.  如果语句是 SELECT 语句，该应用程序将调用一个 CLI 函数来在应用程序缓冲区中返回的结果。 通常情况下，此函数返回一行或一列数据一次。  
  
4.  应用程序调用一个 CLI 函数来断开与 DBMS 的连接。

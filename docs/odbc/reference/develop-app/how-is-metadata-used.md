---
title: 如何使用元数据？ | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 70fb976c-9342-4edd-b066-1140696fd0fa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3604e9f3bd47a10ae1a6e5ec401b198675c2d3e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149290"
---
# <a name="how-is-metadata-used"></a>如何使用元数据？
应用程序需要大多数结果集操作的元数据。 例如，应用程序使用某列的数据类型来确定要将哪一种变量绑定到该列； 它使用字符列的字节的长度来确定它需要显示该列中的数据的空间量。 应用程序确定列的元数据的方式取决于应用程序的类型。  
  
 垂直应用程序使用的预定义的表，并执行对这些表的预定义的操作。 由于此类应用程序的结果集元数据定义应用程序甚至在编写和应用程序开发人员控制之前，它可以是硬编码到应用程序。 例如，如果在数据源中将顺序 ID 列定义为 4 字节整数，则应用程序可以始终将 4 字节整数绑定到该列。 如果元数据在应用程序中为硬编码，则对应用程序所用的表进行更改通常意味着要对应用程序代码进行更改。 这是很少是问题，因为此类更改通常会应用的应用程序的新版本的一部分。  
  
 垂直应用程序，如自定义应用程序通常使用预定义的表并执行对这些表的预定义的操作。 例如，可能会编写应用程序将在三个不同的数据源; 之间的数据传输要传输的数据通常是编写的应用程序是已知的。 因此，自定义应用程序也往往具有硬编码的元数据。  
  
 泛型应用程序，尤其是那些以支持即席查询，几乎不知道他们创建的结果集的元数据。 因此，它们必须在使用的函数的运行时发现元数据**SQLNumResultCols**， **SQLDescribeCol**，并**SQLColAttribute**，描述了这些下一节[SQLDescribeCol 和 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)。  
  
 所有应用程序，而不考虑其类型，可以硬编码为目录函数返回的结果集的元数据。 此手册的参考部分中定义这些结果集。

---
title: 数据长度、 缓冲区长度和截断 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- data length [ODBC]
- truncating data [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 2825c6e7-b9ff-42fe-84fc-7fb39728ac5d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ed2e5ca1fdaba97dde64329c5e8e1b692f43158
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267749"
---
# <a name="data-length-buffer-length-and-truncation"></a>数据长度、缓冲区长度和截断
*数据长度*是数据的字节长度，因为它将存储在应用程序的数据缓冲区，不作为数据源中存储。 这一区别很重要，因为数据通常存储在比数据源中的数据缓冲区中的不同类型。 因此对于发送到数据源的数据，这是前转换为数据源的类型的数据的字节长度。 正在从数据源检索到的数据，这是数据的字节长度后转换到数据缓冲区的类型和之前完成的任何截断。  
  
 对于固定长度的数据，如整数或日期结构的数据的字节长度始终是数据类型的大小。 一般情况下，应用程序分配的数据缓冲区，则数据类型的大小。 如果应用程序分配一个较小的缓冲区，则后果是未定义，因为驱动程序假定数据缓冲区的大小的数据类型并且不会截断数据而无法放入一个较小的缓冲区。 如果应用程序分配较大的缓冲区，则永远不会使用额外的空间。  
  
 对于可变长度数据，如字符或二进制数据，务必识别数据的字节长度是单独的通常是不同的缓冲区的字节长度。 以下两个长度的关系中所述[缓冲区](../../../odbc/reference/develop-app/buffers.md)部分。 如果数据的字节长度大于缓冲区的字节长度，驱动程序将截断到缓冲区的字节长度提取的数据，并返回 SQL_SUCCESS_WITH_INFO 具有 SQLSTATE 01004 （数据被截断）。 但是，返回的字节长度为未截断的数据的长度。  
  
 例如，假设应用程序分配 50 个字节的二进制数据缓冲区。 如果驱动程序具有 10 个字节的二进制数据返回，则在缓冲区中返回这些 10 个字节。 数据的字节长度为 10，并且缓冲区的字节长度为 50。 如果驱动程序具有 60 个字节的二进制数据返回，它将截断到 50 个字节的数据，在缓冲区中，将返回这些字节并返回 SQL_SUCCESS_WITH_INFO。 数据的字节长度为 60 （之前截断长度） 和缓冲区的字节长度仍为 50。  
  
 为每个将被截断的列创建的诊断记录。 由于需要时间来创建这些记录的驱动程序和应用程序来处理它们，截断会降低性能。 通常情况下，应用程序可以虽然这可能无法使用 long 数据时通过分配足够大，缓冲区中避免此问题。 当发生数据截断时，应用程序可以有时分配较大的缓冲区并重新提取数据;这不是在所有情况下，则返回 true。 如果在获取通过调用数据时发生截断**SQLGetData**，无需调用应用程序**SQLGetData**已返回的数据; 有关详细信息，请参阅[入门长整型数据](../../../odbc/reference/develop-app/getting-long-data.md)。

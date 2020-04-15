---
title: 数据长度、缓冲区长度和截断 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2e7b8d1e60cd83594509c2ab5cbc24e04546eca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305223"
---
# <a name="data-length-buffer-length-and-truncation"></a>数据长度、缓冲区长度和截断
*数据长度*是数据存储在应用程序的数据缓冲区中的字节长度，而不是存储在数据源中的字节长度。 这种区别很重要，因为数据通常存储在数据缓冲区中的不同类型，而不是数据存储中。 因此，对于发送到数据源的数据，这是数据转换为数据源类型之前的字节长度。 对于从数据源检索的数据，这是转换为数据缓冲区类型后以及完成任何截断之前数据的字节长度。  
  
 对于固定长度数据（如整数或日期结构），数据的字节长度始终为数据类型的大小。 通常，应用程序分配的数据缓冲区的大小是数据类型的大小。 如果应用程序分配了较小的缓冲区，则后果未定义，因为驱动程序假定数据缓冲区是数据类型的大小，并且不会截截数据以容纳较小的缓冲区。 如果应用程序分配了较大的缓冲区，则永远不会使用额外的空间。  
  
 对于可变长度数据（如字符或二进制数据），请务必认识到数据的字节长度与缓冲区的字节长度是分开的，并且通常与缓冲区的字节长度不同。 这两个长度的关系在[缓冲区](../../../odbc/reference/develop-app/buffers.md)部分中描述。 如果数据的字节长度大于缓冲区的字节长度，驱动程序会截断提取的数据到缓冲区的字节长度，并在 SQLSTATE 01004（数据截断）SQL_SUCCESS_WITH_INFO返回。 但是，返回的字节长度是未压缩数据的长度。  
  
 例如，假设应用程序为二进制数据缓冲区分配 50 个字节。 如果驱动程序要返回 10 个字节的二进制数据，它将返回缓冲区中的 10 个字节。 数据的字节长度为 10，缓冲区的字节长度为 50。 如果驱动程序要返回 60 个字节的二进制数据，它将数据截截为 50 字节，返回缓冲区中的这些字节，并返回SQL_SUCCESS_WITH_INFO。 数据的字节长度为 60（截断前的长度），缓冲区的字节长度仍为 50。  
  
 为截断的每个列创建诊断记录。 由于驱动程序创建这些记录和应用程序处理这些记录需要时间，因此截断可能会降低性能。 通常，应用程序可以通过分配足够大的缓冲区来避免此问题，尽管在使用长数据时可能无法避免此问题。 当发生数据截断时，应用程序有时会分配更大的缓冲区并重新提取数据;因此，应用程序可能会重新分配数据。并非在所有情况下都如此。 如果在通过调用**SQLGetData**获取数据时发生截断，则应用程序无需为已返回的数据调用**SQLGetData;** 有关详细信息，请参阅[获取长数据](../../../odbc/reference/develop-app/getting-long-data.md)。

---
title: "数据长度、 缓冲区长度和截断 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data buffers [ODBC], length
- data length [ODBC]
- truncating data [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 2825c6e7-b9ff-42fe-84fc-7fb39728ac5d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 616dc403fdd23f3233bde4a5db19dd58b6d94cf1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="data-length-buffer-length-and-truncation"></a>数据长度、 缓冲区长度和截断
*数据长度*的字节长度的数据为它的行将存储在应用程序的数据缓冲区，不是存储在数据源。 这一区别很重要，因为数据通常存储在数据源中比数据缓冲区中的不同类型。 对于正在发送到数据源的数据，这就是数据，再到数据源的类型转换的字节长度。 正在从数据源检索数据，这是数据的字节长度后转换到的数据缓冲区的类型和完成任何截断之前。  
  
 对于固定长度的数据，如整数或日期结构的字节长度的数据始终是数据类型的大小。 一般情况下，应用程序分配的数据缓冲区，则数据类型的大小。 如果应用程序分配一个较小的缓冲区，将出现哪些后果是不确定的因为该驱动程序假定数据缓冲区是数据类型的大小，并且不会不会截断数据无法放入较小的缓冲区。 如果应用程序分配较大的缓冲区，则永远不会使用额外的空间。  
  
 长度可变的数据，如字符或二进制数据，务必认识到的字节长度的数据是分开和通常不同于缓冲区的字节长度。 中介绍了以下两个长度的关系[缓冲区](../../../odbc/reference/develop-app/buffers.md)部分。 如果大于缓冲区的字节长度的字节长度的数据，该驱动程序将截断到缓冲区的字节长度的提取的数据，并返回 SQL_SUCCESS_WITH_INFO sqlstate 01004 （数据截断）。 但是，返回的字节长度为未截断的数据的长度。  
  
 例如，假设应用程序分配 50 个字节的二进制数据缓冲区。 如果该驱动程序有 10 个字节的二进制数据返回，则在缓冲区中返回这些 10 个字节。 数据的字节长度为 10，且缓冲区的字节长度为 50。 如果该驱动程序有 60 字节的二进制数据返回，它将截断到 50 个字节的数据，返回缓冲区中的这些字节并返回 SQL_SUCCESS_WITH_INFO。 数据的字节长度为 60 （之前截断的长度），且缓冲区的字节长度仍为 50。  
  
 为将被截断每一列中创建诊断记录。 因为它所需时间，为要创建这些记录的驱动程序和应用程序处理它们，截断会降低性能。 通常情况下，应用程序可以避免此问题通过分配足够大的缓冲区，但这可能不可能使用长数据时。 数据截断时，应用程序可以有时分配较大的缓冲区并重新提取数据;不能在所有情况下同时运行。 如果在使用调用获取数据时发生的截断**SQLGetData**，应用程序无需调用**SQLGetData**已返回的数据; 有关详细信息，请参阅[入门Long 数据](../../../odbc/reference/develop-app/getting-long-data.md)。


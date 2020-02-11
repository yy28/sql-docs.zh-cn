---
title: 数据长度、缓冲区长度和截断 |Microsoft Docs
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
ms.openlocfilehash: 8586157237db1158587e3c39f1320b78d8251fb5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081471"
---
# <a name="data-length-buffer-length-and-truncation"></a>数据长度、缓冲区长度和截断
*数据长度*是数据在应用程序数据缓冲区中存储的字节长度，而不是存储在数据源中。 这一区别很重要，因为数据通常存储在数据缓冲区中的不同类型中，而不是数据源中的不同类型。 因此，对于发送到数据源的数据，这是数据在转换为数据源的类型之前的字节长度。 对于从数据源检索的数据，这是在转换到数据缓冲区类型之后、执行任何截断之前的数据字节长度。  
  
 对于固定长度的数据（如整数或日期结构），数据的字节长度始终为数据类型的大小。 通常，应用程序会分配大小为数据类型的数据缓冲区。 如果应用程序分配的缓冲区较小，则结果是不确定的，因为驱动程序假定数据缓冲区是数据类型的大小，不会截断数据以适应较小的缓冲区。 如果应用程序分配更大的缓冲区，则永远不会使用额外的空间。  
  
 对于长度可变的数据（如字符数据或二进制数据），请务必认识到，数据的字节长度不同于并且通常不同于缓冲区的字节长度。 "[缓冲区](../../../odbc/reference/develop-app/buffers.md)" 部分介绍了这两个长度之间的关系。 如果数据的字节长度大于缓冲区的字节长度，则驱动程序将提取的数据截断到缓冲区的字节长度，并返回 SQL_SUCCESS_WITH_INFO SQLSTATE 01004 （数据已截断）。 但是，返回的字节长度为未截断数据的长度。  
  
 例如，假设某个应用程序为二进制数据缓冲区分配了50字节。 如果驱动程序有10个字节的二进制数据需要返回，则它会在缓冲区中返回这10个字节。 数据的字节长度为10，缓冲区的字节长度为50。 如果驱动程序有60字节的二进制数据要返回，它会将数据截断到50字节，在缓冲区中返回这些字节，并返回 SQL_SUCCESS_WITH_INFO。 数据的字节长度为60（截断之前的长度），缓冲区的字节长度仍为50。  
  
 将为截断的每个列创建一个诊断记录。 由于驱动程序需要花费时间来创建这些记录，并使应用程序处理这些记录，因此截断会降低性能。 通常情况下，应用程序可以通过分配足够大的缓冲区来避免此问题，不过在使用长数据时可能不会这样做。 发生数据截断时，应用程序有时可以分配更大的缓冲区并重新提取数据;这在所有情况下都不是这样。 如果在通过调用**SQLGetData**获取数据时发生截断，则应用程序不需要为已返回的数据调用**SQLGetData** ;有关详细信息，请参阅[获取长数据](../../../odbc/reference/develop-app/getting-long-data.md)。

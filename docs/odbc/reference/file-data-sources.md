---
title: 文件数据源 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], file
- file data sources [ODBC]
ms.assetid: db245c80-981a-4638-bd03-69d04bc67af0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 733b958ee883aa62034b4acc1eec67100b35a74d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62628450"
---
# <a name="file-data-sources"></a>文件数据源
*文件数据源*存储在文件中并可用于单个用户重复使用或在多个用户之间共享的连接信息。 当使用文件数据源时，驱动程序管理器可以与使用.dsn 文件中的信息的数据源的连接。 可以像任何其他文件一样处理此文件。 文件数据源没有数据源名称，如计算机数据源，不会和未注册到任何一个用户或计算机。  
  
 文件数据源简化了连接过程中，因为.dsn 文件包含将不得不对的调用生成的连接字符串**SQLDriverConnect**函数。 .Dsn 文件的另一个优点是使多台计算机可以使用相同的数据源，只要它们具有相应的驱动程序，它可以被复制到任何计算机。 应用程序还可以共享文件数据源。 可以放置在网络上并同时使用多个应用程序可共享的文件数据源。  
  
 .Dsn 文件也可以是共享。 非共享.dsn 文件驻留在一台计算机上，指向计算机数据源。 非共享的文件数据源存在主要是为了允许计算机数据源轻松转换为文件数据源，以便应用程序可以设计为仅使用文件数据源。 驱动程序管理器中的非共享的文件数据源发送的信息，它会连接根据需要为.dsn 文件所指向的计算机数据源。  
  
 有关文件的数据源的详细信息，请参阅[连接使用的文件数据源](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)，或[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)函数说明。

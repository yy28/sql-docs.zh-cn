---
title: 文件数据源 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0661aa424a7a118b8b12f4bf8433987ff83bd788
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306648"
---
# <a name="file-data-sources"></a>文件数据源
*文件数据源*存储在文件中，并允许单个用户重复使用连接信息或在多个用户之间共享。 使用文件数据源时，驱动程序管理器使用 .dsn 文件中的信息与数据源建立连接。 此文件可以像任何其他文件一样作。 文件数据源没有数据源名称，计算机数据源也是如此，并且不注册给任何一个用户或计算机。  
  
 文件数据源简化了连接过程，因为 .dsn 文件包含连接字符串，否则必须为调用**SQLDriverConnect**函数生成连接字符串。 .dsn 文件的另一个优点是它可以复制到任何计算机，因此只要安装了适当的驱动程序，许多计算机就可以使用相同的数据源。 应用程序也可以共享文件数据源。 可共享的文件数据源可以放置在网络上，并由多个应用程序同时使用。  
  
 .dsn 文件也可以不可共享。 不可共享的 .dsn 文件驻留在一台计算机上，并指向计算机数据源。 存在不可共享的文件数据源主要是为了允许将计算机数据源轻松转换为文件数据源，以便应用程序可以设计为仅处理文件数据源。 当驱动程序管理器在不可共享的文件数据源中发送信息时，它将根据需要连接到 .dsn 文件指向的计算机数据源。  
  
 有关文件数据源的详细信息，请参阅[使用文件数据源进行连接](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)或[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)函数描述。

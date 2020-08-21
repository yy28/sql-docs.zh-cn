---
title: 与 SQLDriverConnect 连接 |Microsoft Docs
description: SQLDriverConnect 通过 SQLConnect 提供附加连接功能，其中包括提示用户详细信息的选项。
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- SQLDriverConnect function [ODBC], connecting
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: e46e959f-d3c5-4ddb-810a-107bfcb83fd2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78186e903405aa1b59cfac185e62646dbda6e77a
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2020
ms.locfileid: "88746167"
---
# <a name="connecting-with-sqldriverconnect"></a>使用 SQLDriverConnect 连接

**SQLDriverConnect** 用于连接到使用连接字符串的数据源。 对于以下情况，将使用**SQLDriverConnect**而不是**SQLConnect** ：  
  
- 使用连接字符串建立连接，该字符串包含数据源名称、一个或多个用户 Id、一个或多个密码，以及数据源所需的其他信息。  
  
- 使用部分连接字符串建立连接，或者不使用其他信息建立连接;在这种情况下，驱动程序管理器和驱动程序可以提示用户输入连接信息。  
  
- 建立与系统信息中未定义的数据源的连接。 如果应用程序提供部分连接字符串，则驱动程序可以提示用户输入连接信息。  
  
- 使用从 .dsn 文件中的信息构造的连接字符串建立与数据源的连接。  
  
建立连接后， **SQLDriverConnect** 将返回完成的连接字符串。 应用程序可将此字符串用于后续连接请求。

本部分包含以下主题。  
  
- [特定于驱动程序的连接信息](driver-specific-connection-information.md)  
  
- [提示用户输入连接信息](prompting-the-user-for-connection-information.md)  
  
- [使用文件数据源连接](connecting-using-file-data-sources.md)  
  
- [直接连接到驱动程序](connecting-directly-to-drivers.md)

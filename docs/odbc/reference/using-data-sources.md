---
title: 使用数据源 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], about data sources
ms.assetid: d5550619-22b2-4b16-bd08-fbabb6554c40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c898cb5cd8c9998d9126ec468a2b43587e2e279a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62714115"
---
# <a name="using-data-sources"></a>使用数据源
创建数据源通常是由最终用户或技术人员与程序调用*ODBC 管理器*。 ODBC 管理器会提示使用驱动程序的用户，然后调用该驱动程序。 该驱动程序显示一个对话框，请求连接到数据源所需的信息。 用户输入信息后，该驱动程序会将其存储在系统上。  
  
 更高版本，该应用程序调用驱动程序管理器，并将其传递计算机数据源的名称或包含文件数据源的文件的路径。 传递计算机数据源名称，驱动程序管理器会搜索系统以找到数据源使用的驱动程序。 然后加载该驱动程序，并向其传递的数据源名称。 驱动程序使用的数据源名称来找到它需要连接到数据源的信息。 最后，它连接到数据源，通常提示用户输入用户 ID 和密码，这通常不会存储。  
  
 当传递文件数据源时，驱动程序管理器打开的文件并加载指定的驱动程序。 如果文件还包含连接字符串，它将此传递到驱动程序。 在连接字符串中使用的信息，该驱动程序连接到数据源。 如果不传递了任何连接字符串，该驱动程序通常会提示用户输入所需的信息。

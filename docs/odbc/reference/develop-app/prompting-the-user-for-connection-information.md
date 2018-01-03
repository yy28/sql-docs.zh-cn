---
title: "提示用户输入连接信息 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connecting to data source [ODBC], SqlConnect
- connecting to driver [ODBC], prompting user for information
- connecting to driver [ODBC], SQLConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLConnect function [ODBC], prompting user for connection information
- connecting to data source [ODBC], prompting user for information
- prompting user for connection information [ODBC]
- SQLDriverConnect function [ODBC], prompting user for connection information
ms.assetid: da98e9b9-a4ac-4a9d-bae6-e9252b1fe1e5
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f72a196447399b6df74de8d46fa1eee572910fac
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="prompting-the-user-for-connection-information"></a>提示用户输入连接信息
如果应用程序使用**SQLConnect**并需要提示用户输入的任何连接信息，如用户名和密码，必须这样做本身。 虽然这使应用程序控制其"外观和感觉"，它可能会强制应用程序以包含特定于驱动程序的代码。 当应用程序需要提示用户提供特定于驱动程序的连接信息时，将发生这种情况。 这会带来一个不可能的情况，对于泛型应用程序，用于处理任意和所有驱动程序，包括驱动程序时写入的应用程序不存在。  
  
 **SQLDriverConnect**可以提示用户输入连接信息。 例如，前面所述的自定义程序可以将以下连接字符串到**SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 该驱动程序可能然后显示一个对话框，提示输入用户 Id 和密码，类似于下图。  
  
 ![输入用户 Id 和密码提示对话框](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 该驱动程序可提示输入连接信息是对泛型和垂直应用程序特别有用。 这些应用程序不应包含特定于驱动程序的信息，并具有所需的信息的驱动程序提示符保留该信息从应用程序。 显示为前面两个示例。 当应用程序传递到驱动程序的数据源名称时，应用程序不包含任何特定于驱动程序的信息，因此不与特定的驱动程序关联。 当应用程序传递到驱动程序的完整连接字符串时，它已绑定到的驱动程序无法解释该字符串。  
  
 通用应用程序可能会进一步采取此一个步骤，并甚至不指定数据源。 当**SQLDriverConnect**接收有空连接字符串，该驱动程序管理器将显示以下对话框。  
  
 ![选择数据源对话框中](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 用户选择数据源后，驱动程序管理器将构造一个连接字符串，指定该数据源，并将其传递到该驱动程序。 然后，该驱动程序可以提示用户输入它需要的任何其他信息。  
  
 由控制在其下驱动程序会提示用户的条件*DriverCompletion*标志; 有用于始终给出提示，如有必要，提示或永远不会要求的选项。 此标志的完整说明，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函数说明。

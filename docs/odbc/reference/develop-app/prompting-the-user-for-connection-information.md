---
title: 提示用户输入连接信息 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58df84bf96306a2cfbc0567a3d5f6cb13514a06e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47805565"
---
# <a name="prompting-the-user-for-connection-information"></a>提示用户输入连接信息
如果应用程序使用**SQLConnect**并需要提示用户输入的任何连接信息，如用户名和密码，它必须执行此操作本身。 尽管这样，应用程序来控制其"外观"，它可能会强制应用程序以包含特定于驱动程序的代码。 当应用程序需要提示用户提供特定于驱动程序的连接信息时，将发生这种情况。 这会带来的不可能的情况下，对于通用应用程序，用于处理所有驱动程序，包括编写的应用程序时不存在的驱动程序。  
  
 **SQLDriverConnect**可以提示用户输入连接信息。 例如，前面所述的自定义程序可以将传递到下面的连接字符串**SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 然后，该驱动程序可能显示一个对话框，提示输入用户 Id 和密码，类似于下图。  
  
 ![提示输入用户 Id 和密码的对话框](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 该驱动程序可以提示输入连接信息是对泛型和垂直应用程序特别有用。 这些应用程序不应包含特定于驱动程序的信息，并具有所需的信息的驱动程序提示保持该应用程序中的信息。 这是通过前面的两个示例所示。 当应用程序传递到驱动程序数据源名称时，该应用程序不包含任何特定于驱动程序的信息，并因此是为未绑定到的特定驱动程序。 当应用程序传递到驱动程序的完整连接字符串时，它是为绑定到该字符串无法解释的驱动程序。  
  
 通用应用程序可能会采取进一步的此步骤，并甚至不指定数据源。 当**SQLDriverConnect**收到空连接字符串，该驱动程序管理器显示以下对话框。  
  
 ![选择数据源对话框](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 在用户选择数据源后，驱动程序管理器将构造一个连接字符串，指定该数据源，并将其传递给驱动程序。 然后，驱动程序可以提示用户输入其所需的任何其他信息。  
  
 控制在其下该驱动程序会提示用户的条件*DriverCompletion*标志; 有始终提示，提示如有必要，或者永远不会提示的选项。 此标志的完整说明，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函数说明。

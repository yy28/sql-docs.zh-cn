---
title: 提示用户输入连接信息 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b0f120a1076f14f5e67d506e52a446e0a3d4713
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282080"
---
# <a name="prompting-the-user-for-connection-information"></a>提示用户输入连接信息
如果应用程序使用**SQLConnect，** 并且需要提示用户输入任何连接信息（如用户名和密码），则必须自行执行此操作。 虽然这允许应用程序控制其"外观"，但它可能会强制应用程序包含特定于驱动程序的代码。 当应用程序需要提示用户输入特定于驱动程序的连接信息时，将发生这种情况。 这给通用应用程序带来了一个不可能的情况，这些驱动程序旨在处理任何和所有驱动程序，包括编写应用程序时不存在的驱动程序。  
  
 **SQLDriverConnect**可以提示用户提供连接信息。 例如，前面提到的自定义程序可以将以下连接字符串传递给**SQLDriverConnect**：  
  
```  
DSN=XYZ Corp;  
```  
  
 然后，驱动程序可能会显示一个对话框，提示用户使用 I 和密码，类似于下图。  
  
 ![提示输入用户 ID 和密码的对话框](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 驱动程序可以提示连接信息对于通用和垂直应用程序特别有用。 这些应用程序不应包含特定于驱动程序的信息，并且让驱动程序提示它需要的信息会将该信息从应用程序中排除。 这由前两个示例显示。 当应用程序仅将数据源名称传递给驱动程序时，应用程序不包含任何特定于驱动程序的信息，因此不绑定到特定驱动程序。 当应用程序将完整的连接字符串传递给驱动程序时，它绑定到可以解释该字符串的驱动程序。  
  
 泛型应用程序可能会更进一步，甚至不会指定数据源。 当**SQLDriverConnect**收到空连接字符串时，驱动程序管理器将显示以下对话框。  
  
 ![“选择数据源”对话框](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 用户选择数据源后，驱动程序管理器将构造一个连接字符串，指定该数据源并将其传递给驱动程序。 然后，驱动程序可以提示用户提供所需的任何其他信息。  
  
 驱动程序提示用户的条件由*驱动程序完成*标志控制;有选项可以始终提示、在必要时提示或从不提示。 有关此标志的完整说明，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函数说明。

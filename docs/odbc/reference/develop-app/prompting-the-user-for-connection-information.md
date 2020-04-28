---
title: 提示用户提供连接信息 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282080"
---
# <a name="prompting-the-user-for-connection-information"></a>提示用户输入连接信息
如果应用程序使用**SQLConnect** ，并需要提示用户输入任何连接信息（例如用户名和密码），则它必须是其本身。 虽然这允许应用程序控制其 "外观"，但它可能会强制应用程序包含特定于驱动程序的代码。 当应用程序需要提示用户提供特定于驱动程序的连接信息时，会发生这种情况。 这对于一般应用程序而言是一种不可能的情况，设计用于处理任何和所有驱动程序，包括编写应用程序时不存在的驱动程序。  
  
 **SQLDriverConnect**可以提示用户输入连接信息。 例如，前面提到的自定义程序可以将以下连接字符串传递给**SQLDriverConnect**：  
  
```  
DSN=XYZ Corp;  
```  
  
 然后，驱动程序可能会显示一个对话框，提示输入用户 Id 和密码，如下图所示。  
  
 ![提示输入用户 ID 和密码的对话框](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 驱动程序可以提示连接信息对于一般和垂直应用程序特别有用。 这些应用程序不应包含特定于驱动程序的信息，并且让驱动程序提示其需要的信息会将信息保留在应用程序之外。 上面两个示例显示了这种情况。 当应用程序仅将数据源名称传递给驱动程序时，应用程序不包含任何特定于驱动程序的信息，因此不会绑定到特定驱动程序。 当应用程序将完整的连接字符串传递给驱动程序时，它将绑定到可能解释该字符串的驱动程序。  
  
 一般的应用程序可能会更进一步，甚至不指定数据源。 当**SQLDriverConnect**收到空的连接字符串时，驱动程序管理器将显示以下对话框。  
  
 ![“选择数据源”对话框](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 用户选择数据源之后，驱动程序管理器会构造一个连接字符串，指定该数据源并将其传递给驱动程序。 然后，该驱动程序可以提示用户输入所需的任何其他信息。  
  
 驱动程序提示用户的条件由*DriverCompletion*标志控制;有一些选项可供选择，如有必要，还可以提示或从不提示。 有关此标志的完整说明，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函数说明。

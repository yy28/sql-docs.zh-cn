---
title: 由 Oracle 的 ODBC 驱动程序返回的消息 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], error messages
ms.assetid: 150bde1d-adb6-4e77-90e9-4dc93499a746
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8bdaf4238bd220987364a77aaa1af837885c6e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298857"
---
# <a name="messages-returned-by-the-odbc-driver-for-oracle"></a>Oracle ODBC 驱动程序返回的消息
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 如果 Oracle 错误消息可用，则将在 [Microsoft]、[Oracle 的 ODBC 驱动程序]和 [Oracle] 标记之前返回该错误消息;否则，返回消息时没有 [Oracle] 标记，如以下示例所示：  
  
## <a name="oracle-error-message"></a>Oracle 错误消息：  
  
```  
[Microsoft][ODBC driver for Oracle][Oracle]ORA-nnnnn message-text  
```  
  
## <a name="odbc-driver-for-oracle-error-message"></a>Oracle 错误消息的 ODBC 驱动程序：  
  
```  
[Microsoft][ODBC driver for Oracle]  
```

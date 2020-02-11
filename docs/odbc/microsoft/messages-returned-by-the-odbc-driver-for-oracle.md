---
title: ODBC Driver for Oracle 返回的消息 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bb2fc54692a77441bb2516ad72c0c44951152f56
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68045177"
---
# <a name="messages-returned-by-the-odbc-driver-for-oracle"></a>Oracle ODBC 驱动程序返回的消息
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 如果有 Oracle 错误消息，则将返回该消息，其前面是 [Microsoft]、[用于 Oracle 的 ODBC 驱动程序] 和 [Oracle] 标记;否则，返回的消息不包含 [Oracle] 标记，如以下示例中所示：  
  
## <a name="oracle-error-message"></a>Oracle 错误消息：  
  
```  
[Microsoft][ODBC driver for Oracle][Oracle]ORA-nnnnn message-text  
```  
  
## <a name="odbc-driver-for-oracle-error-message"></a>用于 Oracle 的 ODBC 驱动程序错误消息：  
  
```  
[Microsoft][ODBC driver for Oracle]  
```

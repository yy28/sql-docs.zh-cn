---
title: 用于 Oracle 的 ODBC 驱动程序返回的消息 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 4425c814fb8814ec1ef7822d4642ccf6fcc0dd70
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47719665"
---
# <a name="messages-returned-by-the-odbc-driver-for-oracle"></a>Oracle ODBC 驱动程序返回的消息
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 如果有可用 Oracle 错误消息，它将返回前面的 [Microsoft] [适用于 Oracle 的 ODBC Driver] 和 [Oracle] 标记;否则，没有 [Oracle] 标记，如以下示例所示的情况下返回的消息：  
  
## <a name="oracle-error-message"></a>Oracle 错误消息：  
  
```  
[Microsoft][ODBC driver for Oracle][Oracle]ORA-nnnnn message-text  
```  
  
## <a name="odbc-driver-for-oracle-error-message"></a>Oracle 错误消息的 ODBC 驱动程序：  
  
```  
[Microsoft][ODBC driver for Oracle]  
```

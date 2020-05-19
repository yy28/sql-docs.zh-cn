---
title: 已记录无日志记录修改 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- logged vs. nonlogged modifications [SQL Server Native Client]
- columns [ODBC]
- ODBC data types, image columns
- nonlogged vs. logged modifications
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 20aa5b27-4a2c-46e7-8356-beb0eebf4b7e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3635fee71c92196cbc9408db1487e95da2b489ea
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718769"
---
# <a name="logged-vs-unlogged-modifications"></a>有日志记录的修改与无日志记录的修改
  应用程序可以请求 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驱动程序不记录**text**、 **ntext**和**image**修改。 但应慎用此选项。 它仅适用于**文本**、 **ntext**或**图像**数据不重要的情况，数据所有者愿意权衡恢复数据以提高性能的能力。  
  
 通过调用[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)并将*属性*参数设置为 SQL_SOPT_SS_ TEXTPTR_LOGGING 并将*将 valueptr*设置为 SQL_TL_ON 或 SQL_TL_OFF，可以控制**text**、 **ntext**和**image**修改的日志记录。  
  
## <a name="see-also"></a>另请参阅  
 [管理 Text 和 Image 列](managing-text-and-image-columns.md)  
  
  

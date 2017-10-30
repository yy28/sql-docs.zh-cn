---
title: "SQLError （Visual FoxPro ODBC 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLError function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8315ec16-1c22-447a-a577-39bd94f61070
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 46696509f9276ac4974604c931c4d77acbaae15b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError （Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序相关的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持： 完整  
  
 ODBC API 一致性： 核心级别  
  
 返回有关上一个错误的错误或状态信息。 驱动程序保持堆栈或可以为返回的错误的列表*hstmt*， *hdbc*，和*henv*自变量，具体取决于如何在调用**SQLError**进行。 每个语句后刷新错误队列。  
  
 下表描述了**SQLError**自变量和使用的驱动程序的返回值。  
  
|SQLError 自变量|返回值说明|  
|-----------------------|------------------------------|  
|*szSQLState*|表示错误 SQLSTATE 值。|  
|*pfNativeError*|一个非零值指示[Visual FoxPro ODBC 驱动程序本机错误信息](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)。 值为 0 指示由驱动程序检测到错误并将其映射到相应[ODBC 错误代码](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)。|  
|*szErrorMsg*|本机错误或 ODBC 错误文本。|  
|*pcbErrorMsg*|长度之标识符和消息文本的长度。|  
  
 有关驱动程序错误消息的详细信息，请参阅[错误消息概述](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md)。 有关此函数的详细信息，请参阅[SQLError](../../odbc/reference/syntax/sqlerror-function.md)中*ODBC 程序员参考*。


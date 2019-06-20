---
title: SQLError （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLError function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8315ec16-1c22-447a-a577-39bd94f61070
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3014c5c2af1a0ef8e5f485c790089e4807834446
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313282"
---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持：完全  
  
 ODBC API 一致性：核心级别  
  
 返回有关最后一个错误的错误或状态信息。 驱动程序保持堆栈或可返回的错误的列表*hstmt*， *hdbc*，并*henv*参数，具体取决于如何在调用**SQLError**进行。 每个语句后刷新错误队列。  
  
 下表描述了**SQLError**参数和返回值由驱动程序。  
  
|SQLError 参数|返回值说明|  
|-----------------------|------------------------------|  
|*szSQLState*|用于表示错误的 SQLSTATE 值。|  
|*pfNativeError*|一个非零值指示[Visual FoxPro ODBC 驱动程序本机错误消息](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)。 值为零表示由驱动程序检测到错误并将其映射到适当[ODBC 错误代码](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)。|  
|*szErrorMsg*|本机错误或 ODBC 错误文本。|  
|*pcbErrorMsg*|消息文本以及标识符的长度的长度。|  
  
 有关驱动程序错误消息的详细信息，请参阅[错误消息概述](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md)。 有关此函数的详细信息，请参阅[SQLError](../../odbc/reference/syntax/sqlerror-function.md)中*ODBC 程序员参考*。

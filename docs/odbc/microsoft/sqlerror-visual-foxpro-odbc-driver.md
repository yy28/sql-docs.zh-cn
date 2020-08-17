---
description: SQLError（Visual FoxPro ODBC 驱动程序）
title: SQLError (Visual FoxPro ODBC 驱动程序) |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09f901b72d292f962076bff2aa521c8214e8f0e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340253"
---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅 [ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：完全  
  
 ODBC API 一致性：核心级别  
  
 返回有关上一个错误的错误或状态信息。 驱动程序将维护一个堆栈或可为 *hstmt*、 *hdbc*和 *henv* 参数返回的错误列表，具体取决于对 **SQLError** 的调用的方式。 在每个语句后刷新错误队列。  
  
 下表描述了驱动程序使用的 **SQLError** 参数和返回值。  
  
|SQLError 参数|返回值说明|  
|-----------------------|------------------------------|  
|*szSQLState*|由错误表示的 SQLSTATE 的值。|  
|*pfNativeError*|非零值表示 [Visual FOXPRO ODBC 驱动程序本机错误消息](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)。 如果值为零，则表示该驱动程序检测到错误并映射到相应的 [ODBC 错误代码](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)。|  
|*szErrorMsg*|本机错误或 ODBC 错误的文本。|  
|*pcbErrorMsg*|消息文本的长度加上标识符的长度。|  
  
 有关驱动程序错误消息的详细信息，请参阅 [错误消息概述](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md)。 有关此函数的详细信息，请参阅*ODBC 程序员参考*中的[SQLError](../../odbc/reference/syntax/sqlerror-function.md) 。

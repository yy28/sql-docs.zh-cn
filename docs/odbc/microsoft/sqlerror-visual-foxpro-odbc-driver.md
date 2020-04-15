---
title: SQLError（可视化福克斯Pro ODBC驱动程序） |微软文档
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
ms.openlocfilehash: 0d1247217905187cfb2dbaca6d7b7b562d0175bd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298677"
---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 特定于驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 支持： 完整  
  
 ODBC API 一致性：核心级别  
  
 返回有关上次错误的错误或状态信息。 驱动程序维护一个堆栈或错误列表，这些错误可以返回*用于 hstmt、hdbc*和*henv*参数，具体取决于对**SQLError**的调用方式。 *hdbc* 在每个语句之后刷新错误队列。  
  
 下表描述了驱动程序使用的**SQLError**参数和返回值。  
  
|SQLError 参数|返回值描述|  
|-----------------------|------------------------------|  
|*szSQL国家*|由错误表示的 SQLSTATE 的值。|  
|*pfNativeError*|非零值表示可视[FoxPro ODBC 驱动程序本机错误消息](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)。 值为零表示驱动程序检测到错误并映射到相应的[ODBC 错误代码](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)。|  
|*什洛姆斯格*|本机错误或 ODBC 错误的文本。|  
|*多加错姆斯格*|消息文本的长度加上标识符的长度。|  
  
 有关驱动程序错误消息的详细信息，请参阅[错误消息概述](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md)。 有关此功能的详细信息，请参阅*ODBC 程序员参考*中的[SQLError。](../../odbc/reference/syntax/sqlerror-function.md)

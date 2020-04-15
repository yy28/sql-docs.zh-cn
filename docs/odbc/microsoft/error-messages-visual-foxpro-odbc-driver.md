---
title: 错误消息（可视化福克斯 Pro ODBC 驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], error messages
- SQLSTATE [ODBC]
- FoxPro ODBC driver [ODBC], error messages
ms.assetid: 58ea9734-4edf-44da-ba80-938aa7b340e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31f894e58da93fe6091dba306f8b765d14bac2cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286397"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>错误消息（Visual FoxPro ODBC 驱动程序）
发生错误时，Visual FoxPro 驱动程序返回以下信息：  
  
-   本机错误编号和错误消息文本  
  
-   SQLSTATE（ODBC 错误代码）和错误消息文本  
  
 您可以通过调用[SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)来访问此错误信息。  
  
## <a name="native-errors"></a>本机错误  
 对于数据源中发生的错误，Visual FoxPro 驱动程序返回本机错误编号和错误消息文本。 有关本机错误编号的列表，请参阅可视化[FoxPro ODBC 驱动程序本机错误消息](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)。  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE（ODBC 错误代码）  
 对于 Visual FoxPro 驱动程序检测到和返回的错误，驱动程序将返回的本机错误编号映射到相应的 SQLSTATE。 如果本机错误编号没有要映射到的 ODBC 错误代码，则 Visual FoxPro 驱动程序将返回 SQLSTATE S1000（常规错误）。  
  
 有关 Visual FoxPro ODBC 驱动程序生成的 SQLSTATE 值列表，请参阅[ODBC 错误代码](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)。  
  
## <a name="syntax"></a>语法  
 错误消息具有以下格式：  
  
 **[** *供应商* **]** *ODBC_component* **]** *error_message*  
  
 括号 （* +） 中的前缀标识下表中定义的错误源。  
  
|数据源|前缀|“值”|  
|-----------------|------------|-----------|  
|驱动程序管理器|[供应商]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC 驱动程序管理器]<br />空值|  
|可视化福克斯专业驱动程序|供应商*<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC 视觉福克斯专业驱动程序]<br />空值|  
  
 例如，如果 Visual FoxPro ODBC 驱动程序找不到文件员工.dbf，它可能会返回以下错误消息：  
  
 [*微软*]*ODBC 可视化福克斯Pro驱动程序*[文件 '员工.dbf' 不存在"

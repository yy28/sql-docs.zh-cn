---
title: 错误消息 （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b24db48d6a76c221e72944e8e5e6826cb8d5d55
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804415"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>错误消息（Visual FoxPro ODBC 驱动程序）
出现错误时，Visual FoxPro 驱动程序将返回以下信息：  
  
-   本机错误号和错误消息文本  
  
-   SQLSTATE （ODBC 错误代码） 和错误消息文本  
  
 通过调用访问此错误信息[SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)。  
  
## <a name="native-errors"></a>本机错误  
 对于数据源中出现的错误，Visual FoxPro 驱动程序返回本机错误号和错误消息文本。 有关本机错误号的列表，请参阅[Visual FoxPro ODBC 驱动程序本机错误消息](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)。  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE（ODBC 错误代码）  
 对于检测和 Visual FoxPro 驱动程序返回的错误，该驱动程序将返回本机错误号映射到相应的 SQLSTATE。 如果本机错误号没有要映射到 ODBC 错误代码，Visual FoxPro 驱动程序将返回 SQLSTATE S1000 （常规错误）。  
  
 生成的 Visual FoxPro ODBC 驱动程序的相应 Visual FoxPro 错误的 SQLSTATE 值的列表，请参阅[ODBC 错误代码](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)。  
  
## <a name="syntax"></a>语法  
 错误消息具有以下格式：  
  
 **[** *供应商* **] [** *ODBC_component* **]** *error_message*  
  
 方括号 ([]) 中的前缀来标识错误的源定义下表中。  
  
|数据源|Prefix|ReplTest1|  
|-----------------|------------|-----------|  
|驱动程序管理器|[供应商]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC 驱动程序管理器]<br />N/A|  
|Visual FoxPro 驱动程序|供应商]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC Visual FoxPro 驱动程序]<br />N/A|  
  
 例如，如果 Visual FoxPro ODBC 驱动程序找不到文件 employee.dbf，它可能会返回以下错误消息：  
  
 "[*Microsoft*] [*ODBC Visual FoxPro 驱动程序*] employee.dbf 的文件不存在"

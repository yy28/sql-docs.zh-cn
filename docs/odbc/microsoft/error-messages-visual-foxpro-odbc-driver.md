---
title: "错误消息 （Visual FoxPro ODBC 驱动程序） |Microsoft 文档"
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
- error messages [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], error messages
- SQLSTATE [ODBC]
- FoxPro ODBC driver [ODBC], error messages
ms.assetid: 58ea9734-4edf-44da-ba80-938aa7b340e4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e561aab3359acb1f236aea38e76da33289e630ef
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>错误消息 （Visual FoxPro ODBC 驱动程序）
发生错误时，Visual FoxPro 驱动程序将返回以下信息：  
  
-   本机错误号和错误消息文本  
  
-   SQLSTATE （ODBC 错误代码） 和错误消息文本  
  
 通过调用访问此错误信息[SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)。  
  
## <a name="native-errors"></a>本机错误  
 对于在数据源中发生的错误，Visual FoxPro 驱动程序返回的本机错误号和错误消息文本。 有关本机错误号码的列表，请参阅[Visual FoxPro ODBC 驱动程序本机错误信息](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)。  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE（ODBC 错误代码）  
 有关检测到并 Visual FoxPro 驱动程序返回的错误，该驱动程序将返回的本机错误号映射到相应的 SQLSTATE。 如果本机错误号没有要映射到 ODBC 错误代码，Visual FoxPro 驱动程序将返回 SQLSTATE S1000 （常规错误）。  
  
 生成的相应 Visual FoxPro 错误 Visual FoxPro ODBC 驱动程序的 SQLSTATE 值的列表，请参阅[ODBC 错误代码](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)。  
  
## <a name="syntax"></a>语法  
 错误消息具有以下格式：  
  
 **[** *供应商* **] [** *ODBC_component* **]** *error_message*  
  
 方括号 ([]) 中的前缀确定下表中定义的错误根源。  
  
|数据源|前缀|值|  
|-----------------|------------|-----------|  
|驱动程序管理器|[供应商]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC 驱动程序管理器]<br />N/A|  
|Visual FoxPro 驱动程序|供应商]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC Visual FoxPro 驱动程序]<br />N/A|  
  
 例如，如果 Visual FoxPro ODBC 驱动程序找不到文件 employee.dbf，它可能返回以下错误消息：  
  
 "[*Microsoft*] [*ODBC Visual FoxPro 驱动程序*] 文件 employee.dbf 不存在"

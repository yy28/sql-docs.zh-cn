---
title: 错误消息 （Visual FoxPro ODBC 驱动程序） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- error messages [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], error messages
- SQLSTATE [ODBC]
- FoxPro ODBC driver [ODBC], error messages
ms.assetid: 58ea9734-4edf-44da-ba80-938aa7b340e4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4f6be0c46b1dcc777004edacda8a490438db438c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
  
|数据源|Prefix|“值”|  
|-----------------|------------|-----------|  
|驱动程序管理器|[供应商]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC 驱动程序管理器]<br />N/A|  
|Visual FoxPro 驱动程序|供应商]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC Visual FoxPro 驱动程序]<br />N/A|  
  
 例如，如果 Visual FoxPro ODBC 驱动程序找不到文件 employee.dbf，它可能返回以下错误消息：  
  
 "[*Microsoft*] [*ODBC Visual FoxPro 驱动程序*] 文件 employee.dbf 不存在"

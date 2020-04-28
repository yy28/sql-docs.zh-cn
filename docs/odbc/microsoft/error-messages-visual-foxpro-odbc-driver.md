---
title: 错误消息（Visual FoxPro ODBC 驱动程序） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286397"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>错误消息（Visual FoxPro ODBC 驱动程序）
出现错误时，Visual FoxPro 驱动程序将返回以下信息：  
  
-   本机错误号和错误消息文本  
  
-   SQLSTATE （ODBC 错误代码）和错误消息文本  
  
 可以通过调用[SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)来访问此错误信息。  
  
## <a name="native-errors"></a>本机错误  
 对于数据源中发生的错误，Visual FoxPro 驱动程序返回本机错误号和错误消息文本。 有关本机错误号列表，请参阅[Visual FOXPRO ODBC 驱动程序本机错误消息](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)。  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE（ODBC 错误代码）  
 对于 Visual FoxPro 驱动程序检测到并返回的错误，驱动程序将返回的本机错误号映射到相应的 SQLSTATE。 如果本机错误号没有要映射到的 ODBC 错误代码，则 Visual FoxPro 驱动程序将返回 SQLSTATE S1000 （一般错误）。  
  
 有关 Visual FoxPro ODBC 驱动程序为相应的视觉 FoxPro 错误生成的 SQLSTATE 值的列表，请参阅[ODBC 错误代码](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)。  
  
## <a name="syntax"></a>语法  
 错误消息具有以下格式：  
  
 **[** *供应商* **] [** *ODBC_component* **]** *error_message*  
  
 括号（[]）中的前缀标识了下表中定义的错误源。  
  
|数据源|前缀|值|  
|-----------------|------------|-----------|  
|驱动程序管理器|采购<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC 驱动程序管理器]<br />不适用|  
|Visual FoxPro 驱动程序|采购<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC Visual FoxPro 驱动程序]<br />不适用|  
  
 例如，如果 Visual FoxPro ODBC 驱动程序找不到文件 employee，它可能会返回以下错误消息：  
  
 "[*Microsoft*] [*ODBC Visual FoxPro 驱动程序*] 文件 ' employee. .dbf ' 不存在"

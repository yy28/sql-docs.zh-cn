---
title: SQLGetTypeInfo (Access Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLGetTypeInfo
- SQLGetTypeInfo function [ODBC], Access Driver
ms.assetid: a28b16eb-ca36-4297-9297-ecd7c107a84e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a7c87c0dc81035d59e17db02a6e95c3b573523a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63028687"
---
# <a name="sqlgettypeinfo-access-driver"></a>SQLGetTypeInfo（Access 驱动程序）
> [!NOTE]  
>  本主题提供访问特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 在生成的表中返回的类型 (TYPE_NAME) 名称**SQLGetTypeInfo**将是最常用的数据源的名称。  
  
 SQL_ALL_EXCEPT_LIKE 将返回在可搜索的列中的字节，计数器、 Double、 单、 长时间和 Short 数据类型。 （LIKE 功能可以通过将值转换为使用 ODBC 规范转换函数，然后执行比较的字符。）

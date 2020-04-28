---
title: SQLGetTypeInfo （Access 驱动程序） |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ddfa9bd29f0834adf1c211f9b8a111db0b94d3fe
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81295147"
---
# <a name="sqlgettypeinfo-access-driver"></a>SQLGetTypeInfo（Access 驱动程序）
> [!NOTE]  
>  本主题提供特定于访问驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 **SQLGetTypeInfo**生成的表中返回的类型（TYPE_NAME）的名称将是数据源最常使用的名称。  
  
 对于 Byte、Counter、Double、Single、Long 和 Short 数据类型，将在可搜索列中返回 SQL_ALL_EXCEPT_LIKE。 （可通过使用 ODBC 规范转换函数将值转换为字符，然后执行比较来实现类似的功能。）

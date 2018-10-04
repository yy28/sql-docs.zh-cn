---
title: SQLGetData 和块游标 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- SQLGetData function [ODBC], block cursors
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 12599cdc-7725-4faf-bcae-e163ea0f5851
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a14c98f045fd974b404209cc998496dc5fa7193e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47755515"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData 和块游标
**SQLGetData**作用于单个行的单个列，并且无法提取包含来自多个行的数据的数组。 这是因为主数据库使用的**SQLGetData**是提取在部件中，长整型数据，并且没有很少或没有为多个行执行此操作一次的原因。  
  
 若要使用**SQLGetData**块状游标，与应用程序首先调用**SQLSetPos**将游标定位的单个行。 然后，它调用**SQLGetData**该行中的列。 但是，此行为是可选的。 若要确定驱动程序是否支持使用**SQLGetData**应用程序调用使用块状游标**SQLGetInfo** SQL_GETDATA_EXTENSIONS 选项。

---
title: SQLGet数据和块光标 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b60d7093552b8f1dbed87d9ad8840ddb5a9e0799
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299747"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData 和块游标
**SQLGetData**对单个行的单个列进行操作，无法从多个行获取包含数据的数组。 这是因为**SQLGetData**的主要用途是获取部分长数据，并且很少或没有理由一次对多行执行此操作。  
  
 要将**SQLGetData**与块游标一起使用，应用程序首先调用**SQLSetPos**将光标定位在一行上。 然后，它为该行中的列调用**SQLGetData。** 但是，此行为是可选的。 要确定驱动程序是否支持将**SQLGetData**与块游标一起使用，应用程序使用SQL_GETDATA_EXTENSIONS选项调用**SQLGetInfo。**

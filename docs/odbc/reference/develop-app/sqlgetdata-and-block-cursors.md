---
description: SQLGetData 和块游标
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f53358b2d4d8dfef1a5a820ed3943f07a584a595
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424489"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData 和块游标
**SQLGetData** 作用于单个行的单个列，不能从多个行中提取包含数据的数组。 这是因为， **SQLGetData** 的主要用途是在部分中提取长数据，并且每次只需为多行执行此操作。  
  
 若要将 **SQLGetData** 与块光标一起使用，应用程序首先调用 **SQLSetPos** 将光标置于单个行。 然后，它对该行中的列调用 **SQLGetData** 。 但是，此行为是可选的。 若要确定驱动程序是否支持将 **SQLGetData** 与块光标一起使用，应用程序需要使用 SQL_GETDATA_EXTENSIONS 选项调用 **SQLGetInfo** 。

---
title: SQLGetData 和块状游标 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- SQLGetData function [ODBC], block cursors
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 12599cdc-7725-4faf-bcae-e163ea0f5851
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8642e5c228bb0e7976099d2151fe36f4db683f27
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData 和块状游标
**SQLGetData**作用于单个行的单个列，并且无法提取数组，其中包含来自多个行的数据。 这是因为主利用**SQLGetData**是提取长整型数据在部件中，并且由于很少或没有原因，若要为多个行执行此操作一次。  
  
 若要使用**SQLGetData**与块游标，应用程序首先调用**SQLSetPos**以将光标置于单个行。 然后，它调用**SQLGetData**该行中的列。 但是，此行为是可选的。 若要确定驱动程序是否支持使用**SQLGetData**块状游标与应用程序调用**SQLGetInfo** SQL_GETDATA_EXTENSIONS 选项。

---
title: 创建和打开表（文本文件驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], creating and opening tables
ms.assetid: e6a07dda-a665-4f5b-a8d6-9ff479700513
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae13312299f131d1957557db28bbe4db0bf7b4c7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280917"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>创建和打开表（文本文件驱动程序）
使用文本驱动程序时，将使用 Odbcinst.ini 中指定的格式创建一个新表。 如果未指定，则以 CSVDELIMITED 格式创建表。 默认情况下，整数列默认为11个字符，而 FLOAT 列默认为22个字符。 日期列使用 YYYY-MM-DD 格式。 CHAR 和 LONGCHAR 列是 CREATE 语句中指定的宽度。

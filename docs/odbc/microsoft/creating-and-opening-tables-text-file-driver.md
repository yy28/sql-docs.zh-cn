---
description: 创建和打开表（文本文件驱动程序）
title: 创建和打开 (文本文件驱动程序) 的表 |Microsoft Docs
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
ms.openlocfilehash: c64f74270e8c2bbf4645f72406113e88948d0da9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340963"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>创建和打开表（文本文件驱动程序）
使用文本驱动程序时，将使用 Odbcinst.ini 中指定的格式创建一个新表。 如果未指定，则以 CSVDELIMITED 格式创建表。 默认情况下，整数列默认为11个字符，而 FLOAT 列默认为22个字符。 日期列使用 YYYY-MM-DD 格式。 CHAR 和 LONGCHAR 列是 CREATE 语句中指定的宽度。

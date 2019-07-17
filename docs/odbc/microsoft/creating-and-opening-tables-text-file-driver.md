---
title: 创建和打开表 （文本文件驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b36c02d772682088a799cfca66f5bbf3e169a67f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096545"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>创建和打开表（文本文件驱动程序）
使用文本驱动程序时，使用 Odbcinst.ini 中指定的格式创建一个新表。 如果未指定，CSVDELIMITED 格式创建表。 默认情况下，整数列的默认值为 11 个字符和 FLOAT 列默认为 22 个字符。 日期列使用的年-月-日格式。 CHAR 和 LONGCHAR 列是在 CREATE 语句中指定的宽度。

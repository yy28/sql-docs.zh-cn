---
title: 使用 ExtendedAnsiSQL 启用数据截断检测 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae1aa7a8a8b9ea2c3f3054717546506e660d5270
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280691"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>使用 ExtendedAnsiSQL 启用的数据截断检测
当 ExtendedAnsiSQL 标志打开并且应用程序将数据插入到 char 或 binary 列中并且数据被截断时，将检测到截断。 当 ExtendedAnsiSQL 标志关闭时，数据将被截断，而不会出现警告，因为它在以前版本的 ODBC 桌面数据库驱动程序中。

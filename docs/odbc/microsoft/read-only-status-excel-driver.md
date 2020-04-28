---
title: 只读状态（Excel 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- read-only status for Excel driver [ODBC]
- Excel driver [ODBC], read-only status
ms.assetid: ef5d773b-4f8f-4005-b985-84b53d8e9f9b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb585d4712b6cac5e09b65ee8e13604763cd0164
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304018"
---
# <a name="read-only-status-excel-driver"></a>只读状态（Excel 驱动程序）
使用 Microsoft Excel 驱动程序时，默认情况下，数据源表以只读方式打开，并且一次只能由一个用户打开。 但尽管表具有只读状态，但应用程序可以执行 Microsoft Excel 表的插入和更新。  
  
 当应用程序通过 Microsoft Excel 驱动程序对 Microsoft Excel 数据执行 "另存为" 命令时，应用程序应创建一个新表并插入要保存到新表中的数据。 将追加中的结果插入表中。 在关闭并重新打开表之前，不能对表执行任何其他操作。 一旦表关闭，就不能执行后续插入，因为该表是只读表。  
  
 使用 Microsoft Excel 驱动程序时，可能会更新值，但无法基于 Microsoft Excel 电子表格从表中删除行，因此 Microsoft Excel 驱动程序不会将更新视为正式支持。

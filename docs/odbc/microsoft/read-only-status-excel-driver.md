---
title: 只读状态 （Excel 驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 39f9d2e7ba40ba067659a86f45d2006c83594f3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988045"
---
# <a name="read-only-status-excel-driver"></a>只读状态（Excel 驱动程序）
使用 Microsoft Excel 驱动程序时，默认情况下以只读方式打开数据源表和源一次只能有一个用户可以打开。 即使表具有只读状态，但是，应用程序可以执行插入和更新的 Microsoft Excel 表。  
  
 当应用程序通过 Microsoft Excel 驱动程序的 Microsoft Excel 数据上执行另存为命令时，该应用程序应创建一个新表和插入数据以保存到新表。 插入导致追加到表。 可以对表不执行任何其他操作，直到将它关闭并重新打开。 一旦关闭表，可以不执行任何后续插入，因为表然后是只读的表。  
  
 可以更新值时使用 Microsoft Excel 驱动程序，但不能从基于 Microsoft Excel 电子表格，因此更新被视为不正式支持的 Microsoft Excel 驱动程序对表中删除行。

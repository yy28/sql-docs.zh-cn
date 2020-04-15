---
title: 只读状态（Excel 驱动程序） |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304018"
---
# <a name="read-only-status-excel-driver"></a>只读状态（Excel 驱动程序）
使用 Microsoft Excel 驱动程序时，默认情况下，数据源表作为只读表打开，并且一次只能由一个用户打开。 但是，即使表具有只读状态，应用程序也可以对 Microsoft Excel 表执行插入和更新。  
  
 当应用程序通过 Microsoft Excel 驱动程序对 Microsoft Excel 数据执行"保存为"命令时，应用程序应创建一个新表并将要保存的数据插入到新表中。 插入会导致表追加。 在表关闭并重新打开之前，无法对表执行任何其他操作。 关闭表后，无法执行后续插入，因为该表是只读表。  
  
 使用 Microsoft Excel 驱动程序时可以更新值，但不能从基于 Microsoft Excel 电子表格的表中删除行，因此 Microsoft Excel 驱动程序不被视为正式支持更新。

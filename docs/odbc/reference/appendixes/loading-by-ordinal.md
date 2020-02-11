---
title: 按序号加载 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], loading by ordinal
- compatibility [ODBC], loading by ordinal
- loading by ordinal [ODBC]
ms.assetid: 337d90ab-68eb-4940-a2f3-f7d5693ee766
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fdc7728fe06df708efd973423f5c8c05333ce189
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041600"
---
# <a name="loading-by-ordinal"></a>按序号加载
在 ODBC *2.x 中，* 可以执行按序号进行加载以提高连接过程的性能。 *ODBC 2.x*驱动程序使用序号 199; 导出虚函数。当驱动程序管理器检测到它时，它将按序号而不是按名称解析 ODBC 函数的地址。 ODBC 2.x 驱动程序仍支持此功能，*但 odbc 1.x* *驱动程序不*支持此功能。

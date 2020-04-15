---
title: 按 Ordinal 加载 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 64bff8dcdd3802f75dc402c9ada60f82580aca5c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288717"
---
# <a name="loading-by-ordinal"></a>按序号加载
在 ODBC *2.x*中，可以执行序号加载以提高连接过程的性能。 ODBC *2.x*驱动程序导出带有假函数的虚拟函数 199;当驱动程序管理器检测到它时，它按位数而不是名称解析 ODBC 函数的地址。 ODBC *2.x*驱动程序仍然支持此功能，但 ODBC *3.x*驱动程序不支持此功能。

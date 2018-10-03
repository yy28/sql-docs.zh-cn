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
manager: craigg
ms.openlocfilehash: 702e1fe58080cc370ab9a858c985a7744df85050
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845855"
---
# <a name="loading-by-ordinal"></a>按序号加载
在 ODBC 2。*x*，可以执行按序号加载以提高连接过程的性能。 ODBC 2。*x*驱动程序将导出序号 199 的虚函数; 当驱动程序管理器检测到它，它按序号而不是按名称解析的 ODBC 函数的地址。 ODBC 2 仍支持此功能。*x*驱动程序但不是支持 ODBC 3 *.x*驱动程序。

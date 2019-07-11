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
ms.openlocfilehash: ccecc541143e971d82a225e24e1c8caf6a03c32c
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793193"
---
# <a name="loading-by-ordinal"></a>按序号加载
在 ODBC *2.x*，可以执行按序号加载以提高连接过程的性能。 ODBC *2.x*驱动程序将导出序号 199 的虚函数; 当驱动程序管理器检测到它，它按序号而不是按名称解析的 ODBC 函数的地址。 此功能仍支持 ODBC *2.x*驱动程序但不是支持 ODBC *3.x*驱动程序。

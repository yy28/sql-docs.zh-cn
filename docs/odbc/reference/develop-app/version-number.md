---
title: 版本号 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- version number supported [ODBC]
- interoperability [ODBC], version number supported
ms.assetid: 6eccacdf-b837-4b66-bd48-ba31771acecb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 06f5293f7c4a2f89560970303f599c4759c82bd3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="version-number"></a>版本号
有多个版本的 ODBC，每个都有不同的功能。 应用程序确定驱动程序管理器的 ODBC 版本和特定的驱动程序支持通过调用**SQLGetInfo**使用 SQL_ODBC_VER 和 SQL_DRIVER_ODBC_VER 选项。

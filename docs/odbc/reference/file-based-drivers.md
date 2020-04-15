---
title: 基于文件的驱动程序 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
- drivers [ODBC], file-based drivers
ms.assetid: d92e0c5c-d176-4282-bbe1-d449e2223d50
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 223bd838754f1d656ac71ae37926389097af3ea1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306660"
---
# <a name="file-based-drivers"></a>基于文件的驱动程序
基于文件的驱动程序与数据源（如 dBASE）一起使用，这些数据源不提供独立数据库引擎供驱动程序使用。 这些驱动程序直接访问物理数据，并且必须实现数据库引擎来处理 SQL 语句。 作为一种标准做法，基于文件的驱动程序中的数据库引擎实现由最低 SQL 一致性级别定义的 ODBC SQL 子集;有关此一致性级别的 SQL 语句的列表，请参阅附录[C：SQL 语法](../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
 在比较基于文件的驱动程序和基于 DBMS 的驱动程序时，基于文件的驱动程序更难编写，因为数据库引擎组件，配置起来不太复杂，因为没有网络部分，而且功能较弱，因为很少有人有时间编写数据库引擎，就像数据库公司生成的引擎那样强大。  
  
 下图显示了基于文件的驱动程序的两种不同的配置，一种是数据驻留在本地，另一种位于网络文件服务器上。  
  
 ![基于&#45;驱动程序的两种配置](../../odbc/reference/media/pr06.gif "pr06")

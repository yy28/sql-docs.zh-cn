---
title: 基于文件的驱动程序 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 803da51c8507faa47f92b295d3749f00317bc413
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915385"
---
# <a name="file-based-drivers"></a>基于文件的驱动程序
基于文件的驱动程序与数据源（如 dBASE）一起使用，这些数据源不提供独立的数据库引擎供驱动程序使用。 这些驱动程序直接访问物理数据，必须实现数据库引擎才能处理 SQL 语句。 作为标准做法，基于文件的驱动程序中的数据库引擎实现由最低 SQL 一致性级别定义的 ODBC SQL 子集;有关此一致性级别中的 SQL 语句的列表，请参阅[附录 C： Sql 语法](../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
 在比较基于文件的驱动程序和基于 DBMS 的驱动程序时，基于文件的驱动程序更难写入，这是因为数据库引擎组件、配置不太复杂，而不是网络碎片，因为很少有人有写入数据库的时间功能强大于由数据库公司生成的引擎。  
  
 下图显示了基于文件的驱动程序的两种不同配置，其中的数据存放在一个本地，另一个位于网络文件服务器上。  
  
 ![基于文件&#45;的驱动程序的两种配置](../../odbc/reference/media/pr06.gif "pr06")

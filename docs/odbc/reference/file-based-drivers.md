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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915385"
---
# <a name="file-based-drivers"></a>基于文件的驱动程序
DBASE 等的数据源不提供驱动程序使用一个独立的数据库引擎使用基于文件的驱动程序。 这些驱动程序直接访问物理数据和必须实现到过程的 SQL 语句的数据库引擎。 标准做法是，数据库引擎中基于文件的驱动程序实现最小 SQL 一致性级别; 定义的 ODBC SQL 的子集有关此符合性级别中的 SQL 语句的列表，请参阅[附录 c:SQL 语法](../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
 在比较基于文件的和基于 DBMS 的驱动程序，基于文件的驱动程序是要难编写数据库引擎组件，不太复杂，若要配置，因为没有网络棋子，由于和较不强大因为很少有人有时间写入数据库引擎通过公司的数据库生成的那些同样强大。  
  
 下图显示两个不同的基于文件的驱动程序，数据位于本地的一个，其他驻留在其中配置了网络文件服务器上。  
  
 ![两个配置文件的&#45;基于驱动程序](../../odbc/reference/media/pr06.gif "pr06")

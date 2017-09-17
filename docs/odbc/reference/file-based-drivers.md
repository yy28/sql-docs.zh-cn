---
title: "基于文件的驱动程序 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- file-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
- drivers [ODBC], file-based drivers
ms.assetid: d92e0c5c-d176-4282-bbe1-d449e2223d50
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2ab8cb4066a8c5c7ab2e31401dd1e80d003d5b38
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="file-based-drivers"></a>基于文件的驱动程序
基于文件的驱动程序用于 dBASE 等的数据源，不提供要使用的驱动程序的独立数据库引擎。 这些驱动程序直接访问物理数据，而且必须实现过程 SQL 语句的数据库引擎。 标准做法是，基于文件的驱动程序中的数据库引擎实现定义的最小的 SQL 一致性级别; ODBC SQL 的子集有关此一致性级别中的 SQL 语句的列表，请参阅[附录 c: SQL 语法](../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
 比较基于文件的和基于 DBMS 的驱动程序中基于文件的驱动程序是难以编写数据库引擎组件，不太复杂，无法配置，因为没有任何网络部分中，由于和较弱因为很少有人具有要写入数据库的时间具有强大的功能与由公司的数据库引擎。  
  
 下图显示了网络文件服务器上的基于文件的驱动程序的数据位于本地，其中它所在的其他两个不同的配置。  
  
 ![两个配置文件的 &#45; 基于驱动程序](../../odbc/reference/media/pr06.gif "pr06")

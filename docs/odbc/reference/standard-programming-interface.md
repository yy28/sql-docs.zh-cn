---
title: 标准编程接口 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], programming interface
- programming interface standardization [ODBC]
ms.assetid: a2fa727e-51f2-4123-ae25-0ee28e611231
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c7767f113d0f70569ce253f0200cd35cb83915a4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81279993"
---
# <a name="standard-programming-interface"></a>标准编程接口
编程接口可能是标准化最明显的候选方案。 事实上，在开发 ODBC 时，ANSI 和 ISO 已经为嵌入式 SQL 和 SQL 模块提供了标准。 虽然没有数据库 CLI 的标准，但 SQL Access 组（一个由数据库供应商组成的行业联盟）正在考虑是否创建数据库 CLI;ODBC的一部分后来成为他们工作的基础。  
  
 ODBC 的要求之一是单个应用程序二进制文件必须使用多个 DBMS。 因此，ODBC 不使用嵌入式 SQL 或模块语言。 尽管嵌入式 SQL 和模块语言中的语言是标准化的，但每个语言都与特定于 DBMS 的预编译器相关联。 因此，必须为每个 DBMS 重新编译应用程序，生成的二进制文件仅使用单个 DBMS。 虽然这适用于小型计算机和大型机世界中的低容量应用，但在个人电脑世界中是不能接受的。 首先，向客户交付多个版本的大批量、收缩包装软件是一场后勤噩梦;其次，个人计算机应用程序通常需要同时访问多个 DBMS。  
  
 另一方面，调用级接口可以通过驻留在每个本地计算机上的库或数据库驱动程序实现;每个 DBMS 都需要不同的驱动程序。 由于现代操作系统可以在运行时加载此类库（如 Microsoft® Windows ® 操作系统上的动态链接库），因此单个应用程序无需重新编译即可访问来自不同 DBMS 的数据，还可以同时从多个数据库访问数据。 随着新的数据库驱动程序可用，用户只需在其计算机上安装这些驱动程序，而无需修改、重新编译或重新链接其数据库应用程序。 此外，调用级接口是 ODBC 的一个很好的候选点，因为 Windows（最初开发 ODBC 的平台）已经广泛使用了此类库。

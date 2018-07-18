---
title: 标准编程接口 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], programming interface
- programming interface standardization [ODBC]
ms.assetid: a2fa727e-51f2-4123-ae25-0ee28e611231
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e820b626ce8e4f207885b8c7e5dd5cdc7050f960
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32916102"
---
# <a name="standard-programming-interface"></a>标准编程接口
编程接口可能是标准化的最明显候选。 事实上，当开发 ODBC 时，ANSI 和 ISO 已提供标准嵌入 SQL 和 SQL 的模块。 虽然没有标准存在数据库 CLI，使用 SQL 访问组-数据库供应商行业联合会-已考虑是否要创建一个;更高版本的 ODBC 部分垃圾回收其工作的基础。  
  
 适用于 ODBC 的要求之一是，单个应用程序二进制必须使用多个 Dbms。 它是为此，ODBC 不使用嵌入的 SQL 或模块语言。 尽管中嵌入的 SQL 和模块语言的语言进行了标准化，则将每个与特定于 DBMS 的 precompilers。 因此，必须为每个 DBMS 重新编译应用程序和生成的二进制文件仅使用单个 DBMS。 虽然这是可接受的小型计算机和大型机领域中找到的低容量应用程序，它是不可接受在个人计算机环境中。 首先，它是一种逻辑的场，以向客户; 提供多个版本的大量、 紧缩套装软件其次，个人计算机应用程序通常需要同时访问多个 Dbms。  
  
 另一方面，可以通过库或数据库驱动程序，驻留在每个本地计算机; 上实现调用级接口需要为每个 DBMS 不同驱动程序。 因为现代操作系统可以在运行时加载这种库 （如在 Microsoft® Windows® 操作系统上的动态链接库），单个应用程序可以从无需重新编译的不同 Dbms 访问数据，并且可以访问中的数据同时是多个数据库。 当新的数据库驱动程序变得可用，则用户只可以安装这些在其计算机上而无需修改、 重新编译，或重新链接其数据库应用程序。 此外，调用级接口是适用于 ODBC 的良好候选的因为 Windows-ODBC 最初为其开发平台-已经做了大量使用这种库。

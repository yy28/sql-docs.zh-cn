---
title: 标准编程接口 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e0e10a6b8c15b6522e6b34ab008295fc411fcd3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232066"
---
# <a name="standard-programming-interface"></a>标准编程接口
编程接口可能是标准化的最明显候选项。 事实上，开发 ODBC 时，ANSI 和 ISO 已提供标准的嵌入式 SQL 和 SQL 模块。 尽管没有标准数据库 CLI 已存在，但 SQL 访问组-数据库供应商一个行业协会-已考虑是否要创建一个;更高版本的 ODBC 部分成为了其工作的基础。  
  
 用于 ODBC 的要求之一是二进制的单个应用程序必须能够使用多个 Dbms。 正是出于此原因，ODBC 不使用嵌入的 SQL 或模块语言。 尽管中嵌入 SQL 和模块的语言的语言进行了标准化，每个被绑定到特定于 DBMS 的 precompilers。 因此，应用程序必须为每个 DBMS 重新编译和生成的二进制文件仅使用单个 DBMS。 虽然这是可以接受的小型计算机和大型机领域中找到的低容量应用程序，它是不可接受个人计算机世界中。 首先，它是为客户; 提供多个版本的大容量、 压缩包装软件物流痛苦其次，个人计算机应用程序通常需要同时访问多个 Dbms。  
  
 但是，可以通过库或数据库驱动程序，每个本地计算机; 上驻留的实现调用级别接口每个 DBMS 需要不同的驱动程序。 现代操作系统可以在运行时加载此类库 （如 Microsoft® Windows® 操作系统上的动态链接库），因为单个应用程序可以访问无需重新编译的不同 Dbms 中的数据，也可以访问中的数据同时是多个数据库。 随着新的数据库驱动程序变得可用，用户可以只安装在其计算机上而无需修改、 重新编译，或将其数据库应用程序重新链接。 此外，调用级别接口是 ODBC 的良好候选项，因为 Windows-为其 ODBC 最初开发-已作出这样的库的广泛使用的平台。

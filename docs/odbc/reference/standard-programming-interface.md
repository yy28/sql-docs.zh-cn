---
description: 标准编程接口
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8fd0e9e3901ea6b3dcf9a09366b13fe532f1198
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448880"
---
# <a name="standard-programming-interface"></a>标准编程接口
编程接口可能是标准化的最显而易见的候选项。 事实上，在开发 ODBC 时，ANSI 和 ISO 已为嵌入式 SQL 和 SQL 模块提供了标准。 尽管没有适用于数据库 CLI 的标准，但 SQL 访问组（数据库供应商的行业协会）却在考虑是否要创建一个;稍后的 ODBC 部分成为其工作的基础。  
  
 ODBC 的要求之一是，单个应用程序的二进制文件必须与多个 Dbms 一起使用。 出于此原因，ODBC 不使用嵌入的 SQL 或模块语言。 尽管嵌入式 SQL 和模块语言中的语言是标准化的，但每个语言都与 DBMS 特定的 precompilers 相关联。 因此，必须为每个 DBMS 重新编译应用程序，并且生成的二进制文件仅适用于单个 DBMS。 虽然这对于 minicomputer 和大型机领域内的低容量应用程序是可接受的，但它在个人计算机世界中是不可接受的。 首先，这是一项后勤工作，可向客户提供多个版本的大容量压缩软件：其次，个人计算机应用程序通常需要同时访问多个 Dbms。  
  
 另一方面，可以通过驻留在每个本地计算机上的库或数据库驱动程序来实现调用级接口。每个 DBMS 需要不同的驱动程序。 由于现代操作系统可在 Microsoft® Windows®操作系统) 上加载此类库 (例如动态链接库，因此，单个应用程序可以从不同 Dbms 访问数据而无需重新编译，还可以同时访问来自多个数据库的数据。 当新数据库驱动程序可用时，用户只需在他们的计算机上安装这些驱动程序，无需修改、重新编译或重新链接其数据库应用程序。 此外，调用级别接口非常适合用于 ODBC，因为 Windows 是最初为其开发 ODBC 的平台-已广泛利用此类库。

---
description: “数据源”
title: 数据源 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC]
- data sources [ODBC], about data sources
ms.assetid: 4ae44fa2-0b9b-4e19-ab45-c1dc93b68406
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b9f980ad9ccd1fa38b6fce863703ec706e21a76
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386053"
---
# <a name="data-sources"></a>“数据源”
*数据源*就是数据源。 它可以是文件、DBMS 上的特定数据库，甚至是实时数据馈送。 数据可以与程序位于同一台计算机上，也可以位于网络中某个位置的另一台计算机上。 例如，数据源可能是在 OS/2®操作系统上运行的 Oracle DBMS，由 Novell® Netware 访问;通过网关访问的 IBM DB2 DBMS;服务器目录中 Xbase 文件的集合;或本地 Microsoft® Access 数据库文件。  
  
 数据源的用途是将访问数据所需的所有技术信息（驱动程序名称、网络地址、网络软件等）收集到一个位置，并将其从用户隐藏。 用户应能够查看包括工资单、库存和人员的列表，从列表中选择工资单，并使应用程序连接到工资单数据，所有这些都不会知道工资单数据的驻留位置或应用程序的来源。  
  
 术语 " *数据源* " 不应与类似的术语混淆。 在本手册中， *DBMS* 或 *数据库* 是指数据库程序或引擎。 在 *桌面数据库* 之间进行进一步的区分，这些数据库旨在在个人计算机上运行，并且经常缺少完整的 SQL 和事务支持以及 *服务器数据库，* 设计用于在客户端/服务器情况下运行，并以独立数据库引擎和丰富的 SQL 和事务支持为特征。 *数据库* 还引用特定的数据集合，例如目录中的 Xbase 文件集合或 SQL Server 上的数据库。 它通常等效于本手册的其他地方使用的术语 " *目录* " 或早期版本的 ODBC 中的术语 " *限定符* "。  
  
 本部分包含以下主题。  
  
-   [数据源的类型](../../odbc/reference/types-of-data-sources.md)  
  
-   [使用数据源](../../odbc/reference/using-data-sources.md)  
  
-   [数据源示例](../../odbc/reference/data-source-example.md)

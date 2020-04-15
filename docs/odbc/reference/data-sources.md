---
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
ms.openlocfilehash: 9b7e464963471b0cad41c5b93d50507d0fa9bf96
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306508"
---
# <a name="data-sources"></a>“数据源”
*数据源*只是数据源。 它可以是文件、DBMS 上的特定数据库，甚至是实时数据馈送。 数据可能位于与程序相同的计算机上，或者位于网络上的另一台计算机上。 例如，数据源可能是运行在 OS/2® 操作系统上的 Oracle DBMS，由 Novell® Netware 访问;通过网关访问的 IBM DB2 DBMS;服务器目录中的 Xbase 文件的集合;或本地 Microsoft®访问数据库文件。  
  
 数据源的目的是将数据（驱动程序名称、网络地址、网络软件等）收集到单个位置，并将其隐藏到单个位置，并将其隐藏到用户位置。 用户应该能够查看包含工资单、库存和人员的列表，从列表中选择"工资单"，让应用程序连接到工资单数据，而不知道工资数据驻留的位置或应用程序如何访问它。  
  
 术语*数据源*不应与类似的术语混淆。 在本手册中 *，DBMS*或*数据库*是指数据库程序或引擎。 *桌面数据库*（设计为在个人计算机上运行且通常缺乏完整的 SQL 和事务支持）和*服务器数据库*（旨在在客户端/服务器情况下运行，其特点是独立数据库引擎和丰富的 SQL 和事务支持）之间进一步进行了区分。 *数据库*还引用特定的数据集合，例如目录中的 Xbase 文件集合或 SQL Server 上的数据库。 它通常等效于本手册其他部分使用的术语*目录*，或早期版本的 ODBC 中的术语*限定符*。  
  
 本部分包含以下主题。  
  
-   [数据源的类型](../../odbc/reference/types-of-data-sources.md)  
  
-   [使用数据源](../../odbc/reference/using-data-sources.md)  
  
-   [数据源示例](../../odbc/reference/data-source-example.md)

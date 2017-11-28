---
title: "确定目标 Dbms 和驱动程序 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- target DBMSs and drivers in interoperability [ODBC]
- interoperability [ODBC], target dbmss and drivers
ms.assetid: 23bee0f6-e12a-4598-b34e-df11a8086829
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 76daa1e2753c91df7a016d4801ddea48bc285eb5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="determining-the-target-dbmss-and-drivers"></a>确定目标 Dbms 和驱动程序
要考虑的下一步问题是，哪些应用程序的目标 Dbms 和支持这些 Dbms 使用哪些驱动程序都可用？ 通用应用程序往往是高度可互操作，因为目标 Dbms 的问题是最适用于自定义和垂直应用程序。 但是，这一问题目标驱动程序适用于所有应用程序，因为驱动程序差别很大速度、 质量、 支持的功能和可用性。 此外，如果驱动程序与应用程序一起重新分发，成本和可用性的许可计划需要考虑。  
  
 对于许多自定义应用程序，目标 Dbms 是明显： 它们现有的应用程序旨在为 Dbms 访问。 此外应考虑到的计划将来的迁移的 Dbms。 但是，这些应用程序的主要问题是哪些驱动程序或驱动程序以使用它们。 其他自定义应用程序-那些不用于访问现有的 DBMS-可以选择目标 Dbms 取决于支持的功能、 并发用户支持、 驱动程序可用性和经济性。  
  
 对于垂直应用程序，通常选择 Dbms 的目标会根据支持的功能、 驱动程序可用性和市场。 例如，为小型企业设计的垂直应用程序都必须为目标是为这些企业; 经济实惠的 Dbms为现有 Dbms 外的接程序必须面向广泛的设计目的的垂直应用程序使用 Dbms。  
  
 选择目标 Dbms 时, 应考虑台式机和服务器的数据库之间的差异。 如 dBASE、 Paradox 和 Btrieve 桌面数据库性能没有那么强大比 server 数据库。 它们通常会通过最基于文件的驱动程序中找到的权力较小 SQL 引擎访问的因为它们通常缺少完整事务的支持，支持更少的并发用户，并具有有限的 SQL。 但是，它们是成本较低，而且具有大的客户的群。  
  
 例如 Oracle、 DB2 和 SQL Server 的 server 数据库提供完整的事务支持，支持很多的并发用户，并具有丰富的 SQL。 它们开销大得多，而且具有较小的客户的群。 另一方面，软件价格往往能够更高版本，某种程度上偏移较小的潜在市场。  
  
 因此，可以基于按应用程序和应用程序的目标市场所需的功能选择有时目标 Dbms。 例如，对于大型公司而言订单输入系统可能不面向桌面数据库，因为这些缺少足够的事务的支持。 小型企业设计的类似系统可能排除基于成本的多数服务器数据库。 和的通用应用程序的开发人员可能面向同时但避免使用在服务器数据库中发现的高级的功能。

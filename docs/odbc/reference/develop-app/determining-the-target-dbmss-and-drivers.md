---
title: 确定目标 DBMS 和驱动程序 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- target DBMSs and drivers in interoperability [ODBC]
- interoperability [ODBC], target dbmss and drivers
ms.assetid: 23bee0f6-e12a-4598-b34e-df11a8086829
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f8811e4d289a8fc89c2c3773aab973df523025f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305868"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>确定目标 DBMS 和驱动程序
需要考虑的下一个问题是，应用程序的目标 DBMS 是什么，哪些驱动程序支持这些 DBMS？ 由于通用应用程序往往高度可互操作，因此目标 DBMS 问题最适用于自定义和垂直应用程序。 但是，目标驱动程序的问题适用于所有应用程序，因为驱动程序在速度、质量、功能支持和可用性方面差异很大。 此外，如果要与应用程序重新分发驱动程序，需要考虑许可计划的成本和可用性。  
  
 对于许多自定义应用程序，目标 DBMS 是显而易见的：它们是应用程序设计为要访问的现有 DBMS。 还应考虑计划向其迁移的 DBMS。 但是，对于这些应用程序来说，主要问题是要使用它们的驱动程序或驱动程序。 对于其他自定义应用程序（那些不是旨在访问现有 DBMS 的应用程序），可以根据功能支持、并发用户支持、驱动程序可用性和可负担性选择目标 DBMS。  
  
 对于垂直应用，目标 DBMS 通常基于功能支持、驱动程序可用性和市场进行选择。 例如，专为小型企业设计的垂直应用程序必须针对这些企业负担得起的 DBMS;设计为现有 DBMS 的附加组件的垂直应用程序必须针对广泛使用的 DBMS。  
  
 在选择目标 DBMS 时，应考虑桌面数据库和服务器数据库之间的差异。 桌面数据库（如 dBASE、Paradox 和 Btrieve）不如服务器数据库强大。 因为它们通常通过大多数基于文件的驱动程序中功能较弱的 SQL 引擎进行访问，因此它们通常缺乏完整的事务支持，支持较少的并发用户，并且 SQL 有限。 但是，它们价格低廉，并且具有较大的客户群。  
  
 Oracle、DB2 和 SQL Server 等服务器数据库提供完整的事务支持、支持许多并发用户以及具有丰富的 SQL。 它们的成本要高得多，而且安装基础更小。 另一方面，软件价格往往较高，多少抵消了较小的潜在市场。  
  
 因此，有时可以根据应用程序和应用程序的目标市场所需的功能选择目标 DBMS。 例如，大型企业的订单输入系统可能不是针对桌面数据库的目标，因为这些数据库缺乏足够的事务支持。 为小型企业设计的类似系统可能会根据成本排除大多数服务器数据库。 通用应用程序的开发人员可能同时针对这两种功能，但应避免使用服务器数据库中的高级功能。

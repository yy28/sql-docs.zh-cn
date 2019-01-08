---
title: 确定目标 Dbms 和驱动程序 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 92da788205213394edc75257d8266752a2a9d8df
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535776"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>确定目标 DBMS 和驱动程序
要考虑的下一步问题是，什么是应用程序的目标 Dbms 和哪些驱动程序可支持这些 Dbms？ 泛型应用程序往往是高度可互操作，因为目标 Dbms 的问题是最适用于自定义和垂直应用程序。 但是，目标驱动程序的问题适用于所有应用程序，因为驱动程序差异很大在速度、 质量、 支持的功能和可用性。 此外，如果驱动程序来与应用程序一起重新发布，成本和可用性的许可计划需要考虑。  
  
 对于许多自定义应用程序目标 Dbms 非常明显：它们现有的应用程序设计为 Dbms 访问。 此外应考虑到以后的迁移计划内的 Dbms。 但是，这些应用程序的主要问题是哪些驱动程序或驱动程序，以使用它们。 对于其他自定义应用程序的那些并不用于访问现有的 DBMS 的目标 Dbms，可以选择根据支持的功能、 并发用户支持、 驱动程序可用性和经济性。  
  
 对于垂直应用程序，通常选择 Dbms 的目标基于支持的功能、 驱动程序可用性和市场。 例如，对于小型企业设计的垂直应用程序必须面向这些企业; 买得起的 Dbms向现有 Dbms 外的接程序必须面向广泛，设计一个垂直应用程序使用 Dbms。  
  
 选择目标 Dbms 时, 应考虑台式机和服务器数据库之间的差异。 桌面数据库，如 dBASE、 Paradox 和 Btrieve 没有那么强大比服务器的数据库。 因为它们通常通过较不强大的 SQL 引擎中大多数基于文件的驱动程序进行访问，它们通常缺少完整事务的支持、 支持较少的并发用户，并具有有限的 SQL。 但是，它们是成本较低，并且具有较大的客户的群。  
  
 例如 Oracle、 DB2 和 SQL Server 的服务器数据库提供完整的事务支持，支持许多并发用户，并具有丰富的 SQL。 它们是昂贵得多，并且具有较小的客户的群。 但是，往往更高版本，某种程度上偏移较小的潜在市场软件价格。  
  
 因此，可以根据所需的应用程序和应用程序的目标市场的功能选择有时目标 Dbms。 例如，大型公司的订单输入系统不可能针对桌面数据库，因为这些缺少足够的事务支持。 对于小型企业设计的类似系统中可能排除基于成本的多数服务器数据库。 和通用应用程序的开发人员可能都但避免使用在服务器数据库中的高级的功能。

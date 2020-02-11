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
ms.openlocfilehash: 7065aa88d60a508df9946d38d0dded220c4bb7a1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68106143"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>确定目标 DBMS 和驱动程序
要考虑的下一个问题是，应用程序的目标 Dbms 是什么，哪些驱动程序可支持这些 Dbms？ 由于一般应用程序的互操作性很高，因此目标 Dbms 的问题最适用于自定义应用程序和垂直应用程序。 但是，目标驱动程序的问题适用于所有应用程序，因为驱动程序的速度、质量、功能支持和可用性多种多样。 此外，如果驱动程序要随应用程序一起重新分发，则需要考虑许可计划的成本和可用性。  
  
 对于许多自定义应用程序，目标 Dbms 明显如下：应用程序设计为可访问的现有 Dbms。 还应考虑计划未来迁移的 Dbms。 但是，这些应用程序的主要问题是与它们一起使用的驱动程序和驱动程序。 对于其他自定义应用程序（这些应用程序未设计为访问现有 DBMS），可以根据功能支持、并发用户支持、驱动程序可用性和经济性来选择目标 Dbms。  
  
 对于垂直应用程序，通常会根据功能支持、驱动程序可用性和市场选择目标 Dbms。 例如，为小型企业设计的垂直应用程序必须针对那些企业经济实惠的 Dbms;作为现有 Dbms 的外接程序而设计的垂直应用程序必须针对广泛使用的 Dbms。  
  
 选择目标 Dbms 时，应考虑桌面数据库和服务器数据库之间的差异。 桌面数据库（如 dBASE、Paradox 和 Btrieve）的功能低于服务器数据库。 由于通常是通过大多数基于文件的驱动程序中的不太强大的 SQL 引擎来访问它们，因此它们通常缺乏完全事务支持、支持更少的并发用户以及具有有限的 SQL。 但是，它们的价格较低，并且已安装一个较大的基准。  
  
 Oracle、DB2 和 SQL Server 等服务器数据库提供完全事务支持、支持许多并发用户以及具有丰富的 SQL。 它们的成本更高，且安装更小。 另一方面，软件价格往往较高，而有些则会抵消较小的潜在市场。  
  
 因此，有时可以根据应用程序所需的功能和应用程序的目标目标 Dbms 选择目标 Dbms。 例如，大型公司的订单输入系统可能不会以桌面数据库为目标，因为这种情况缺乏足够的事务支持。 为小型企业设计的类似系统可能会根据成本排除大多数服务器数据库。 一般应用程序的开发人员可能以这两者为目标，但要避免使用在服务器数据库中找到的高级功能。

---
title: SqlClient 中的数据发现和分类
description: 介绍如何检查 SQL Server 数据库是否支持数据分类，以及如何通过 SqlDataReader 对象访问数据分类信息。
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: 27b9c232fe785d3c016848f3bb952236b8e7cd75
ms.sourcegitcommit: 6b3569977b034554883a94d73d1c4df6e2f74fe2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2020
ms.locfileid: "85110095"
---
# <a name="data-discovery-and-classification-in-sqlclient"></a>SqlClient 中的数据发现和分类

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

[数据发现和分类](https://docs.microsoft.com/sql/relational-databases/security/sql-data-discovery-and-classification?view=sql-server-2017)是一组高级服务，可用于发现数据库中的敏感数据并对其进行分类、标记和报告。 在基础数据源支持的情况下，SqlClient 会提供一个可公开只读“数据发现和分类”信息的 API。 可通过 SqlDataReader 访问此信息。

此示例应用程序演示如何访问 SqlDataReader 的数据分类属性。

[!code-csharp [SqlDataReader_DataDiscoveryAndClassification#1](~/../sqlclient/doc/samples/SqlDataReader_DataDiscoveryAndClassification.cs#1)]

**另请参阅**  

 [SQL Server 功能和 ADO.NET](sql-server-features-adonet.md)   

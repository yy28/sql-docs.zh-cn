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
ms.openlocfilehash: 6d82bfd3c49576a35b24f5a04cdc2c03dceeb766
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081496"
---
# <a name="data-discovery-and-classification-in-sqlclient"></a>SqlClient 中的数据发现和分类

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

[数据发现和分类](../../../relational-databases/security/sql-data-discovery-and-classification.md)是一组高级服务，可用于发现数据库中的敏感数据并对其进行分类、标记和报告。 在基础数据源支持的情况下，SqlClient 会提供一个可公开只读“数据发现和分类”信息的 API。 可通过 SqlDataReader 访问此信息。

此示例应用程序演示如何访问 SqlDataReader 的数据分类属性。

[!code-csharp [SqlDataReader_DataDiscoveryAndClassification#1](~/../sqlclient/doc/samples/SqlDataReader_DataDiscoveryAndClassification.cs#1)]

**另请参阅**  

 [SQL Server 功能和 ADO.NET](sql-server-features-adonet.md)
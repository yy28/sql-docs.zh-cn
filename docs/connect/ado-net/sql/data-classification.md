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
ms.openlocfilehash: b53e71c4c302145af14c1f2e37f30fe0e3c8f8e2
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725718"
---
# <a name="data-discovery-and-classification-in-sqlclient"></a>SqlClient 中的数据发现和分类

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

[数据发现和分类](../../../relational-databases/security/sql-data-discovery-and-classification.md?view=sql-server-2017)是一组高级服务，可用于发现数据库中的敏感数据并对其进行分类、标记和报告。 在基础数据源支持的情况下，SqlClient 会提供一个可公开只读“数据发现和分类”信息的 API。 可通过 SqlDataReader 访问此信息。

此示例应用程序演示如何访问 SqlDataReader 的数据分类属性。

[!code-csharp [SqlDataReader_DataDiscoveryAndClassification#1](~/../sqlclient/doc/samples/SqlDataReader_DataDiscoveryAndClassification.cs#1)]

**另请参阅**  

 [SQL Server 功能和 ADO.NET](sql-server-features-adonet.md)
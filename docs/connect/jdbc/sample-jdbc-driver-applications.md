---
title: 示例 JDBC 驱动程序应用程序
description: JDBC Driver for SQL Server 示例应用程序展示了在使用 JDBC 驱动程序时可以使用的各种功能，以及可以遵循的良好编程做法。
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e136b87c-a138-45d6-8c3e-bcef94b7e483
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 17479d32cd752650b4bfb1d03f5bc36ab52d8ca4
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915911"
---
# <a name="sample-jdbc-driver-applications"></a>示例 JDBC 驱动程序应用程序

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 示例应用程序展示了 JDBC 驱动程序的各项功能。 此外，还展示了在结合使用 JDBC 驱动程序和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库时可以遵循的最佳编程做法。

所有示例应用程序都包含在 *.java 代码文件中，它们可以在您的本地计算机上编译和运行，并且位于以下位置中的不同子文件夹下：

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples
```

此部分的主题说明了如何配置和运行示例应用程序，还包括了对示例应用程序所说明内容的讨论。

## <a name="in-this-section"></a>在本节中

| 主题                                                                            | 说明                                                                                                                                                                                                                                                             |
| -------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [连接和检索数据](connecting-and-retrieving-data.md)              | 这些示例应用程序展示了如何连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。 此外，还展示了各种用于从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库检索数据的方法。 |
| [使用数据类型 &#40;JDBC&#41;](working-with-data-types-jdbc.md)        | 这些示例应用程序展示了如何使用 JDBC 驱动程序数据类型方法来处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的数据。                                                                                           |
| [使用结果集](working-with-result-sets.md)                          | 这些示例应用程序展示了如何使用结果集来处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的数据。                                                                                                         |
| [处理大型数据](working-with-large-data.md)                            | 这些示例应用程序展示了如何使用自适应缓冲从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库检索大值数据，同时免去服务器游标开销。                                                      |
| [SQL 数据发现和分类](data-discovery-classification-sample.md) | 此示例应用程序展示了如何使用 JDBC 驱动程序从 ResultSet 对象检索 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中包含的数据发现和分类信息。                                         |

## <a name="see-also"></a>另请参阅

[JDBC 驱动程序概述](overview-of-the-jdbc-driver.md)

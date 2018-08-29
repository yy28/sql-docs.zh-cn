---
title: 示例 JDBC 驱动程序应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e136b87c-a138-45d6-8c3e-bcef94b7e483
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: affc0c18f38ca45e572a65d92a204457025ccd55
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42783988"
---
# <a name="sample-jdbc-driver-applications"></a>示例 JDBC 驱动程序应用程序

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 示例应用程序展示了 JDBC 驱动程序的各项功能。 此外，还展示了在结合使用 JDBC 驱动程序和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库时可以遵循的最佳编程做法。  
  
所有示例应用程序都包含在 *.java 代码文件中，它们可以在您的本地计算机上编译和运行，并且位于以下位置中的不同子文件夹下：  

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples  
```

 此部分的主题说明了如何配置和运行示例应用程序，还包括了对示例应用程序所说明内容的讨论。  
  
## <a name="in-this-section"></a>本节内容  
  
| 主题                                                                                                                  | 描述                                                                                                                                                                                                                                                                   |
| ---------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [连接和检索数据](../../../connect/jdbc/code-samples/connecting-and-retrieving-data.md)                              | 这些示例应用程序展示了如何连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库。 此外，还展示了各种用于从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库检索数据的方法。 |
| [使用数据类型 &#40;JDBC&#41;](../../../connect/jdbc/code-samples/working-with-data-types-jdbc.md)                        | 这些示例应用程序展示了如何使用 JDBC 驱动程序数据类型方法来处理 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库中的数据。                                                                                              |
| [使用结果集](../../../connect/jdbc/code-samples/working-with-result-sets.md)                                          | 这些示例应用程序展示了如何使用结果集来处理 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库中的数据。                                                                                                            |
| [处理大型数据](../../../connect/jdbc/code-samples/working-with-large-data.md)                                            | 这些示例应用程序展示了如何使用自适应缓冲从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库检索大值数据，同时免去服务器游标开销。                                                         |
| [SQL 数据发现和分类](../../jdbc/code-samples/data-discovery-and-classification-sample.md) | 此示例应用程序演示了如何检索的数据发现和分类的信息包含在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]从 ResultSet 对象使用 JDBC 驱动程序的数据库。                                            |
  
## <a name="see-also"></a>另请参阅

[JDBC 驱动程序的概述](../../../connect/jdbc/overview-of-the-jdbc-driver.md)
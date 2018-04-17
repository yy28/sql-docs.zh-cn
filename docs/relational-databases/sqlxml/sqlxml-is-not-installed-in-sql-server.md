---
title: 在 SQL Server 中未安装 SQLXML |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 72c84ff3e8de0ebadd25441ed8723be19c5f0777
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>SQL Server 中未安装 SQLXML
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之前，SQLXML 4.0 随 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一起发布，是所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本（[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 除外）默认安装的一部分。 从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 开始，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不再包括 SQLXML 的最新版本 (SQLXML 4.0 SP1)。 若要安装 SQLXML 4.0 SP1，请从[SQLXML 4.0 SP1 的安装位置](https://www.microsoft.com/en-us/download/details.aspx?id=30403)。  
  
 如果应用程序在运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和需要 SQLXML 4.0，你必须下载并安装 SQLXML 4.0 SP1。  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>在使用 SQLOLEDB 和 SQL Server Native Client OLE DB 访问接口的新数据类型时 SQLXML 4.0 SP1 的行为  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 引入了以下使用 SQLXML 的开发人员可能想要使用的数据类型：  
  
-   **日期**  
  
-   **Time**  
  
-   **DateTime2**  
  
-   **DateTimeOffset**  
  
 使用具有任一 SQLOLEDB SQLXML 4.0 SP1 时或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 从[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，这些类型会显示为字符串转换为开发人员。 SQLXML 4.0 SP1 将作为内置标量类型一起使用时启用这些四个新的数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口 11.0 或更高版本。 在下载 SQLXML 4.0 SP1 之前，将这些类型映射到非字符串类型可能会导致截断某些数据。 例如，映射**DateTime2**到**xsd:date**将导致数据截断为[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] **DateTime**的 3.33 毫秒精度。  
  
## <a name="see-also"></a>另请参阅  
 [SQLXML 4.0 编程概念](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)  
  
  

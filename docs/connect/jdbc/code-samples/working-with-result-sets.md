---
title: 使用结果集 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4fc4b1c6-3075-4ad7-9244-865d9ede7ae6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab423f616a782816415a551104c62c53e62591b6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="working-with-result-sets"></a>使用结果集
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  当你处理中包含的数据的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据库的操作数据的一种方法是使用结果集。 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]支持使用的结果集通过[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。 通过使用 SQLServerResultSet 对象，可以检索的 SQL 语句或存储的过程返回的数据，根据需要更新的数据，然后将持久保存数据回数据库。  
  
 此外，SQLServerResultSet 对象提供用于在数据其行中导航、 获取或设置它包含的数据以及在基础数据库中建立不同级别的更改的敏感性方法。  
  
> [!NOTE]  
>  有关管理结果集，包括其敏感度到更改，请参阅[管理使用 JDBC 驱动程序的结果集](../../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)。  
  
 本部分中的主题介绍你可以使用结果集来操作中包含的数据的不同方式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据库。  
  
## <a name="in-this-section"></a>本節內容  
  
|主题|Description|  
|-----------|-----------------|  
|[结果集数据检索示例](../../../connect/jdbc/retrieving-result-set-data-sample.md)|介绍如何使用结果集要从中检索数据[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据库并将其显示。|  
|[结果集数据修改示例](../../../connect/jdbc/modifying-result-set-data-sample.md)|介绍如何使用某一结果集插入、 检索和修改数据在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据库。|  
|[结果集数据缓存示例](../../../connect/jdbc/caching-result-set-data-sample.md)|介绍如何使用某一结果集检索大量数据从[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据库，以及如何将该数据缓存在客户端的控件。|  
  
## <a name="see-also"></a>另请参阅  
 [示例 JDBC 驱动程序应用程序](../../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  

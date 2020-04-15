---
title: SQL 外键 |微软文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLForeignKeys function
ms.assetid: 6c01ce0d-30d7-4c86-8705-3ab254d8a845
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b934ec05cf5f7b908efe83eeeb68bb358cd45156
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298472"
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过外键约束机制支持级联更新和删除操作。 如果在 FOREIGN KEY 约束的 ON UPDATE 和/或 ON DELETE 子句中指定 CASCADE 选项，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将为 UPDATE_RULE 和/或 DELETE_RULE 列返回 SQL_CASCADE。 如果未在 FOREIGN KEY 约束的 ON UPDATE 和/或 ON DELETE 子句中指定 NO ACTION 选项，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 则为 UPDATE_RULE 和/或 DELETE_RULE 列返回 SQL_NO_ACTION。  
  
 当任何**SQL 外键**参数中存在无效值时 **，SQL 外键**在执行时返回SQL_SUCCESS。 当在这些参数中使用无效值时 **，SQLFetch**将返回SQL_NO_DATA。  
  
 **SQL 外交密钥**可以在静态服务器游标上执行。 尝试在可向上（动态或键集）游标上执行**SQL 外键**将返回SQL_SUCCESS_WITH_INFO指示游标类型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序通过接受*FKCatalogName*和*PKCatalogName*参数的两部分名称 *（Linked_Server_Name.Catalog_Name*）支持报告链接服务器上的表的信息。  
  
## <a name="see-also"></a>另请参阅  
 [SQL 外键函数](https://go.microsoft.com/fwlink/?LinkId=59344)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  

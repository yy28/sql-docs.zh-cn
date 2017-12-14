---
title: "Oracle 发布服务器的数据类型映射 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], data type mapping
- data types [SQL Server replication], Oracle publishing
- mapping data types [SQL Server replication]
ms.assetid: 6da0e4f4-f252-4b7e-ba60-d2e912aa278e
caps.latest.revision: "47"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 8c754c1796f76236b5efeda3f53bb785c8daf76f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="data-type-mapping-for-oracle-publishers"></a>Oracle 发布服务器的数据类型映射
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Oracle 数据类型并非与 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型完全匹配。 如果可能，在发布 Oracle 表时会自动选择匹配的数据类型。 在单一数据类型映射不清晰的情况下，提供备用的数据类型映射。 有关如何选择备用映射的信息，请参阅本主题后面的“指定备用数据类型映射”部分。  
  
 下表显示了将数据从 Oracle 发布服务器移动到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器时，在 Oracle 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之间数据类型的默认映射情况。 “备用”列指示备用映射是否可用。  
  
|Oracle 数据类型|SQL Server 数据类型|备用|  
|----------------------|--------------------------|------------------|  
|BFILE|VARBINARY(MAX)|是|  
|BLOB|VARBINARY(MAX)|是|  
|CHAR([1-2000])|CHAR([1-2000])|是|  
|CLOB|VARCHAR(MAX)|是|  
|DATE|DATETIME|是|  
|FLOAT|FLOAT|是|  
|FLOAT([1-53])|FLOAT([1-53])|是|  
|FLOAT([54-126])|FLOAT|是|  
|INT|NUMERIC(38)|是|  
|INTERVAL|DATETIME|是|  
|LONG|VARCHAR(MAX)|是|  
|LONG RAW|IMAGE|是|  
|NCHAR([1-1000])|NCHAR([1-1000])|是|  
|NCLOB|NVARCHAR(MAX)|是|  
|NUMBER|FLOAT|是|  
|NUMBER([1-38])|NUMERIC([1-38])|是|  
|NUMBER([0-38],[1-38])|NUMERIC([0-38],[1-38])|是|  
|NVARCHAR2([1-2000])|NVARCHAR([1-2000])|是|  
|RAW([1-2000])|VARBINARY([1-2000])|是|  
|REAL|FLOAT|是|  
|ROWID|CHAR(18)|是|  
|TIMESTAMP|DATETIME|是|  
|TIMESTAMP(0-7)|DATETIME|是|  
|TIMESTAMP(8-9)|DATETIME|是|  
|TIMESTAMP(0-7) WITH TIME ZONE|VARCHAR(37)|是|  
|TIMESTAMP(8-9) WITH TIME ZONE|VARCHAR(37)|是|  
|TIMESTAMP(0-7) WITH LOCAL TIME ZONE|VARCHAR(37)|是|  
|TIMESTAMP(8-9) WITH LOCAL TIME ZONE|VARCHAR(37)|是|  
|UROWID|CHAR(18)|是|  
|VARCHAR2([1-4000])|VARCHAR([1-4000])|是|  
  
## <a name="considerations-for-data-type-mapping"></a>数据类型映射注意事项  
 在从 Oracle 数据库复制数据时需注意下列数据类型问题。  
  
### <a name="unsupported-data-types"></a>不支持的数据类型  
 不支持以下数据类型，具有这些类型的列无法进行复制：  
  
-   对象类型  
  
-   XML 类型  
  
-   Varray  
  
-   嵌套表  
  
-   使用 REF 的列  
  
### <a name="the-date-data-type"></a>DATE 数据类型  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的日期范围为自公元 1753 年 到公元 9999 年，而 Oracle 中的日期范围为自公元前 4712 年 到公元 4712 年。 如果类型为 DATE 的列包含超出 SQL Server 范围的值，则为该列选择备用数据类型 VARCHAR(19)。  
  
### <a name="float-and-number-types"></a>FLOAT 和 NUMBER 类型  
 在 FLOAT 和 NUMBER 数据类型映射期间指定的小数位数和精度取决于为 Oracle 数据库中使用该数据类型的列指定的小数位数和精度。 精度指数字的位数。 小数位数指小数点后的数字位数。 例如，数 123.45 的精度是 5，小数位数是 2。  
  
 Oracle 允许定义小数位数大于精度的数，如 NUMBER(4,5)，但 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 要求精度等于或大于小数位数。 为了确保不发生数据截断，如果在 Oracle 发布服务器上出现小数位数大于精度的情况，则会在映射数据类型时将精度设置为等于小数位数，例如 NUMBER(4,5) 将映射为 NUMERIC(5,5)。  
  
> [!NOTE]  
>  如果未指定 NUMBER 的小数位数和精度， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将默认使用最大的小数位数 (8) 和精度 (38)。 建议您在 Oracle 中设置特定小数位数和精度，以在复制数据时能够改善存储和性能。  
  
### <a name="large-object-types"></a>大型对象类型  
 Oracle 最多支持 4 GB，而 SQL Server 最多支持 2 GB。 大于 2 GB 的复制数据会被截断。  
  
 如果 Oracle 表中包括一个 BFILE 列，则该列的数据将存储在文件系统中。 必须使用以下语法授予复制管理用户帐户对存储数据的目录的访问权限：  
  
 `GRANT READ ON DIRECTORY <directory_name> TO <replication_administrative_user_schema>`  
  
 有关大型对象类型的详细信息，请参阅 [Oracle 发布服务器的设计注意事项和限制](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)中的“大型对象注意事项”部分。  
  
## <a name="specifying-alternative-data-type-mappings"></a>指定备用数据类型映射  
 通常，默认数据类型映射便可满足需要，但对于许多 Oracle 数据类型，您可以从一组备用映射中选择数据类型映射来代替默认映射。 指定备用映射的方式有两种：  
  
-   使用存储过程或新建发布向导覆盖每个项目上的默认数据类型映射。  
  
-   使用存储过程全局更改所有将来项目的默认数据类型映射（不更改现有项目的默认数据类型映射）。  
  
 若要指定备用数据类型映射，请参阅 [Specify Data Type Mappings for an Oracle Publisher](../../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)。  
  
## <a name="see-also"></a>另请参阅  
 [配置 Oracle 发布服务器](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle 发布服务器的设计注意事项和限制](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  

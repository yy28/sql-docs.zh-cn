---
title: Unicode 压缩的实现 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-data-compression
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Unicode data compression
- compression [SQL Server], Unicode data
ms.assetid: 44e69e60-9b35-43fe-b9c7-8cf34eaea62a
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 53c1b66b26fe785fe932870f02ff67326c335e31
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026782"
---
# <a name="unicode-compression-implementation"></a>Unicode 压缩的实现
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 Unicode 标准压缩方案 (SCSU) 算法实现来压缩在行或页压缩对象中存储的 Unicode 值。 对于这些压缩对象，Unicode 压缩对于 `nchar(n)` 和 `nvarchar(n)` 列而言是自动的。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 将 Unicode 数据存储为 2 个字节，无论区域设置如何。 这称为 UCS-2 编码。 对于某些区域设置而言，在 SQL Server 中实现 SCSU 压缩可节省高达 50% 的存储空间。  
  
## <a name="supported-data-types"></a>支持的数据类型  
 Unicode 压缩支持固定长度 `nchar(n)` 和 `nvarchar(n)` 数据类型。 存储于行外或 `nvarchar(max)` 列中的数据值不压缩。  
  
> [!NOTE]  
>  不支持 Unicode 压缩`nvarchar(max)`即使行中存储数据。 但是，此数据类型仍可以从页压缩中受益。  
  
## <a name="upgrading-from-earlier-versions-of-sql-server"></a>从 SQL Server 的早期版本升级  
 在某一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]时，将不会对任何数据库对象（无论是压缩的还是未压缩的）进行与 Unicode 压缩相关的更改。 在数据库升级后，对象会受到影响，如下所示：  
  
-   如果该对象未压缩，则不会进行更改，并且对象继续像以前一样工作。  
  
-   行或页压缩的对象继续像以前那样工作。 未压缩的数据将一直保持未压缩的形式，直到其值被更新。  
  
-   插入行或页压缩表的新行使用 Unicode 压缩进行压缩。  
  
    > [!NOTE]  
    >  为了充分利用 Unicode 压缩的好处，必须使用页或行压缩重新生成对象。  
  
## <a name="how-unicode-compression-affects-data-storage"></a>Unicode 压缩影响数据存储的方式  
 在创建或重新生成某一索引时，或者在使用行或页压缩进行压缩的表中更改某一值时，只有在其压缩大小小于其当前大小时，受影响的索引或值才以压缩的形式存储。 这样可避免表或索引中的行由于 Unicode 压缩而增大。  
  
 压缩节省的存储空间取决于所压缩数据的特性和数据的区域设置。 下表列出了可以为若干区域设置节省的空间。  
  
|区域设置|压缩百分比|  
|------------|-------------------------|  
|英语|50%|  
|德语|50%|  
|Hindi|50%|  
|土耳其语|48%|  
|越南语|39%|  
|日语|15%|  
  
## <a name="see-also"></a>请参阅  
 [数据压缩](data-compression.md)   
 [sp_estimate_data_compression_savings (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql)   
 [页压缩的实现](page-compression-implementation.md)   
 [sys.dm_db_persisted_sku_features (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-persisted-sku-features-transact-sql)  
  
  

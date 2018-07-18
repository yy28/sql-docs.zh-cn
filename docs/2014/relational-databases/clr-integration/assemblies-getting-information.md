---
title: 获取有关程序集的信息 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], metadata
- status information [SQL Server], assemblies
- metadata [SQL Server], assemblies
ms.assetid: 6aa7f18e-baad-4481-9777-8c3b230b392f
caps.latest.revision: 19
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 592d0e86353179377a73c24da84ed8f21a8e48e7
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37349489"
---
# <a name="getting-information-about-assemblies"></a>获取有关程序集的信息
  可以查询下列目录视图和函数来获取有关程序集的元数据。  
  
 **若要获取有关各个程序集信息**  
  
-   [ASSEMBLYPROPERTY &#40;Transact SQL&#41;](/sql/t-sql/functions/assemblyproperty-transact-sql)  
  
 **若要获取数据库中的所有程序集的信息**  
  
-   [sys.assemblies &#40;Transact SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assemblies-transact-sql)  
  
 **若要获取有关程序集文件，包括程序集二进制文件的信息源文件，并调试文件**  
  
-   [sys.assembly_files &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-files-transact-sql)  
  
 **若要获取有关跨程序集引用的信息**  
  
-   [sys.assembly_references &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-references-transact-sql)  
  
 **若要获取有关用户定义类型的程序集信息**  
  
-   [sys.assembly_types &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-types-transact-sql)  
  
-   [sys.types (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-types-transact-sql)  
  
 **若要获取程序集信息有关公共语言运行时 (CLR) 存储过程、 触发器和函数**  
  
-   [sys.assembly_modules (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)  
  
 **若要获取有关非 CLR 对象的信息**  
  
-   [sys.sql_modules (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)  
  
## <a name="see-also"></a>请参阅  
 [程序集&#40;数据库引擎&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [设计程序集](../../relational-databases/clr-integration/assemblies-designing.md)   
 [实现程序集](assemblies-implementing.md)  
  
  

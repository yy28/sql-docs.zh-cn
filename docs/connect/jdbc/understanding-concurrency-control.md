---
title: 了解并发控制 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 98b7dabe-9b12-4e1d-adeb-e5b5cb0c96f3
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 71ca87537cef389ac6cedb47b21a39ce76ba1b97
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="understanding-concurrency-control"></a>了解并发控制
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  并发控制指的是当多个用户同时更新行时，用于保护数据库完整性的各种技术。 并发机制不正确可能导致脏读、虚拟读取和不可重复读等问题。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供的接口连接到使用的所有并发技术[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]若要解决这些问题。  
  
> [!NOTE]  
>  有关详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]的并发程度，请参阅中的"管理并发数据访问"[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]联机丛书。  
  
## <a name="remarks"></a>注释  
 JDBC 驱动程序支持以下并发类型：  
  
|并发类型|特征|行锁|Description|  
|----------------------|---------------------|---------------|-----------------|  
|CONCUR_READ_ONLY|只读|否|不允许通过游标进行更新，并且针对组成结果集的行不持有锁。|  
|CONCUR_UPDATABLE|乐观读写|否|数据库假定未必会发生行争用现象，但存在这种可能性。 使用时间戳比较来检查行完整性。|  
|CONCUR_SS_SCROLL_LOCKS|悲观读写|是|数据库假定可能会发生行争用现象。 通过行锁定来确保行完整性。|  
|CONCUR_SS_OPTIMISTIC_CC|乐观读写|否|数据库假定未必会发生行争用现象，但存在这种可能性。 使用时间戳比较来验证行的完整性。<br /><br /> 有关[!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]和更高版本，服务器将会更改此到 CONCUR_SS_OPTIMISTIC_CCVAL 如果表不包含时间戳列。<br /><br /> 有关[!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)]，即使指定乐观 WITH VALUES 如果基础表具有时间戳列，使用开放式使用行版本控制。 如果指定了 OPTIMISTIC WITH ROW VERSIONING 并且表不具有时间戳，则使用 OPTIMISTIC WITH VALUES。|  
|CONCUR_SS_OPTIMISTIC_CCVAL|乐观读写|否|数据库假定未必会发生行争用现象，但存在这种可能性。 使用行数据比较来检查行完整性。|  
  
## <a name="result-sets-that-are-not-updateable"></a>不可更新的结果集  
 可更新的结果集是指可以在其中插入、更新和删除行的结果集。 在以下情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]无法创建可更新的游标。 生成的异常为“结果集不可更新”。  
  
|原因|Description|补救措施|  
|-----------|-----------------|------------|  
|语句不是使用 JDBC 2.0（或更高版本）语法创建的|JDBC 2.0 引入了新的方法来创建语句。 如果使用 JDBC 1.0 语法，则结果集默认为只读。|创建语句时，指定结果集类型和并发机制。|  
|语句是使用 TYPE_SCROLL_INSENSITIVE 创建的|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 创建静态快照游标。 这将从基础表行中断开连接，以帮助保护游标，从而防止其他用户进行更新。|将 TYPE_SCROLL_SENSITIVE、TYPE_SS_SCROLL_KEYSET、TYPE_SS_SCROLL_DYNAMIC 或 TYPE_FORWARD_ONLY 用于 CONCUR_UPDATABLE 以避免创建静态游标。|  
|表设计排除了 KEYSET 或 DYNAMIC 游标。|基础表没有唯一键，若要启用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]以唯一标识行。|向表中添加唯一键，以便为每行提供唯一的标识。|  
  
## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序管理结果集](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  

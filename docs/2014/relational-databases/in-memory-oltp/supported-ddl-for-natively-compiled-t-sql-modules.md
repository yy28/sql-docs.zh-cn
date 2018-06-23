---
title: 在本机编译存储过程上支持构造 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6b21f47e-bceb-4054-8b3c-9d39bb9583c0
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: c54f811f2257adcb5c08f1741018be3211c1e874
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138192"
---
# <a name="supported-constructs-on-natively-compiled-stored-procedures"></a>在本机编译存储过程支持的结构
  本主题列出了本机编译的存储过程中支持的构造。  
  
 有关不支持的构造的信息，请参阅[内存中 OLTP 不支持的 Transact-SQL 构造](transact-sql-constructs-not-supported-by-in-memory-oltp.md)。  
  
## <a name="procedure-ddl"></a>过程 DDL  
 支持以下各项：  
  
-   CREATE PROCEDURE  
  
-   DROP PROCEDURE  
  
-   SCHEMABINDING（对于本机编译存储过程是必需的）  
  
-   NATIVE_COMPILATION  
  
-   可将参数声明为 NOT NULL。  
  
-   表值参数。  
  
## <a name="security"></a>Security  
 支持以下各项：  
  
-   用于过程：EXECUTE AS OWNER、SELF 和 USER。  
  
-   表和过程的 GRANT 和 DENY 权限。  
  
## <a name="see-also"></a>请参阅  
 [本机编译的存储过程](natively-compiled-stored-procedures.md)  
  
  
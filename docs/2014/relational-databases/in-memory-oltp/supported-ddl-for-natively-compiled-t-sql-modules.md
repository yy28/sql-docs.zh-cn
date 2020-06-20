---
title: 本机编译的存储过程支持的构造 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6b21f47e-bceb-4054-8b3c-9d39bb9583c0
author: rothja
ms.author: jroth
ms.openlocfilehash: ba83dbb706b674581a35d5927639208adc061122
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025649"
---
# <a name="supported-constructs-on-natively-compiled-stored-procedures"></a>本机编译的存储过程支持的构造
  本主题列出了本机编译的存储过程中支持的构造。  
  
 有关不支持的构造的信息，请参阅 [内存中 OLTP 不支持的 Transact-SQL 构造](transact-sql-constructs-not-supported-by-in-memory-oltp.md)。  
  
## <a name="procedure-ddl"></a>过程 DDL  
 支持以下各项：  
  
-   CREATE PROCEDURE  
  
-   DROP PROCEDURE  
  
-   SCHEMABINDING（对于本机编译存储过程是必需的）  
  
-   NATIVE_COMPILATION  
  
-   可将参数声明为 NOT NULL。  
  
-   表值参数。  
  
## <a name="security"></a>安全性  
 支持以下各项：  
  
-   用于过程：EXECUTE AS OWNER、SELF 和 USER。  
  
-   表和过程的 GRANT 和 DENY 权限。  
  
## <a name="see-also"></a>另请参阅  
 [本机编译的存储过程](natively-compiled-stored-procedures.md)  
  
  

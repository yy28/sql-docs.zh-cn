---
title: SQLSTATE （ODBC 错误代码） |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- ODBC error handling, cause information
- messages [ODBC], cause information
- SQLSTATEs
- errors [ODBC], cause information
ms.assetid: 84cce528-edb0-473f-a85f-3eb87fbe2cf3
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6fd38e5eb03e99ad1b2e9385cc3680c227065862
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35697168"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE（ODBC 错误代码）
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  SQLSTATE 提供与警告或错误的原因有关的详细信息。 在数据发生的错误源检测到，并且返回的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序将返回的本机错误号映射到相应的 SQLSTATE。 如果本机错误号没有要映射到，ODBC 错误代码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序返回 SQLSTATE 42000 （"语法错误或访问冲突"）。 检测到的驱动程序，错误[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序生成适当的 SQLSTATE。  
  
 有关状态错误代码的详细信息，请参阅下面的主题：  
  
-   [附录 A：ODBC 错误代码](http://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [SQLSTATE 映射](http://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>请参阅  
 [处理错误和消息](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  

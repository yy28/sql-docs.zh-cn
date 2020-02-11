---
title: SQLSTATE （ODBC 错误代码） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 162f6ff15a95c1839ef59b10c659935b687aeb59
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "73783208"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE（ODBC 错误代码）
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQLSTATE 提供与警告或错误的原因有关的详细信息。 对于在检测并返回的数据源中发生的错误[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native Client ODBC 驱动程序将返回的本机错误号映射到相应的 SQLSTATE。 如果本机错误号没有要映射到的 ODBC 错误代码，则 native Client ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驱动程序将返回 SQLSTATE 42000 （"语法错误或访问冲突"）。 对于驱动程序检测到的错误， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驱动程序将生成相应的 SQLSTATE。  
  
 有关状态错误代码的详细信息，请参阅下面的主题：  
  
-   [附录 A：ODBC 错误代码](https://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [SQLSTATE 映射](https://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>另请参阅  
 [处理错误和消息](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  

---
title: 本机错误号 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, native error numbers
- SQL Server Native Client ODBC driver, errors
- native error numbers [SQL Server Native Client]
- messages [ODBC], native error numbers
- errors [ODBC], native error numbers
ms.assetid: 77cbc826-f47f-4803-8e7a-223d6df069b1
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b1bc1f9383ab615a24b0506b86cf0ec5e37b6c74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "73783405"
---
# <a name="native-error-numbers"></a>本机错误号
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  对于数据源中发生的错误（由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回）， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native Client ODBC 驱动程序返回由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回的本机错误号。 对于驱动程序检测到的错误， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驱动程序返回本机错误号0。 有关本机错误号列表的详细信息，请参阅中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **master**数据库中**sysmessages**系统表的错误列。  
  
 有关状态错误代码的信息，请参阅[SQLSTATE &#40;ODBC 错误代码&#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md)。 对于网络库返回的错误，本机错误号来自于基础网络软件。  
  
## <a name="see-also"></a>另请参阅  
 [处理错误和消息](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  

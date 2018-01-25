---
title: SQLParamData | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: SQLParamData function
ms.assetid: 92349482-ea22-4a6a-8484-e9c6566794fa
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8654eda16ddea81bd1d28a7bc02b24a8b5c487b3
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="sqlparamdata"></a>SQLParamData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  当 SQLParamData 返回*ValuePtrPtr*与表值参数相关联，该应用程序应调用与 SQLPutData *StrLen_Or_Ind*。 如果*StrLen_Or_Ind*具有值大于 0，这意味着应用程序是否准备好进行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端来收集的下一步的表值参数行的参数数据。 如果*StrLen_Or_Ind*具有值为 0，意味着有更多的行的表值参数的数据。 有关详细信息，请参阅[绑定和 Data Transfer of Table-Valued 参数和列的值](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)。  
  
 有关表值参数的详细信息，请参阅[表值参数 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLParamData](http://go.microsoft.com/fwlink/?LinkId=80706)   
 [ODBC API 实现详细信息](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  

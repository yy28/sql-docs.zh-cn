---
title: SQLParamData | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLParamData function
ms.assetid: 92349482-ea22-4a6a-8484-e9c6566794fa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 79285523ec83d3f10ad6f23010a7f9a6398e5980
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890109"
---
# <a name="sqlparamdata"></a>SQLParamData
  当 SQLParamData 返回与表值参数关联的*ValuePtrPtr*时, 应用程序应调用 SQLPutData 和*StrLen_Or_Ind*。 如果*StrLen_Or_Ind*的值大于 0, 则表示应用程序已准备就绪, 可供[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 收集下一个表值参数行的参数数据。 如果*StrLen_Or_Ind*的值为 0, 则表示表值参数没有更多的数据行。 有关详细信息, 请参阅[表值参数和列值的绑定和数据传输](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)。  
  
 有关表值参数的详细信息, 请参阅[表值参数&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLParamData](/sql/odbc/reference/syntax/sqlparamdata-function)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  

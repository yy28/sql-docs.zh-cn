---
title: SQLParamData |Microsoft Docs
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
ms.openlocfilehash: da50163b90d4a871c2524e1723797474386be8f6
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356213"
---
# <a name="sqlparamdata"></a>SQLParamData
  当返回 SQLParamData *ValuePtrPtr*与表值参数关联，应用程序应调用使用 SQLPutData *StrLen_Or_Ind*。 如果*StrLen_Or_Ind*的值大于 0，则意味着该应用程序准备好进行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 收集下一个表值参数行的参数数据。 如果*StrLen_Or_Ind*具有值为 0，这意味着没有更多的行的表值参数的数据。 有关详细信息，请参阅[绑定和 Data Transfer of Table-Valued 参数和列值](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)。  
  
 有关表值参数的详细信息，请参阅[表值参数&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLParamData](https://go.microsoft.com/fwlink/?LinkId=80706)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  

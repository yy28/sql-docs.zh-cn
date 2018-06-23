---
title: SQLParamData |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLParamData function
ms.assetid: 92349482-ea22-4a6a-8484-e9c6566794fa
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: bd3fefeaa05f806650b58d1778658fda0ed63fa2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028131"
---
# <a name="sqlparamdata"></a>SQLParamData
  当 SQLParamData 返回*ValuePtrPtr*与表值参数相关联，该应用程序应调用与 SQLPutData *StrLen_Or_Ind*。 如果*StrLen_Or_Ind*具有值大于 0，这意味着应用程序是否准备好进行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端来收集的下一步的表值参数行的参数数据。 如果*StrLen_Or_Ind*具有值为 0，意味着有更多的行的表值参数的数据。 有关详细信息，请参阅[绑定和 Data Transfer of Table-Valued 参数和列的值](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)。  
  
 有关表值参数的详细信息，请参阅[表值参数&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLParamData](http://go.microsoft.com/fwlink/?LinkId=80706)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
---
title: 表值参数数据转换及其他错误和警告 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), data conversion
- table-valued parameters (ODBC), error messages
ms.assetid: edd45234-59dc-4338-94fc-330e820cc248
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf8506311d0d95ac9d0f8eedc7632379b6bd9ce0
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37431866"
---
# <a name="table-valued-parameter-data-conversion-and-other-errors-and-warnings"></a>表值参数数据转换及其他错误和警告
  表值参数列值可按照与其他列和参数值相同的方式在客户端和服务器数据类型之间转换。 但是由于表值参数可以包含多个列和多个行，所以必须能够标识出现错误的实际值，这一点很重要。  
  
 当在表值参数列中检测到错误或警告时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 将生成诊断记录。 错误消息将包含表值参数的参数编号，以及列序号和行号。 应用程序还可以使用诊断记录中的诊断字段 SQL_DIAG_SS_TABLE_COLUMN_NUMBER 和 SQL_DIAG_SS_TABLE_ROW_NUMBER 确定与错误和警告关联的值。 这些诊断字段在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本中提供。  
  
 诊断记录的 SQLSTATE 和消息部分将在所有其他方面符合现有的 ODBC 行为。 也就是说，除参数、行和列标识信息之外，表值参数与非表值参数具有相同的错误消息值。  
  
## <a name="see-also"></a>请参阅  
 [表值参数&#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  

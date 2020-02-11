---
title: 表值参数数据转换和其他错误和警告 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), data conversion
- table-valued parameters (ODBC), error messages
ms.assetid: edd45234-59dc-4338-94fc-330e820cc248
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 576e8e49411412264afc5828fe606a19cc3751f6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62468250"
---
# <a name="table-valued-parameter-data-conversion-and-other-errors-and-warnings"></a>表值参数数据转换及其他错误和警告
  表值参数列值可按照与其他列和参数值相同的方式在客户端和服务器数据类型之间转换。 但是由于表值参数可以包含多个列和多个行，所以必须能够标识出现错误的实际值，这一点很重要。  
  
 当在表值参数列中检测到错误或警告时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 将生成诊断记录。 错误消息将包含表值参数的参数编号，以及列序号和行号。 应用程序还可以使用诊断记录中的诊断字段 SQL_DIAG_SS_TABLE_COLUMN_NUMBER 和 SQL_DIAG_SS_TABLE_ROW_NUMBER 确定与错误和警告关联的值。 这些诊断字段在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本中提供。  
  
 诊断记录的 SQLSTATE 和消息部分将在所有其他方面符合现有的 ODBC 行为。 也就是说，除了参数、行和列标识信息外，错误消息对于表值参数具有相同的值，这与非表值参数的值相同。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC&#41;&#40;表值参数](table-valued-parameters-odbc.md)  
  
  

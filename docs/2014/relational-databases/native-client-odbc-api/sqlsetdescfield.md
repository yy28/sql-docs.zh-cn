---
title: SQLSetDescField |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLSetDescField function
ms.assetid: de4bed15-15be-4825-994c-1046255e725a
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5810760fc0cbc8aba9a1ea743f1dab33df501964
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37414306"
---
# <a name="sqlsetdescfield"></a>SQLSetDescField
  SQLSetDescField 可以用于设置表值参数和表值参数列的描述符字段。 有关可用字段的信息，请参阅[表值参数描述符字段](../native-client-odbc-table-valued-parameters/table-valued-parameter-descriptor-fields.md)并[表值参数构成列的描述符字段](../native-client-odbc-table-valued-parameters/descriptor-fields-for-table-valued-parameter-constituent-columns.md)。  
  
## <a name="remarks"></a>Remarks  
 表值参数列仅在将描述符标头字段 SQL_SOPT_SS_PARAM_FOCUS 设置为特定记录（其 SQL_DESC_TYPE 设置为 SQL_SS_TABLE）的序数时可用。 有关 SQL_SOPT_SS_PARAM_FOCUS 的详细信息，请参阅[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
 如果尝试将 SQL_SOPT_SS_PARAM_FOCUS 设置为不是表值参数的参数的序号，SQLSetStmtAttr 返回 SQL_ERROR，并且诊断记录创建具有 SQLSTATE = HY024 和消息"属性值无效"。 返回 SQL_ERROR 时，不更改 SQL_SOPT_SS_PARAM_FOCUS。  
  
 将 SQL_SOPT_SS_PARAM_FOCUS 设置为 0 可以恢复对参数的描述符记录的访问权限。  
  
 有关表值参数的详细信息，请参阅[表值参数&#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlsetdescfield-support-for-enhanced-date-and-time-features"></a>SQLSetDescField 对日期和时间增强功能的支持  
 ODBC 中已增强了日期/时间功能。 有关为新的日期/时间类型提供的描述符字段的信息，请参阅[参数和结果元数据](../native-client-odbc-date-time/metadata-parameter-and-result.md)。  
  
 有关详细信息，请参阅[日期和时间改进&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlsetdescfield-support-for-large-clr-udts"></a>SQLSetDescField 对大型 CLR UDT 的支持  
 SQLSetDescField 支持大型 CLR 用户定义类型 (Udt)。 有关详细信息，请参阅[Large CLR User-Defined 类型&#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="sqlsetdescfield-support-for-sparse-columns"></a>SQLSetDescField 对稀疏列的支持  
 SQLSetDecField 可以用于将 SQL_SOPT_SS_NAME_SCOPE 设置为值 SQL_SS_NAME_SCOPE_EXTENDED 和 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET 应用程序参数描述符 (APD) 中。  
  
 有关详细信息，请参阅[稀疏列支持&#40;ODBC&#41;](../native-client/odbc/sparse-columns-support-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLSetDescField](http://go.microsoft.com/fwlink/?LinkId=80705)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  

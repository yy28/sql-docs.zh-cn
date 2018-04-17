---
title: 表值参数类型发现 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
ms.assetid: f55818c2-ebb5-4cf6-8c0c-0da41f592560
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1a02771d253aa140fda52ae19ca983a463d4b7f8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="table-valued-parameter-type-discovery"></a>表值参数类型发现
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  使用者-即，客户端应用程序使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口 — 可以发现每个命令参数的类型，如果已将命令文本提供给 OLE DB 访问接口。 表值参数的类型未未知后，使用者可以发现表值参数的各个列的元数据信息。  
  
 对于大多数参数类型，ICommandWithParameters::GetParameterInfo 支持过程参数的类型信息。 开头[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，与用户定义的类型的简介和**xml**数据类型，GetParameterInfo 方法不是为此目的足够因为它不是可以提供用户定义的类型通过 ICommandWithParameters 的信息 （名称、 架构和目录）。 定义新接口，ISSCommandWithParameters，是为了提供扩展的类型信息。  
  
 对于表值参数，你还使用 ISSCommandWithParameters 接口发现的详细的信息。 在准备命令对象后，客户端调用 ISSCommandWithParameters::GetParameterInfo。 有关表值参数， *wType* DBPARAMINFO 结构中的成员设置为 DBTYPE_TABLE 提供程序。 *UlParamSize* DBPARAMINFO 结构字段的值为 ~ 0。  
  
 使用者将通过使用 ISSCommandWithParamters 然后请求其他属性 （表值参数类型目录名称、 表值参数类型架构名称、 表值参数类型名称、 列排序和默认列）::GetParameterProperties。  
  
 已知的类型名称后，若要检索使用者必须调用的单个列信息 IOpenRowset::OpenRowsetor 获取 DBSCHEMA_TABLE_TYPE_COLUMNS 行集通过指定表值参数类型名称作为表名。  
  
## <a name="see-also"></a>另请参阅  
 [表值参数&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [使用表值参数 & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  

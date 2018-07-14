---
title: 表值参数类型发现 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
ms.assetid: f55818c2-ebb5-4cf6-8c0c-0da41f592560
caps.latest.revision: 20
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 021109d32ceed7055348aea0bb0cb9ac32a4c7c8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37231947"
---
# <a name="table-valued-parameter-type-discovery"></a>表值参数类型发现
  使用者 — 也就是说，客户端应用程序中使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口 — 如果已将命令文本提供给 OLE DB 访问接口可以发现每个命令参数的类型。 表值参数的类型已知时后，使用者可以发现表值参数各列的元数据信息。  
  
 对于大多数参数类型，icommandwithparameters:: Getparameterinfo 支持过程参数的类型信息。 开头[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，与引入了用户定义的类型和`xml`数据类型，GetParameterInfo 方法未实现此目的足够因为它不能提供用户定义类型信息 (名称、 架构和目录） 通过 ICommandWithParameters。 新接口，ISSCommandWithParameters，定义为提供的扩展的类型信息。  
  
 对于表值参数，你还使用 ISSCommandWithParameters 接口发现详细的信息。 客户端调用 ISSCommandWithParameters::GetParameterInfo 准备命令对象之后。 对于表值参数， *wType*访问接口将 DBPARAMINFO 结构中的成员设置为 DBTYPE_TABLE。 *UlParamSize* DBPARAMINFO 结构字段的值为 ~ 0。  
  
 使用者然后会使用 ISSCommandWithParamters 请求附加属性 （表值参数类型目录名称、 表值参数类型架构名称、 表值参数类型名称、 列排序和默认列）::GetParameterProperties。  
  
 已知的类型名称后，若要检索各个列信息使用者必须调用 IOpenRowset::OpenRowsetor 获取 DBSCHEMA_TABLE_TYPE_COLUMNS 行集表值参数类型名称指定为表名。  
  
## <a name="see-also"></a>请参阅  
 [表值参数&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [使用表值参数&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  

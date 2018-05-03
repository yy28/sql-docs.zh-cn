---
title: DefaultDatabase 属性 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::DefaultDatabase
helpviewer_keywords:
- DefaultDatabase property
ms.assetid: 41e8a8dd-e69c-4a09-8736-93502e01961c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a62362ea626155c002a291185c935163b1126e28
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="defaultdatabase-property"></a>DefaultDatabase 属性
指示的默认数据库[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字符串**从提供程序的计算结果为可用的数据库的名称的值。  
  
## <a name="remarks"></a>注释  
 使用**DefaultDatabase**属性来设置或返回的默认数据库的名称对特定**连接**对象。  
  
 如果没有默认数据库，SQL 字符串可以使用非限定的语法来访问该数据库中的对象。 之外中指定的数据库中访问对象**DefaultDatabase**属性，必须限定对象名称的所需的数据库名称。 在连接时提供程序将写入到的默认数据库信息**DefaultDatabase**属性。 某些访问接口允许每个连接只有一个数据库，在这种情况下不能更改**DefaultDatabase**属性。  
  
 某些数据源和提供程序可能不支持此功能，并且可能会返回错误或空字符串。  
  
> [!NOTE]
>  **远程数据服务使用情况**此属性不是可在客户端上**连接**对象。  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [提供程序和 DefaultDatabase 属性示例 (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Provider 和 DefaultDatabase 属性示例 (VC++)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vc.md)   

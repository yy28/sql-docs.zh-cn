---
title: DefaultDatabase 属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::DefaultDatabase
helpviewer_keywords:
- DefaultDatabase property
ms.assetid: 41e8a8dd-e69c-4a09-8736-93502e01961c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2cd93826e03f7767455ec4b656ed14d1c35c21d2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47757446"
---
# <a name="defaultdatabase-property"></a>DefaultDatabase 属性
指示的默认数据库[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字符串**从提供程序的计算结果为可用的数据库名称的值。  
  
## <a name="remarks"></a>备注  
 使用**DefaultDatabase**属性设置或返回的默认数据库的名称在特定**连接**对象。  
  
 如果没有默认数据库，SQL 字符串可能会使用非限定的语法来访问该数据库中的对象。 访问数据库中的对象中指定以外**DefaultDatabase**属性，必须限定对象名称的所需的数据库名称。 连接后，该提供程序会将默认数据库信息写入**DefaultDatabase**属性。 某些提供程序允许每个连接只有一个数据库，在这种情况下不能更改**DefaultDatabase**属性。  
  
 某些数据源和提供程序可能不支持此功能，并且可能会返回错误或空字符串。  
  
> [!NOTE]
>  **远程数据服务使用情况**客户端上，此属性不可**连接**对象。  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Provider 和 DefaultDatabase 属性示例 (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Provider 和 DefaultDatabase 属性示例 (VC++)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vc.md)   

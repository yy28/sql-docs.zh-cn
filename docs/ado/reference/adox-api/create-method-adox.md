---
description: Create 方法 (ADOX)
title: Create Method (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::raw_Create
- _Catalog::Create
helpviewer_keywords:
- Create method [ADOX]
ms.assetid: 64f5c21c-b581-42d8-bdc7-c4f1bebaf105
author: rothja
ms.author: jroth
ms.openlocfilehash: b5add8972d95413841a6c9c45de2dcc26d8cbb24
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770836"
---
# <a name="create-method-adox"></a>Create 方法 (ADOX)
创建新的目录。  
  
## <a name="syntax"></a>语法  
  
```  
  
Catalog.Create ConnectString  
```  
  
#### <a name="parameters"></a>parameters  
 *ConnectString*  
 用于连接到数据源的 **字符串** 值。  
  
## <a name="remarks"></a>备注  
 **Create**方法创建新的 ADO 连接并打开与*ConnectString*中指定的数据源的[连接](../ado-api/connection-object-ado.md)。 如果成功，新 **连接** 对象将分配给 [ActiveConnection](./activeconnection-property-adox.md) 属性。  
  
 如果提供程序不支持创建新目录，则会发生错误。  
  
## <a name="applies-to"></a>适用于  
 [目录对象 (ADOX)](./catalog-object-adox.md)  
  
## <a name="see-also"></a>另请参阅  
 [Create Method (VB) ](./create-method-example-vb.md)   
 [ActiveConnection 属性 (ADOX)](./activeconnection-property-adox.md)
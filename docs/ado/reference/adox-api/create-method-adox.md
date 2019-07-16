---
title: 创建方法 (ADOX) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aafcab3ad379dc25a2681a5d4f0d3f5e8d6eab5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966671"
---
# <a name="create-method-adox"></a>Create 方法 (ADOX)
创建一个新目录。  
  
## <a name="syntax"></a>语法  
  
```  
  
Catalog.Create ConnectString  
```  
  
#### <a name="parameters"></a>Parameters  
 *ConnectString*  
 一个**字符串**值，该值用于连接到数据源。  
  
## <a name="remarks"></a>备注  
 **创建**方法创建并打开新的 ADO[连接](../../../ado/reference/ado-api/connection-object-ado.md)到数据源中指定*ConnectString*。 如果成功，新**连接**对象分配给[ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md)属性。  
  
 如果提供程序不支持创建新的目录，将会出错。  
  
## <a name="applies-to"></a>适用范围  
 [目录对象 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>请参阅  
 [Create 方法示例 (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [ActiveConnection 属性 (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)

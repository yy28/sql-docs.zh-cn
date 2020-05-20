---
title: PageSize 属性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::PageSize
helpviewer_keywords:
- PageSize property [ADO]
ms.assetid: e57930a6-46c4-4a17-a3b6-f79e94d5c9c7
author: rothja
ms.author: jroth
ms.openlocfilehash: 97902985dcd2110b165498be5324393ad5588bac
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761966"
---
# <a name="pagesize-property-ado"></a>PageSize 属性 (ADO)
指示记录[集中](../../../ado/reference/ado-api/recordset-object-ado.md)有一页的记录数。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个**长整型**值，该值指示页上有多少记录。 默认值为**10**。  
  
## <a name="remarks"></a>备注  
 使用**PageSize**属性来确定构成逻辑页数据的记录数。 通过建立页面大小，可以使用[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)属性移动到特定页面的第一条记录。 当你希望允许用户逐页浏览数据，一次查看一定数量的记录时，这非常有用。  
  
 此属性可随时设置，它的值将用于计算特定页面的第一条记录的位置。  
  
## <a name="applies-to"></a>应用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [AbsolutePage、PageCount 和 PageSize 属性示例（VB）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、PageCount 和 PageSize 属性示例（VC + +）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePage 属性（ADO）](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [PageCount 属性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)

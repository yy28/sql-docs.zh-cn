---
title: "MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (RDS) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- MoveLast method [RDS]
- MovePrevious method [RDS]
- MoveFirst method [RDS]
- MoveNext method [RDS]
ms.assetid: 45c80bb5-136f-4204-9df2-78740fa55574
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ae28d49a51d2bd4dbf516a7cc96bbf20381ccdfe
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-rds"></a>MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (RDS)
将移动到第一个，最后，在指定的下一步，或上一个记录[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
DataControl.Recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
#### <a name="parameters"></a>Parameters  
 *DataControl*  
 表示的对象变量[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。  
  
## <a name="remarks"></a>注释  
 你可以使用**移动**方法**rds.DataControl**对象来浏览网页上的数据绑定控件中的数据记录。 例如，假设你显示**记录集**在通过绑定到网格中**rds.DataControl**对象。 然后，可以包括名、 姓、 下一步和上一步按钮可供用户单击与第一个移动、 最后、 下一步，或在所显示的上一条记录**记录集**。 执行此操作通过调用**MoveFirst**， **MoveLast**， **MoveNext**，和**MovePrevious**方法**rds.DataControl**分别对象名、 姓、 下一步和上一步按钮的 onClick 过程中。 [通讯簿示例](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)演示如何执行此操作。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [Move 方法 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [移动记录方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)




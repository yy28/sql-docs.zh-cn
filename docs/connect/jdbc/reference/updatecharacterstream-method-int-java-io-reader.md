---
title: updateCharacterStream 方法 （int、 java.io.Reader） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4dddf885-0482-4776-8e9a-69f6c6270931
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c24424c7c7f4183293871a39bb8eb04d72dacd05
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32848244"
---
# <a name="updatecharacterstream-method-int-javaioreader"></a>updateCharacterStream 方法 (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用字符流值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateCharacterStream(int columnIndex,  
                                  java.io.Reader x)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnIndex  
  
 指示列索引的 int。  
  
 *x*  
  
 一个读取器对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 updateCharacterStream 方法指定此 updateCharacterStream 方法。  
  
 此方法将从读取器对象的 Unicode 字符传递到所选的文本和二进制列。 这包括所有文本列和**二进制**， **varbinary**， **varbinary （max)**，**映像**，和**xml**列，但不是**udt**列。  
  
 使用此方法对于**映像**，**文本**，和**ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据类型可能会影响性能。  
  
## <a name="see-also"></a>另请参阅  
 [updateCharacterStream 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

---
title: updateCharacterStream 方法 (int, java.io.Reader) | Microsoft Docs
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
ms.openlocfilehash: 58980081aafd10046b9268a6d23d62b7c1990c00
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784160"
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
  
## <a name="remarks"></a>Remarks  
 此 updateCharacterStream 方法由 java.sql.ResultSet 接口中的 updateCharacterStream 方法指定。  
  
 此方法将来自 Reader 对象的 Unicode 字符传递给所选文本和二进制列。 这包括所有文本列与 binary、varbinary、varbinary(max)、image 和 xml 列，但不包括 udt 列。  
  
 使用此方法对于**图像**，**文本**，并**ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型可能会影响性能。  
  
## <a name="see-also"></a>另请参阅  
 [updateCharacterStream 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

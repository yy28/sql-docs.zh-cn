---
title: setCharacterStream 方法 (SQLServerClob) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.setCharacterStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c02778f2-6681-4a84-a58b-2bcfac4233e4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: da842fbc6240b072c7fe907aaa344d8d2ff1c6e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974650"
---
# <a name="setcharacterstream-method-sqlserverclob"></a>setCharacterStream 方法 (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回用来将 Unicode 字符流写入起始于给定位置的 CLOB 的流。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.io.Writer setCharacterStream(long pos)  
```  
  
#### <a name="parameters"></a>Parameters  
 pos   
  
 开始写入 CLOB 对象的位置。  
  
## <a name="return-value"></a>返回值  
 可向其中写入 Unicode 编码字符的流。  
  
## <a name="exceptions"></a>异常  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 此 setCharacterStream 方法由 setCharacterStream 方法在 Clob 接口中指定。  
  
 编写器从指定位置开始覆盖 CLOB 中的字符数据，并可以超过 CLOB 的初始长度。 指定“位置+1”值将追加字符。 指定“位置+2”或更大值（或零或更小值）会引发位置错误。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerClob 方法](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 成员](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 类](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  

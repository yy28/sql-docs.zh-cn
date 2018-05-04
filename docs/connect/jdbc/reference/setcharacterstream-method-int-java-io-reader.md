---
title: setCharacterStream 方法 （int、 java.io.Reader） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b8d4e1f7-14fc-4590-af98-1eda30d2ca6d
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7fa0e3edcc88e105f631105fb6d3735c6baa6348
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="setcharacterstream-method-int-javaioreader"></a>setCharacterStream 方法 (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定的参数设置为指定的 java.io.Reader 对象中。  
  
> [!NOTE]  
>  此功能引入开头[!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 驱动程序版本 2.0。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setCharacterStream(int parameterIndex,  
                              java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>Parameters  
 *parameterIndex*  
  
 **Int** ，该值指示参数号。  
  
 *读取器*  
  
 包含 Unicode 数据的 java.io.Reader 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.PreparedStatement 接口中的 setCharacterStream 方法指定此 setCharacterStream 方法。  
  
## <a name="see-also"></a>另请参阅  
 [setCharacterStream 方法&#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setcharacterstream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  

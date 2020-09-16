---
description: isSparseColumnSet 方法 (SQLServerResultSetMetaData)
title: isSparseColumnSet 方法 (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ac363670-78ae-49f1-aeda-4fba3329a258
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 86fbbcdc34259e6b3d783d34ca77af57bcfba89f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433369"
---
# <a name="issparsecolumnset-method-sqlserverresultsetmetadata"></a>isSparseColumnSet 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指示结果集中的某个列是否为稀疏列集。  
  
## <a name="syntax"></a>语法  
  
```scr  
public boolean isSparseColumnSet(int column)  
```  
  
#### <a name="parameters"></a>参数  
 *column*  
  
 列的（从 1 开始的）索引。  
  
## <a name="return-value"></a>返回值  
 如果结果集中的列为稀疏列集，则为 true****；否则为 false****。  
  
## <a name="remarks"></a>注解  
 此方法不从数据库中检索信息。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成员](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 类](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  

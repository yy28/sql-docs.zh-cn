---
title: "命令 (ADO-WFC 语法) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Command collection [ADO], ADO/WFC syntax
ms.assetid: 39d0aa06-03ac-4c9a-8400-83947756ef99
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 867ebe5a6eec1d340c0d02f77d8f5b687766ee89
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="command-ado---wfc-syntax"></a>命令 (ADO-WFC 语法)
## <a name="package-commswfcdata"></a>包 com.ms.wfc.data  
  
### <a name="constructor"></a>构造函数  
  
```  
public Command()  
public Command(String commandtext)  
```  
  
### <a name="methods"></a>方法  
  
```  
public void cancel()  
public com.ms.wfc.data.Parameter createParameter(String  
    Name, int Type, int Direction, int Size, Object Value)  
public Recordset execute()  
public Recordset execute(Object[] parameters)  
public Recordset execute(Object[] parameters, int options)  
public int executeUpdate(Object[] parameters)  
public int executeUpdate(Object[] parameters, int options)  
public int executeUpdate()  
```  
  
 **ExecuteUpdate**方法是一种特殊的大小写方法，调用基础 ADO**执行**带有某些参数的方法。 **ExecuteUpdate**方法不支持的返回**记录集**对象，因此**执行**方法的*选项*参数是使用修改**AdoEnums.ExecuteOptions.NORECORDS**。 后**执行**方法完成，其更新*RecordsAffected*参数被传递回**executeUpdate**方法，作为最后返回**int**。  
  
### <a name="properties"></a>属性  
  
```  
public com.ms.wfc.data.Connection getActiveConnection()  
public void setActiveConnection(com.ms.wfc.data.Connection con)  
public void setActiveConnection(String conString)  
public String getCommandText()  
public void setCommandText(String command)  
public int getCommandTimeout()  
public void setCommandTimeout(int timeout)  
public int getCommandType()  
public void setCommandType(int type)  
public String getName()  
public void setName(String name)  
public boolean getPrepared()  
public void setPrepared(boolean prepared)  
public int getState()  
public com.ms.wfc.data.Parameter getParameter(int n)  
public com.ms.wfc.data.Parameter getParameter(String n)  
public com.ms.wfc.data.Parameters getParameters()  
public AdoProperties getProperties()  
```  
  
## <a name="see-also"></a>另请参阅  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)


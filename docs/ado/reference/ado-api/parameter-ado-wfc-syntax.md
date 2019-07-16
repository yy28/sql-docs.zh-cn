---
title: 参数 (ADO-WFC 语法) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Parameter collection [ADO], ADO/WFC syntax
ms.assetid: d00d1e1e-14b1-41a2-a00f-2a3cb7396f15
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22f9d928cf008396346067a3e166fa281be4093d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931717"
---
# <a name="parameter-ado---wfc-syntax"></a>参数（ADO - WFC 语法）
## <a name="package-commswfcdata"></a>包 com.ms.wfc.data  
  
### <a name="constructor"></a>构造函数  
  
```  
public Parameter()  
public Parameter(String name)  
public Parameter(String name, int type)  
public Parameter(String name, int type, int dir)  
public Parameter(String name, int type, int dir, int size)  
public Parameter(String name, int type, int dir, int size, Object value)  
```  
  
### <a name="methods"></a>方法  
  
```  
public void appendChunk(byte[] bytes)  
public void appendChunk(char[] chars)  
public void appendChunk(String chars)  
```  
  
### <a name="properties"></a>properties  
  
```  
public int getAttributes()  
public void setAttributes(int attr)  
public int getDirection()  
public void setDirection(int dir)  
public String getName()  
public void setName(String name)  
public int getNumericScale()  
public void setNumericScale(int scale)  
public int getPrecision()  
public void setPrecision(int prec)  
public int getSize()  
public void setSize(int size)  
public int getType()  
public void setType(int type)  
public com.ms.com.Variant getValue()  
public void setValue(Object v)  
public AdoProperties getProperties()  
```  
  
## <a name="parameter-accessor-methods"></a>参数访问器方法  
 [值](../../../ado/reference/ado-api/value-property-ado.md)的属性[参数](../../../ado/reference/ado-api/parameter-object.md)对象获取或设置该对象的内容。 内容表示为变体，可以分配一个值的对象的类型和任意多个数据类型。  
  
 ADO/WFC 实现**值**具有属性**getValue**方法，该返回变体的对象; 方法并**setValue**方法，它使用作为参数的变体。 变体是在某些语言中，如 Microsoft Visual Basic 高效率。  
  
 除了**值**属性，提供了 ADO/WFC*访问器*方法使用 Java 数据类型来获取和设置的内容**参数**对象。 这些方法中的大多数其名称分别为窗体**获取**_数据类型_或**设置**_数据类型_。  
  
 还有一个值得注意的例外：没有任何**getNull**属性; 而是有**isNull**返回一个布尔值，该值指示字段是否为 null 的属性。  
  
```  
public boolean getBoolean()  
public void setBoolean(boolean v)  
public byte getByte()  
public void setByte(byte v)  
public double getDouble()  
public void setDouble(double v)  
public float getFloat()  
public void setFloat(float v)  
public int getInt()  
public void setInt(int v)  
public long getLong()  
public void setLong(long v)  
public short getShort()  
public void setShort(short v)  
public String getString()  
public void setString(String v)  
public boolean isNull()  
public void setNull()  
```  
  
## <a name="see-also"></a>请参阅  
 [参数对象](../../../ado/reference/ado-api/parameter-object.md)

---
title: "参数 (ADO-WFC 语法) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Parameter collection [ADO], ADO/WFC syntax
ms.assetid: d00d1e1e-14b1-41a2-a00f-2a3cb7396f15
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7006bc7073693cc70dcb8eebce1bd8998895a9e8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="parameter-ado---wfc-syntax"></a>参数 (ADO-WFC 语法)
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
  
### <a name="properties"></a>属性  
  
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
 [值](../../../ado/reference/ado-api/value-property-ado.md)属性[参数](../../../ado/reference/ado-api/parameter-object.md)对象获取或设置该对象的内容。 内容表示为一个变量，可以为其指定值的对象的类型和任何几种数据类型。  
  
 ADO/WFC 实现**值**具有属性**getValue**方法，返回的变体对象; 与**setValue**方法，后者采用 VARIANT 类型作为自变量。 变体，可以在某些语言中，如 Microsoft Visual Basic 高效率。  
  
 除了**值**属性，ADO/WFC 提供*访问器*使用 Java 数据类型来获取和设置的内容的方法**参数**对象。 具有窗体的名称，这些方法中的大多数**获取***DataType*或**设置***DataType*。  
  
 一种更具吸引力情况例外： 有没有**getNull**属性; 而是有**isNull**返回一个布尔值，该值指示字段是否为 null 的属性。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [参数对象](../../../ado/reference/ado-api/parameter-object.md)

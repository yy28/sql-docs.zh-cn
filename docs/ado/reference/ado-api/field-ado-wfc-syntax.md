---
title: 字段 (ADO-WFC 语法) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Field collection [ADO], ADO/WFC syntax
ms.assetid: 7e01cb24-2338-4f92-ad46-8d97248e1a4d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea2245c3f57b5ad3b14847f15791575afde1043c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63031964"
---
# <a name="field-ado---wfc-syntax"></a>字段（ADO - WFC 语法）
## <a name="package-commswfcdata"></a>package com.ms.wfc.data  
  
### <a name="methods"></a>方法  
  
```  
public void appendChunk(byte[] bytes)  
public void appendChunk(char[] chars)  
public void appendChunk(String chars)  
public byte[] getByteChunk(int len)  
public char[] getCharChunk(int len)  
public String getStringChunk(int len)  
```  
  
### <a name="properties"></a>属性  
  
```  
public int getActualSize()  
public int getAttributes()  
public void setAttributes(int pl)  
public com.ms.com.IUnknown getDataFormat()  
public void setDataFormat(com.ms.com.IUnknown format)  
```  
  
 （有关详细信息，请参阅 com.ms.wfc.data.IDataFormat 接口的文档）。  
  
```  
public int getDefinedSize()  
public void setDefinedSize(int pl)  
public String getName()  
public int getNumericScale()  
public void setNumericScale(byte pbNumericScale)  
public Variant getOriginalValue()  
public int getPrecision()  
public void setPrecision(byte pbPrecision)  
public int getType()  
public void setType(int pDataType)  
public Variant getUnderlyingValue()  
public Variant getValue()  
public void setValue(Variant value)  
public AdoProperties getProperties()  
```  
  
### <a name="field-accessor-methods"></a>字段访问器方法  
 [值](../../../ado/reference/ado-api/value-property-ado.md)的属性[字段](../../../ado/reference/ado-api/field-object.md)对象获取或设置该对象的内容。 内容表示为变体，可以分配一个值的对象的类型和任意多个数据类型。  
  
 ADO/WFC 实现**值**具有属性**getValue**方法，该返回变体的对象; 方法并**setValue**方法，它使用作为参数的变体。 变体是在某些语言中，如 Microsoft Visual Basic 高效率。  
  
 除了**值**属性，提供了 ADO/WFC*访问器*方法使用 Java 数据类型来获取和设置的内容**字段**对象。 这些方法中的大多数其名称分别为窗体**获取**_数据类型_或**设置**_数据类型_。  
  
 有两个值得注意的例外情况：之一**getObject**方法会返回强制转换为指定类的对象。 没有任何**getNull**属性; 而是有**isNull**返回一个布尔值，该值指示字段是否为 null 的属性。  
  
```  
public native boolean getBoolean();  
public void setBoolean(boolean v)  
public native byte getByte();  
public void setByte(byte v)  
public native byte[] getBytes();  
public void setBytes(byte[] v)  
public native double getDouble();  
public void setDouble(double v)  
public native float getFloat();  
public void setFloat(float v)  
public native int getInt();  
public void setInt(int v)  
public native long getLong();  
public void setLong(long v)  
public native short getShort();  
public void setShort(short v)  
public native String getString();  
public void setString(String v)  
public native boolean isNull();  
public void setNull()  
public Object getObject()  
public Object getObject(Class c)  
public void setObject(Object value)  
```  
  
## <a name="see-also"></a>请参阅  
 [字段对象](../../../ado/reference/ado-api/field-object.md)

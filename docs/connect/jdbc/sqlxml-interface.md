---
title: SQLXML 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7c67be98-efb5-446c-a0e3-ee67c43cb170
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2cb8975c4eda311b93c7a26c1d83eecbbfa581f4
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37991645"
---
# <a name="sqlxml-interface"></a>SQLXML 接口
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  JDBC 驱动程序提供对 JDBC 4.0 API 的支持，后者引入了 java.sql.SQLXML 接口。 SQLXML 接口定义与 XML 数据交互以及操作 XML 数据的方法。 **SQLXML**数据类型映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **xml**数据类型。  
  
 SQLXML 接口提供了用于访问形式的 XML 值的方法**字符串**即**读取器**或**编写器**，或作为**Stream**。 XML 值还可以通过 Source 来访问，或者设置为 Result，两者与 XML 分析器 API（如文档对象模型 (DOM)、Simple API for XML (SAX) 和 Streaming API for XML (StAX)）以及 XSLT 转换和 XPath 一起使用。  
  
## <a name="remarks"></a>Remarks  
 下表介绍了 SQLXML 接口中定义的方法：  
  
|方法语法|方法说明|  
|-------------------|------------------------|  
|[void free()](http://go.microsoft.com/fwlink/?LinkId=131685)|此方法释放 SQLXML 对象以及它所持有的资源。|  
|[InputStream getBinaryStream()](http://go.microsoft.com/fwlink/?LinkId=131754)|返回一个用于从 SQLXML 中读取数据的输入流。|  
|[Reader getCharacterStream()](http://go.microsoft.com/fwlink/?LinkId=131755)|将 XML 数据作为 java.io.Reader 对象或字符流返回。|  
|[T extends Source T getSource(Class\<T> sourceClass)](http://go.microsoft.com/fwlink/?LinkId=131756)|返回**源**进行读取**XML**指定此值**SQLXML**对象。<br /><br /> 注意：getSource 方法支持下列源：javax.xml.transform.dom.DOMSource、javax.xml.transform.sax.SAXSource、javax.xml.transform.stax.StAXSource 和 java.io.InputStream。|  
|[String getString()](http://go.microsoft.com/fwlink/?LinkId=131757)|返回此 SQLXML 对象所指定的 XML 值的字符串表示形式。|  
|[OutputStream setBinaryStream()](http://go.microsoft.com/fwlink/?LinkId=131758)|检索可用于写入此 SQLXML 对象所表示的 XML 值的流。|  
|[Writer setCharacterStream()](http://go.microsoft.com/fwlink/?LinkId=131759)|返回可用于写入此 SQLXML 对象所表示的 XML 值的流。|  
|[T extends Result T setResult(Class\<T> resultClass)](http://go.microsoft.com/fwlink/?LinkId=131760)|返回**结果**设置为**XML**指定此值**SQLXML**对象。<br /><br /> 注意：setResult 方法支持下列源：javax.xml.transform.dom.DOMResult、javax.xml.transform.sax.SAXResult、javax.xml.transform.stax.StaxResult 和 java.io.OutputStream。|  
|[void setString(String value)](http://go.microsoft.com/fwlink/?LinkId=131762)|将此 SQLXML 对象所指定的 XML 值设置为指定的字符串表示形式。|  
  
 应用程序只能从/向 SQLXML 对象中读取/写入 XML 值一次。  
  
 调用 free() 方法后，SQLXML 对象将变为无效，既不可读也不可写。 如果应用程序尝试对该 SQLXML 对象调用 free() 方法以外的方法，将引发异常。  
  
 SQLXML 对象将变为既不可读也可写应用程序调用任意以下 getter 方法时： getSource，getCharacterStream，getBinaryStream，和 getString。  
  
 SQLXML 对象将变为既不可写也可读时应用程序调用任意以下的 setter 方法： setResult、 setCharacterStream、 setBinaryStream，setString 和。  
  
## <a name="see-also"></a>另请参阅  
 [支持 XML 数据](../../connect/jdbc/supporting-xml-data.md)  
  
  

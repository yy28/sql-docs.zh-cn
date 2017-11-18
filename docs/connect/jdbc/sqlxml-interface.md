---
title: "SQLXML 接口 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7c67be98-efb5-446c-a0e3-ee67c43cb170
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7c636345439175c516b647a2951ac3bfa8824b06
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlxml-interface"></a>SQLXML 接口
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  JDBC 驱动程序提供对 JDBC 4.0 API 的支持，后者引入了 java.sql.SQLXML 接口。 SQLXML 接口定义进行交互并处理 XML 数据的方法。 **SQLXML**数据类型映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **xml**数据类型。  
  
 SQLXML 接口可提供用于访问作为的 XML 值的方法**字符串**、**读取器**或**编写器**，或被**流**。 XML 值也可以通过访问**源**或者设置为**结果**，用于使用 XML 分析器 Api，例如文档对象模型 (DOM)、 简单 API XML (SAX) 和流式处理 API for XML (StAX) 作为也能使用 XSLT 转换和 XPath。  
  
## <a name="remarks"></a>注释  
 下表介绍了 SQLXML 接口中定义的方法：  
  
|方法语法|方法说明|  
|-------------------|------------------------|  
|[void free （)](http://go.microsoft.com/fwlink/?LinkId=131685)|此方法释放 SQLXML 对象以及它所持有的资源。|  
|[InputStream getBinaryStream()](http://go.microsoft.com/fwlink/?LinkId=131754)|返回一个用于从 SQLXML 中读取数据的输入流。|  
|[读取器 getCharacterStream()](http://go.microsoft.com/fwlink/?LinkId=131755)|返回**XML**数据作为 java.io.Reader 对象或字符流。|  
|[T 扩展源 T getSource (类\<T > sourceClass)](http://go.microsoft.com/fwlink/?LinkId=131756)|返回**源**读取**XML**指定此值**SQLXML**对象。<br /><br /> **注意：** getSource 方法支持以下源： javax.xml.transform.dom.DOMSource、 javax.xml.transform.sax.SAXSource、 javax.xml.transform.stax.StAXSource 和 java.io.InputStream。|  
|[字符串 getString()](http://go.microsoft.com/fwlink/?LinkId=131757)|返回的字符串表示形式**XML**此 SQLXML 对象指定的值。|  
|[OutputStream setBinaryStream()](http://go.microsoft.com/fwlink/?LinkId=131758)|检索可以用于写入的流**XML**此 SQLXML 对象表示的值。|  
|[编写器 setCharacterStream()](http://go.microsoft.com/fwlink/?LinkId=131759)|返回要用于写入的流**XML**此 SQLXML 对象表示的值。|  
|[T 扩展结果 T setResult (类\<T > 等效)](http://go.microsoft.com/fwlink/?LinkId=131760)|返回**结果**设置**XML**指定此值**SQLXML**对象。<br /><br /> **注意：** setResult 方法支持以下源： javax.xml.transform.dom.DOMResult、 javax.xml.transform.sax.SAXResult、 javax.xml.transform.stax.StaxResult 和 java.io.OutputStream。|  
|[void setString(String value)](http://go.microsoft.com/fwlink/?LinkId=131762)|设置为指定此 SQLXML 对象指定的 XML 值**字符串**表示形式。|  
  
 应用程序只能从/向 SQLXML 对象中读取/写入 XML 值一次。  
  
 当调用 free （） 方法时，SQLXML 对象将变为无效，并且既不可读的也可写。 如果应用程序尝试调用以外 free （） 方法该 SQLXML 对象上的方法，将引发异常。  
  
 在 SQLXML 对象变为既不可读的也可写，当应用程序调用任何以下 getter 方法： getSource，getCharacterStream，getBinaryStream，和 getString。  
  
 在 SQLXML 对象变为既没有可写，也没有可读，当应用程序调用以下 setter 方法的任何： setResult，setCharacterStream，setBinaryStream，和 setString。  
  
## <a name="see-also"></a>另请参阅  
 [支持 XML 数据](../../connect/jdbc/supporting-xml-data.md)  
  
  


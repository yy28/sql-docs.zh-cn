---
title: 执行 XPath 查询 （sqlxmloledb 访问接口） 的命名空间与 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, executing XPath queries
- namespaces property
- queries [SQLXML], SQLXMLOLEDB Provider
- XPath queries [SQLXML], namespaces
- XPath queries [SQLXML], SQLXMLOLEDB Provider
- namespaces [SQLXML], XPath queries
ms.assetid: 024a4b7d-435d-47ba-9e80-2c2f640108f5
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d5a5149b56d98cc319a06b9cbb8129f7699a17fe
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37301727"
---
# <a name="executing-xpath-queries-with-namespaces-sqlxmloledb-provider"></a>执行带命名空间的 XPath 查询（SQLXMLOLEDB 访问接口）
  XPath 查询可以包含命名空间。 如果架构元素为限定命名空间（即，包含目标命名空间），则针对该架构的 XPath 查询必须指定该命名空间。  
  
 由于 SQLXML 4.0 中不支持使用通配符 (*)，因此必须使用命名空间前缀来指定 XPath 查询。 若要解决此前缀，使用命名空间属性指定命名空间绑定。  
  
 在以下示例中，XPath 查询指定命名空间使用通配符字符 (\*) 和 local-name （) and namespace-uri （) XPath 函数。 此 XPath 查询将返回其本地名称为 `Contact` 且其命名空间 URI 为 `urn:myschema:Contacts` 的所有元素。  
  
```  
/*[local-name() = 'Contact' and namespace-uri() = 'urn:myschema:Contacts']  
```  
  
 在 SQLXML 4.0 中，必须用命名空间前缀来指定此 XPath 查询。 例如，`x:Contact`，其中 `x` 为命名空间前缀。 请看以下 XSD 架构：  
  
```  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
            xmlns:con="urn:myschema:Contacts"  
            targetNamespace="urn:myschema:Contacts">  
<complexType name="ContactType">  
  <attribute name="CID" sql:field="ContactID" type="ID"/>  
  <attribute name="FName" sql:field="FirstName" type="string"/>  
  <attribute name="LName" sql:field="LastName"/>   
</complexType>  
<element name="Contact" type="con:ContactType" sql:relation="Person.Contact"/>  
</schema>  
```  
  
 由于此架构定义了目标命名空间，因此针对此架构的 XPath 查询（如“Employee”）必须包含该命名空间。  
  
 以下是一个 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 应用程序示例，针对前述 XSD 架构执行 XPath 查询 (x:Employee)。 若要解析此前缀，使用命名空间属性指定了命名空间绑定。  
  
> [!NOTE]  
>  在该代码中，必须在连接字符串中提供 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。 此外，本示例还指定使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) 作为数据访问接口，该访问接口需要安装其他网络客户端软件。 有关详细信息，请参阅[SQL Server Native Client 的系统要求](../../native-client/system-requirements-for-sql-server-native-client.md)。  
  
```  
Option Explicit  
Private Sub Form_Load()  
    Dim con As New ADODB.Connection  
    Dim cmd As New ADODB.Command  
    Dim stm As New ADODB.Stream  
    con.Open "provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Data Source=SqlServerName;Initial Catalog=AdventureWorks;Integrated Security=SSPI;"  
    Set cmd.ActiveConnection = con  
    stm.Open  
    cmd.Properties("Output Stream").Value = stm  
    cmd.Properties("Output Encoding") = "utf-8"  
    cmd.Properties("Mapping schema") = "C:\DirectoryPath\con-ex.xml"  
    cmd.Properties("namespaces") = "xmlns:x='urn:myschema:Contacts'"  
    '  Debug.Print "Set Command Dialect to DBGUID_XPATH"  
    cmd.Dialect = "{ec2a4293-e898-11d2-b1b7-00c04f680c56}"  
    cmd.CommandText = "x:Contact"  
    cmd.Execute , , adExecuteStream   
    stm.Position = 0  
    Debug.Print stm.ReadText(adReadAll)  
End Sub  
```  
  
### <a name="to-test-this-application"></a>测试此应用程序  
  
1.  将示例 XSD 架构保存到文件夹中。  
  
2.  创建 Visual Basic 可执行项目，并将代码复制到其中。 根据需要更改指定的目录路径。  
  
3.  添加以下项目引用：  
  
    ```  
    "Microsoft ActiveX Data Objects 2.8 Library"  
    ```  
  
4.  执行应用程序。  
  
 下面是部分结果：  
  
```  
<y0:Employee xmlns:y0="urn:myschema:Contacts"   
             LName="Achong" CID="1" FName="Gustavo"/>  
<y0:Employee xmlns:y0="urn:myschema:Employees"   
             LName="Abel" CID="2" FName="Catherine"/>  
```  
  
 在 XML 文档中生成的前缀是任意的，但都映射到同一个命名空间。  
  
  

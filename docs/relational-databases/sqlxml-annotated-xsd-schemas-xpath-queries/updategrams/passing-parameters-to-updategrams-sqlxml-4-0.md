---
title: 将参数传递给 Updategram (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- nullvalue attribute
- passing parameters [SQLXML]
- parameters [SQLXML]
- updategrams [SQLXML], passing parameters
- null values [SQLXML]
ms.assetid: 2354e6e7-1860-471f-8711-4e374c5a4ed2
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 501ee9f2bde6d77e8f07fcbdfa6a43a0fa6f3b3a
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041568"
---
# <a name="passing-parameters-to-updategrams-sqlxml-40"></a>将参数传递给 Updategram (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Updategram 为模板，因此您可以向其传递参数。 有关将参数传递给模板的详细信息，请参阅[Updategram 的安全注意事项&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)。  
  
 Updategram 允许您将 NULL 作为参数值传递。 若要将传递 NULL 参数值，指定**nullvalue**属性。 分配给的值**nullvalue**然后提供属性作为参数值。 Updategram 将该值视为 NULL。  
  
> [!NOTE]  
>  在 **\<sql:header >** 并 **\<updg:header >**，则应指定**nullvalue**为非限定; 而中**\<updg:sync >**，则指定**nullvalue**为限定 (例如， **updg: nullvalue**)。  
  
## <a name="examples"></a>示例  
 若要创建使用以下示例的工作示例，必须满足中指定的要求[运行 SQLXML 示例的要求](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
 在使用 updategram 示例前，请注意以下事项：  
  
-   此示例使用默认映射（即未在 updategram 中指定映射架构）。 有关使用映射架构的 updategram 的更多示例，请参阅[在 Updategram 中指定带批注的映射架构&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
### <a name="a-passing-parameters-to-an-updategram"></a>A. 将参数传递给 updategram  
 在本示例中，updategram 更改了 HumanResources.Shift 表中一位雇员的姓氏。 向 updategram 传递了两个参数：ShiftID，用于唯一标识轮班，并将命名。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:header>  
  <updg:param name="ShiftID"/>  
  <updg:param name="Name" />  
</updg:header>  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="$ShiftID" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="$Name" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>测试 updategram  
  
1.  将上面的 updategram 复制到记事本中并将其另存为 UpdategramWithParameters.xml 文件。  
  
2.  在中准备 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs)[使用 ADO 执行 SQLXML 4.0 查询](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)若要通过添加以下行后的执行 updategram `cmd.Properties("Output Stream").Value = outStream`:  
  
    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value  
    cmd.Parameters.Append cmd.CreateParameter("@ShiftID",  2, 1,  0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@Name",   200, 1, 50, "New Name")  
    ```  
  
### <a name="b-passing-null-as-a-parameter-value-to-an-updategram"></a>B. 将 NULL 作为参数值传递给 updategram  
 在执行 updategram 的过程中，会将“isnull”值赋给要设置为 NULL 的参数。 Updategram 将“isnulll”参数值转换为 NULL 并对其进行相应处理。  
  
 以下 updategram 将设置为 NULL 的员工标题：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:header nullvalue="isnull" >  
  <updg:param name="EmployeeID"/>  
  <updg:param name="ManagerID" />  
</updg:header>  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Employee EmployeeID="$EmployeeID" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Employee ManagerID="$ManagerID" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>测试 updategram  
  
1.  将上面的 updategram 复制到记事本中并将其另存为 UpdategramPassingNullvalues.xml 文件。  
  
2.  在中准备 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs)[使用 ADO 执行 SQLXML 4.0 查询](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)若要通过添加以下行后的执行 updategram `cmd.Properties("Output Stream").Value = outStream`:  
  
    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value   
    cmd.Parameters.Append cmd.CreateParameter("@EmployeeID", 3, 1, 0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@ManagerID",  3, 1, 0, Null)  
    ```  
  
## <a name="see-also"></a>请参阅  
 [Updategram 安全注意事项&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  

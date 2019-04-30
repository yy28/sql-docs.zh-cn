---
title: 创建和更改对象 (XMLA) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 86f52c2ea61b8b62ea9bfe5ffe6b3c7b06977740
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63231955"
---
# <a name="creating-and-altering-objects-xmla"></a>创建和更改对象 (XMLA)
  可以单独创建、更改和删除主要对象。 主要对象包括以下对象：  
  
-   服务器  
  
-   数据库  
  
-   维度  
  
-   多维数据集  
  
-   度量值组  
  
-   “度量值组”  
  
-   透视  
  
-   挖掘模型  
  
-   角色  
  
-   与服务器或数据库关联的命令  
  
-   数据源  
  
 您使用[创建](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)的实例上创建主要对象命令[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，和[Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)命令更改实例上的现有主要对象。 这两个命令使用运行[Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法。  
  
## <a name="creating-objects"></a>创建对象  
 通过使用创建对象时**创建**方法，必须首先标识包含父对象[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]要创建对象。 通过提供中的对象引用来标识父对象[ParentObject](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)的属性**创建**命令。 每个对象引用都包含唯一标识的父对象所需的对象标识符**创建**命令。 有关对象引用的详细信息，请参阅[定义和标识对象&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)。  
  
 例如，若要为某一多维数据集创建新的度量值组，则必须提供对该多维数据集的对象引用。 在多维数据集的对象引用**ParentObject**属性包含数据库标识符和多维数据集标识符，为同一个多维数据集标识符可能可以使用不同的数据库上。  
  
 [ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla)元素包含定义要创建的主要对象的 Analysis Services 脚本语言 (ASSL) 元素。 有关 ASSL 的详细信息，请参阅[使用 Analysis Services 脚本语言进行开发&#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)。  
  
 如果您设置**AllowOverwrite**的属性**创建**命令为 true 时，您可以覆盖具有指定的标识符的现有主要对象。 否则，如果具有指定标识符的主要对象仍存在于父对象中，则会发生错误。  
  
 有关详细信息**创建**命令，请参阅[创建元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)。  
  
### <a name="creating-session-objects"></a>创建会话对象  
 会话对象是一些临时对象，它们仅可用于客户端应用程序所使用的显式或隐式会话，且在会话结束后会删除这些会话对象。 您可以通过设置创建会话对象**作用域**的属性**创建**命令*会话*。  
  
> [!NOTE]  
>  使用时*会话*设置， **ObjectDefinition**元素只能包含[维度](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl)，[多维数据集](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl)，或[MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) ASSL 元素。  
  
## <a name="altering-objects"></a>更改对象  
 通过修改对象时**Alter**方法，必须首先标识要修改通过提供中的对象引用的对象[对象](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)属性**Alter**命令。 每个对象引用都包含唯一标识的对象所需的对象标识符**Alter**命令。 有关对象引用的详细信息，请参阅[定义和标识对象&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)。  
  
 例如，若要修改某一多维数据集的结构，必须提供对该多维数据集的对象引用。 在多维数据集的对象引用**对象**属性包含数据库标识符和多维数据集标识符，为同一个多维数据集标识符可能可以使用不同的数据库上。  
  
 **ObjectDefinition**元素包含定义要修改的主要对象的 ASSL 元素。 有关 ASSL 的详细信息，请参阅[使用 Analysis Services 脚本语言进行开发&#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)。  
  
 如果您设置**AllowCreate**的属性**Alter**命令为 true，如果不存在该对象可以创建指定的主要对象。 否则，如果指定的主要对象尚不存在，则会出现错误。  
  
### <a name="using-the-objectexpansion-attribute"></a>使用 ObjectExpansion 属性  
 如果您要更改仅主要对象的属性并不重新定义主要对象所包含的次要对象，则可以设置**ObjectExpansion**的属性**Alter**命令*ObjectProperties*。 **ObjectDefinition**属性然后只有包含该主要对象的属性的元素和**Alter**命令将保留不变的主要对象关联的次要对象。  
  
 若要重新定义的主要对象的次要对象，必须设置**ObjectExpansion**归于*ExpandFull*和对象定义必须包含该主要对象包含的所有次要对象。 如果**ObjectDefinition**的属性**Alter**命令未显式包括包含该主要对象的某一次要对象，将删除未包含该次要对象。  
  
### <a name="altering-session-objects"></a>更改会话对象  
 若要修改所创建的会话对象**创建**命令，将**作用域**的属性**Alter**命令*会话*。  
  
> [!NOTE]  
>  使用时*会话*设置， **ObjectDefinition**元素只能包含[维度](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl)，[多维数据集](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl)，或[MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) ASSL 元素。  
  
## <a name="creating-or-altering-subordinate-objects"></a>创建或更改从属对象  
 尽管**创建**或**Alter**命令创建或更改只有一个最顶层的主要对象，要创建或修改该主要对象可以包含在包含它的定义**ObjectDefinition**属于其他主要和次要对象的属性。 例如，如果定义多维数据集，则指定的父数据库中**ParentObject**，和的多维数据集定义中**ObjectDefinition**可以定义多维数据集，并在该度量值的度量值组组可以定义每个度量值组分区。 次要对象只能在其所属的主要对象下定义。 有关主要和次要对象的详细信息，请参阅[数据库对象&#40;Analysis Services-多维数据&#41;](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="description"></a>Description  
 下面的示例创建引用的关系数据源[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]示例[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。  
  
### <a name="code"></a>代码  
  
```  
<Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    </ParentObject>  
    <ObjectDefinition>  
        <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RelationalDataSource">  
            <ID>AdventureWorksDW2012</ID>  
            <Name>AdventureWorksDW2012</Name>  
            <ConnectionString>Data Source=localhost;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=True</ConnectionString>  
            <ImpersonationInfo>  
                <ImpersonationMode>ImpersonateServiceAccount</ImpersonationMode>  
            </ImpersonationInfo>  
            <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
            <Timeout>PT0S</Timeout>  
        </DataSource>  
    </ObjectDefinition>  
</Create>  
```  
  
### <a name="description"></a>Description  
 下面的示例对上例中创建的关系数据源进行了更改：将该数据源的查询超时设置为 30 秒。  
  
### <a name="code"></a>代码  
  
```  
<Alter ObjectExpansion="ObjectProperties" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DataSourceID>AdventureWorksDW2012</DataSourceID>  
    </Object>  
    <ObjectDefinition>  
        <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RelationalDataSource">  
            <ID>AdventureWorksDW2012</ID>  
            <Name>AdventureWorksDW2012</Name>  
            <ConnectionString>Data Source=fr-dwk-02;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=True</ConnectionString>  
            <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
            <Timeout>PT30S</Timeout>  
        </DataSource>  
    </ObjectDefinition>  
</Alter>  
```  
  
### <a name="comments"></a>注释  
 **ObjectExpansion**的属性**Alter**命令已设置为*ObjectProperties*。 此设置允许[ImpersonationInfo](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl)元素中，次要对象，若要从数据源中定义排除**ObjectDefinition**。 因此，该数据源的模拟信息仍设置为在第一个示例中所指定的服务帐户。  
  
## <a name="see-also"></a>请参阅  
 [执行方法&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)   
 [使用 Analysis Services 脚本语言 (ASSL) 开发](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [在 Analysis Services 中使用 XMLA 开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  

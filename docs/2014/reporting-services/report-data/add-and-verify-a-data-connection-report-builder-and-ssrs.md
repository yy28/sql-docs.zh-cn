---
title: 添加和验证数据连接或数据源 （报表生成器和 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1d3b2573-e29d-480d-9dde-d26379c86618
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4256a55f0dab891834aa633f4f06ca92f2c4c020
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37292177"
---
# <a name="add-and-verify-a-data-connection-or-data-source-report-builder-and-ssrs"></a>添加和验证数据连接或数据源（报表生成器和 SSRS）
  在报表生成器中，您可以从报表服务器添加共享数据源或为您的报表创建嵌入数据源。 在报表设计器中，您可以创建共享数据源或嵌入数据源，并且将其部署到报表服务器上。  
  
 若要将共享数据源添加到报表，请浏览报表服务器并选择共享数据源。 报表中的共享数据源指向报表服务器上的共享数据源定义。  
  
 若要创建嵌入数据源，您必须具有到外部数据源的连接信息并知道需要何种权限才能访问数据。 此信息通常来自数据源的所有者。 可以测试该连接以验证指定的凭据是否有效。  
  
 有关详细信息，请参阅[报表生成器中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)或[在报表生成器中指定凭据](../specify-credentials-in-report-builder.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-create-a-reference-to-a-shared-data-source"></a>创建对共享数据源的引用  
  
1.  在“报表数据”窗格的工具栏上，单击 **“新建”** ，然后单击 **“数据源”**。 此时将打开 **“数据源属性”** 对话框。  
  
2.  在 **“名称”** 文本框中，键入数据源的名称。  
  
    > [!NOTE]  
    >  此名称保存在本地报表定义中， 它不是报表服务器上共享数据源的名称。  
  
3.  选择 **“使用共享连接或报表模型”**。 将显示最近使用的共享数据源和报表模型的列表。 若要从报表服务器选择一个共享数据源，请单击 **“浏览”** 并找到报表服务器上包含共享数据源的文件夹。  
  
4.  选择该共享数据源，然后单击 **“打开”**。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 数据源将显示在“报表数据”窗格中。  
  
### <a name="to-create-an-embedded-data-source"></a>创建嵌入数据源  
  
1.  在“报表数据”窗格的工具栏上，单击 **“新建”**，然后单击 **“数据源”**。 此时将打开 **“数据源属性”** 对话框。  
  
2.  在 **“名称”** 文本框中，键入数据源的名称，或接受默认值。  
  
3.  确认选中 **“使用嵌在我的报表中的连接”** 。  
  
    1.  从“选择连接类型”下拉列表中，选择一个数据源类型，例如“Microsoft SQL Server”或“OLE DB”。  
  
    2.  采用以下备选方案之一指定连接字符串：  
  
    -   直接在 **“连接字符串”** 文本框中键入连接字符串。 有关示例连接字符串的列表，请参阅[数据连接、 数据源和报表生成器中的连接字符串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)。  
  
    -   单击表达式 (**fx** ) 按钮创建计算结果为连接字符串的表达式。 在 **“表达式”** 对话框的“表达式”窗格中，键入该表达式。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    -   单击 **“生成”** 打开在步骤 2 中选择的数据源类型的 **“连接属性”** 对话框。  
  
         根据需要，在 **“连接属性”** 对话框中为该数据源类型填写字段。 连接属性包括数据源的类型、名称以及要使用的凭据。 在此对话框中指定值之后，单击 **“测试连接”** 以确保该数据源可用并且指定的凭据是正确的。  
  
4.  单击 **“凭据”**。  
  
     指定用于此数据源的凭据。 数据源所有者将选择支持的凭据类型。 在某些情况下，数据源所有者会维护报表服务器上的共享数据源并使用可用凭据配置该数据源。 有关此信息，请与数据源所有者联系。 有关详细信息，请参阅 [在报表生成器中指定凭据](../specify-credentials-in-report-builder.md)。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 数据源将显示在“报表数据”窗格中。  
  
### <a name="to-verify-a-data-connection"></a>验证数据连接  
  
1.  在“报表数据”窗格的工具栏上，双击该数据源。 此时将打开 **“数据源属性”** 对话框。  
  
2.  单击 **“测试连接”**。  
  
3.  如果连接成功，则显示以下消息：“已成功地创建连接”。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  如果连接失败，则显示以下消息：“无法连接到数据源”。  
  
5.  单击 **“详细信息”**，然后使用该信息来解决问题。  
  
     有关详细信息，请参阅 [在报表生成器中指定凭据](../specify-credentials-in-report-builder.md)。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [向报表添加数据&#40;报表生成器和 SSRS&#41;](report-datasets-ssrs.md)   
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [查找、查看和管理报表（报表生成器和 SSRS）](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [报表生成器中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
  

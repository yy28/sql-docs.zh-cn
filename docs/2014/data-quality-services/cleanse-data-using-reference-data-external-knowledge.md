---
title: 使用引用数据（外部）知识清理数据 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 158009e9-8069-4741-8085-c14a5518d3fc
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2c2ad64e98e5dbee5661554272f498bf5cde0164
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37213947"
---
# <a name="cleanse-data-using-reference-data-external-knowledge"></a>使用引用数据（外部）知识清理数据
  本主题说明如何使用引用数据提供程序中的知识清理数据。 尽管运行清理活动的所有步骤与使用来自引用数据提供程序的知识清理数据（请参阅[使用 DQS（内部）知识清理数据[!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)]中的说明）的步骤相同，但本主题提供的信息特定于使用 ](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md) (DQS) 中的引用数据服务清理数据。  
  
 在您使用 DQS 中的引用数据服务功能清理数据时，该 DQS 清理过程将映射的域值以批处理请求的形式发送到引用数据服务提供程序中。 引用数据服务将会响应以下信息：  
  
-   建议的更正  
  
-   置信度  
  
-   有关映射的域的其他信息。 引用数据还可以对源执行标准化和分析，也可以使用其他数据丰富源的内容。 此信息在响应的附加字段中提供。  
  
 在从引用数据服务获取响应后，在清理活动过程中在 DQS 中将发生以下情况：  
  
-   基于在将域与引用数据服务进行映射的过程中指定的 **“自动更正阈值”** 和 **“最低置信度”** 值，将根据置信度自动更正或建议域值。  
  
    > [!NOTE]  
    >  您在将域映射到引用数据服务过程中指定的阈值在使用引用数据服务中的知识清理数据时同样适用，但在 **“常规设置”** 选项卡的 **“配置”** 部分中指定的阈值则不适用。 有关为引用数据清理指定阈值的信息，请参阅中的步骤 9[将域或复合域附加到引用数据](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md)。  
  
-   域值划分为以下几个类别： **“建议”**、 **“新建”**、 **“无效”**、 **“已更正”** 和 **“正确”**。  
  
-   附加数据将追加到源中，并且该信息与清理后的数据一起提供以供导出。  
  
## <a name="before-you-begin"></a>开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
 您必须将 DQS 知识库中的所需域映射到适当的引用数据服务。 此外，知识库必须包含有关您要清理的数据类型的知识。 例如，如果您要清理包含美国地址的源数据，则必须将您的域映射到为美国地址提供高质量数据的引用数据服务提供程序。 有关详细信息，请参阅[将域或复合域附加到引用数据](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_kb_operator 角色，才能执行数据清理。  
  
##  <a name="Cleanse"></a> 使用引用数据知识清理您的数据  
 我们将继续以同一个示例使用在上一主题中，我们映射的域[将域或复合域附加到引用数据](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md)，与 Windows Azure marketplace 的 Melissa Data 服务。 现在，我们将使用相同的域来清理一些示例美国地址。 清理数据的步骤与[使用 DQS（内部）知识清理数据](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)中介绍的步骤相同。 但是，我们在该过程中将会在需要时提醒您注意。  
  
1.  创建一个数据质量项目，并且选择 **“清理”** 活动。 请参阅[创建数据质量项目](../../2014/data-quality-services/create-a-data-quality-project.md)。  
  
2.  在 **“映射”** 页上，将以下 4 个域与您的源数据中的相应列进行映射： **Address Line**、 **City**、 **State**和 **Zip**。 单击“下一步” 。  
  
    > [!NOTE]  
    >  当您在 **“地址验证”** 复合域中映射了所有 4 个域后，数据清理现在将在复合域级别完成，而非在单独的域级别完成。  
  
3.  在 **“清理”** 页上，通过单击 **“开始”** 运行计算机辅助的清理过程。 在清理过程结束后，单击 **“下一步”**。  
  
    > [!NOTE]  
    >  在 **“清理”** 页上，DQS 通过以下两种方式显示与附加到引用数据服务的域有关的信息：  
    >   
    >  -   “开始”按钮下会显示一条消息：“Domains \<Domain1>, \<Domain2>,… \<DomainN> 已使用引用数据服务提供程序进行清理。” 在此示例中，将显示以下消息：“使用引用数据服务提供程序清理域地址验证。”  
    > -   ![将域附加到 RDS](../../2014/data-quality-services/media/dqs-rdsindicator.JPG "Domain is attached to RDS") 图标根据附加到引用数据服务提供程序的域显示在“探查器”区域中。 在此示例中，将针对 **“地址验证”** 复合域显示该图标。  
  
4.  在 **“管理和查看结果”** 页上，查看您的域值。 根据在将域映射到引用数据服务的过程中在 **“建议的候选项”** 框中指定的建议的最大数目，引用数据服务可为一个值显示多个建议（如果可用）。 例如，为下面的美国地址显示两项建议：  
  
     **原始值：**  
  
    |Address Line|City|State|Zip|  
    |------------------|----------|-----------|---------|  
    |1 msft way|Redmond||98052|  
  
     **建议的值：**  
  
    |Address Line|City|State|Zip|  
    |------------------|----------|-----------|---------|  
    |1 Microsoft Way|Redmond|WA|98052|  
    |PO Box 1|Redmond|WA|98073|  
  
     ![使用引用数据服务清理](../../2014/data-quality-services/media/dqs-rdscleansing.JPG "Cleansing using reference data service")  
  
    > [!NOTE]  
    >  对于复合域，DQS 还以不同的颜色突出显示计算机辅助清理过程中已更正的单独域。 例如，在这个示例中， **Address Line** 和 **State** 域已更正，因此以青色突出显示。  
  
5.  在您检查完所有域值后，单击 **“下一步”** 以导出数据。  
  
6.  在 **“导出”** 页上，您将注意到除了与每个域的清理活动有关的常规信息（“源”、“原因”、“置信度”和“状态”）之外，还有 Melissa Data 引用数据服务提供的与您的地址有关的附加信息，例如您的地址的经度和维度、国家/地区名称、地址类型（多层楼房、街道等）等。  
  
7.  将您的数据导出到所需目标（SQL Server、CSV 或 Excel），然后单击 **“完成”** 关闭该项目。  
  
    > [!IMPORTANT]  
    >  如果您使用的是 64 位版本的 Excel，则无法将已清理的数据导出到 Excel 文件；只能导出到 SQL Server 数据库或 .csv 文件。  
  
  

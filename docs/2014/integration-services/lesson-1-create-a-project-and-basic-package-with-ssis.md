---
title: 第 1 课： 创建项目和基本包 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 84d0b877-603f-4f8e-bb6b-671558ade5c2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 62a4a0737f57d6040d2c166847f191f13d435071
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48229478"
---
# <a name="lesson-1-creating-the-project-and-basic-package"></a>第 1 课：创建项目和基本包
  在本课中，将创建一个简单 ETL 包，该包可以从单个平面文件源中提取数据，使用两个查找转换组件转换该数据，然后将该数据写入 **AdventureWorksDW2012** 的 **FactCurrency**事实数据表中。 在本课中，您还将学习如何创建新包、添加和配置数据源和目标连接以及使用新的控制流和数据流组件。  
  
> [!IMPORTANT]  
>  本教程需要 **AdventureWorksDW2012** 示例数据库。 有关如何安装和部署 **AdventureWorksDW2012**的详细信息，请参阅 [CodePlex 上的 Reporting Services 产品示例](http://go.microsoft.com/fwlink/p/?LinkID=52691)。  
  
## <a name="understanding-the-package-requirements"></a>了解包要求  
 本教程需要 Microsoft SQL Server Data Tools。  
  
 有关安装 SQL Server Data Tools 的详细信息，请参阅 [SQL Server Data Tools 下载](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017)。  
  
 在创建包之前，需要充分了解在源数据和目标数据中使用的格式。 了解了这些数据格式后，便可定义将源数据映射到目标数据所需的转换。  
  
### <a name="looking-at-the-source"></a>查看源  
 在本教程中，源数据是平面文件 SampleCurrencyData.txt 中包含的一组历史货币数据。 源数据具有以下四列：货币的平均汇率、货币键、日期键和收盘汇率。  
  
 下面是 SampleCurrencyData.txt 文件中所包含的源数据示例：  
  
 `1.00070049USD9/3/05 0:001.001201442`  
  
 `1.00020004USD9/4/05 0:001`  
  
 `1.00020004USD9/5/05 0:001.001201442`  
  
 `1.00020004USD9/6/05 0:001`  
  
 `1.00020004USD9/7/05 0:001.00070049`  
  
 `1.00070049USD9/8/05 0:000.99980004`  
  
 `1.00070049USD9/9/05 0:001.001502253`  
  
 `1.00070049USD9/10/05 0:000.99990001`  
  
 `1.00020004USD9/11/05 0:001.001101211`  
  
 `1.00020004USD9/12/05 0:000.99970009`  
  
 在使用平面文件源数据时，需要了解平面文件连接管理器如何解释平面文件数据，这一点很重要。 如果平面文件源是 Unicode 编码的，则平面文件连接管理将所有列定义为 [DT_WSTR]，默认列宽为 50。 如果平面文件源是 ANSI 编码的，则将列定义为 [DT_STR]，默认列宽为 50。 您可能必须更改这些默认设置，才能使字符串列类型与所使用的数据更相符。 为此，您需要查看将写入数据的目标的数据类型，然后在平面文件连接管理器中选择正确的类型。  
  
### <a name="looking-at-the-destination"></a>查看目标  
 源数据的最终目标是 **AdventureWorksDW** 中的 **FactCurrency**事实数据表。 **FactCurrency** 事实数据表有四列，并且与两个维度表有关系，如下表所示。  
  
|列名|数据类型|查找表|查找列|  
|-----------------|---------------|------------------|-------------------|  
|AverageRate|FLOAT|None|None|  
|CurrencyKey|int (FK)|DimCurrency|CurrencyKey (PK)|  
|DateKey|int (FK)|DimDate|DateKey (PK)|  
|EndOfDayRate|FLOAT|None|None|  
  
### <a name="mapping-source-data-to-be-compatible-with-the-destination"></a>将源数据映射为与目标兼容  
 对源数据和目标数据的分析指出需要查找 **CurrencyKey** 和 **DateKey** 值。 将执行这些查找的转换通过使用 **DimCurrency** 和 **DimDate** 维度表中的备用键来获取 **CurrencyKey** 和 **DateKey** 值。  
  
|平面文件列|表名|列名|数据类型|  
|----------------------|----------------|-----------------|---------------|  
|0|AdventureWorksDW2012|AverageRate|float|  
|1|DimCurrency|CurrencyAlternateKey|nchar(3)|  
|2|DimDate|FullDateAlternateKey|日期|  
|3|AdventureWorksDW2012|EndOfDayRate|FLOAT|  
  
## <a name="lesson-tasks"></a>课程任务  
 本课程包含以下任务：  
  
-   [步骤 1：创建新的 Integration Services 项目](lesson-1-1-creating-a-new-integration-services-project.md)  
  
-   [步骤 2：添加和配置平面文件连接管理器](lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
-   [步骤 3：添加并配置 OLE DB 连接管理器](lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
-   [步骤 4：将数据流任务添加到包](lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
-   [步骤 5：添加并配置平面文件源](lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
-   [步骤 6：添加并配置查找转换](lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
-   [步骤 7：添加并配置 OLE DB 目标](lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
-   [步骤 8：使第 1 课包更易理解](lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
-   [步骤 9：测试第 1 课教程包](lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>开始课程  
 [步骤 1：创建新的 Integration Services 项目](lesson-1-1-creating-a-new-integration-services-project.md)  
  
  

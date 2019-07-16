---
title: Wide World Importers-sql 示例数据库 |Microsoft 文档
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c178d116dddb5dc18b1bec91066205fe08f6d0c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067612"
---
# <a name="wide-world-importers-sample-databases-for-microsoft-sql"></a>Microsoft sql 的 wide World Importers 示例数据库
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
这是虚构的公司 Wide World Importers 和 WideWorldImporters 示例数据库中的 SQL Server 和 Azure SQL 数据库进行寻址的工作流的概述。  

Wide World Importers (WWI) 是批发新奇商品导入程序和从 San Francisco 托架区域运行的分发服务器。

批发商，为 WWI 的客户是主要转售对个人的公司。 WWI 销售到零售客户包括专门存储，超市，美国各计算存储、 旅游引力服务提供商，以及某些个人。 WWI 还销售给其他批发商通过提升 WWI 的代表产品的代理的网络。 同时 WWI 的客户的所有当前基于在美国，该公司想要推送到其他国家/地区的扩展。

WWI 从供应商包括新奇和玩具制造商以及其他新奇批发商购买商品。 它们常用在其 WWI 仓库和重新排序，从供应商商品，以满足客户订单。 它们还购买大量的资料、 打包和销售这些较小数量中为方便起见的客户。

最近已开始 WWI 销售各种如 chilli edible novelties 甜蜜。  该公司以前没有 chilled 的项处理。 现在，为了满足处理要求的食物，它们必须监视其冷却器房间和任何具有冷却器部分及其卡车中的温度。

## <a name="workflow-for-warehouse-stock-items"></a>仓库库存商品的工作流

如何项已存储和分发的典型流如下所示：
- WWI 创建采购订单，并将提交到供应商的订单。
- 供应商发送项目、 WWI 接收它们和库存在其仓库中。
- 从 WWI 客户订单项
- WWI 填充具有股票项在仓库中的客户订单和时他们没有足够的股票，它们从供应商订购其他股票。
- 某些客户不希望等待不在库存中的项目。 如果他们另外订购了假设五个不同股票项和四个可用，他们想要接收的四个项目和延期交货剩余的项。 该项将它们发送更高版本中单独发货。
- WWI 发票的股票项目，客户通常通过将订单转换为发票。
- 客户可能不在库存中的项进行排序。 这些项是延期交货。
- WWI 客户通过其自己货车，或通过其他快递或运费方法提供股票项。
- 客户支付给 WWI 发票。
- 我们会定期 WWI 支付供应商的采购订单上的项。 这是通常一段时间后它们已接收商品。

## <a name="data-warehouse-and-analysis-workflow"></a>数据仓库和分析工作流

虽然 WWI 的团队使用 SQL Server Reporting Services 从 WideWorldImporters 数据库生成的操作报表，它们还需要对其数据执行分析，需要生成战略报告。 团队有 WideWorldImportersDW 的数据库中创建多维数据模型。 此数据库由 Integration Services 包填充。

SQL Server Analysis Services 用于从多维数据模型中的数据中创建分析数据模型。 SQL Server Reporting Services 用于直接从多维数据模型，以及分析模型中生成战略报告。 Power BI 用于从相同的数据创建仪表板。 用于仪表板上的网站，并在手机和平板电脑上。 *注意： 这些数据模型和报表尚不可用*

## <a name="additional-workflows"></a>其他工作流

这些是额外的工作流。
- WWI 问题信用额度说明时出于某种原因，或当货物可以发生故障时，客户不会接收良好。 这些被视为负发票。
- WWI 定期对股票项，以确保其系统上显示为可用的库存数量是准确的现有数量进行计数。 （执行此操作的过程被称为 stocktake）。
- 冷的房间温度。 腐烂的产品存储在 refrigerated 聊天室。 这些房间内的传感器数据引入到监视和分析目的的数据库。
- 车辆位置跟踪。 为 WWI 运输货物的车辆包括跟踪的位置的传感器。 此位置重新引入到数据库中进行监视，和进一步分析。

## <a name="fiscal-year"></a>会计年度

该公司在 11 月 1 日开始的财务年份进行操作。

## <a name="terms-of-use"></a>使用条款

此处所述的示例数据库和示例代码的许可证： [license.txt](https://github.com/Microsoft/sql-server-samples/blob/master/license.txt)

示例数据库中包含已从 data.gov 和自然 EarthData 加载的公共数据。 使用条款位于以下位置： [https://www.naturalearthdata.com/about/terms-of-use/](https://www.naturalearthdata.com/about/terms-of-use/)

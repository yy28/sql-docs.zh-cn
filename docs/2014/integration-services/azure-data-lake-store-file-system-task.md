---
title: Azure Data Lake Store 文件系统任务 | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSTASK.F1
- SQL11.DTS.DESIGNER.AFPADLSTASK.F1
ms.assetid: 02b9edd7-6ef9-463e-abbf-e1830bcae875
caps.latest.revision: 3
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.openlocfilehash: 240780efd1b12596b0ebb6156ad98c508f0e8051
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014108"
---
# <a name="azure-data-lake-store-file-system-task"></a>Azure Data Lake Store 文件系统任务
**Azure 数据湖存储文件系统任务**使用户能够执行各种文件系统操作[Azure 数据湖存储 (ADLS)](https://azure.microsoft.com/en-us/services/data-lake-store/)。

若要将 Azure Data Lake Store 文件系统任务添加到某个包，请将它从 SSIS 工具箱拖到设计器画布中。 然后双击该任务，或右键单击该任务并选择**编辑**，若要打开任务编辑器对话框。

“操作”属性指定要执行的文件系统操作。 支持以下操作。

* **CopyToADLS：** 将文件上载到 ADLS。
* **CopyFromADLS：** 从 ADLS 下载文件。

对任何操作都必须指定 Azure Data Lake 连接管理器。

以下是特定于每个操作的属性的说明。

## <a name="copytoadls"></a>CopyToADLS
* **LocalDirectory:** 指定包含要上载的文件的源目录。
* **FileNamePattern：** 指定源文件的文件名筛选器。 只有其名称与指定的模式匹配的文件将会上载。 支持 `*` 和 `?` 通配符。
* **SearchRecursively：** 指定是否在源目录中以递归方式搜索要上载的文件。
* **AzureDataLakeDirectory：** 指定要将文件上载到的 ADLS 目标目录。
* **FileExpiry:** 指定过期日期和时间的文件上载到 ADLS，或将此属性留空以指示文件永不过期。

## <a name="copyfromadls"></a>CopyFromADLS
* **AzureDataLakeDirectory：** 指定包含待下载文件的 ADLS 源目录。
* **SearchRecursively：** 指定是否在源目录中以递归方式搜索要下载的文件。
* **LocalDirectory：** 指定要存储已下载文件的目标目录。

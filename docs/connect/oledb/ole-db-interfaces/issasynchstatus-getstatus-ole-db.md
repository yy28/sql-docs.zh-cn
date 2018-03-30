---
title: ISSAsynchStatus::GetStatus (OLE DB) |Microsoft 文档
description: ISSAsynchStatus::GetStatus (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAsynchStatus::GetStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- GetStatus method
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 394539d4788df395e64c96f76c55edf0465326e2
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="issasynchstatusgetstatus-ole-db"></a>ISSAsynchStatus::GetStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  返回异步执行操作的状态。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT GetStatus(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation,  
        DBCOUNTITEM *pulProgress,  
        DBCOUNTITEM *pulProgressMax,  
        DBASYNCHPHASE *peAsynchPhase,  
        LPOLESTR *ppwszStatusText);  
```  
  
## <a name="arguments"></a>参数  
 *hChapter*[in]  
 章节句柄。 如果轮询的对象不是行集对象，或该操作不会应用于一章，它应设置为 DB_NULL_HCHAPTER，忽略由提供程序。  
  
 *eOperation*[in]  
 请求其异步状态的操作。 应使用以下值：  
  
 DBASYNCHOP_OPEN – 使用者请求有关异步打开或填充行集或者异步初始化数据源对象的信息。 如果访问接口是支持直接 URL 绑定且与 OLE DB 2.5 兼容的访问接口，使用者则请求有关异步初始化或填充数据源、行集、行或流对象的信息。  
  
 *pulProgress*[out]  
 指向内存中用于返回相对于预期的最大异步操作的当前进度的指针所示*pulProgressMax*参数。 有关的含义的详细信息*pulProgress*，请参阅说明*peAsynchPhase*。  
  
 如果*pulProgress*是 null 指针，返回没有取得进展。  
  
 *pulProgressMax*[out]  
 指向内存中要返回的预期最大值的指针*pulProgress*参数。 此值可以随此方法的每次调用而更改。 有关的含义的详细信息*pulProgressMax*，请参阅说明*peAsynchPhase*。  
  
 如果*pulProgressMax*是 null 指针，不返回任何预期的最大值。  
  
 *peAsynchPhase*[out]  
 指向在其中有关进度的异步操作返回的其他信息的内存的指针。 有效值包括：  
  
 DBASYNCHPHASE_INITIALIZATION - 对象处于初始化阶段。 自变量*pulProgress*和*pulProgressMax*指示完成到估计的比率。 对象尚未完全具体化。 尝试调用任何其他接口可能失败，并且可能无法对该对象使用整套接口。 如果异步操作调用的结果**ICommand::Execute**的更新的命令删除，或插入行，如果*cParamSets*大于 1， *pulProgress*和*pulProgressMax*可能表示为一组参数或完整的数组的参数集的进度。  
  
 DBASYNCHPHASE_POPULATION - 对象处于填充阶段。 尽管已完全初始化行集，并且可针对该对象使用整套接口，但是可能还有其他行尚未填充到行集中。 虽然*pulProgress*和*pulProgressMax*可以基于上填充的行数，它们通常基于的时间或填充行集所需的工作。 因此，调用方应将此信息用作对此过程所需时间的粗略估计，而不是最终的行计数。 此阶段仅在填充行集期间返回；它永远不会在数据源对象初始化期间返回，也不会因执行更新、删除或插入行的命令而返回。  
  
 DBASYNCHPHASE_COMPLETE - 已完成对象的所有异步处理。 **ISSAsynchStatus::GetStatus**方法返回 HRESULT，指示该操作的结果。 通常，如果已同步调用操作，则将返回 HRESULT。 如果异步操作调用的结果**ICommand::Execute**命令的更新、 删除或插入行， *pulProgress*和*pulProgressMax*是等于命令受影响的行总数。 如果*cParamSets*是大于 1，这是通过执行过程中指定的参数集的所有受影响的行总数。 如果*peAsynchPhase*是 null 指针，则返回任何状态代码。  
  
 DBASYNCHPHASE_CANCELED - 已中止对象的异步处理。 **ISSAsynchStatus::GetStatus**方法返回 DB_E_CANCELED。 如果异步操作调用的结果**ICommand::Execute**命令的更新、 删除或插入行， *pulProgress*等于总行数，对于所有的参数集，受影响之前取消命令。  
  
 *ppwszStatusText*[in/out]  
 指向包含有关操作的其他信息的内存的指针。 访问接口可以使用此值区分不同的操作元素，例如，要访问的不同资源。 该字符串的本地化形式基于数据源对象的 DBPROP_INIT_LCID 属性。  
  
 如果*ppwszStatusText*是输入非 null，该提供程序返回标识的特定元素与关联的状态*ppwszStatusText*。 如果*ppwszStatusText*并不表示的元素*eOperation*，该提供程序返回使用，则为 S_OK *pulProgress*和*pulProgressMax*设置为相同的值。 如果提供程序不区分基于文本的标识符的元素，则将设置*ppwszStatusText*到 NULL 并返回有关操作的信息作为一个整体; 否则为如果*ppwszStatusText*是输入非 null，该提供程序离开*ppwszStatusText*不变。  
  
 如果*ppwszStatusText*的输入，提供程序集为 null *ppwszStatusText*到一个值，该值有关此操作，或为 NULL 的详细信息，如果没有此类信息可用，或者如果**ISSAsynchStatus::GetStatus**方法将返回错误。 当*ppwszStatusText*是 null 输入，提供程序的状态字符串为分配内存和的地址返回到此内存。 使用者释放此内存， **IMalloc::Free**当不再需要字符串。  
  
 如果*ppwszStatusText*输入为 NULL 返回没有状态字符串，该提供程序一般情况下返回有关操作的任何元素或操作的相关信息。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 该方法已成功返回。  
  
-   如果*peAsynchPhase*是等于 DBASYNCHPHASE_INITIALIZATION，该对象尚未完全初始化; 尝试调用任何其他接口可能会失败，并且完整的接口集可能不会在对象上获取。  
  
-   如果*peAsynchPhase*是等于 DBASYNCHPHASE_POPULATION，行集完全初始化和接口的完整范围是可在对象上; 但是，可能有其他尚未填充到行集中的行。  
  
-   如果*peAsynchPhase*是等于 DBASYNCHPHASE_COMPLETE，已完成的对象的所有异步处理。 已完全初始化并填充该对象。  
  
 DB_E_CANCELED  
 异步处理在行集填充过程中取消。 填充停止，但是对于已填充的行，该行集仍保持有效。  
  
 异步处理在数据源对象的初始化过程中取消。 数据源对象处于未初始化状态。  
  
 E_INVALIDARG  
 *HChapter*参数不正确。  
  
 E_UNEXPECTED  
 **ISSAsynchStatus::GetStatus**对数据源对象，调用了方法和**idbinitialize:: Initialize**尚未调用对数据源对象。  
  
 **ISSAsynchStatus::GetStatus**对行集，调用了方法**itransaction:: 提交**或**ITransaction::Abort**调用，并在对象处于僵停状态。  
  
 **ISSAsynchStatus::GetStatus**在已以异步方式取消其初始化阶段中的行集上调用了方法。 该行集处于僵停状态。  
  
 E_FAIL  
 发生了特定于访问接口的错误。  
  
## <a name="remarks"></a>注释  
 **ISSAsynchStatus::GetStatus**方法的行为完全相同**IDBAsynchStatus::GetStatus**方法处在于如果初始化的数据源对象被中止，E_UNEXPECTED 返回而不是比 DB_E_CANCELED (尽管[ISSAsynchStatus::WaitForAsynchCompletion](../../oledb/ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)将返回 DB_E_CANCELED)。 这是因为以便进一步初始化操作可能已尝试，数据源对象不会保留在以下了 abort，常用僵停状态。  
  
 如果异步初始化或填充行集，则必须支持此方法。  
  
 除了列出的返回值**ISSAsynchStatus::GetStatus**可以返回任何 HRESULT 由启动异步操作的方法返回，指示该操作成功与否。  
  
 某些异步操作可能无法返回任何以外"完成"状态和"未完成。" 它们应设置*pulProgressMax*为值 1，指示其估计值，全盘接受或者全盘粒度以便其答案将 0/1 / 1。  
  
 一个提供程序可能会更改*pulProgressMax*在后续调用中和甚至返回较小比以前，如果这反映了改进的估计的完成任务的程度。  
  
 访问接口不必保证任何进一步的准确性，但是对于可以对完成情况进行合理估计的情况，建议执行此工作。 这一工作将改进用户界面的质量，因为此函数的主要用途是向用户提供进度反馈。 由于改善了长期运行的不可见任务的反馈质量，用户的满意度也随之提高。  
  
 调用**ISSAsynchStatus::GetStatus**上初始化的数据源对象或填充的行集，或将值传递*eOperation*以外 DBASYNCHOP_OPEN，返回与，则为 S_OK *pulProgress*和*pulProgressMax*设置为相同的值。 如果**ISSAsynchStatus::GetStatus**的命令的更新、 删除或插入行，在执行创建的对象上调用方法同时*pulProgress*和*pulProgressMax*指示命令受影响的行总数。  
  
## <a name="see-also"></a>另请参阅  
 [执行异步操作](../../oledb/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus &#40; OLE DB &#41;](../../oledb/ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  

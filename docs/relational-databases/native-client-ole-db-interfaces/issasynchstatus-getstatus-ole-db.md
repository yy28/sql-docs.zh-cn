---
title: 'Issasynchstatus:: Getstatus (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAsynchStatus::GetStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- GetStatus method
ms.assetid: 354b6ee4-b5a1-48f6-9403-da3bdc911067
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d39998e41fd26bb2928290f62dd08fc54a0f567a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37407859"
---
# <a name="issasynchstatusgetstatus-ole-db"></a>ISSAsynchStatus::GetStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

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
 章节句柄。 如果轮询的对象不是行集对象或操作不适用于某一章节，则应将此参数设置为 DB_NULL_HCHAPTER，访问接口将忽略此参数。  
  
 *eOperation*[in]  
 请求其异步状态的操作。 其值应为：  
  
 DBASYNCHOP_OPEN – 使用者请求有关异步打开或填充行集或者异步初始化数据源对象的信息。 如果访问接口是支持直接 URL 绑定且与 OLE DB 2.5 兼容的访问接口，使用者则请求有关异步初始化或填充数据源、行集、行或流对象的信息。  
  
 *pulProgress*[out]  
 指向用于返回预期的最大值相关的异步操作的当前进度的内存的指针所示*pulProgressMax*参数。 有关详细信息的含义*pulProgress*，请参阅的说明*peAsynchPhase*。  
  
 如果*pulProgress*是 null 指针，不返回进度。  
  
 *pulProgressMax*[out]  
 指向内存中要返回的预期最大值的指针*pulProgress*参数。 此值可以随此方法的每次调用而更改。 有关详细信息的含义*pulProgressMax*，请参阅的说明*peAsynchPhase*。  
  
 如果*pulProgressMax*是 null 指针，不返回任何预期的最大值。  
  
 *peAsynchPhase*[out]  
 指向内存的指针，将在此内存中返回有关异步操作的进度的其他信息。 有效值包括：  
  
 DBASYNCHPHASE_INITIALIZATION - 对象处于初始化阶段。 自变量*pulProgress*并*pulProgressMax*指示估计的完成比率。 对象尚未完全具体化。 尝试调用任何其他接口可能失败，并且可能无法对该对象使用整套接口。 如果异步操作是因调用**icommand:: Execute**有关命令的更新、 删除或插入行以及是否*cParamSets*大于 1， *pulProgress*并*pulProgressMax*可能表示一组参数或参数集的完整阵列的进度。  
  
 DBASYNCHPHASE_POPULATION - 对象处于填充阶段。 尽管已完全初始化行集，并且可针对该对象使用整套接口，但是可能还有其他行尚未填充到行集中。 虽然*pulProgress*并*pulProgressMax*可以基于填充的行数，它们通常基于填充行集所需工作量的时间。 因此，调用方应将此信息用作对此过程所需时间的粗略估计，而不是最终的行计数。 此阶段仅在填充行集期间返回；它永远不会在数据源对象初始化期间返回，也不会因执行更新、删除或插入行的命令而返回。  
  
 DBASYNCHPHASE_COMPLETE - 已完成对象的所有异步处理。 **Issasynchstatus:: Getstatus**返回一个 HRESULT，指示操作的结果。 通常，如果已同步调用操作，则将返回 HRESULT。 如果异步操作是因调用**icommand:: Execute**的命令的更新、 删除或插入行， *pulProgress*并*pulProgressMax*是等于受影响的命令行的总数。 如果*cParamSets*是大于 1，这是受影响的所有执行过程中指定的参数集行的总数。 如果*peAsynchPhase*是 null 指针，则返回任何状态代码。  
  
 DBASYNCHPHASE_CANCELED - 已中止对象的异步处理。 **Issasynchstatus:: Getstatus**返回 DB_E_CANCELED。 如果异步操作是因调用**icommand:: Execute**的命令的更新、 删除或插入行， *pulProgress*等于行，所有的参数集的总数在取消之前命令所影响。  
  
 *ppwszStatusText*[in/out]  
 指向包含有关操作的其他信息的内存的指针。 访问接口可以使用此值区分不同的操作元素，例如，要访问的不同资源。 该字符串的本地化形式基于数据源对象的 DBPROP_INIT_LCID 属性。  
  
 如果*ppwszStatusText*是输入非 null，访问接口将返回与标识的特定元素相关联的状态*ppwszStatusText*。 如果*ppwszStatusText*并不表示的元素*eOperation*，该提供程序返回 S_OK，并*pulProgress*和*pulProgressMax*设置为相同值。 如果提供程序不区分基于文本标识符元素，它会设置*ppwszStatusText* NULL，并返回有关的信息操作作为一个整体; 否则为如果*ppwszStatusText*是在输入非 null，访问接口将使*ppwszStatusText*保持不变。  
  
 如果*ppwszStatusText*的输入，提供程序集为 null *ppwszStatusText*到一个值，该值有关此操作，或为 NULL 的详细信息，如果没有此类信息不可用，或如果**Issasynchstatus:: Getstatus**返回错误。 当*ppwszStatusText*是 null 输入时，该提供程序为状态字符串分配内存并返回此内存地址。 使用者释放此内存以及**imalloc:: Free**当不再需要该字符串。  
  
 如果*ppwszStatusText*在输入为 NULL，返回没有状态字符串和提供程序一般情况下返回有关操作的任何元素或操作的相关信息。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 该方法已成功返回。  
  
-   如果*peAsynchPhase*是等于 DBASYNCHPHASE_INITIALIZATION，该对象尚未完全初始化; 尝试调用任何其他接口可能会失败，并且完整的接口集可能不可用的对象上。  
  
-   如果*peAsynchPhase*是等于 DBASYNCHPHASE_POPULATION，完全初始化行集和接口的完整范围是可针对该对象; 但是，可能有其他行尚未填充到行集中。  
  
-   如果*peAsynchPhase*是等于 DBASYNCHPHASE_COMPLETE，已完成的对象的所有异步处理。 已完全初始化并填充该对象。  
  
 DB_E_CANCELED  
 异步处理在行集填充过程中取消。 填充停止，但是对于已填充的行，该行集仍保持有效。  
  
 异步处理在数据源对象的初始化过程中取消。 数据源对象处于未初始化状态。  
  
 E_INVALIDARG  
 *HChapter*参数不正确。  
  
 E_UNEXPECTED  
 **Issasynchstatus:: Getstatus**调用对数据源对象，并**idbinitialize:: Initialize**尚未调用数据源对象。  
  
 **Issasynchstatus:: Getstatus**的行集，已调用**itransaction:: Commit**或**itransaction:: Abort**调用，并在对象处于僵停状态。  
  
 **Issasynchstatus:: Getstatus**已以异步方式取消初始化阶段中的行集时调用。 该行集处于僵停状态。  
  
 E_FAIL  
 发生了特定于访问接口的错误。  
  
## <a name="remarks"></a>Remarks  
 **Issasynchstatus:: Getstatus**方法的行为完全相同**IDBAsynchStatus::GetStatus**方法，不同之处在于如果源对象的数据初始化被中止，将返回 E_UNEXPECTED，而不是比 DB_E_CANCELED (尽管[issasynchstatus:: Waitforasynchcompletion](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)将返回 DB_E_CANCELED)。 这是因为在中止后，数据源对象不会照常处于僵停状态，以便进一步尝试初始化操作。  
  
 如果异步初始化或填充行集，则必须支持此方法。  
  
 除了列出的返回值**issasynchstatus:: Getstatus**可以返回任何 HRESULT，则由启动异步操作，该方法返回，该值指示该操作成功与否。  
  
 某些异步操作可能无法返回除“完成”和“尚未完成”以外的任何状态。 它们应设置*pulProgressMax*为值 1，指示其估计值，要么粒度以便将为 0/1 / 1。  
  
 一个提供程序可能会更改*pulProgressMax*在后续调用中，甚至返回比例较低比以前，如果这反映了任务的完成程度的改善估计。  
  
 访问接口不必保证任何进一步的准确性，但是对于可以对完成情况进行合理估计的情况，建议执行此工作。 这一工作将改进用户界面的质量，因为此函数的主要用途是向用户提供进度反馈。 由于改善了长期运行的不可见任务的反馈质量，用户的满意度也随之提高。  
  
 调用**issasynchstatus:: Getstatus**上初始化的数据源对象或填充行集，或将值传递*eOperation*除 dbasynchop_open 以外，返回 S_OK，并*pulProgress*并*pulProgressMax*设置为相同值。 如果**issasynchstatus:: Getstatus**上执行的命令的更新、 删除或插入行，从创建的对象调用同时*pulProgress*和*pulProgressMax*指示受命令影响的总行数。  
  
## <a name="see-also"></a>请参阅  
 [执行异步操作](../../relational-databases/native-client/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  

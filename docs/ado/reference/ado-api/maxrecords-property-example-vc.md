---
title: "最大记录的属性示例 （VC + +） |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- MaxRecords property [ADO], VC++ example
ms.assetid: af6b399b-e546-4de5-9cd1-5a6e0ec7ddc7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 77ab4e80cb319aa95f7a566462e648ccbb9bbadb
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="maxrecords-property-example-vc"></a>最大记录的属性示例 （VC + +）
此示例使用[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)以打开[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)包含中的 10 成本最高标题***标题***表。  
  
## <a name="example"></a>示例  
  
```  
// MaxRecords_Property_Example.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF","EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
#include "icrsint.h"  
  
// This class extracts titles and type from the titles table  
class CTitleRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CTitleRs)  
  
      // Column title is the 1st field in the Recordset  
      ADO_VARIABLE_LENGTH_ENTRY2(1, adVarChar,m_szau_Title,  
      sizeof(m_szau_Title), lau_TitleStatus, FALSE)  
  
      // Column price is the 2nd field in the Recordset  
      ADO_VARIABLE_LENGTH_ENTRY2(2, adDouble, m_szau_Price,  
      sizeof(m_szau_Price), lau_PriceStatus, FALSE)  
  
   END_ADO_BINDING()  
  
public:  
   CHAR m_szau_Title[81];  
   ULONG lau_TitleStatus;  
   DOUBLE m_szau_Price;  
   ULONG lau_PriceStatus;  
};  
  
// Function Declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void MaxRecordsX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   MaxRecordsX();  
   ::CoUninitialize();  
}  
  
void  MaxRecordsX() {  
   // Define ADO ObjectPointers.  Initialize Pointers on define  
   // These are in the ADODB :: namespace  
   _RecordsetPtr pRstTemp = NULL;  
  
   // Define Other Variables  
   IADORecordBinding *picRs = NULL;   // Interface Pointer Declared    
   CTitleRs titlers;   // C++ Class Object  
  
   try {  
      // Assign Connection String to Variable  
      _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
      // Open Recordset containing the 10 most expensive titles in the Titles table.  
      TESTHR(pRstTemp.CreateInstance(__uuidof(Recordset)));  
  
      pRstTemp->MaxRecords = 10;  
  
      pRstTemp->Open("SELECT title,price FROM Titles ORDER BY Price DESC",  
         strCnn, adOpenForwardOnly, adLockReadOnly, adCmdText);  
  
      // Open IADORecordBinding interface pointer for binding Recordset to a class  
      TESTHR(pRstTemp->QueryInterface(__uuidof(IADORecordBinding), (LPVOID*)&picRs));  
  
      // Bind the Recordset to a C++ class here  
      TESTHR(picRs->BindToRecordset(&titlers));  
  
      // Display the contents of the Recordset  
      printf("Top Ten Titles by Price:\n\n");  
  
      while ( !(pRstTemp->EndOfFile) ) {  
         printf("%s ---  %6.2lf\n", titlers.lau_TitleStatus == adFldOK ?   
            titlers.m_szau_Title : "<NULL>", titlers.lau_PriceStatus == adFldOK ?   
            titlers.m_szau_Price : 0.00);  
         pRstTemp->MoveNext();  
      }  
   }  
   catch(_com_error &e) {  
      // Display errors, if any.  Pass connection pointer accessed from the Recordset.  
      _variant_t vtConnect = pRstTemp->GetActiveConnection();  
  
      // GetActiveConnection returns connect string if connection   
      // is not open, else returns Connection object.  
      switch(vtConnect.vt) {  
      case VT_BSTR:  
         PrintComError(e);  
         break;  
      case VT_DISPATCH:  
         PrintProviderError(vtConnect);  
         break;  
      default:  
         printf("Errors occured.");  
         break;  
      }  
   }  
  
   // Clean up objects before exit. Release the IADORecordset Interface here     
   if (picRs)  
      picRs->Release();  
  
   if (pRstTemp)  
      if (pRstTemp->State == adStateOpen)  
         pRstTemp->Close();  
};  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object  
   // pErr is a record object in the Connection's Error collection  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count)>0 ) {  
      long nCount = pConnection->Errors->Count;  
  
      // Collection ranges from 0 to nCount-1  
      for ( long i = 0 ; i < nCount ; i++ ) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("\t Error Number :%x \t %s", pErr->Number, pErr->Description);  
      }  
   }  
}  
  
void PrintComError(_com_error &e) {  
   _bstr_t bstrSource(e.Source());  
   _bstr_t bstrDescription(e.Description());  
  
   // Print Com errors.    
   printf("Error\n");  
   printf("\tCode = %08lx\n", e.Error());  
   printf("\tCode meaning = %s\n", e.ErrorMessage());  
   printf("\tSource = %s\n", (LPCSTR) bstrSource);  
   printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
```  
  
 **按价格的前十个标题：**  
**但它是用户友好？---22.95**  
**计算机 Phobic 和非 Phobic 个人： 行为变体---21.59**  
**洋葱、 Leeks 和蒜蓉： 烹饪地中海地区---20.95 机密**  
**硅谷---20.00 的密钥**  
**忙高级管理人员的数据库指南---19.99**  
**直谈一谈计算机---19.99**  
**硅谷 Gastronomic 将---19.99**  
**长时间的数据 Deprivation： 四个案例研究---19.99**  
**寿司，任何人？---14.99**  
**Buckingham 宫殿厨房---11.95 中的 50 个年**   
## <a name="see-also"></a>另请参阅  
 [最大记录属性 (ADO)](../../../ado/reference/ado-api/maxrecords-property-ado.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)


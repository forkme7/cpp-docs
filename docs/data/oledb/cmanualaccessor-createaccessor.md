---
title: "CManualAccessor::CreateAccessor | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.technology: ["cpp-data"]
ms.topic: "reference"
f1_keywords: ["ATL::CManualAccessor::CreateAccessor", "CreateAccessor", "ATL.CManualAccessor.CreateAccessor", "CManualAccessor.CreateAccessor", "CManualAccessor::CreateAccessor"]
dev_langs: ["C++"]
helpviewer_keywords: ["CreateAccessor method"]
ms.assetid: 594c8d6d-b49a-4818-a9a5-81c8115d4e42
author: "mikeblome"
ms.author: "mblome"
ms.workload: ["cplusplus", "data-storage"]
---
# CManualAccessor::CreateAccessor
Allocates memory for the column bind structures and initializes the column data members.  
  
## Syntax  
  
```
HRESULT CreateAccessor(int nBindEntries,   
  void* pBuffer,   
   DBLENGTH nBufferSize) throw();  
```  
  
#### Parameters  
 `nBindEntries`  
 [in] Number of columns. This number should match the number of calls to the [CManualAccessor::AddBindEntry](../../data/oledb/cmanualaccessor-addbindentry.md) function.  
  
 `pBuffer`  
 [in] A pointer to the buffer where the output columns are stored.  
  
 `nBufferSize`  
 [in] The size of the buffer in bytes.  
  
## Return Value  
 One of the standard `HRESULT` values.  
  
## Remarks  
 Call this function before you call the `CManualAccessor::AddBindEntry` function.  
  
## Requirements  
 **Header:** atldbcli.h  
  
## See Also  
 [CManualAccessor Class](../../data/oledb/cmanualaccessor-class.md)   
 [DBViewer sample](../../visual-cpp-samples.md)
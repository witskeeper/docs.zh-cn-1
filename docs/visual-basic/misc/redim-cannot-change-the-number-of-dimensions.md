---
title: “ReDim”无法更改维数
ms.date: 07/20/2015
f1_keywords:
- vbrArray_RankMismatch
ms.assetid: 52505298-9985-4682-8f6e-ff7d56077f34
ms.openlocfilehash: fb60c93f988ca40305f13cca07f55a70bd779081
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69664398"
---
# <a name="redim-cannot-change-the-number-of-dimensions"></a>“ReDim”无法更改维数
某操作尝试使用 `ReDim` 更改数组的秩（维数）。 `ReDim` 可以更改已形式声明的数组的一个或多个维度的大小，但它不能更改数组的秩。  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
- 确保想要更改的是数组的秩而不是其维度的大小，尽可能使用 `Dim` 声明具有所需秩的新数组。  
  
## <a name="see-also"></a>请参阅

- [Visual Basic 中的数组](../programming-guide/language-features/arrays/index.md)
- [Visual Basic 中的数组维度](../programming-guide/language-features/arrays/array-dimensions.md)
- [ReDim 语句](../../visual-basic/language-reference/statements/redim-statement.md)
- [Dim 语句](../../visual-basic/language-reference/statements/dim-statement.md)

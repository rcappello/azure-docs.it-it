---
title: Operatori utili nelle query di Azure Log Analytics | Microsoft Docs
description: Funzioni comuni da usare per diversi scenari nelle query di Log Analytics.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/21/2018
ms.author: bwren
ms.component: na
ms.openlocfilehash: 0b14c13462f15dd90285ed9e37080487324a4d85
ms.sourcegitcommit: 26cc9a1feb03a00d92da6f022d34940192ef2c42
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2018
ms.locfileid: "48831280"
---
# <a name="useful-operators-in-log-analytics-queries"></a>Operatori utili nelle query di Log Analytics

La tabella di seguito riporta alcune funzioni comuni da usare per diversi scenari nelle query di Log Analytics.

## <a name="useful-operators"></a>Operatori utili

Categoria                                |Funzione di analisi pertinente
----------------------------------------|----------------------------------------
Alias di colonna e selezione            |`project`, `project-away`, `extend`
Costanti e tabelle temporanee          |`let scalar_alias_name = …;` <br> `let table_alias_name =  …  …  … ;`| 
Operatori di stringa e confronto         |`startswith`, `!startswith`, `has`, `!has` <br> `contains`, `!contains`, `containscs` <br> `hasprefix`, `!hasprefix`, `hassuffix`, `!hassuffix`, `in`, `!in` <br> `matches regex` <br> `==`, `=~`, `!=`, `!~`
Funzioni stringa comuni                 |`strcat()`, `replace()`, `tolower()`, `toupper()`, `substring()`, `strlen()`
Funzioni matematiche comuni                   |`sqrt()`, `abs()` <br> `exp()`, `exp2()`, `exp10()`, `log()`, `log2()`, `log10()`, `pow()` <br> `gamma()`, `gammaln()`
Testo di analisi                            |`extract()`, `extractjson()`, `parse`, `split()`
Limitazione dell'output                         |`take`, `limit`, `top`, `sample`
Funzioni di data                          |`now()`, `ago()` <br> `datetime()`, `datepart()`, `timespan` <br> `startofday()`, `startofweek()`, `startofmonth()`, `startofyear()` <br> `endofday()`, `endofweek()`, `endofmonth()`, `endofyear()` <br> `dayofweek()`, `dayofmonth()`, `dayofyear()` <br> `getmonth()`, `getyear()`, `weekofyear()`, `monthofyear()`
Raggruppamento e aggregazioni                |`summarize by` <br> `max()`, `min()`, `count()`, `dcount()`, `avg()`, `sum()` <br> `stddev()`, `countif()`, `dcountif()`, `argmax()`, `argmin()` <br> `percentiles()`, `percentile_array()`
Join e unioni                        |`join kind=leftouter`, `inner`, `rightouter`, `fullouter`, `leftanti` <br> `union`
Ordinamento                             |`sort`, `order` 
Oggetto dinamico (JSON e matrice)         |`parsejson()` <br> `makeset()`, `makelist()` <br> `split()`, `arraylength()` <br> `zip()`, `pack()`
Operatori logici                       |`and`, `or`, `iff(condition, value_t, value_f)` <br> `binary_and()`, `binary_or()`, `binary_not()`, `binary_xor()`
Machine learning                        |`evaluate autocluster`, `basket`, `diffpatterns`, `extractcolumns`


## <a name="next-steps"></a>Passaggi successivi

- Esaminare la lezione sulla [scrittura di query in Log Analytics](get-started-queries.md).

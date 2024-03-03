# Filter GO table with keywords

After GO analysis, it is possible to obtain too many GO terms we need. Therefore, it is necessary to filter those GO terms according to the pathways of interest.

For example, we have a table of GO terms from the result of `gost {gprofiler2}`.

```r
head(gotable)
```

```csv
   V1 query significant       p_value term_size query_size intersection_size precision    recall    term_id source                                 term_name
1:  1  Down        TRUE 1.681437e-163      1875       1841               487 0.2645301 0.2597333 GO:0044281  GO:BP          small molecule metabolic process
2:  2  Down        TRUE 3.848459e-114      1007       1841               302 0.1640413 0.2999007 GO:0006082  GO:BP            organic acid metabolic process
3:  3  Down        TRUE 8.493759e-114       998       1841               300 0.1629549 0.3006012 GO:0043436  GO:BP                 oxoacid metabolic process
4:  4  Down        TRUE 1.826713e-111       978       1841               294 0.1596958 0.3006135 GO:0019752  GO:BP         carboxylic acid metabolic process
5:  5  Down        TRUE 9.949427e-102      6589       1841               856 0.4649647 0.1299135 GO:1901564  GO:BP organonitrogen compound metabolic process
6:  6  Down        TRUE  3.203960e-76      1450       1841               310 0.1683867 0.2137931 GO:0006629  GO:BP                   lipid metabolic process
```

And our interested pathways are:

* Metabolism-related markers include glucose and fatty acid metabolism.&#x20;
* Markers related to inflammation.&#x20;
* Markers related to fibrosis.&#x20;
* Markers related to pre-cancer.&#x20;
* Markers related to adverse effects.

```r
library(tidyverse)

filter_gotable <- gotable %>% 
  filter(str_detect(term_name, "glucose|fatty acid|inflammation|fibrosis|pre-cancer|adverse"))
```

`filter_gotable` will be the filtered result.

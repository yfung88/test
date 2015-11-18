```{.python .input  n=1}
import pandas as pd
import matplotlib.pyplot as plt
from bokeh.plotting import *
from bokeh.charts import HeatMap, Bar
import seaborn as sns

%matplotlib inline
```

```{.json .output n=1}
[
 {
  "ename": "ImportError",
  "evalue": "No module named seaborn",
  "output_type": "error",
  "traceback": [
   "\u001b[1;31m---------------------------------------------------------------------------\u001b[0m",
   "\u001b[1;31mImportError\u001b[0m                               Traceback (most recent call last)",
   "\u001b[1;32m<ipython-input-1-e898e9b939b5>\u001b[0m in \u001b[0;36m<module>\u001b[1;34m()\u001b[0m\n\u001b[0;32m      3\u001b[0m \u001b[1;32mfrom\u001b[0m \u001b[0mbokeh\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mplotting\u001b[0m \u001b[1;32mimport\u001b[0m \u001b[1;33m*\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m      4\u001b[0m \u001b[1;32mfrom\u001b[0m \u001b[0mbokeh\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mcharts\u001b[0m \u001b[1;32mimport\u001b[0m \u001b[0mHeatMap\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mBar\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m----> 5\u001b[1;33m \u001b[1;32mimport\u001b[0m \u001b[0mseaborn\u001b[0m \u001b[1;32mas\u001b[0m \u001b[0msns\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m      6\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m      7\u001b[0m \u001b[0mget_ipython\u001b[0m\u001b[1;33m(\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mmagic\u001b[0m\u001b[1;33m(\u001b[0m\u001b[1;34mu'matplotlib inline'\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;31mImportError\u001b[0m: No module named seaborn"
  ]
 }
]
```

```{.python .input  n=3}

```

```{.json .output n=3}
[
 {
  "ename": "SyntaxError",
  "evalue": "invalid syntax (<ipython-input-3-a357a8be2f4b>, line 1)",
  "output_type": "error",
  "traceback": [
   "\u001b[1;36m  File \u001b[1;32m\"<ipython-input-3-a357a8be2f4b>\"\u001b[1;36m, line \u001b[1;32m1\u001b[0m\n\u001b[1;33m    pip install git+git://github.com/mwaskom/seaborn.git#egg=seaborn\u001b[0m\n\u001b[1;37m              ^\u001b[0m\n\u001b[1;31mSyntaxError\u001b[0m\u001b[1;31m:\u001b[0m invalid syntax\n"
  ]
 }
]
```

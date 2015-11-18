```{.python .input  n=42}
import pandas as pd
from sklearn.ensemble import RandomForestClassifier
from sklearn.ensemble import RandomForestRegressor
```

```{.python .input  n=43}
cf = pd.read_excel('C:/Users/105059483/Desktop/HC-OrdersScrub.xlsx')
```

```{.python .input  n=44}
# cf.corr()
# cf.describe()
cf.head(5)
```

```{.json .output n=44}
[
 {
  "data": {
   "text/html": "<div>\n<table border=\"1\" class=\"dataframe\">\n  <thead>\n    <tr style=\"text-align: right;\">\n      <th></th>\n      <th>Order Year</th>\n      <th>Order Month</th>\n      <th>GL Modality Description</th>\n      <th>Product Group</th>\n      <th>Zone</th>\n      <th>LCT</th>\n      <th>Customer Name</th>\n      <th>Qty</th>\n      <th>List</th>\n      <th>Sales Rep Name</th>\n      <th>NEOV\nNew List</th>\n      <th>MM_SM</th>\n      <th>Cost Price</th>\n      <th>SM Rate</th>\n      <th>Target Disc %</th>\n      <th>OP SM%</th>\n      <th>Disc</th>\n    </tr>\n  </thead>\n  <tbody>\n    <tr>\n      <th>0</th>\n      <td>2012</td>\n      <td>July</td>\n      <td>GDXR-RAD</td>\n      <td>Discovery XR656 2D</td>\n      <td>West</td>\n      <td>Pacific NW</td>\n      <td>CALIFORNIA PACIFIC MEDICAL CENTER PACIFIC CAMPUS</td>\n      <td>1</td>\n      <td>879600.00</td>\n      <td>Robert Reeve</td>\n      <td>437269.050</td>\n      <td>290656.290</td>\n      <td>146612.76</td>\n      <td>0.664708</td>\n      <td>0.50</td>\n      <td>0.607313</td>\n      <td>0.502877</td>\n    </tr>\n    <tr>\n      <th>1</th>\n      <td>2014</td>\n      <td>August</td>\n      <td>GDXR Mammo</td>\n      <td>Mammo Other</td>\n      <td>West</td>\n      <td>Rocky Mountain</td>\n      <td>SCOTTSDALE ADVANCED IMAGING</td>\n      <td>0</td>\n      <td>4500.00</td>\n      <td>Lindsey Bye</td>\n      <td>2385.000</td>\n      <td>910.850</td>\n      <td>1474.15</td>\n      <td>0.381908</td>\n      <td>0.00</td>\n      <td>0.000000</td>\n      <td>0.470000</td>\n    </tr>\n    <tr>\n      <th>2</th>\n      <td>2012</td>\n      <td>February</td>\n      <td>Nuclear</td>\n      <td>Discovery NM-CT 670</td>\n      <td>East</td>\n      <td>Chesapeake</td>\n      <td>AUGUSTA HEALTH</td>\n      <td>1</td>\n      <td>1260318.32</td>\n      <td>Lawrence Schechtel</td>\n      <td>693175.063</td>\n      <td>419217.813</td>\n      <td>273957.25</td>\n      <td>0.604779</td>\n      <td>0.42</td>\n      <td>0.584000</td>\n      <td>0.450000</td>\n    </tr>\n    <tr>\n      <th>3</th>\n      <td>2012</td>\n      <td>February</td>\n      <td>Nuclear</td>\n      <td>Infinia Hawkeye</td>\n      <td>East</td>\n      <td>Chesapeake</td>\n      <td>AUGUSTA HEALTH</td>\n      <td>1</td>\n      <td>773040.00</td>\n      <td>Lawrence Schechtel</td>\n      <td>371839.200</td>\n      <td>169949.250</td>\n      <td>201889.95</td>\n      <td>0.457050</td>\n      <td>0.47</td>\n      <td>0.558000</td>\n      <td>0.518991</td>\n    </tr>\n    <tr>\n      <th>4</th>\n      <td>2012</td>\n      <td>February</td>\n      <td>Nuclear</td>\n      <td>Xeleris 3 Upgrades</td>\n      <td>East</td>\n      <td>Chesapeake</td>\n      <td>AUGUSTA HEALTH</td>\n      <td>6</td>\n      <td>68900.00</td>\n      <td>Lawrence Schechtel</td>\n      <td>33072.000</td>\n      <td>12493.320</td>\n      <td>20578.68</td>\n      <td>0.377761</td>\n      <td>0.50</td>\n      <td>0.507000</td>\n      <td>0.520000</td>\n    </tr>\n  </tbody>\n</table>\n</div>",
   "text/plain": "   Order Year Order Month GL Modality Description        Product Group  Zone  \\\n0        2012        July                GDXR-RAD   Discovery XR656 2D  West   \n1        2014      August              GDXR Mammo          Mammo Other  West   \n2        2012    February                 Nuclear  Discovery NM-CT 670  East   \n3        2012    February                 Nuclear      Infinia Hawkeye  East   \n4        2012    February                 Nuclear   Xeleris 3 Upgrades  East   \n\n              LCT                                     Customer Name  Qty  \\\n0      Pacific NW  CALIFORNIA PACIFIC MEDICAL CENTER PACIFIC CAMPUS    1   \n1  Rocky Mountain                       SCOTTSDALE ADVANCED IMAGING    0   \n2      Chesapeake                                    AUGUSTA HEALTH    1   \n3      Chesapeake                                    AUGUSTA HEALTH    1   \n4      Chesapeake                                    AUGUSTA HEALTH    6   \n\n         List      Sales Rep Name  NEOV\\nNew List        MM_SM  Cost Price  \\\n0   879600.00        Robert Reeve       437269.050  290656.290   146612.76   \n1     4500.00         Lindsey Bye         2385.000     910.850     1474.15   \n2  1260318.32  Lawrence Schechtel       693175.063  419217.813   273957.25   \n3   773040.00  Lawrence Schechtel       371839.200  169949.250   201889.95   \n4    68900.00  Lawrence Schechtel        33072.000   12493.320    20578.68   \n\n    SM Rate  Target Disc %    OP SM%      Disc  \n0  0.664708           0.50  0.607313  0.502877  \n1  0.381908           0.00  0.000000  0.470000  \n2  0.604779           0.42  0.584000  0.450000  \n3  0.457050           0.47  0.558000  0.518991  \n4  0.377761           0.50  0.507000  0.520000  "
  },
  "execution_count": 44,
  "metadata": {},
  "output_type": "execute_result"
 }
]
```

```{.python .input  n=45}
import statsmodels as sm
import statsmodels.formula.api as smf
```

```{.python .input  n=46}
# cf.rename(columns={'Product Groyp': 'Prodgrp', '$Customer Name': 'Custname'}, inplace=True)
```

```{.python .input  n=47}
cf.columns = [ c.replace(' ', '_') for c in cf.columns ]
```

```{.python .input  n=48}
# cf.head(5)
# mod = smf.ols(formula='Disc ~  C(Customer_Name) + C(Product_Group) + C(Sales_Rep_Name) + C(Zone) + C(LCT)+ List * Qty + TargetDisc', data=cf)
# # res = mod.fit()
# print res.summary()
```

```{.python .input  n=49}
# res = mod.fit()
# print res.summary()
```

```{.python .input  n=50}
Data = cf.iloc[:,:15]
```

```{.python .input  n=51}
Target = cf.iloc[:,-1]
```

```{.python .input  n=52}
clf = RandomForestRegressor(n_estimators = 15)
```

```{.python .input  n=75}
from sklearn.cross_validation import train_test_split
from sklearn.cross_validation import cross_val_score
from sklearn import cross_validation, linear_model
import numpy as np
```

```{.python .input  n=76}

X = Data
Y = Target
```

```{.python .input  n=77}
c = pd.get_dummies(Data)
```

```{.json .output n=77}
[
 {
  "ename": "MemoryError",
  "evalue": "",
  "output_type": "error",
  "traceback": [
   "\u001b[1;31m---------------------------------------------------------------------------\u001b[0m",
   "\u001b[1;31mMemoryError\u001b[0m                               Traceback (most recent call last)",
   "\u001b[1;32m<ipython-input-77-324b18db36ea>\u001b[0m in \u001b[0;36m<module>\u001b[1;34m()\u001b[0m\n\u001b[1;32m----> 1\u001b[1;33m \u001b[0mc\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mpd\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mget_dummies\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mData\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\reshape.pyc\u001b[0m in \u001b[0;36mget_dummies\u001b[1;34m(data, prefix, prefix_sep, dummy_na, columns, sparse)\u001b[0m\n\u001b[0;32m   1050\u001b[0m                                     dummy_na=dummy_na, sparse=sparse)\n\u001b[0;32m   1051\u001b[0m             \u001b[0mwith_dummies\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mappend\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mdummy\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 1052\u001b[1;33m         \u001b[0mresult\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mconcat\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mwith_dummies\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0maxis\u001b[0m\u001b[1;33m=\u001b[0m\u001b[1;36m1\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   1053\u001b[0m     \u001b[1;32melse\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   1054\u001b[0m         result = _get_dummies_1d(data, prefix, prefix_sep, dummy_na,\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\tools\\merge.pyc\u001b[0m in \u001b[0;36mconcat\u001b[1;34m(objs, axis, join, join_axes, ignore_index, keys, levels, names, verify_integrity, copy)\u001b[0m\n\u001b[0;32m    753\u001b[0m                        \u001b[0mverify_integrity\u001b[0m\u001b[1;33m=\u001b[0m\u001b[0mverify_integrity\u001b[0m\u001b[1;33m,\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m    754\u001b[0m                        copy=copy)\n\u001b[1;32m--> 755\u001b[1;33m     \u001b[1;32mreturn\u001b[0m \u001b[0mop\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mget_result\u001b[0m\u001b[1;33m(\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m    756\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m    757\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\tools\\merge.pyc\u001b[0m in \u001b[0;36mget_result\u001b[1;34m(self)\u001b[0m\n\u001b[0;32m    924\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m    925\u001b[0m             new_data = concatenate_block_managers(\n\u001b[1;32m--> 926\u001b[1;33m                 mgrs_indexers, self.new_axes, concat_axis=self.axis, copy=self.copy)\n\u001b[0m\u001b[0;32m    927\u001b[0m             \u001b[1;32mif\u001b[0m \u001b[1;32mnot\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mcopy\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m    928\u001b[0m                 \u001b[0mnew_data\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_consolidate_inplace\u001b[0m\u001b[1;33m(\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\internals.pyc\u001b[0m in \u001b[0;36mconcatenate_block_managers\u001b[1;34m(mgrs_indexers, axes, concat_axis, copy)\u001b[0m\n\u001b[0;32m   4061\u001b[0m                                                 copy=copy),\n\u001b[0;32m   4062\u001b[0m                          placement=placement)\n\u001b[1;32m-> 4063\u001b[1;33m               for placement, join_units in concat_plan]\n\u001b[0m\u001b[0;32m   4064\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   4065\u001b[0m     \u001b[1;32mreturn\u001b[0m \u001b[0mBlockManager\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mblocks\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0maxes\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\internals.pyc\u001b[0m in \u001b[0;36mconcatenate_join_units\u001b[1;34m(join_units, concat_axis, copy)\u001b[0m\n\u001b[0;32m   4150\u001b[0m         \u001b[1;32mraise\u001b[0m \u001b[0mAssertionError\u001b[0m\u001b[1;33m(\u001b[0m\u001b[1;34m\"Concatenating join units along axis0\"\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   4151\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 4152\u001b[1;33m     \u001b[0mempty_dtype\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mupcasted_na\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mget_empty_dtype_and_na\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mjoin_units\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   4153\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   4154\u001b[0m     to_concat = [ju.get_reindexed_values(empty_dtype=empty_dtype,\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\internals.pyc\u001b[0m in \u001b[0;36mget_empty_dtype_and_na\u001b[1;34m(join_units)\u001b[0m\n\u001b[0;32m   4114\u001b[0m         \u001b[1;31m# are only null blocks, when same upcasting rules must be applied to\u001b[0m\u001b[1;33m\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   4115\u001b[0m         \u001b[1;31m# null upcast classes.\u001b[0m\u001b[1;33m\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 4116\u001b[1;33m         \u001b[1;32mif\u001b[0m \u001b[0munit\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mis_null\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   4117\u001b[0m             \u001b[0mnull_upcast_classes\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0madd\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mupcast_cls\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   4118\u001b[0m         \u001b[1;32melse\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mpandas\\src\\properties.pyx\u001b[0m in \u001b[0;36mpandas.lib.cache_readonly.__get__ (pandas\\lib.c:41917)\u001b[1;34m()\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\internals.pyc\u001b[0m in \u001b[0;36mis_null\u001b[1;34m(self)\u001b[0m\n\u001b[0;32m   4379\u001b[0m         \u001b[1;31m# a block is NOT null, chunks should help in such cases.  1000 value\u001b[0m\u001b[1;33m\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   4380\u001b[0m         \u001b[1;31m# was chosen rather arbitrarily.\u001b[0m\u001b[1;33m\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 4381\u001b[1;33m         \u001b[0mvalues_flat\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mblock\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mvalues\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mravel\u001b[0m\u001b[1;33m(\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   4382\u001b[0m         \u001b[0mtotal_len\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mvalues_flat\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mshape\u001b[0m\u001b[1;33m[\u001b[0m\u001b[1;36m0\u001b[0m\u001b[1;33m]\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   4383\u001b[0m         \u001b[0mchunk_len\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mmax\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mtotal_len\u001b[0m \u001b[1;33m//\u001b[0m \u001b[1;36m40\u001b[0m\u001b[1;33m,\u001b[0m \u001b[1;36m1000\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;31mMemoryError\u001b[0m: "
  ]
 }
]
```

```{.python .input  n=74}
xtrain, xtest, ytrain, ytest = train_test_split(c, Target, test_size=0.3)

```

```{.json .output n=74}
[
 {
  "ename": "MemoryError",
  "evalue": "",
  "output_type": "error",
  "traceback": [
   "\u001b[1;31m---------------------------------------------------------------------------\u001b[0m",
   "\u001b[1;31mMemoryError\u001b[0m                               Traceback (most recent call last)",
   "\u001b[1;32m<ipython-input-74-9a7533afd729>\u001b[0m in \u001b[0;36m<module>\u001b[1;34m()\u001b[0m\n\u001b[1;32m----> 1\u001b[1;33m \u001b[0mxtrain\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mxtest\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mytrain\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mytest\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mtrain_test_split\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mc\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mTarget\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mtest_size\u001b[0m\u001b[1;33m=\u001b[0m\u001b[1;36m0.3\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\sklearn\\cross_validation.pyc\u001b[0m in \u001b[0;36mtrain_test_split\u001b[1;34m(*arrays, **options)\u001b[0m\n\u001b[0;32m   1814\u001b[0m     \u001b[0mtrain\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mtest\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mnext\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0miter\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mcv\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   1815\u001b[0m     return list(chain.from_iterable((safe_indexing(a, train),\n\u001b[1;32m-> 1816\u001b[1;33m                                      safe_indexing(a, test)) for a in arrays))\n\u001b[0m\u001b[0;32m   1817\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   1818\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\sklearn\\cross_validation.pyc\u001b[0m in \u001b[0;36m<genexpr>\u001b[1;34m((a,))\u001b[0m\n\u001b[0;32m   1814\u001b[0m     \u001b[0mtrain\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mtest\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mnext\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0miter\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mcv\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   1815\u001b[0m     return list(chain.from_iterable((safe_indexing(a, train),\n\u001b[1;32m-> 1816\u001b[1;33m                                      safe_indexing(a, test)) for a in arrays))\n\u001b[0m\u001b[0;32m   1817\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   1818\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\sklearn\\utils\\__init__.pyc\u001b[0m in \u001b[0;36msafe_indexing\u001b[1;34m(X, indices)\u001b[0m\n\u001b[0;32m    150\u001b[0m     \u001b[1;32mif\u001b[0m \u001b[0mhasattr\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mX\u001b[0m\u001b[1;33m,\u001b[0m \u001b[1;34m\"iloc\"\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m    151\u001b[0m         \u001b[1;31m# Pandas Dataframes and Series\u001b[0m\u001b[1;33m\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m--> 152\u001b[1;33m         \u001b[1;32mreturn\u001b[0m \u001b[0mX\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0miloc\u001b[0m\u001b[1;33m[\u001b[0m\u001b[0mindices\u001b[0m\u001b[1;33m]\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m    153\u001b[0m     \u001b[1;32melif\u001b[0m \u001b[0mhasattr\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mX\u001b[0m\u001b[1;33m,\u001b[0m \u001b[1;34m\"shape\"\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m    154\u001b[0m         if hasattr(X, 'take') and (hasattr(indices, 'dtype') and\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\indexing.pyc\u001b[0m in \u001b[0;36m__getitem__\u001b[1;34m(self, key)\u001b[0m\n\u001b[0;32m   1187\u001b[0m             \u001b[1;32mreturn\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_getitem_tuple\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mkey\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   1188\u001b[0m         \u001b[1;32melse\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 1189\u001b[1;33m             \u001b[1;32mreturn\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_getitem_axis\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mkey\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0maxis\u001b[0m\u001b[1;33m=\u001b[0m\u001b[1;36m0\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   1190\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   1191\u001b[0m     \u001b[1;32mdef\u001b[0m \u001b[0m_getitem_axis\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mself\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mkey\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0maxis\u001b[0m\u001b[1;33m=\u001b[0m\u001b[1;36m0\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\indexing.pyc\u001b[0m in \u001b[0;36m_getitem_axis\u001b[1;34m(self, key, axis)\u001b[0m\n\u001b[0;32m   1478\u001b[0m                 \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_is_valid_integer\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mkey\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0maxis\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   1479\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 1480\u001b[1;33m             \u001b[1;32mreturn\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_get_loc\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mkey\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0maxis\u001b[0m\u001b[1;33m=\u001b[0m\u001b[0maxis\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   1481\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   1482\u001b[0m     \u001b[1;32mdef\u001b[0m \u001b[0m_convert_to_indexer\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mself\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mobj\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0maxis\u001b[0m\u001b[1;33m=\u001b[0m\u001b[1;36m0\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mis_setter\u001b[0m\u001b[1;33m=\u001b[0m\u001b[0mFalse\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\indexing.pyc\u001b[0m in \u001b[0;36m_get_loc\u001b[1;34m(self, key, axis)\u001b[0m\n\u001b[0;32m     87\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m     88\u001b[0m     \u001b[1;32mdef\u001b[0m \u001b[0m_get_loc\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mself\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mkey\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0maxis\u001b[0m\u001b[1;33m=\u001b[0m\u001b[1;36m0\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m---> 89\u001b[1;33m         \u001b[1;32mreturn\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mobj\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_ixs\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mkey\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0maxis\u001b[0m\u001b[1;33m=\u001b[0m\u001b[0maxis\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m     90\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m     91\u001b[0m     \u001b[1;32mdef\u001b[0m \u001b[0m_slice\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mself\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mobj\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0maxis\u001b[0m\u001b[1;33m=\u001b[0m\u001b[1;36m0\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mkind\u001b[0m\u001b[1;33m=\u001b[0m\u001b[0mNone\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\frame.pyc\u001b[0m in \u001b[0;36m_ixs\u001b[1;34m(self, i, axis)\u001b[0m\n\u001b[0;32m   1720\u001b[0m                 \u001b[1;32mif\u001b[0m \u001b[0misinstance\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mlabel\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mIndex\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   1721\u001b[0m                     \u001b[1;31m# a location index by definition\u001b[0m\u001b[1;33m\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 1722\u001b[1;33m                     \u001b[0mresult\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mtake\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mi\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0maxis\u001b[0m\u001b[1;33m=\u001b[0m\u001b[0maxis\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   1723\u001b[0m                     \u001b[0mcopy\u001b[0m\u001b[1;33m=\u001b[0m\u001b[0mTrue\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   1724\u001b[0m                 \u001b[1;32melse\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\generic.pyc\u001b[0m in \u001b[0;36mtake\u001b[1;34m(self, indices, axis, convert, is_copy)\u001b[0m\n\u001b[0;32m   1353\u001b[0m         \"\"\"\n\u001b[0;32m   1354\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 1355\u001b[1;33m         \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_consolidate_inplace\u001b[0m\u001b[1;33m(\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   1356\u001b[0m         new_data = self._data.take(indices,\n\u001b[0;32m   1357\u001b[0m                                    \u001b[0maxis\u001b[0m\u001b[1;33m=\u001b[0m\u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_get_block_manager_axis\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0maxis\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m,\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\generic.pyc\u001b[0m in \u001b[0;36m_consolidate_inplace\u001b[1;34m(self)\u001b[0m\n\u001b[0;32m   2199\u001b[0m         \u001b[1;32mdef\u001b[0m \u001b[0mf\u001b[0m\u001b[1;33m(\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   2200\u001b[0m             \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_data\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_data\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mconsolidate\u001b[0m\u001b[1;33m(\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 2201\u001b[1;33m         \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_protect_consolidate\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mf\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   2202\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   2203\u001b[0m     \u001b[1;32mdef\u001b[0m \u001b[0mconsolidate\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mself\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0minplace\u001b[0m\u001b[1;33m=\u001b[0m\u001b[0mFalse\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\generic.pyc\u001b[0m in \u001b[0;36m_protect_consolidate\u001b[1;34m(self, f)\u001b[0m\n\u001b[0;32m   2190\u001b[0m         \u001b[1;34m\"\"\" consolidate _data. if the blocks have changed, then clear the cache \"\"\"\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   2191\u001b[0m         \u001b[0mblocks_before\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mlen\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_data\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mblocks\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 2192\u001b[1;33m         \u001b[0mresult\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mf\u001b[0m\u001b[1;33m(\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   2193\u001b[0m         \u001b[1;32mif\u001b[0m \u001b[0mlen\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_data\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mblocks\u001b[0m\u001b[1;33m)\u001b[0m \u001b[1;33m!=\u001b[0m \u001b[0mblocks_before\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   2194\u001b[0m             \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_clear_item_cache\u001b[0m\u001b[1;33m(\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\generic.pyc\u001b[0m in \u001b[0;36mf\u001b[1;34m()\u001b[0m\n\u001b[0;32m   2198\u001b[0m         \u001b[1;34m\"\"\" we are inplace consolidating; return None \"\"\"\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   2199\u001b[0m         \u001b[1;32mdef\u001b[0m \u001b[0mf\u001b[0m\u001b[1;33m(\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 2200\u001b[1;33m             \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_data\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_data\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mconsolidate\u001b[0m\u001b[1;33m(\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   2201\u001b[0m         \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_protect_consolidate\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mf\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   2202\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\internals.pyc\u001b[0m in \u001b[0;36mconsolidate\u001b[1;34m(self)\u001b[0m\n\u001b[0;32m   2832\u001b[0m         \u001b[0mbm\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m__class__\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mblocks\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0maxes\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   2833\u001b[0m         \u001b[0mbm\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_is_consolidated\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mFalse\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 2834\u001b[1;33m         \u001b[0mbm\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_consolidate_inplace\u001b[0m\u001b[1;33m(\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   2835\u001b[0m         \u001b[1;32mreturn\u001b[0m \u001b[0mbm\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   2836\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\internals.pyc\u001b[0m in \u001b[0;36m_consolidate_inplace\u001b[1;34m(self)\u001b[0m\n\u001b[0;32m   2837\u001b[0m     \u001b[1;32mdef\u001b[0m \u001b[0m_consolidate_inplace\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mself\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   2838\u001b[0m         \u001b[1;32mif\u001b[0m \u001b[1;32mnot\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mis_consolidated\u001b[0m\u001b[1;33m(\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 2839\u001b[1;33m             \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mblocks\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mtuple\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0m_consolidate\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mblocks\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   2840\u001b[0m             \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_is_consolidated\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mTrue\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   2841\u001b[0m             \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_known_consolidated\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mTrue\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\internals.pyc\u001b[0m in \u001b[0;36m_consolidate\u001b[1;34m(blocks)\u001b[0m\n\u001b[0;32m   3819\u001b[0m     \u001b[1;32mfor\u001b[0m \u001b[1;33m(\u001b[0m\u001b[0m_can_consolidate\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mdtype\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mgroup_blocks\u001b[0m \u001b[1;32min\u001b[0m \u001b[0mgrouper\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   3820\u001b[0m         merged_blocks = _merge_blocks(list(group_blocks), dtype=dtype,\n\u001b[1;32m-> 3821\u001b[1;33m                                       _can_consolidate=_can_consolidate)\n\u001b[0m\u001b[0;32m   3822\u001b[0m         \u001b[1;32mif\u001b[0m \u001b[0misinstance\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mmerged_blocks\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mlist\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   3823\u001b[0m             \u001b[0mnew_blocks\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mextend\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mmerged_blocks\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\internals.pyc\u001b[0m in \u001b[0;36m_merge_blocks\u001b[1;34m(blocks, dtype, _can_consolidate)\u001b[0m\n\u001b[0;32m   3845\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   3846\u001b[0m         \u001b[0margsort\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mnp\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0margsort\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mnew_mgr_locs\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 3847\u001b[1;33m         \u001b[0mnew_values\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mnew_values\u001b[0m\u001b[1;33m[\u001b[0m\u001b[0margsort\u001b[0m\u001b[1;33m]\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   3848\u001b[0m         \u001b[0mnew_mgr_locs\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mnew_mgr_locs\u001b[0m\u001b[1;33m[\u001b[0m\u001b[0margsort\u001b[0m\u001b[1;33m]\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   3849\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;31mMemoryError\u001b[0m: "
  ]
 }
]
```

```{.python .input}
out = clf.fit(xtrain,ytrain)
```

```{.python .input  n=31}
train_pred = out.predict(xtrain)
```

```{.python .input  n=32}
test_pred = out.predict(xtest)
```

```{.python .input  n=33}
err_train = np.sqrt(np.mean(ytrain-train_pred)**2)
```

```{.python .input  n=34}
err_train
```

```{.json .output n=34}
[
 {
  "data": {
   "text/plain": "1.8621666825104123e-05"
  },
  "execution_count": 34,
  "metadata": {},
  "output_type": "execute_result"
 }
]
```

```{.python .input  n=35}
err_pred = np.sqrt(np.mean(ytest-test_pred)**2)
```

```{.python .input  n=36}
err_pred
```

```{.json .output n=36}
[
 {
  "data": {
   "text/plain": "0.00084874545657727938"
  },
  "execution_count": 36,
  "metadata": {},
  "output_type": "execute_result"
 }
]
```

```{.python .input}
out.predict(c)
```

```{.python .input  n=39}
X['Prediction'] = out.predict(c)
```

```{.python .input  n=39}
X['Discount'] = Y
```

```{.python .input  n=40}
res = []
uc = []
b = []
```

```{.python .input  n=42}
b = 0
res = []
for i in range(15):
    b = 0
#     print i
#     print b
    b = out.estimators_[i].predict(c)
#     print b
    res.append(b)
print len(res)
```

```{.json .output n=42}
[
 {
  "name": "stdout",
  "output_type": "stream",
  "text": "15\n"
 }
]
```

```{.python .input  n=44}
res3 = []
import numpy as np 
res2 = np.matrix(res)
# print len(res2)
# print res2
res4 = res2.transpose()
for i in res4:
    res3.append(i.std())
# res3 = res2.std()
# print res3
# print res3
X['New'] = res3[::]
# for i in res3:
#     res6 = int(res3[i]*2)
# # X['Prediction']
# print (res3)
# del X['New2']
X['New'] = X['New'] * 2
X['Cupper'] = X['Prediction'] + X['New']
X['Clower'] = X['Prediction'] - X['New']
X['PredCheck'] = (X['Cupper'] - X['Clower'])/2 + X['Clower']

```

```{.python .input  n=78}
import matplotlib.pyplot as plt
% pylab inline
```

```{.json .output n=78}
[
 {
  "name": "stdout",
  "output_type": "stream",
  "text": "Populating the interactive namespace from numpy and matplotlib\n"
 },
 {
  "name": "stderr",
  "output_type": "stream",
  "text": "WARNING: pylab import has clobbered these variables: ['clf']\n`%matplotlib` prevents importing * from pylab and numpy\n"
 }
]
```

```{.python .input  n=79}
XSorted = X.sort('Discount')
XSorted = XSorted.reset_index()
```

```{.json .output n=79}
[
 {
  "ename": "KeyError",
  "evalue": "'Discount'",
  "output_type": "error",
  "traceback": [
   "\u001b[1;31m---------------------------------------------------------------------------\u001b[0m",
   "\u001b[1;31mKeyError\u001b[0m                                  Traceback (most recent call last)",
   "\u001b[1;32m<ipython-input-79-e7b7a7825e2e>\u001b[0m in \u001b[0;36m<module>\u001b[1;34m()\u001b[0m\n\u001b[1;32m----> 1\u001b[1;33m \u001b[0mXSorted\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mX\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0msort\u001b[0m\u001b[1;33m(\u001b[0m\u001b[1;34m'Discount'\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m      2\u001b[0m \u001b[0mXSorted\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mXSorted\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mreset_index\u001b[0m\u001b[1;33m(\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\frame.pyc\u001b[0m in \u001b[0;36msort\u001b[1;34m(self, columns, axis, ascending, inplace, kind, na_position)\u001b[0m\n\u001b[0;32m   2913\u001b[0m         \"\"\"\n\u001b[0;32m   2914\u001b[0m         return self.sort_index(by=columns, axis=axis, ascending=ascending,\n\u001b[1;32m-> 2915\u001b[1;33m                                inplace=inplace, kind=kind, na_position=na_position)\n\u001b[0m\u001b[0;32m   2916\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   2917\u001b[0m     def sort_index(self, axis=0, by=None, ascending=True, inplace=False,\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\frame.pyc\u001b[0m in \u001b[0;36msort_index\u001b[1;34m(self, axis, by, ascending, inplace, kind, na_position)\u001b[0m\n\u001b[0;32m   2981\u001b[0m             \u001b[1;32melse\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   2982\u001b[0m                 \u001b[0mby\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mby\u001b[0m\u001b[1;33m[\u001b[0m\u001b[1;36m0\u001b[0m\u001b[1;33m]\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 2983\u001b[1;33m                 \u001b[0mk\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m[\u001b[0m\u001b[0mby\u001b[0m\u001b[1;33m]\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mvalues\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   2984\u001b[0m                 \u001b[1;32mif\u001b[0m \u001b[0mk\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mndim\u001b[0m \u001b[1;33m==\u001b[0m \u001b[1;36m2\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   2985\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\frame.pyc\u001b[0m in \u001b[0;36m__getitem__\u001b[1;34m(self, key)\u001b[0m\n\u001b[0;32m   1795\u001b[0m             \u001b[1;32mreturn\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_getitem_multilevel\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mkey\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   1796\u001b[0m         \u001b[1;32melse\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 1797\u001b[1;33m             \u001b[1;32mreturn\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_getitem_column\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mkey\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   1798\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   1799\u001b[0m     \u001b[1;32mdef\u001b[0m \u001b[0m_getitem_column\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mself\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mkey\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\frame.pyc\u001b[0m in \u001b[0;36m_getitem_column\u001b[1;34m(self, key)\u001b[0m\n\u001b[0;32m   1802\u001b[0m         \u001b[1;31m# get column\u001b[0m\u001b[1;33m\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   1803\u001b[0m         \u001b[1;32mif\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mcolumns\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mis_unique\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 1804\u001b[1;33m             \u001b[1;32mreturn\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_get_item_cache\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mkey\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   1805\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   1806\u001b[0m         \u001b[1;31m# duplicate columns & possible reduce dimensionaility\u001b[0m\u001b[1;33m\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\generic.pyc\u001b[0m in \u001b[0;36m_get_item_cache\u001b[1;34m(self, item)\u001b[0m\n\u001b[0;32m   1082\u001b[0m         \u001b[0mres\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mcache\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mget\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mitem\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   1083\u001b[0m         \u001b[1;32mif\u001b[0m \u001b[0mres\u001b[0m \u001b[1;32mis\u001b[0m \u001b[0mNone\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 1084\u001b[1;33m             \u001b[0mvalues\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_data\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mget\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mitem\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   1085\u001b[0m             \u001b[0mres\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_box_item_values\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mitem\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mvalues\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   1086\u001b[0m             \u001b[0mcache\u001b[0m\u001b[1;33m[\u001b[0m\u001b[0mitem\u001b[0m\u001b[1;33m]\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mres\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\internals.pyc\u001b[0m in \u001b[0;36mget\u001b[1;34m(self, item, fastpath)\u001b[0m\n\u001b[0;32m   2849\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   2850\u001b[0m             \u001b[1;32mif\u001b[0m \u001b[1;32mnot\u001b[0m \u001b[0misnull\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mitem\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 2851\u001b[1;33m                 \u001b[0mloc\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mitems\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mget_loc\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mitem\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   2852\u001b[0m             \u001b[1;32melse\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   2853\u001b[0m                 \u001b[0mindexer\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mnp\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0marange\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mlen\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mitems\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m[\u001b[0m\u001b[0misnull\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mitems\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m]\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mC:\\Users\\105059483\\AppData\\Local\\Continuum\\Anaconda\\lib\\site-packages\\pandas\\core\\index.pyc\u001b[0m in \u001b[0;36mget_loc\u001b[1;34m(self, key, method)\u001b[0m\n\u001b[0;32m   1570\u001b[0m         \"\"\"\n\u001b[0;32m   1571\u001b[0m         \u001b[1;32mif\u001b[0m \u001b[0mmethod\u001b[0m \u001b[1;32mis\u001b[0m \u001b[0mNone\u001b[0m\u001b[1;33m:\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[1;32m-> 1572\u001b[1;33m             \u001b[1;32mreturn\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0m_engine\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mget_loc\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0m_values_from_object\u001b[0m\u001b[1;33m(\u001b[0m\u001b[0mkey\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0m\u001b[0;32m   1573\u001b[0m \u001b[1;33m\u001b[0m\u001b[0m\n\u001b[0;32m   1574\u001b[0m         \u001b[0mindexer\u001b[0m \u001b[1;33m=\u001b[0m \u001b[0mself\u001b[0m\u001b[1;33m.\u001b[0m\u001b[0mget_indexer\u001b[0m\u001b[1;33m(\u001b[0m\u001b[1;33m[\u001b[0m\u001b[0mkey\u001b[0m\u001b[1;33m]\u001b[0m\u001b[1;33m,\u001b[0m \u001b[0mmethod\u001b[0m\u001b[1;33m=\u001b[0m\u001b[0mmethod\u001b[0m\u001b[1;33m)\u001b[0m\u001b[1;33m\u001b[0m\u001b[0m\n",
   "\u001b[1;32mpandas\\index.pyx\u001b[0m in \u001b[0;36mpandas.index.IndexEngine.get_loc (pandas\\index.c:3824)\u001b[1;34m()\u001b[0m\n",
   "\u001b[1;32mpandas\\index.pyx\u001b[0m in \u001b[0;36mpandas.index.IndexEngine.get_loc (pandas\\index.c:3704)\u001b[1;34m()\u001b[0m\n",
   "\u001b[1;32mpandas\\hashtable.pyx\u001b[0m in \u001b[0;36mpandas.hashtable.PyObjectHashTable.get_item (pandas\\hashtable.c:12280)\u001b[1;34m()\u001b[0m\n",
   "\u001b[1;32mpandas\\hashtable.pyx\u001b[0m in \u001b[0;36mpandas.hashtable.PyObjectHashTable.get_item (pandas\\hashtable.c:12231)\u001b[1;34m()\u001b[0m\n",
   "\u001b[1;31mKeyError\u001b[0m: 'Discount'"
  ]
 }
]
```

```{.python .input}
plt.figure(figsize=(10,6))
plt.scatter(XSorted.index,XSorted['Discount'], c = 'black')
# plt.scatter(XSorted.index,XSorted['Prediction'], c='black')
plt.errorbar(XSorted.index, XSorted['Prediction'],yerr = XSorted['New'],c = 'red',fmt ='o')
```

```{.python .input}

```

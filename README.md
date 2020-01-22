
# Evidently: Simulate Evidence Accumulation Models in Python

`Evidently` is a python package for working with evidence accumulation models.

It provides

- Efficient functions for simulating data from a range of models.
- Classes that make it easier to tweak model parameters and manage simulated data.
- A consistent way to implement new models.
- Visualisation, including interactive widgets for Jupyter.
- Kernel density-based methods for estimating 
  the likelihood of real data under a given model/set of parameters,
  allowing parameter estimation and model comparision.
  


## Basic Use


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import evidently
```

## Set up a model and provide parameters


```python
model = evidently.models.Diffusion(pars=[1., .5, -.25, .8, .4], max_time=5., dt=.001)
model
```




    Classic Drift Diffusion Model
    Parameters: [t0 = 1.00, v = 0.50, z = -0.25, a = 0.80, c = 0.40]




```python
model.describe_parameters()
```

    Parameters for Classic Drift Diffusion Model:
    - t0   : 1.00  ~ Non-decision time
    - v    : 0.50  ~ Drift rate
    - z    : -0.25 ~ Starting point
    - a    : 0.80  ~ Threshold (±)
    - c    : 0.40  ~ Noise SD


## Simulate data


```python
X, responses, rts = model.do_dataset(n=1000)
```


```python
X.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0.000</th>
      <th>0.001</th>
      <th>0.002</th>
      <th>0.003</th>
      <th>0.004</th>
      <th>0.005</th>
      <th>0.006</th>
      <th>0.007</th>
      <th>0.008</th>
      <th>0.009</th>
      <th>...</th>
      <th>4.990</th>
      <th>4.991</th>
      <th>4.992</th>
      <th>4.993</th>
      <th>4.994</th>
      <th>4.995</th>
      <th>4.996</th>
      <th>4.997</th>
      <th>4.998</th>
      <th>4.999</th>
    </tr>
    <tr>
      <th>sim</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.177320</td>
      <td>-0.172509</td>
      <td>-0.180896</td>
      <td>-0.170542</td>
      <td>-0.180081</td>
      <td>-0.185857</td>
      <td>-0.219079</td>
      <td>-0.216570</td>
      <td>-0.243592</td>
      <td>-0.228941</td>
      <td>...</td>
      <td>0.806232</td>
      <td>0.788164</td>
      <td>0.806839</td>
      <td>0.803457</td>
      <td>0.801539</td>
      <td>0.809231</td>
      <td>0.801905</td>
      <td>0.790250</td>
      <td>0.760990</td>
      <td>0.754869</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.186142</td>
      <td>-0.184029</td>
      <td>-0.180858</td>
      <td>-0.154955</td>
      <td>-0.162967</td>
      <td>-0.181358</td>
      <td>-0.175131</td>
      <td>-0.182371</td>
      <td>-0.188530</td>
      <td>-0.177745</td>
      <td>...</td>
      <td>0.669138</td>
      <td>0.666357</td>
      <td>0.685992</td>
      <td>0.684661</td>
      <td>0.698854</td>
      <td>0.697201</td>
      <td>0.710906</td>
      <td>0.701409</td>
      <td>0.683404</td>
      <td>0.698551</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.200028</td>
      <td>-0.192888</td>
      <td>-0.181851</td>
      <td>-0.177324</td>
      <td>-0.166068</td>
      <td>-0.160294</td>
      <td>-0.155698</td>
      <td>-0.155691</td>
      <td>-0.150309</td>
      <td>-0.150653</td>
      <td>...</td>
      <td>1.964930</td>
      <td>1.961359</td>
      <td>1.947321</td>
      <td>1.940496</td>
      <td>1.927814</td>
      <td>1.932019</td>
      <td>1.947697</td>
      <td>1.950462</td>
      <td>1.963250</td>
      <td>1.968946</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.201833</td>
      <td>-0.202006</td>
      <td>-0.196713</td>
      <td>-0.189972</td>
      <td>-0.197487</td>
      <td>-0.203684</td>
      <td>-0.200066</td>
      <td>-0.185335</td>
      <td>-0.204493</td>
      <td>-0.203075</td>
      <td>...</td>
      <td>3.281451</td>
      <td>3.284107</td>
      <td>3.300431</td>
      <td>3.316514</td>
      <td>3.328128</td>
      <td>3.343874</td>
      <td>3.347172</td>
      <td>3.348986</td>
      <td>3.348839</td>
      <td>3.352577</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.190844</td>
      <td>-0.169060</td>
      <td>-0.169779</td>
      <td>-0.176012</td>
      <td>-0.175741</td>
      <td>-0.198513</td>
      <td>-0.201160</td>
      <td>-0.201007</td>
      <td>-0.193516</td>
      <td>-0.197130</td>
      <td>...</td>
      <td>1.668648</td>
      <td>1.663570</td>
      <td>1.643179</td>
      <td>1.639827</td>
      <td>1.658923</td>
      <td>1.669544</td>
      <td>1.676298</td>
      <td>1.679252</td>
      <td>1.677764</td>
      <td>1.659028</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 5000 columns</p>
</div>




```python
print(responses[:5]) 
print(rts[:5])
```

    [ 1. -1.  1.  1.  1.]
    [3.445 0.553 1.811 1.888 3.087]


## Visualise

The `evidently.viz` submodule contains a collection of `matplotlib`-based functions for visualising model simulations. Here are a few examples.


```python
ax = evidently.viz.setup_ddm_plot(model) # Uses model info to draw bounds.
evidently.viz.plot_trace_mean(model, X, ax=ax); # Plots simulations
```


![png](imgs/README_12_0.png)



```python
ax = evidently.viz.setup_ddm_plot(model)
evidently.viz.plot_traces(model, X, responses, rts, ax=ax, 
                          terminate=True, show_mean=True); # Show raw data
```

    /home/eoin/miniconda3/lib/python3.7/site-packages/evidently/viz.py:162: RuntimeWarning: invalid value encountered in greater
      X.iloc[i, t > rt] = np.nan



![png](imgs/README_13_1.png)



```python
ax = evidently.viz.setup_ddm_plot(model)
for resp in [1, -1]:
    mask = (responses == resp) # Split by response
    evidently.viz.plot_trace_mean(model, X[mask], ax=ax, label='Response: %i' % resp)
plt.legend();
```


![png](imgs/README_14_0.png)



```python
mX = evidently.utils.lock_to_movement(X, rts, duration=2) # Time-lock to threshold crossing
ax = evidently.viz.setup_ddm_plot(model, time_range=(-2, 0))
evidently.viz.plot_traces(model, mX, responses, rts, ax=ax, show_mean=True);
```


![png](imgs/README_15_0.png)



```python
ax = evidently.viz.setup_ddm_plot(model, time_range=(-2, 0))
for resp in [1, -1]:
    mask = responses == resp
    resp_mX = evidently.utils.lock_to_movement(X[mask], rts[mask])
    evidently.viz.plot_trace_mean(model, resp_mX, ax=ax, label='Response: %i' % resp)
plt.legend();
```


![png](imgs/README_16_0.png)


There high-level functions can create multi-axis figures.


```python
evidently.viz.visualise_model(model, model_type='ddm', measure='means');
```


![png](imgs/README_18_0.png)


## Interactive Visualisation

Using the `ipywidgets` package, we can wrap high level visualisation functions like `accum.viz.visualise_ddm` in a call to `ipywidgets` to make them interactive.

To try the interactive plots, download this repository to your own computer,
or run the code in the cloud by visiting [this Binder notebook]().


<!-- This will work once we run gen_readme.sh -->
![](imgs/interactive.gif)


```python
from ipywidgets import interact, FloatSlider
def fs(v, low, high, step, desc=''):
    return FloatSlider(value=v, min=low, max=high, step=step, description=desc, continuous_update=False)

def ddm_simulation_plot(t0=1., v=.5, z=0., a=.5, c=.1):
    model = evidently.Diffusion(pars=[t0, v, z, a, c])
    evidently.viz.visualise_model(model)
    title = 't0 = %.1f, Drift = %.1f, Bias = %.1f, Threshold = %.1f; Noise SD = %.1f' % (t0, v, z, a, c)
    plt.suptitle(title, y=1.01)

interact(ddm_simulation_plot,
         t0  = fs(1., 0, 2., .1,   't0'),
         v   = fs(.5, 0, 2., .1,   'Drift'),
         z   = fs(0., -1., 1., .1,  'Bias'),
         a     = fs(.5, 0., 2., .1,   'Threshold'),
         c   = fs(.1, 0., 1., .1,   'Noise SD'));
```


![png](imgs/README_21_0.png)


# Other Models

The following model classes are currently available:

- Diffusion
- Wald
- HDiffision (Hierarchical Diffusion)
- HWald (Hierarchical Wald)
- Race

See the [API](http://eointravers.com/code/evidently/api.html) for more details.

# Road Map


## More Models!

I have already implemented several of these models, but have to integrate them with the rest of the package.

- Leaky Competing Accumulator model.
- LCA/Race models with > 2 options.
- Leaky/unstable Diffusion.
- Time-varying parameters, including
    - Collapsing decision bounds
    - Time-varying evidence
- Heirarchical models with regressors that differ across trials.

## Reparameterisation

Ideally, parameterisation with other packages used for fitting accumulator models 
such as [HDDM](http://ski.clps.brown.edu/hddm_docs/) and
[PyDDM](https://pyddm.readthedocs.io/en/latest/), (for Python) 
and [rtdists](https://github.com/rtdists/rtdists) and 
[DMC](http://www.tascl.org/dmc.html) (for R). 
This would make it possible to efficiently fit models using those packages, 
then explore their dynamics here.

Model probably should also specify default parameters.

##  Visualisation

There's no shortage of ways to visualise accumulator models. 
Future versions will include both more low-level plotting functions
and high-level wrappers.

I'll also be implementing vector field plots, e.g. Figure 2 of 
[Bogacz et al. (2007)](https://people.socsci.tau.ac.il/mu/usherlab/files/2014/03/m2.pdf).

## Likelihood


The `evidently.likelihood` model contains functions for estimating 
the likelihood of data $x$ under parameters $\theta$ and model $M$,
based on the "likelihood-free" technique introduced by 
[Turner and Sederberg (2007)](https://link.springer.com/article/10.3758/s13423-013-0530-0).
These functions aren't properly tested yet,
and haven't been documented.



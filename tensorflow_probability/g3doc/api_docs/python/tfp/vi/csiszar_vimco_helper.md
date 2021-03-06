<div itemscope itemtype="http://developers.google.com/ReferenceObject">
<meta itemprop="name" content="tfp.vi.csiszar_vimco_helper" />
<meta itemprop="path" content="Stable" />
</div>

# tfp.vi.csiszar_vimco_helper


<table class="tfo-notebook-buttons tfo-api" align="left">
</table>



Helper to `csiszar_vimco`; computes `log_avg_u`, `log_sooavg_u`. (deprecated)

``` python
tfp.vi.csiszar_vimco_helper(
    *args,
    **kwargs
)
```



<!-- Placeholder for "Used in" -->

Warning: THIS FUNCTION IS DEPRECATED. It will be removed after 2019-10-01.
Instructions for updating:
`csiszar_vimco_helper` is deprecated. Instead use: `log_avg_u, log_sooavg_u = tfp.math.log_soomean_exp(logu, axis=0)[::-1]`. (Note: `tfp.math.log_soomean_exp` reverses the order of return values.)

`axis = 0` of `logu` is presumed to correspond to iid samples from `q`, i.e.,

```none
logu[j] = log(u[j])
u[j] = p(x, h[j]) / q(h[j] | x)
h[j] iid~ q(H | x)
```

#### Args:


* <b>`logu`</b>: Floating-type `Tensor` representing `log(p(x, h) / q(h | x))`.
* <b>`name`</b>: Python `str` name prefixed to Ops created by this function.


#### Returns:


* <b>`log_avg_u`</b>: `logu.dtype` `Tensor` corresponding to the natural-log of the
  average of `u`. The sum of the gradient of `log_avg_u` is `1`.
* <b>`log_sooavg_u`</b>: `logu.dtype` `Tensor` characterized by the natural-log of the
  average of `u`` except that the average swaps-out `u[i]` for the
  leave-`i`-out Geometric-average. The mean of the gradient of
  `log_sooavg_u` is `1`. Mathematically `log_sooavg_u` is,
  ```none
  log_sooavg_u[i] = log(Avg{h[j ; i] : j=0, ..., m-1})
  h[j ; i] = { u[j]                              j!=i
             { GeometricAverage{u[k] : k != i}   j==i
  ```
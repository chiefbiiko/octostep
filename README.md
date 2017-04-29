octostep
================

Iterate lists getting a *window* argument list to your callback.

------------------------------------------------------------------------

API
---

``` r
octostep::octostep(x, func, 
                   pad=1L, use.names=TRUE, transform.previous=FALSE)
```

-   `x` List **required**.
-   `func` Function with arity 2L \* pad + 1L **required**.
-   `pad` Integer controlling how many items should be padded around the current item, must be within 1L:((length(x) - 1L) / 2L) **optional**.
-   `use.names` Copy names? **optional**.
-   `transform.previous` Should the previous arguments of the callback take the values of previous callbacks rather than the plain values of the initial input list? **optional**.

------------------------------------------------------------------------

``` r
# see arguments evolve
octo <- octostep(as.list(1L:5L), function(pre, cur, nxt) {
  c(pre=if (is.null(pre)) NA else pre, 
    cur=cur, 
    nxt=if (is.null(nxt)) NA else nxt)
})
```

------------------------------------------------------------------------

``` r
# increase padding
paddle <- octostep(as.list(1L:9L), function(pre1, pre2, cur, nxt1, nxt2) {
  c(pre1=if (is.null(pre1)) NA else pre1, 
    pre2=if (is.null(pre2)) NA else pre2, 
    cur=cur, 
    nxt1=if (is.null(nxt1)) NA else nxt1,
    nxt2=if (is.null(nxt2)) NA else nxt2)
}, pad=2L)
```

------------------------------------------------------------------------

``` r
# new input
cable <- list(a=1, b=2, z=3, d=4, u=5)

# iterate with default options
mule <- octostep(cable, function(pre, cur, nxt) {
  if (!any.null(pre, nxt)) sum(pre, cur, nxt) else cur
}, pad=1L, use.names=TRUE, transform.previous=FALSE)  # all defaults
```

------------------------------------------------------------------------

``` r
# transform previous items while iterating
mutant <- octostep(cable, function(pre, cur, nxt) {
  if (!any.null(pre, nxt)) sum(pre, cur, nxt) else cur
}, pad=1L, use.names=TRUE, transform.previous=TRUE)
```

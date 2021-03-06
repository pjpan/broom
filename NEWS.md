broom 0.3.6.9000
-----------

* Added tidiers for "plm" (panel linear model) objects from the plm package.
* Added `tidy.coeftest` for coeftest objects from the lmtest package.
* Set up `tidy.lm` to work with "mlm" (multiple linear model) objects (those with multiple response columns).
* Added `tidy` and `glance` for "biglm" and "bigglm" objects from the biglm package.
* Fixed bug in `tidy.coxph` when one-row matrices are returned 
* Added `tidy.power.htest`
* Add `tidy` and `glance` for `summaryDefault` objects

broom 0.3.6
-----------

* Fixed bug in `tidy.pairwise.htest`, which now can handle cases where the grouping variable is numeric.
* Added `tidy.aovlist` method. This added `stringr` package to IMPORTS to trim whitespace from the beginning and end of the `term` and `stratum` columns. This also required adjusting `tidy.aov` so that it could handle strata that are missing p-values.
* Set up `glance.lm` to work with `aov` objects along with `lm` objects.
* Added `tidy` and `glance` for matrix objects, with `tidy.matrix` converting a matrix to a data frame with rownames included, and `glance.matrix` returning the same result as `glance.data.frame`.
* Changed DESCRIPTION Authors@R to new format

broom 0.3.5
-----------

* Fixed small bug in `felm` where the `.fitted` and `.resid` columns were matrices rather than vectors.
* Added tidiers for `rlm` (robust linear model) and `gam` (generalized additive model) objects, including adjustments to "lm" tidiers in order to handle them. See `?rlm_tidiers` and `?gam_tidiers` for more.
* Removed rownames from `tidy.cv.glmnet` output

broom 0.3.4
-----------

* The behavior of `augment`, particularly with regard to missing data and the `na.exclude` argument, has through the use of the `augment_columns` function been made consistent across the following models:
    * `lm`
    * `glm`
    * `nls`
    * `merMod` (`lme4`)
    * `survreg` (`survival`)
    * `coxph` (`survival`)

    Unit tests in `tests/testthat/test-augment.R` were added to ensure consistency across these models.
* `tidy`, `augment` and `glance` methods were added for `rowwise_df` objects, and are set up to apply across their rows. This allows for simple patterns such as:
      
        regressions <- mtcars %>% group_by(cyl) %>% do(mod = lm(mpg ~ wt, .))
        regressions %>% tidy(mod)
        regressions %>% augment(mod)
    
    See `?rowwise_df_tidiers` for more.
* Added `tidy` and `glance` methods for `Arima` objects, and `tidy` for `pairwise.htest` objects.
* Fixes for CRAN: change package description to title case, removed NOTES, mostly by adding `globals.R` to declare global variables.
* This is the original version published on CRAN.


broom 0.3
---------

* Tidiers have been added for S3 objects from the following packages:
    * `lme4`
    * `glmnet`
    * `survival`
    * `zoo`
    * `felm`
    * `MASS` (`ridgelm` objects)
* `tidy` and `glance` methods for data.frames have also been added, and `augment.data.frame` produces an error (rather than returning the same data.frame).
* `stderror` has been changed to `std.error` (affects many functions) to be consistent with broom's naming conventions for columns.
* A function `bootstrap` has been added based on [this example](https://github.com/hadley/dplyr/issues/269), to perform the common use case of bootstrapping models.

broom 0.2
---------

* Added "augment" S3 generic and various implementations. "augment" does something different from tidy: it adds columns to the original dataset, including predictions, residuals, or cluster assignments. This was originally described as "fortify" in ggplot2.
* Added "glance" S3 generic and various implementations. "glance" produces a *one-row* data frame summary, which is necessary for tidy outputs with values like R^2 or F-statistics.
* Re-wrote intro broom vignette/README to introduce all three methods.
* Wrote a new kmeans vignette.
* Added tidying methods for multcomp, sp, and map objects (from fortify-multcomp, fortify-sp, and fortify-map from ggplot2).
* Because this integrates substantial amounts of ggplot2 code (with permission), added Hadley Wickham as an author in DESCRIPTION.

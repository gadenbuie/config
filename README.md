config package for R
================

The **config** package makes it easy to manage environment specific configuration values (e.g. to use distinct values for development, testing, and production environments).

Basic Usage
-----------

Configurations are defined using a [YAML](http://www.yaml.org/about.html) text file and are stored (by default) in a file named `config.yml`. Configuration files include default values as well as values for arbitrary other named configurations, for example:

``` yaml
default:
  trials: 5
  dataset: "data-sampled.csv"
  
production:
  trials: 30
  dataset: "data.csv"
```

To read values from this configuration file you call the `config::get` function, which returns a list containing all of the values for the currently active configuration:

``` r
config <- config::get()
config$trials
```

    ## [1] 5

You can also read a single value from the configuration as follows:

``` r
trials <- config::get("trials")
```

The `get` function takes a `config` argument which determines which configuration to read values from. By default, `config` is read from the `R_CONFIG_NAME` environment variable. This variable is in turn typically set within a site sitewide `Renviron` or `Rprofile` (see [R Startup](https://stat.ethz.ch/R-manual/R-devel/library/base/html/Startup.html) for details on these files).

``` r
Sys.setenv(R_CONFIG_NAME = "production")
config::get("trials")
```

    ## [1] 30

<pre>
some test output code
</pre>
-   read from an alternate configuration (via env variable)

-   executing r code

-   alternate config file

-   inherit from default automatically
-   inherit from other configuration

-   "local" config file
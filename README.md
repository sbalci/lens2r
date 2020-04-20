
<!-- README.md is generated from README.Rmd. Please edit that file -->

# lens2r

<!-- badges: start -->

[![Project Status: WIP – Initial development is in progress, but there
has not yet been a stable, usable release suitable for the
public.](https://www.repostatus.org/badges/latest/wip.svg)](https://www.repostatus.org/#wip)

[![R CMD Check via
{tic}](https://github.com/sbalci/lens2r/workflows/R%20CMD%20Check%20via%20%7Btic%7D/badge.svg?branch=master)](https://github.com/sbalci/lens2r/actions)
[![Travis build
status](https://travis-ci.com/sbalci/lens2r.svg?branch=master)](https://travis-ci.com/sbalci/lens2r)
<!-- badges: end -->

The goal of lens2r is to …

## Installation

You can install the released version of lens2r from
[CRAN](https://CRAN.R-project.org) with:

``` r
install.packages("lens2r")
```

And the development version from [GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("sbalci/lens2r")
```

## Example

<!-- This is a basic example which shows you how to solve a common problem: -->

``` r
# library(lens2r)
```

    request <- '{
        "query": {
            "match_phrase": {
                "author.affiliation.name": "Harvard University"
            }
        },
        "size": 1,
        "sort": [{
            "year_published": "desc"
        }]
    }'
    
    output_content <- content(data, "text")
    
    
    output <- jsonlite::fromJSON(output_content)
    output <- output$data

``` r
request <- '{
    "query": {
        "match_phrase": {
            "author.affiliation.name": "Harvard University"
        }
    },
    "size": 1,
    "sort": [{
        "year_published": "desc"
    }]
}'
data <- get_scholarly_data(query = request)

output_content <- content(data, "text")

# output <- jsonlite::fromJSON(output_content)

output_flatten <- jsonlite::fromJSON(output_content, flatten = TRUE)

output_flatten_data <- output_flatten$data

output_flatten <- as.data.frame(output_flatten)


```

    Scholarly Works:
    
    [POST] https://api.lens.org/scholarly/search
    [GET] https://api.lens.org/scholarly/search
    Collections:
    
    [POST] https://api.lens.org/collections/{collection_id}
    [GET] https://api.lens.org/collections/{collection_id}

## Similar Works

### lensr

A package to access patent data from the Lens Patent Database Deprecated

<https://github.com/poldham/lensr>

### R codes in Lens.org API documentation

<https://docs.api.lens.org/samples.html#r>

These are the basic codes this package uses

``` r
require(httr)
getScholarlyData <- function(token, query){
    url <- 'https://api.lens.org/scholarly/search'
    headers <- c('Authorization' = token, 'Content-Type' = 'application/json')
    httr::POST(url = url, add_headers(.headers=headers), body = query)
}
token <- 'your-access-token'
request <- '{
    "query": {
        "match_phrase": {
            "author.affiliation.name": "Harvard University"
        }
    },
    "size": 1,
    "sort": [{
        "year_published": "desc"
    }]
}'
data <- getScholarlyData(token, request)
content(data, "text")
```

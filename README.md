# RcppJson

This provides Niels Lohmann's excellent [json library](https://github.com/nlohmann/json) for Rcpp.  All credit goes to him.

## Installation

```
remotes::install_github("nfultz/RcppJson")
```

It can also theoretically be used by a package by adding `LinkingTo: RcppJson` to your DESCRIPTION file


## Motivating Example

This demonstrates creating a json directly, as well as parsing and dumping text.

```
sourceCpp(code='

// [[Rcpp::depends(RcppJson)]]
// [[Rcpp::plugins(cpp14)]]

#include <nlohmann/json.hpp>

// for convenience
using json = nlohmann::json;

// [[Rcpp::export]]
auto boxme(const int &x) {


  auto j2 = R"(
    {
              "happy": true,
              "pi": 3.141
              }
  )"_json;

  j2["x"] = x;


  return j2.dump();


}          


// [[Rcpp::export]]
int unboxme(std::string x) {


  json j2 = json::parse(x);

  return j2["x"];


}          


          
')
```



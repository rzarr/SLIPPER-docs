---
title: src/Analysis.cxx

---

# src/Analysis.cxx



## Functions

|                | Name           |
| -------------- | -------------- |
| int | **[main](/Files/Analysis_8cxx.md#function-main)**(int argc, char ** argv) |


## Functions Documentation

### function main

```cpp
int main(
    int argc,
    char ** argv
)
```




## Source code

```cpp
#include "cxxopts.hpp"
#include "DataAnalysis.h"

int main(int argc, char **argv)
{
    cxxopts::Options options(argv[0], "Program info: Analyze data for WaveDAQ detectors");
    options.add_options()
        ("i, inputfilename","Pre-processed input filename (.root)",  cxxopts::value<std::string>())
        ("o, outputfilename","Output filename (.root)",  cxxopts::value<std::string>())
        ("h, help", "Print help");

    auto result = options.parse(argc, argv);
    if (!result.count("inputfilename"))
    {
        Message::DisplayFatalError(TString::Format("Missing Input file Name\n\n %s", options.help().c_str()));
        return 0;
    }
    if (!result.count("outputfilename"))
    {
        Message::DisplayFatalError(TString::Format("Missing Output file name\n\n %s", options.help().c_str()));
        return 0;
    }
    //
    DataAnalysis d;
    d.DoAll(result["inputfilename"].as<std::string>(), result["outputfilename"].as<std::string>());

    return 0;

}
```


-------------------------------

Updated on 2021-12-30 at 11:00:09 +0000

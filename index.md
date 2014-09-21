---
title       : Developing Data Products Slide Deck
subtitle    : Using progress inidcator in Shiny
author      : jp4711
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## A Shiny Application with Progress Indicator

 - Demonstrates the use of progress indicator during long running task
 - Downloads data "pml" from internet if not on machine
 - Loads data set into memory
 - Shows progress indicator when loading 'pml' data set into memory
 - Show summary info of loaded data set
 - Shows first n rows of data set
 
 
How to create Shiny App With Progress Indicator
 - create ui.R
 - create server.R
 - load library ShinyIncubator

--- .class #id 

## Progress Indicator within Shiny 

 - in ui.R

```r
library(shinyIncubator)

# and inside the layout

  progressInit(),
```

This will initiate progress indicator

---
## Progress Indicator Server Code

### Inside server.R code:
 - call withProgress to create dialog with progress bar
 - update the progress bar periodicially

#### Sample Code

```r
library(shinyIncubator)

# and inside the server code

withProgress(session, min = 0, max = 10, {
      setProgress(message = "Training the model:")
```

---
## Server Side Example Code

 - an long running operation
 

```r
  anExpensiveOperation <- function() {
    #
    # sdet min/max and setProgress(value=x) for progress bar
    withProgress(session, min = 0, max = 10, {
      setProgress(message = "Training the model:")
      for (i in 1:10) {
        setProgress(value = i)
        # wait more for background process to complete
        if (!hasMyTaskCompleted())
            Sys.sleep(1.0)
      }
    })
  }
```

---
## Conclusion

With Shiny and ShinyIncubator long running processes can be created and progress shown during execution time

ShinyIncubator is under development and new features are added.

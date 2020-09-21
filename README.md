GPT-Q
================

## Packages

``` r
# Install these packages if you don't have them yet
# if (!require("pacman")) install.packages("pacman")

pacman::p_load(tidyverse, rvest, tidybrowse, magrittr)
```

## Scrape Data

``` r
# First Container
chrome <- docker$new(
  image_src = "selenium/standalone-chrome-debug", #Image to be used (model for the container)
  container_name = "chrome",
  other_arguments = "-p 4446:4444 -p 4447:5900"
)

view_container("chrome") #Since we have not yet initialized any browser, we do not see anything, but the raw container/mini-computer.

chrome_driver <- get_driver(4446)

chrome_driver$open()

chrome_driver$navigate("https://qanon.pub/#142")

## store page
q <- chrome_driver$getPageSource() %>% 
  extract2(1) 

## save ot
saveRDS(q, file = "q.rds")
```

## Look at Trivia

``` r
q <- readRDS(file = "q.rds")

q_trivia <- q %>% 
  read_html() %>% 
  html_nodes(".text") %>%
  as.character() %>%
  str_split("<br>") %>%
  unlist()

write_lines(q_trivia, path = "q_trivia.txt", sep = "\n")

q_trivia
```

    ##  [1] "<div class=\"text\">How did Soros replace family ‘y’?"                                  
    ##  [2] "Who is family ‘y’? "                                                                    
    ##  [3] "Trace the bloodlines of these (3) families."                                            
    ##  [4] "What happened during WWII?"                                                             
    ##  [5] "Was Hitler a puppet?"                                                                   
    ##  [6] "Who was his handler?"                                                                   
    ##  [7] "What was the purpose?"                                                                  
    ##  [8] "What was the real purpose of the war? "                                                 
    ##  [9] "What age was <abbr title=\"George Soros\">GS</abbr>?"                                   
    ## [10] "What is the Soros family history?"                                                      
    ## [11] "What has occurred since the fall of N Germany?"                                         
    ## [12] "Who is A. Merkel? "                                                                     
    ## [13] "What is A. Merkel’s family history?"                                                    
    ## [14] "Follow the bloodline."                                                                  
    ## [15] "Who died on the Titanic?"                                                               
    ## [16] "What year did the Titanic sink?"                                                        
    ## [17] "Why is this relevant?"                                                                  
    ## [18] "What ‘exactly’ happened to the Titanic?"                                                
    ## [19] "What ‘class of people’ were guaranteed a lifeboat?"                                     
    ## [20] "Why did select ‘individuals’ not make it into the lifeboats?"                           
    ## [21] "Why is this relevant?"                                                                  
    ## [22] "How do we know who was on the lifeboats (D or A)?"                                      
    ## [23] "How were names and bodies recorded back then?"                                          
    ## [24] "When were tickets purchased for her maiden voyage? "                                    
    ## [25] "Who was ‘specifically’ invited?"                                                        
    ## [26] "Less than 10."                                                                          
    ## [27] "What is the <abbr title=\"Federal Reserve\">FED</abbr>?"                                
    ## [28] "What does the <abbr title=\"Federal Reserve\">FED</abbr> control?"                      
    ## [29] "Who controls the <abbr title=\"Federal Reserve\">FED</abbr>?"                           
    ## [30] "Who approved the formation of the <abbr title=\"Federal Reserve\">FED</abbr>?"          
    ## [31] "Why did <abbr title=\"Hollywood\">H-wood</abbr> glorify Titanic as a tragic love story?"
    ## [32] "Who lived in the movie (what man)?"                                                     
    ## [33] "Why is this relevant? "                                                                 
    ## [34] "Opposite is true."                                                                      
    ## [35] "What is brainwashing? "                                                                 
    ## [36] "What is a PSYOP?"                                                                       
    ## [37] "What happened to the Hindenburg?"                                                       
    ## [38] "What really happened to the Hindenburg?"                                                
    ## [39] "Who died during the ‘accident’?"                                                        
    ## [40] "Why is this relevant?"                                                                  
    ## [41] "What are sheep?"                                                                        
    ## [42] "Who controls the narrative?"                                                            
    ## [43] "The truth would put 99% of people in the hospital. "                                    
    ## [44] "It must be controlled."                                                                 
    ## [45] "Snow White."                                                                            
    ## [46] "Iron Eagle."                                                                            
    ## [47] "Jason Bourne (CIA/Dream)."                                                              
    ## [48] "Q</div>"

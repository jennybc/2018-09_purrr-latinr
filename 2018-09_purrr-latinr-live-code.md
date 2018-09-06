Live code from purrr workshop at Latin-R
================
Jenny Bryan
2018-09-06

This is a snapshot of a `.R` script I use to share my live code during
workshops. This is the state at the end of the workshop.

Use `rmarkdown::render()` on this or, in RStudio, click on the “Compile
Report” spiral-notebook icon.

## Workshop material starts here

``` r
library(purrr)
library(repurrrsive)
#help(package  = "repurrrsive")

## How many elements are in got_chars?
length(got_chars)
#> [1] 30

## Who is the 9th person listed in got_chars?
## What information is given for this person?
got_chars[[9]]
#> $url
#> [1] "https://www.anapioficeandfire.com/api/characters/1303"
#> 
#> $id
#> [1] 1303
#> 
#> $name
#> [1] "Daenerys Targaryen"
#> 
#> $gender
#> [1] "Female"
#> 
#> $culture
#> [1] "Valyrian"
#> 
#> $born
#> [1] "In 284 AC, at Dragonstone"
#> 
#> $died
#> [1] ""
#> 
#> $alive
#> [1] TRUE
#> 
#> $titles
#> [1] "Queen of the Andals and the Rhoynar and the First Men, Lord of the Seven Kingdoms"
#> [2] "Khaleesi of the Great Grass Sea"                                                  
#> [3] "Breaker of Shackles/Chains"                                                       
#> [4] "Queen of Meereen"                                                                 
#> [5] "Princess of Dragonstone"                                                          
#> 
#> $aliases
#>  [1] "Dany"                    "Daenerys Stormborn"     
#>  [3] "The Unburnt"             "Mother of Dragons"      
#>  [5] "Mother"                  "Mhysa"                  
#>  [7] "The Silver Queen"        "Silver Lady"            
#>  [9] "Dragonmother"            "The Dragon Queen"       
#> [11] "The Mad King's daughter"
#> 
#> $father
#> [1] ""
#> 
#> $mother
#> [1] ""
#> 
#> $spouse
#> [1] "https://www.anapioficeandfire.com/api/characters/1346"
#> 
#> $allegiances
#> [1] "House Targaryen of King's Landing"
#> 
#> $books
#> [1] "A Feast for Crows"
#> 
#> $povBooks
#> [1] "A Game of Thrones"    "A Clash of Kings"     "A Storm of Swords"   
#> [4] "A Dance with Dragons"
#> 
#> $tvSeries
#> [1] "Season 1" "Season 2" "Season 3" "Season 4" "Season 5" "Season 6"
#> 
#> $playedBy
#> [1] "Emilia Clarke"
str(got_chars[[9]])
#> List of 18
#>  $ url        : chr "https://www.anapioficeandfire.com/api/characters/1303"
#>  $ id         : int 1303
#>  $ name       : chr "Daenerys Targaryen"
#>  $ gender     : chr "Female"
#>  $ culture    : chr "Valyrian"
#>  $ born       : chr "In 284 AC, at Dragonstone"
#>  $ died       : chr ""
#>  $ alive      : logi TRUE
#>  $ titles     : chr [1:5] "Queen of the Andals and the Rhoynar and the First Men, Lord of the Seven Kingdoms" "Khaleesi of the Great Grass Sea" "Breaker of Shackles/Chains" "Queen of Meereen" ...
#>  $ aliases    : chr [1:11] "Dany" "Daenerys Stormborn" "The Unburnt" "Mother of Dragons" ...
#>  $ father     : chr ""
#>  $ mother     : chr ""
#>  $ spouse     : chr "https://www.anapioficeandfire.com/api/characters/1346"
#>  $ allegiances: chr "House Targaryen of King's Landing"
#>  $ books      : chr "A Feast for Crows"
#>  $ povBooks   : chr [1:4] "A Game of Thrones" "A Clash of Kings" "A Storm of Swords" "A Dance with Dragons"
#>  $ tvSeries   : chr [1:6] "Season 1" "Season 2" "Season 3" "Season 4" ...
#>  $ playedBy   : chr "Emilia Clarke"
str(got_chars[[9]], list.len = 4)
#> List of 18
#>  $ url        : chr "https://www.anapioficeandfire.com/api/characters/1303"
#>  $ id         : int 1303
#>  $ name       : chr "Daenerys Targaryen"
#>  $ gender     : chr "Female"
#>   [list output truncated]
#View(got_chars[[9]])
#View(got_chars)

## What is the difference between got_chars[9] and got_chars[[9]]?
got_chars[1]
#> [[1]]
#> [[1]]$url
#> [1] "https://www.anapioficeandfire.com/api/characters/1022"
#> 
#> [[1]]$id
#> [1] 1022
#> 
#> [[1]]$name
#> [1] "Theon Greyjoy"
#> 
#> [[1]]$gender
#> [1] "Male"
#> 
#> [[1]]$culture
#> [1] "Ironborn"
#> 
#> [[1]]$born
#> [1] "In 278 AC or 279 AC, at Pyke"
#> 
#> [[1]]$died
#> [1] ""
#> 
#> [[1]]$alive
#> [1] TRUE
#> 
#> [[1]]$titles
#> [1] "Prince of Winterfell"                                
#> [2] "Captain of Sea Bitch"                                
#> [3] "Lord of the Iron Islands (by law of the green lands)"
#> 
#> [[1]]$aliases
#> [1] "Prince of Fools" "Theon Turncloak" "Reek"            "Theon Kinslayer"
#> 
#> [[1]]$father
#> [1] ""
#> 
#> [[1]]$mother
#> [1] ""
#> 
#> [[1]]$spouse
#> [1] ""
#> 
#> [[1]]$allegiances
#> [1] "House Greyjoy of Pyke"
#> 
#> [[1]]$books
#> [1] "A Game of Thrones" "A Storm of Swords" "A Feast for Crows"
#> 
#> [[1]]$povBooks
#> [1] "A Clash of Kings"     "A Dance with Dragons"
#> 
#> [[1]]$tvSeries
#> [1] "Season 1" "Season 2" "Season 3" "Season 4" "Season 5" "Season 6"
#> 
#> [[1]]$playedBy
#> [1] "Alfie Allen"
got_chars[[1]]
#> $url
#> [1] "https://www.anapioficeandfire.com/api/characters/1022"
#> 
#> $id
#> [1] 1022
#> 
#> $name
#> [1] "Theon Greyjoy"
#> 
#> $gender
#> [1] "Male"
#> 
#> $culture
#> [1] "Ironborn"
#> 
#> $born
#> [1] "In 278 AC or 279 AC, at Pyke"
#> 
#> $died
#> [1] ""
#> 
#> $alive
#> [1] TRUE
#> 
#> $titles
#> [1] "Prince of Winterfell"                                
#> [2] "Captain of Sea Bitch"                                
#> [3] "Lord of the Iron Islands (by law of the green lands)"
#> 
#> $aliases
#> [1] "Prince of Fools" "Theon Turncloak" "Reek"            "Theon Kinslayer"
#> 
#> $father
#> [1] ""
#> 
#> $mother
#> [1] ""
#> 
#> $spouse
#> [1] ""
#> 
#> $allegiances
#> [1] "House Greyjoy of Pyke"
#> 
#> $books
#> [1] "A Game of Thrones" "A Storm of Swords" "A Feast for Crows"
#> 
#> $povBooks
#> [1] "A Clash of Kings"     "A Dance with Dragons"
#> 
#> $tvSeries
#> [1] "Season 1" "Season 2" "Season 3" "Season 4" "Season 5" "Season 6"
#> 
#> $playedBy
#> [1] "Alfie Allen"
str(got_chars[1], max.level = 1)
#> List of 1
#>  $ :List of 18
str(got_chars[[1]], max.level = 0)
#> List of 18

## What is the length of each GoT character's aliases?
daenerys <- got_chars[[9]]
length(daenerys[["aliases"]])
#> [1] 11

map(got_chars, ~ length(.x[["aliases"]]))
#> [[1]]
#> [1] 4
#> 
#> [[2]]
#> [1] 11
#> 
#> [[3]]
#> [1] 1
#> 
#> [[4]]
#> [1] 1
#> 
#> [[5]]
#> [1] 1
#> 
#> [[6]]
#> [1] 1
#> 
#> [[7]]
#> [1] 1
#> 
#> [[8]]
#> [1] 1
#> 
#> [[9]]
#> [1] 11
#> 
#> [[10]]
#> [1] 5
#> 
#> [[11]]
#> [1] 16
#> 
#> [[12]]
#> [1] 1
#> 
#> [[13]]
#> [1] 2
#> 
#> [[14]]
#> [1] 5
#> 
#> [[15]]
#> [1] 3
#> 
#> [[16]]
#> [1] 3
#> 
#> [[17]]
#> [1] 3
#> 
#> [[18]]
#> [1] 5
#> 
#> [[19]]
#> [1] 0
#> 
#> [[20]]
#> [1] 3
#> 
#> [[21]]
#> [1] 4
#> 
#> [[22]]
#> [1] 1
#> 
#> [[23]]
#> [1] 8
#> 
#> [[24]]
#> [1] 2
#> 
#> [[25]]
#> [1] 1
#> 
#> [[26]]
#> [1] 5
#> 
#> [[27]]
#> [1] 1
#> 
#> [[28]]
#> [1] 4
#> 
#> [[29]]
#> [1] 7
#> 
#> [[30]]
#> [1] 3

## How many x does each (GoT or SW) character have?
## (x = 3 titles, allegiances, vehicles, starships)
map(got_chars, ~ length(.x[["titles"]]))
#> [[1]]
#> [1] 3
#> 
#> [[2]]
#> [1] 2
#> 
#> [[3]]
#> [1] 2
#> 
#> [[4]]
#> [1] 1
#> 
#> [[5]]
#> [1] 1
#> 
#> [[6]]
#> [1] 1
#> 
#> [[7]]
#> [1] 1
#> 
#> [[8]]
#> [1] 1
#> 
#> [[9]]
#> [1] 5
#> 
#> [[10]]
#> [1] 4
#> 
#> [[11]]
#> [1] 1
#> 
#> [[12]]
#> [1] 1
#> 
#> [[13]]
#> [1] 3
#> 
#> [[14]]
#> [1] 2
#> 
#> [[15]]
#> [1] 1
#> 
#> [[16]]
#> [1] 1
#> 
#> [[17]]
#> [1] 1
#> 
#> [[18]]
#> [1] 1
#> 
#> [[19]]
#> [1] 5
#> 
#> [[20]]
#> [1] 5
#> 
#> [[21]]
#> [1] 3
#> 
#> [[22]]
#> [1] 3
#> 
#> [[23]]
#> [1] 1
#> 
#> [[24]]
#> [1] 2
#> 
#> [[25]]
#> [1] 4
#> 
#> [[26]]
#> [1] 1
#> 
#> [[27]]
#> [1] 1
#> 
#> [[28]]
#> [1] 1
#> 
#> [[29]]
#> [1] 1
#> 
#> [[30]]
#> [1] 1
map(sw_people, ~ length(.x[["starships"]]))
#> [[1]]
#> [1] 2
#> 
#> [[2]]
#> [1] 0
#> 
#> [[3]]
#> [1] 0
#> 
#> [[4]]
#> [1] 1
#> 
#> [[5]]
#> [1] 0
#> 
#> [[6]]
#> [1] 0
#> 
#> [[7]]
#> [1] 0
#> 
#> [[8]]
#> [1] 0
#> 
#> [[9]]
#> [1] 1
#> 
#> [[10]]
#> [1] 5
#> 
#> [[11]]
#> [1] 3
#> 
#> [[12]]
#> [1] 0
#> 
#> [[13]]
#> [1] 2
#> 
#> [[14]]
#> [1] 2
#> 
#> [[15]]
#> [1] 0
#> 
#> [[16]]
#> [1] 0
#> 
#> [[17]]
#> [1] 1
#> 
#> [[18]]
#> [1] 1
#> 
#> [[19]]
#> [1] 0
#> 
#> [[20]]
#> [1] 0
#> 
#> [[21]]
#> [1] 1
#> 
#> [[22]]
#> [1] 0
#> 
#> [[23]]
#> [1] 0
#> 
#> [[24]]
#> [1] 1
#> 
#> [[25]]
#> [1] 0
#> 
#> [[26]]
#> [1] 0
#> 
#> [[27]]
#> [1] 0
#> 
#> [[28]]
#> [1] 1
#> 
#> [[29]]
#> [1] 0
#> 
#> [[30]]
#> [1] 1
#> 
#> [[31]]
#> [1] 0
#> 
#> [[32]]
#> [1] 0
#> 
#> [[33]]
#> [1] 0
#> 
#> [[34]]
#> [1] 0
#> 
#> [[35]]
#> [1] 0
#> 
#> [[36]]
#> [1] 0
#> 
#> [[37]]
#> [1] 1
#> 
#> [[38]]
#> [1] 0
#> 
#> [[39]]
#> [1] 0
#> 
#> [[40]]
#> [1] 0
#> 
#> [[41]]
#> [1] 0
#> 
#> [[42]]
#> [1] 1
#> 
#> [[43]]
#> [1] 0
#> 
#> [[44]]
#> [1] 0
#> 
#> [[45]]
#> [1] 0
#> 
#> [[46]]
#> [1] 0
#> 
#> [[47]]
#> [1] 0
#> 
#> [[48]]
#> [1] 0
#> 
#> [[49]]
#> [1] 0
#> 
#> [[50]]
#> [1] 0
#> 
#> [[51]]
#> [1] 0
#> 
#> [[52]]
#> [1] 0
#> 
#> [[53]]
#> [1] 0
#> 
#> [[54]]
#> [1] 0
#> 
#> [[55]]
#> [1] 1
#> 
#> [[56]]
#> [1] 0
#> 
#> [[57]]
#> [1] 1
#> 
#> [[58]]
#> [1] 0
#> 
#> [[59]]
#> [1] 0
#> 
#> [[60]]
#> [1] 0
#> 
#> [[61]]
#> [1] 0
#> 
#> [[62]]
#> [1] 0
#> 
#> [[63]]
#> [1] 0
#> 
#> [[64]]
#> [1] 0
#> 
#> [[65]]
#> [1] 0
#> 
#> [[66]]
#> [1] 0
#> 
#> [[67]]
#> [1] 0
#> 
#> [[68]]
#> [1] 0
#> 
#> [[69]]
#> [1] 0
#> 
#> [[70]]
#> [1] 0
#> 
#> [[71]]
#> [1] 0
#> 
#> [[72]]
#> [1] 0
#> 
#> [[73]]
#> [1] 0
#> 
#> [[74]]
#> [1] 0
#> 
#> [[75]]
#> [1] 0
#> 
#> [[76]]
#> [1] 0
#> 
#> [[77]]
#> [1] 1
#> 
#> [[78]]
#> [1] 0
#> 
#> [[79]]
#> [1] 0
#> 
#> [[80]]
#> [1] 0
#> 
#> [[81]]
#> [1] 0
#> 
#> [[82]]
#> [1] 0
#> 
#> [[83]]
#> [1] 0
#> 
#> [[84]]
#> [1] 1
#> 
#> [[85]]
#> [1] 0
#> 
#> [[86]]
#> [1] 0
#> 
#> [[87]]
#> [1] 3

# What's each character's name?
map_chr(got_chars, ~.x[["name"]])
#>  [1] "Theon Greyjoy"      "Tyrion Lannister"   "Victarion Greyjoy" 
#>  [4] "Will"               "Areo Hotah"         "Chett"             
#>  [7] "Cressen"            "Arianne Martell"    "Daenerys Targaryen"
#> [10] "Davos Seaworth"     "Arya Stark"         "Arys Oakheart"     
#> [13] "Asha Greyjoy"       "Barristan Selmy"    "Varamyr"           
#> [16] "Brandon Stark"      "Brienne of Tarth"   "Catelyn Stark"     
#> [19] "Cersei Lannister"   "Eddard Stark"       "Jaime Lannister"   
#> [22] "Jon Connington"     "Jon Snow"           "Aeron Greyjoy"     
#> [25] "Kevan Lannister"    "Melisandre"         "Merrett Frey"      
#> [28] "Quentyn Martell"    "Samwell Tarly"      "Sansa Stark"
map_chr(sw_people, ~.x[["name"]])
#>  [1] "Luke Skywalker"        "C-3PO"                
#>  [3] "R2-D2"                 "Darth Vader"          
#>  [5] "Leia Organa"           "Owen Lars"            
#>  [7] "Beru Whitesun lars"    "R5-D4"                
#>  [9] "Biggs Darklighter"     "Obi-Wan Kenobi"       
#> [11] "Anakin Skywalker"      "Wilhuff Tarkin"       
#> [13] "Chewbacca"             "Han Solo"             
#> [15] "Greedo"                "Jabba Desilijic Tiure"
#> [17] "Wedge Antilles"        "Jek Tono Porkins"     
#> [19] "Yoda"                  "Palpatine"            
#> [21] "Boba Fett"             "IG-88"                
#> [23] "Bossk"                 "Lando Calrissian"     
#> [25] "Lobot"                 "Ackbar"               
#> [27] "Mon Mothma"            "Arvel Crynyd"         
#> [29] "Wicket Systri Warrick" "Nien Nunb"            
#> [31] "Qui-Gon Jinn"          "Nute Gunray"          
#> [33] "Finis Valorum"         "Jar Jar Binks"        
#> [35] "Roos Tarpals"          "Rugor Nass"           
#> [37] "Ric Olié"              "Watto"                
#> [39] "Sebulba"               "Quarsh Panaka"        
#> [41] "Shmi Skywalker"        "Darth Maul"           
#> [43] "Bib Fortuna"           "Ayla Secura"          
#> [45] "Dud Bolt"              "Gasgano"              
#> [47] "Ben Quadinaros"        "Mace Windu"           
#> [49] "Ki-Adi-Mundi"          "Kit Fisto"            
#> [51] "Eeth Koth"             "Adi Gallia"           
#> [53] "Saesee Tiin"           "Yarael Poof"          
#> [55] "Plo Koon"              "Mas Amedda"           
#> [57] "Gregar Typho"          "Cordé"                
#> [59] "Cliegg Lars"           "Poggle the Lesser"    
#> [61] "Luminara Unduli"       "Barriss Offee"        
#> [63] "Dormé"                 "Dooku"                
#> [65] "Bail Prestor Organa"   "Jango Fett"           
#> [67] "Zam Wesell"            "Dexter Jettster"      
#> [69] "Lama Su"               "Taun We"              
#> [71] "Jocasta Nu"            "Ratts Tyerell"        
#> [73] "R4-P17"                "Wat Tambor"           
#> [75] "San Hill"              "Shaak Ti"             
#> [77] "Grievous"              "Tarfful"              
#> [79] "Raymus Antilles"       "Sly Moore"            
#> [81] "Tion Medon"            "Finn"                 
#> [83] "Rey"                   "Poe Dameron"          
#> [85] "BB8"                   "Captain Phasma"       
#> [87] "Padmé Amidala"

# What color is each SW character's hair?
map_chr(sw_people, ~ .x[["hair_color"]])
#>  [1] "blond"         "n/a"           "n/a"           "none"         
#>  [5] "brown"         "brown, grey"   "brown"         "n/a"          
#>  [9] "black"         "auburn, white" "blond"         "auburn, grey" 
#> [13] "brown"         "brown"         "n/a"           "n/a"          
#> [17] "brown"         "brown"         "white"         "grey"         
#> [21] "black"         "none"          "none"          "black"        
#> [25] "none"          "none"          "auburn"        "brown"        
#> [29] "brown"         "none"          "brown"         "none"         
#> [33] "blond"         "none"          "none"          "none"         
#> [37] "brown"         "black"         "none"          "black"        
#> [41] "black"         "none"          "none"          "none"         
#> [45] "none"          "none"          "none"          "none"         
#> [49] "white"         "none"          "black"         "none"         
#> [53] "none"          "none"          "none"          "none"         
#> [57] "black"         "brown"         "brown"         "none"         
#> [61] "black"         "black"         "brown"         "white"        
#> [65] "black"         "black"         "blonde"        "none"         
#> [69] "none"          "none"          "white"         "none"         
#> [73] "none"          "none"          "none"          "none"         
#> [77] "none"          "brown"         "brown"         "none"         
#> [81] "none"          "black"         "brown"         "brown"        
#> [85] "none"          "unknown"       "brown"

# Is the GoT character alive?
map_lgl(got_chars, ~ .x[["alive"]])
#>  [1]  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
#> [12] FALSE  TRUE  TRUE FALSE  TRUE  TRUE FALSE  TRUE FALSE  TRUE  TRUE
#> [23]  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE  TRUE

# Is the SW character female?
map_lgl(sw_people, ~ .x[["gender"]] == "female")
#>  [1] FALSE FALSE FALSE FALSE  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE
#> [12] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#> [23] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
#> [34] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE  TRUE
#> [45] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE
#> [56] FALSE FALSE  TRUE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE
#> [67]  TRUE FALSE FALSE  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE FALSE
#> [78] FALSE FALSE  TRUE FALSE FALSE  TRUE FALSE FALSE  TRUE  TRUE

# How heavy is each SW character?
map_dbl(sw_people, ~ .x[["mass"]])
#> Error: Can't coerce element 1 from a character to a double
map_chr(sw_people, ~ .x[["mass"]])
#>  [1] "77"      "75"      "32"      "136"     "49"      "120"     "75"     
#>  [8] "32"      "84"      "77"      "84"      "unknown" "112"     "80"     
#> [15] "74"      "1,358"   "77"      "110"     "17"      "75"      "78.2"   
#> [22] "140"     "113"     "79"      "79"      "83"      "unknown" "unknown"
#> [29] "20"      "68"      "89"      "90"      "unknown" "66"      "82"     
#> [36] "unknown" "unknown" "unknown" "40"      "unknown" "unknown" "80"     
#> [43] "unknown" "55"      "45"      "unknown" "65"      "84"      "82"     
#> [50] "87"      "unknown" "50"      "unknown" "unknown" "80"      "unknown"
#> [57] "85"      "unknown" "unknown" "80"      "56.2"    "50"      "unknown"
#> [64] "80"      "unknown" "79"      "55"      "102"     "88"      "unknown"
#> [71] "unknown" "15"      "unknown" "48"      "unknown" "57"      "159"    
#> [78] "136"     "79"      "48"      "80"      "unknown" "unknown" "unknown"
#> [85] "unknown" "unknown" "45"
map_dbl(sw_people, ~ as.character(.x[["mass"]]))
#> Error: Can't coerce element 1 from a character to a double
map_dbl(sw_people, ~ readr::parse_number(.x[["mass"]]))
#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown

#> Warning: 1 parsing failure.
#> row col expected  actual
#>   1  -- a number unknown
#>  [1]   77.0   75.0   32.0  136.0   49.0  120.0   75.0   32.0   84.0   77.0
#> [11]   84.0     NA  112.0   80.0   74.0 1358.0   77.0  110.0   17.0   75.0
#> [21]   78.2  140.0  113.0   79.0   79.0   83.0     NA     NA   20.0   68.0
#> [31]   89.0   90.0     NA   66.0   82.0     NA     NA     NA   40.0     NA
#> [41]     NA   80.0     NA   55.0   45.0     NA   65.0   84.0   82.0   87.0
#> [51]     NA   50.0     NA     NA   80.0     NA   85.0     NA     NA   80.0
#> [61]   56.2   50.0     NA   80.0     NA   79.0   55.0  102.0   88.0     NA
#> [71]     NA   15.0     NA   48.0     NA   57.0  159.0  136.0   79.0   48.0
#> [81]   80.0     NA     NA     NA     NA     NA   45.0

## Explore a GoT or SW list and find a new element to look at
## Extract it across the whole list with name and position shortcuts for .f
## Use map_TYPE() to get an atomic vector as output
got_chars %>%
  map_chr("culture")
#>  [1] "Ironborn"    ""            "Ironborn"    ""            "Norvoshi"   
#>  [6] ""            ""            "Dornish"     "Valyrian"    "Westeros"   
#> [11] "Northmen"    "Reach"       "Ironborn"    "Westeros"    "Free Folk"  
#> [16] "Northmen"    ""            "Rivermen"    "Westerman"   "Northmen"   
#> [21] "Westerlands" "Stormlands"  "Northmen"    "Ironborn"    ""           
#> [26] "Asshai"      "Rivermen"    "Dornish"     "Andal"       "Northmen"

sw_people %>%
  map_chr("birth_year")
#>  [1] "19BBY"   "112BBY"  "33BBY"   "41.9BBY" "19BBY"   "52BBY"   "47BBY"  
#>  [8] "unknown" "24BBY"   "57BBY"   "41.9BBY" "64BBY"   "200BBY"  "29BBY"  
#> [15] "44BBY"   "600BBY"  "21BBY"   "unknown" "896BBY"  "82BBY"   "31.5BBY"
#> [22] "15BBY"   "53BBY"   "31BBY"   "37BBY"   "41BBY"   "48BBY"   "unknown"
#> [29] "8BBY"    "unknown" "92BBY"   "unknown" "91BBY"   "52BBY"   "unknown"
#> [36] "unknown" "unknown" "unknown" "unknown" "62BBY"   "72BBY"   "54BBY"  
#> [43] "unknown" "48BBY"   "unknown" "unknown" "unknown" "72BBY"   "92BBY"  
#> [50] "unknown" "unknown" "unknown" "unknown" "unknown" "22BBY"   "unknown"
#> [57] "unknown" "unknown" "82BBY"   "unknown" "58BBY"   "40BBY"   "unknown"
#> [64] "102BBY"  "67BBY"   "66BBY"   "unknown" "unknown" "unknown" "unknown"
#> [71] "unknown" "unknown" "unknown" "unknown" "unknown" "unknown" "unknown"
#> [78] "unknown" "unknown" "unknown" "unknown" "unknown" "unknown" "unknown"
#> [85] "unknown" "unknown" "46BBY"

got_chars %>%
  map("allegiances") %>%
  View()
#> Error in (function (..., row.names = NULL, check.rows = FALSE, check.names = TRUE, : arguments imply differing number of rows: 1, 0, 2, 3

## What if the thing you are extracting is not there or
## length 0 or of lenght > 1?

map(sw_vehicles, "pilots", .default = NA)
#> [[1]]
#> [1] NA
#> 
#> [[2]]
#> [1] NA
#> 
#> [[3]]
#> [1] NA
#> 
#> [[4]]
#> [1] NA
#> 
#> [[5]]
#> [1] "http://swapi.co/api/people/1/"  "http://swapi.co/api/people/18/"
#> 
#> [[6]]
#> [1] NA
#> 
#> [[7]]
#> [1] NA
#> 
#> [[8]]
#> [1] "http://swapi.co/api/people/13/"
#> 
#> [[9]]
#> [1] NA
#> 
#> [[10]]
#> [1] NA
#> 
#> [[11]]
#> [1] NA
#> 
#> [[12]]
#> [1] NA
#> 
#> [[13]]
#> [1] "http://swapi.co/api/people/1/" "http://swapi.co/api/people/5/"
#> 
#> [[14]]
#> [1] NA
#> 
#> [[15]]
#> [1] NA
#> 
#> [[16]]
#> [1] NA
#> 
#> [[17]]
#> [1] NA
#> 
#> [[18]]
#> [1] NA
#> 
#> [[19]]
#> [1] "http://swapi.co/api/people/10/" "http://swapi.co/api/people/32/"
#> 
#> [[20]]
#> [1] "http://swapi.co/api/people/44/"
#> 
#> [[21]]
#> [1] "http://swapi.co/api/people/11/"
#> 
#> [[22]]
#> [1] "http://swapi.co/api/people/70/"
#> 
#> [[23]]
#> [1] "http://swapi.co/api/people/11/"
#> 
#> [[24]]
#> [1] NA
#> 
#> [[25]]
#> [1] NA
#> 
#> [[26]]
#> [1] "http://swapi.co/api/people/79/"
#> 
#> [[27]]
#> [1] NA
#> 
#> [[28]]
#> [1] NA
#> 
#> [[29]]
#> [1] NA
#> 
#> [[30]]
#> [1] NA
#> 
#> [[31]]
#> [1] NA
#> 
#> [[32]]
#> [1] NA
#> 
#> [[33]]
#> [1] NA
#> 
#> [[34]]
#> [1] NA
#> 
#> [[35]]
#> [1] NA
#> 
#> [[36]]
#> [1] NA
#> 
#> [[37]]
#> [1] "http://swapi.co/api/people/67/"
#> 
#> [[38]]
#> [1] NA
#> 
#> [[39]]
#> [1] NA

map_chr(sw_vehicles, list("pilots", 1), .default = NA)
#>  [1] NA                               NA                              
#>  [3] NA                               NA                              
#>  [5] "http://swapi.co/api/people/1/"  NA                              
#>  [7] NA                               "http://swapi.co/api/people/13/"
#>  [9] NA                               NA                              
#> [11] NA                               NA                              
#> [13] "http://swapi.co/api/people/1/"  NA                              
#> [15] NA                               NA                              
#> [17] NA                               NA                              
#> [19] "http://swapi.co/api/people/10/" "http://swapi.co/api/people/44/"
#> [21] "http://swapi.co/api/people/11/" "http://swapi.co/api/people/70/"
#> [23] "http://swapi.co/api/people/11/" NA                              
#> [25] NA                               "http://swapi.co/api/people/79/"
#> [27] NA                               NA                              
#> [29] NA                               NA                              
#> [31] NA                               NA                              
#> [33] NA                               NA                              
#> [35] NA                               NA                              
#> [37] "http://swapi.co/api/people/67/" NA                              
#> [39] NA

## Names make life nicer!
got_chars_named <- set_names(got_chars, map_chr(got_chars, "name"))
View(got_chars_named)
#> Error in (function (..., row.names = NULL, check.rows = FALSE, check.names = TRUE, : arguments imply differing number of rows: 1, 3, 4, 2, 6

got_chars_named %>%
  map_lgl("alive")
#>      Theon Greyjoy   Tyrion Lannister  Victarion Greyjoy 
#>               TRUE               TRUE               TRUE 
#>               Will         Areo Hotah              Chett 
#>              FALSE               TRUE              FALSE 
#>            Cressen    Arianne Martell Daenerys Targaryen 
#>              FALSE               TRUE               TRUE 
#>     Davos Seaworth         Arya Stark      Arys Oakheart 
#>               TRUE               TRUE              FALSE 
#>       Asha Greyjoy    Barristan Selmy            Varamyr 
#>               TRUE               TRUE              FALSE 
#>      Brandon Stark   Brienne of Tarth      Catelyn Stark 
#>               TRUE               TRUE              FALSE 
#>   Cersei Lannister       Eddard Stark    Jaime Lannister 
#>               TRUE              FALSE               TRUE 
#>     Jon Connington           Jon Snow      Aeron Greyjoy 
#>               TRUE               TRUE               TRUE 
#>    Kevan Lannister         Melisandre       Merrett Frey 
#>              FALSE               TRUE              FALSE 
#>    Quentyn Martell      Samwell Tarly        Sansa Stark 
#>              FALSE               TRUE               TRUE

## Challenge:
## Create a named copy of a GoT or SW list with set_names().
## Find an element with tricky presence/absence or length.
##
## Extract it many ways:
## - by name
## - by position
## - by list("name", pos) or c(pos, pos)
## - use .default for missing data
## - use map_TYPE() to coerce output to atomic vector

## is 'books' tricky? yeah, some characters are in 0 books
## (how is that even possible?!) and others are in 5
got_chars_named %>%
  map("books") %>%
  map_int(length) %>%
  table()
#> .
#> 0 1 2 3 4 5 
#> 1 7 6 8 6 2

which(names(got_chars[[1]]) == "books")
#> [1] 15

identical(
  map(got_chars_named, "books"),
  map(got_chars_named, 15)
)
#> [1] TRUE

map(got_chars_named, "books", .default = "no book!")
#> $`Theon Greyjoy`
#> [1] "A Game of Thrones" "A Storm of Swords" "A Feast for Crows"
#> 
#> $`Tyrion Lannister`
#> [1] "A Feast for Crows"         "The World of Ice and Fire"
#> 
#> $`Victarion Greyjoy`
#> [1] "A Game of Thrones" "A Clash of Kings"  "A Storm of Swords"
#> 
#> $Will
#> [1] "A Clash of Kings"
#> 
#> $`Areo Hotah`
#> [1] "A Game of Thrones" "A Clash of Kings"  "A Storm of Swords"
#> 
#> $Chett
#> [1] "A Game of Thrones" "A Clash of Kings" 
#> 
#> $Cressen
#> [1] "A Storm of Swords" "A Feast for Crows"
#> 
#> $`Arianne Martell`
#> [1] "A Game of Thrones"    "A Clash of Kings"     "A Storm of Swords"   
#> [4] "A Dance with Dragons"
#> 
#> $`Daenerys Targaryen`
#> [1] "A Feast for Crows"
#> 
#> $`Davos Seaworth`
#> [1] "A Feast for Crows"
#> 
#> $`Arya Stark`
#> [1] "no book!"
#> 
#> $`Arys Oakheart`
#> [1] "A Game of Thrones"    "A Clash of Kings"     "A Storm of Swords"   
#> [4] "A Dance with Dragons"
#> 
#> $`Asha Greyjoy`
#> [1] "A Game of Thrones" "A Clash of Kings" 
#> 
#> $`Barristan Selmy`
#> [1] "A Game of Thrones"         "A Clash of Kings"         
#> [3] "A Storm of Swords"         "A Feast for Crows"        
#> [5] "The World of Ice and Fire"
#> 
#> $Varamyr
#> [1] "A Storm of Swords"
#> 
#> $`Brandon Stark`
#> [1] "A Feast for Crows"
#> 
#> $`Brienne of Tarth`
#> [1] "A Clash of Kings"     "A Storm of Swords"    "A Dance with Dragons"
#> 
#> $`Catelyn Stark`
#> [1] "A Feast for Crows"    "A Dance with Dragons"
#> 
#> $`Cersei Lannister`
#> [1] "A Game of Thrones" "A Clash of Kings"  "A Storm of Swords"
#> 
#> $`Eddard Stark`
#> [1] "A Clash of Kings"          "A Storm of Swords"        
#> [3] "A Feast for Crows"         "A Dance with Dragons"     
#> [5] "The World of Ice and Fire"
#> 
#> $`Jaime Lannister`
#> [1] "A Game of Thrones" "A Clash of Kings" 
#> 
#> $`Jon Connington`
#> [1] "A Storm of Swords"         "A Feast for Crows"        
#> [3] "The World of Ice and Fire"
#> 
#> $`Jon Snow`
#> [1] "A Feast for Crows"
#> 
#> $`Aeron Greyjoy`
#> [1] "A Game of Thrones"    "A Clash of Kings"     "A Storm of Swords"   
#> [4] "A Dance with Dragons"
#> 
#> $`Kevan Lannister`
#> [1] "A Game of Thrones" "A Clash of Kings"  "A Storm of Swords"
#> [4] "A Feast for Crows"
#> 
#> $Melisandre
#> [1] "A Clash of Kings"  "A Storm of Swords" "A Feast for Crows"
#> 
#> $`Merrett Frey`
#> [1] "A Game of Thrones"    "A Clash of Kings"     "A Feast for Crows"   
#> [4] "A Dance with Dragons"
#> 
#> $`Quentyn Martell`
#> [1] "A Game of Thrones" "A Clash of Kings"  "A Storm of Swords"
#> [4] "A Feast for Crows"
#> 
#> $`Samwell Tarly`
#> [1] "A Game of Thrones"    "A Clash of Kings"     "A Dance with Dragons"
#> 
#> $`Sansa Stark`
#> [1] "A Dance with Dragons"

got_chars_named %>%
  map("books", .default = "no book!") %>%
  map_chr(paste, collapse = ", ") %>%
  map_chr(substr, start = 1, stop = 60)
#>                                                  Theon Greyjoy 
#>      "A Game of Thrones, A Storm of Swords, A Feast for Crows" 
#>                                               Tyrion Lannister 
#>                 "A Feast for Crows, The World of Ice and Fire" 
#>                                              Victarion Greyjoy 
#>       "A Game of Thrones, A Clash of Kings, A Storm of Swords" 
#>                                                           Will 
#>                                             "A Clash of Kings" 
#>                                                     Areo Hotah 
#>       "A Game of Thrones, A Clash of Kings, A Storm of Swords" 
#>                                                          Chett 
#>                          "A Game of Thrones, A Clash of Kings" 
#>                                                        Cressen 
#>                         "A Storm of Swords, A Feast for Crows" 
#>                                                Arianne Martell 
#> "A Game of Thrones, A Clash of Kings, A Storm of Swords, A Da" 
#>                                             Daenerys Targaryen 
#>                                            "A Feast for Crows" 
#>                                                 Davos Seaworth 
#>                                            "A Feast for Crows" 
#>                                                     Arya Stark 
#>                                                     "no book!" 
#>                                                  Arys Oakheart 
#> "A Game of Thrones, A Clash of Kings, A Storm of Swords, A Da" 
#>                                                   Asha Greyjoy 
#>                          "A Game of Thrones, A Clash of Kings" 
#>                                                Barristan Selmy 
#> "A Game of Thrones, A Clash of Kings, A Storm of Swords, A Fe" 
#>                                                        Varamyr 
#>                                            "A Storm of Swords" 
#>                                                  Brandon Stark 
#>                                            "A Feast for Crows" 
#>                                               Brienne of Tarth 
#>    "A Clash of Kings, A Storm of Swords, A Dance with Dragons" 
#>                                                  Catelyn Stark 
#>                      "A Feast for Crows, A Dance with Dragons" 
#>                                               Cersei Lannister 
#>       "A Game of Thrones, A Clash of Kings, A Storm of Swords" 
#>                                                   Eddard Stark 
#> "A Clash of Kings, A Storm of Swords, A Feast for Crows, A Da" 
#>                                                Jaime Lannister 
#>                          "A Game of Thrones, A Clash of Kings" 
#>                                                 Jon Connington 
#> "A Storm of Swords, A Feast for Crows, The World of Ice and F" 
#>                                                       Jon Snow 
#>                                            "A Feast for Crows" 
#>                                                  Aeron Greyjoy 
#> "A Game of Thrones, A Clash of Kings, A Storm of Swords, A Da" 
#>                                                Kevan Lannister 
#> "A Game of Thrones, A Clash of Kings, A Storm of Swords, A Fe" 
#>                                                     Melisandre 
#>       "A Clash of Kings, A Storm of Swords, A Feast for Crows" 
#>                                                   Merrett Frey 
#> "A Game of Thrones, A Clash of Kings, A Feast for Crows, A Da" 
#>                                                Quentyn Martell 
#> "A Game of Thrones, A Clash of Kings, A Storm of Swords, A Fe" 
#>                                                  Samwell Tarly 
#>    "A Game of Thrones, A Clash of Kings, A Dance with Dragons" 
#>                                                    Sansa Stark 
#>                                         "A Dance with Dragons"

## Challenge (pick one or more):

##  Which SW film has the most characters?
#View(sw_films)
film_names <- map_chr(sw_films, "title")
sw_films %>%
  set_names(film_names) %>%
  map("characters") %>%
  map_int(length) %>%
  sort() %>%
  tail(1)
#> Attack of the Clones 
#>                   40
## I think it's Attack of the Clones?

##  Which SW species has the most possible eye colors?
library(tidyverse)
#> [1] "ggplot2" "tibble"  "tidyr"   "readr"   "dplyr"   "stringr" "forcats"
#> ── Attaching packages ───────────────────────────────────── tidyverse 1.2.1.9000 ──
#> ✔ ggplot2 3.0.0     ✔ dplyr   0.7.6
#> ✔ tibble  1.4.2     ✔ stringr 1.3.1
#> ✔ tidyr   0.8.1     ✔ forcats 0.3.0
#> ✔ readr   1.2.0
#> ── Conflicts ───────────────────────────────────────────── tidyverse_conflicts() ──
#> ✖ dplyr::filter() masks stats::filter()
#> ✖ dplyr::lag()    masks stats::lag()

df <- tibble(
  who = map_chr(sw_people, "name"),
  eye_color = map_chr(sw_people, "eye_color"),
  species = map_chr(sw_people, "species", .default = NA)
)
df %>%
  group_by(species) %>%
  summarize(eye_color_n = n_distinct(eye_color)) %>%
  arrange()
#> # A tibble: 38 x 2
#>    species                         eye_color_n
#>    <chr>                                 <int>
#>  1 http://swapi.co/api/species/1/            6
#>  2 http://swapi.co/api/species/10/           1
#>  3 http://swapi.co/api/species/11/           1
#>  4 http://swapi.co/api/species/12/           1
#>  5 http://swapi.co/api/species/13/           1
#>  6 http://swapi.co/api/species/14/           1
#>  7 http://swapi.co/api/species/15/           2
#>  8 http://swapi.co/api/species/16/           1
#>  9 http://swapi.co/api/species/17/           1
#> 10 http://swapi.co/api/species/18/           1
#> # ... with 28 more rows
## http://swapi.co/api/species/1/

View(sw_species)
#> Error in (function (..., row.names = NULL, check.rows = FALSE, check.names = TRUE, : arguments imply differing number of rows: 1, 3, 2
species_urls <- sw_species %>%
  map_chr("url")
this_one <- which(species_urls == "http://swapi.co/api/species/1/")
sw_species[[this_one]][["name"]]
#> [1] "Human"
## Human!

## easier way :(
sw_species_names <- map_chr(sw_species, "name")
sw_species %>%
  set_names(sw_species_names) %>%
  map_chr("eye_colors") %>%
  map(~ strsplit(.x, split = ",")[[1]]) %>%
  map_int(length) %>%
  sort()
#>   Mon Calamari      Sullustan         Gungan      Toydarian         Aleena 
#>              1              1              1              1              1 
#>     Vulptereen          Xexto          Toong         Cerean       Nautolan 
#>              1              1              1              1              1 
#>       Iktotchi       Quermian       Chagrian       Clawdite       Besalisk 
#>              1              1              1              1              1 
#>       Kaminoan        Skakoan           Muun        Kaleesh         Pau'an 
#>              1              1              1              1              1 
#>          Droid         Rodian           Hutt     Trandoshan           Ewok 
#>              1              1              2              2              2 
#>      Neimodian            Dug         Zabrak     Tholothian        Kel Dor 
#>              2              2              2              2              2 
#>      Geonosian Yoda's species        Twi'lek       Mirialan        Togruta 
#>              2              3              4              6              6 
#>        Wookiee          Human 
#>              6              6

people_names <- map(sw_people, "title")
sw_films %>%
  set_names(film_names) %>%
  map("characters")
#> $`A New Hope`
#>  [1] "http://swapi.co/api/people/1/"  "http://swapi.co/api/people/2/" 
#>  [3] "http://swapi.co/api/people/3/"  "http://swapi.co/api/people/4/" 
#>  [5] "http://swapi.co/api/people/5/"  "http://swapi.co/api/people/6/" 
#>  [7] "http://swapi.co/api/people/7/"  "http://swapi.co/api/people/8/" 
#>  [9] "http://swapi.co/api/people/9/"  "http://swapi.co/api/people/10/"
#> [11] "http://swapi.co/api/people/12/" "http://swapi.co/api/people/13/"
#> [13] "http://swapi.co/api/people/14/" "http://swapi.co/api/people/15/"
#> [15] "http://swapi.co/api/people/16/" "http://swapi.co/api/people/18/"
#> [17] "http://swapi.co/api/people/19/" "http://swapi.co/api/people/81/"
#> 
#> $`Attack of the Clones`
#>  [1] "http://swapi.co/api/people/2/"  "http://swapi.co/api/people/3/" 
#>  [3] "http://swapi.co/api/people/6/"  "http://swapi.co/api/people/7/" 
#>  [5] "http://swapi.co/api/people/10/" "http://swapi.co/api/people/11/"
#>  [7] "http://swapi.co/api/people/20/" "http://swapi.co/api/people/21/"
#>  [9] "http://swapi.co/api/people/22/" "http://swapi.co/api/people/33/"
#> [11] "http://swapi.co/api/people/36/" "http://swapi.co/api/people/40/"
#> [13] "http://swapi.co/api/people/43/" "http://swapi.co/api/people/46/"
#> [15] "http://swapi.co/api/people/51/" "http://swapi.co/api/people/52/"
#> [17] "http://swapi.co/api/people/53/" "http://swapi.co/api/people/58/"
#> [19] "http://swapi.co/api/people/59/" "http://swapi.co/api/people/60/"
#> [21] "http://swapi.co/api/people/61/" "http://swapi.co/api/people/62/"
#> [23] "http://swapi.co/api/people/63/" "http://swapi.co/api/people/64/"
#> [25] "http://swapi.co/api/people/65/" "http://swapi.co/api/people/66/"
#> [27] "http://swapi.co/api/people/67/" "http://swapi.co/api/people/68/"
#> [29] "http://swapi.co/api/people/69/" "http://swapi.co/api/people/70/"
#> [31] "http://swapi.co/api/people/71/" "http://swapi.co/api/people/72/"
#> [33] "http://swapi.co/api/people/73/" "http://swapi.co/api/people/74/"
#> [35] "http://swapi.co/api/people/75/" "http://swapi.co/api/people/76/"
#> [37] "http://swapi.co/api/people/77/" "http://swapi.co/api/people/78/"
#> [39] "http://swapi.co/api/people/82/" "http://swapi.co/api/people/35/"
#> 
#> $`The Phantom Menace`
#>  [1] "http://swapi.co/api/people/2/"  "http://swapi.co/api/people/3/" 
#>  [3] "http://swapi.co/api/people/10/" "http://swapi.co/api/people/11/"
#>  [5] "http://swapi.co/api/people/16/" "http://swapi.co/api/people/20/"
#>  [7] "http://swapi.co/api/people/21/" "http://swapi.co/api/people/32/"
#>  [9] "http://swapi.co/api/people/33/" "http://swapi.co/api/people/34/"
#> [11] "http://swapi.co/api/people/36/" "http://swapi.co/api/people/37/"
#> [13] "http://swapi.co/api/people/38/" "http://swapi.co/api/people/39/"
#> [15] "http://swapi.co/api/people/40/" "http://swapi.co/api/people/41/"
#> [17] "http://swapi.co/api/people/42/" "http://swapi.co/api/people/43/"
#> [19] "http://swapi.co/api/people/44/" "http://swapi.co/api/people/46/"
#> [21] "http://swapi.co/api/people/48/" "http://swapi.co/api/people/49/"
#> [23] "http://swapi.co/api/people/50/" "http://swapi.co/api/people/51/"
#> [25] "http://swapi.co/api/people/52/" "http://swapi.co/api/people/53/"
#> [27] "http://swapi.co/api/people/54/" "http://swapi.co/api/people/55/"
#> [29] "http://swapi.co/api/people/56/" "http://swapi.co/api/people/57/"
#> [31] "http://swapi.co/api/people/58/" "http://swapi.co/api/people/59/"
#> [33] "http://swapi.co/api/people/47/" "http://swapi.co/api/people/35/"
#> 
#> $`Revenge of the Sith`
#>  [1] "http://swapi.co/api/people/1/"  "http://swapi.co/api/people/2/" 
#>  [3] "http://swapi.co/api/people/3/"  "http://swapi.co/api/people/4/" 
#>  [5] "http://swapi.co/api/people/5/"  "http://swapi.co/api/people/6/" 
#>  [7] "http://swapi.co/api/people/7/"  "http://swapi.co/api/people/10/"
#>  [9] "http://swapi.co/api/people/11/" "http://swapi.co/api/people/12/"
#> [11] "http://swapi.co/api/people/13/" "http://swapi.co/api/people/20/"
#> [13] "http://swapi.co/api/people/21/" "http://swapi.co/api/people/33/"
#> [15] "http://swapi.co/api/people/46/" "http://swapi.co/api/people/51/"
#> [17] "http://swapi.co/api/people/52/" "http://swapi.co/api/people/53/"
#> [19] "http://swapi.co/api/people/54/" "http://swapi.co/api/people/55/"
#> [21] "http://swapi.co/api/people/56/" "http://swapi.co/api/people/58/"
#> [23] "http://swapi.co/api/people/63/" "http://swapi.co/api/people/64/"
#> [25] "http://swapi.co/api/people/67/" "http://swapi.co/api/people/68/"
#> [27] "http://swapi.co/api/people/75/" "http://swapi.co/api/people/78/"
#> [29] "http://swapi.co/api/people/79/" "http://swapi.co/api/people/80/"
#> [31] "http://swapi.co/api/people/81/" "http://swapi.co/api/people/82/"
#> [33] "http://swapi.co/api/people/83/" "http://swapi.co/api/people/35/"
#> 
#> $`Return of the Jedi`
#>  [1] "http://swapi.co/api/people/1/"  "http://swapi.co/api/people/2/" 
#>  [3] "http://swapi.co/api/people/3/"  "http://swapi.co/api/people/4/" 
#>  [5] "http://swapi.co/api/people/5/"  "http://swapi.co/api/people/10/"
#>  [7] "http://swapi.co/api/people/13/" "http://swapi.co/api/people/14/"
#>  [9] "http://swapi.co/api/people/16/" "http://swapi.co/api/people/18/"
#> [11] "http://swapi.co/api/people/20/" "http://swapi.co/api/people/21/"
#> [13] "http://swapi.co/api/people/22/" "http://swapi.co/api/people/25/"
#> [15] "http://swapi.co/api/people/27/" "http://swapi.co/api/people/28/"
#> [17] "http://swapi.co/api/people/29/" "http://swapi.co/api/people/30/"
#> [19] "http://swapi.co/api/people/31/" "http://swapi.co/api/people/45/"
#> 
#> $`The Empire Strikes Back`
#>  [1] "http://swapi.co/api/people/1/"  "http://swapi.co/api/people/2/" 
#>  [3] "http://swapi.co/api/people/3/"  "http://swapi.co/api/people/4/" 
#>  [5] "http://swapi.co/api/people/5/"  "http://swapi.co/api/people/10/"
#>  [7] "http://swapi.co/api/people/13/" "http://swapi.co/api/people/14/"
#>  [9] "http://swapi.co/api/people/18/" "http://swapi.co/api/people/20/"
#> [11] "http://swapi.co/api/people/21/" "http://swapi.co/api/people/22/"
#> [13] "http://swapi.co/api/people/23/" "http://swapi.co/api/people/24/"
#> [15] "http://swapi.co/api/people/25/" "http://swapi.co/api/people/26/"
#> 
#> $`The Force Awakens`
#>  [1] "http://swapi.co/api/people/1/"  "http://swapi.co/api/people/3/" 
#>  [3] "http://swapi.co/api/people/5/"  "http://swapi.co/api/people/13/"
#>  [5] "http://swapi.co/api/people/14/" "http://swapi.co/api/people/27/"
#>  [7] "http://swapi.co/api/people/84/" "http://swapi.co/api/people/85/"
#>  [9] "http://swapi.co/api/people/86/" "http://swapi.co/api/people/87/"
#> [11] "http://swapi.co/api/people/88/"

##  Which GoT character has the most allegiances? Aliases? Titles?
##
##  Which GoT character has been played by multiple actors?

## walk
library(tidyverse)
library(gapminder)

countries <- c("Argentina", "Brazil", "Canada")
gap_small <- gapminder %>%
  filter(country %in% countries, year > 1996)
gap_small
#> # A tibble: 9 x 6
#>   country   continent  year lifeExp       pop gdpPercap
#>   <fct>     <fct>     <int>   <dbl>     <int>     <dbl>
#> 1 Argentina Americas   1997    73.3  36203463    10967.
#> 2 Argentina Americas   2002    74.3  38331121     8798.
#> 3 Argentina Americas   2007    75.3  40301927    12779.
#> 4 Brazil    Americas   1997    69.4 168546719     7958.
#> 5 Brazil    Americas   2002    71.0 179914212     8131.
#> 6 Brazil    Americas   2007    72.4 190010647     9066.
#> 7 Canada    Americas   1997    78.6  30305843    28955.
#> 8 Canada    Americas   2002    79.8  31902268    33329.
#> 9 Canada    Americas   2007    80.7  33390141    36319.

filename <- paste0("Argentina", ".csv")
dataset <- filter(gap_small, country == "Argentina")
write_csv(dataset, filename)

write_one <- function(x) {
  filename <- paste0(x, ".csv")
  dataset <- filter(gap_small, country == x)
  write_csv(dataset, filename)
}

map(countries, write_one)
#> [[1]]
#> # A tibble: 3 x 6
#>   country   continent  year lifeExp      pop gdpPercap
#>   <chr>     <chr>     <int>   <dbl>    <int>     <dbl>
#> 1 Argentina Americas   1997    73.3 36203463    10967.
#> 2 Argentina Americas   2002    74.3 38331121     8798.
#> 3 Argentina Americas   2007    75.3 40301927    12779.
#> 
#> [[2]]
#> # A tibble: 3 x 6
#>   country continent  year lifeExp       pop gdpPercap
#>   <chr>   <chr>     <int>   <dbl>     <int>     <dbl>
#> 1 Brazil  Americas   1997    69.4 168546719     7958.
#> 2 Brazil  Americas   2002    71.0 179914212     8131.
#> 3 Brazil  Americas   2007    72.4 190010647     9066.
#> 
#> [[3]]
#> # A tibble: 3 x 6
#>   country continent  year lifeExp      pop gdpPercap
#>   <chr>   <chr>     <int>   <dbl>    <int>     <dbl>
#> 1 Canada  Americas   1997    78.6 30305843    28955.
#> 2 Canada  Americas   2002    79.8 31902268    33329.
#> 3 Canada  Americas   2007    80.7 33390141    36319.
walk(countries, write_one)
list.files(pattern = "*.csv")
#> [1] "Argentina.csv" "Brazil.csv"    "Canada.csv"

## doing the inverse
library(tidyverse)

csv_files <- list.files(pattern = "*.csv")
csv_files
#> [1] "Argentina.csv" "Brazil.csv"    "Canada.csv"

map_dfr(csv_files, ~ read_csv(.x))
#> Parsed with column specification:
#> cols(
#>   country = col_character(),
#>   continent = col_character(),
#>   year = col_double(),
#>   lifeExp = col_double(),
#>   pop = col_double(),
#>   gdpPercap = col_double()
#> )
#> Parsed with column specification:
#> cols(
#>   country = col_character(),
#>   continent = col_character(),
#>   year = col_double(),
#>   lifeExp = col_double(),
#>   pop = col_double(),
#>   gdpPercap = col_double()
#> )
#> Parsed with column specification:
#> cols(
#>   country = col_character(),
#>   continent = col_character(),
#>   year = col_double(),
#>   lifeExp = col_double(),
#>   pop = col_double(),
#>   gdpPercap = col_double()
#> )
#> # A tibble: 9 x 6
#>   country   continent  year lifeExp       pop gdpPercap
#>   <chr>     <chr>     <dbl>   <dbl>     <dbl>     <dbl>
#> 1 Argentina Americas   1997    73.3  36203463    10967.
#> 2 Argentina Americas   2002    74.3  38331121     8798.
#> 3 Argentina Americas   2007    75.3  40301927    12779.
#> 4 Brazil    Americas   1997    69.4 168546719     7958.
#> 5 Brazil    Americas   2002    71.0 179914212     8131.
#> 6 Brazil    Americas   2007    72.4 190010647     9066.
#> 7 Canada    Americas   1997    78.6  30305843    28955.
#> 8 Canada    Americas   2002    79.8  31902268    33329.
#> 9 Canada    Americas   2007    80.7  33390141    36319.
```

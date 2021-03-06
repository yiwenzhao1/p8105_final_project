Data Clean
================

``` r
# clean data
crime_2016 =
   read.csv("./data/Crimes_-_2016.csv") %>% 
   drop_na() %>% 
   janitor::clean_names() %>%
   filter(arrest=="true",domestic=="true")
crime_2017 =
   read.csv("./data/Crimes_-_2017.csv") %>% 
   drop_na() %>% 
   janitor::clean_names() %>%
   filter(arrest=="true",domestic=="true")
crime_2018 =
   read.csv("./data/Crimes_-_2018.csv") %>% 
   drop_na() %>% 
   janitor::clean_names() %>%
   filter(arrest=="true",domestic=="true")
crime_2019 =
   read.csv("./data/Crimes_-_2019.csv") %>% 
   drop_na() %>% 
   janitor::clean_names() %>%
   filter(arrest=="true",domestic=="true")
crime_2020 =
   read.csv("./data/Crimes_-_2020.csv") %>% 
   drop_na() %>% 
   janitor::clean_names() %>%
   filter(arrest=="true",domestic=="true")
crime_2021 =
   read.csv("./data/Crimes_-_2021.csv") %>% 
   drop_na() %>% 
   janitor::clean_names() %>%
   filter(arrest=="true",domestic=="true")
```

``` r
full_df=
   do.call("rbind",list(crime_2016,crime_2017,crime_2018,crime_2019,crime_2020,crime_2020,crime_2021)) %>% 
   mutate(
      date=strptime(date, "%m/%d/%Y %I:%M:%S %p"),
      date=as.Date(date,"%Y-%m-%d"),
      year = as.numeric(format(date, format = "%Y")),
      month = as.numeric(format(date, format = "%m")),
      day = as.numeric(format(date, format = "%d"))
      ) %>% 
   relocate(year,month,day,.before = date)
write.csv(full_df,file="./data/data_clean.csv")
```

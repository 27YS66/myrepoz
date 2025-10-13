# Исследование метаданных DNS трафика
iablokovasofia@yandex.ru

## Цель работы:

1.  Зекрепить практические навыки использования языка программирования R
    для обработки данных
2.  Закрепить знания основных функций обработки данных экосистемы
    tidyverse языка R
3.  Закрепить навыки исследования метаданных DNS трафика

## Исходные данные

1.  Программное обеспечение Windows 10
2.  Rstudio Desktop
3.  Наше рабочее окружение

``` r
sessionInfo()
```

    R version 4.5.1 (2025-06-13 ucrt)
    Platform: x86_64-w64-mingw32/x64
    Running under: Windows 10 x64 (build 19045)

    Matrix products: default
      LAPACK version 3.12.1

    locale:
    [1] LC_COLLATE=Russian_Russia.utf8  LC_CTYPE=Russian_Russia.utf8   
    [3] LC_MONETARY=Russian_Russia.utf8 LC_NUMERIC=C                   
    [5] LC_TIME=Russian_Russia.utf8    

    time zone: Europe/Moscow
    tzcode source: internal

    attached base packages:
    [1] stats     graphics  grDevices utils     datasets  methods   base     

    loaded via a namespace (and not attached):
     [1] compiler_4.5.1    fastmap_1.2.0     cli_3.6.5         tools_4.5.1      
     [5] htmltools_0.5.8.1 rstudioapi_0.17.1 yaml_2.3.10       rmarkdown_2.30   
     [9] knitr_1.50        jsonlite_2.0.0    xfun_0.53         digest_0.6.37    
    [13] rlang_1.1.6       evaluate_1.0.5   

## План

Используя R и среду разработки RstudioIDE, выполнить задания.

## Шаги:

    > library(tidyverse)
    Ошибка в library(tidyverse) : нет пакета под названием ‘tidyverse’

    > install.packages("tidyverse")
    WARNING: Rtools is required to build R packages but is not currently installed. Please download and install the appropriate version of Rtools before proceeding:

    https://cran.rstudio.com/bin/windows/Rtools/
    Устанавливаю пакет в ‘C:/Users/София/AppData/Local/R/win-library/4.5’
    (потому что ‘lib’ не определено)
    устанавливаю также зависимость ‘bit’, ‘farver’, ‘labeling’, ‘RColorBrewer’, ‘viridisLite’, ‘rematch’, ‘bit64’, ‘prettyunits’, ‘backports’, ‘blob’, ‘DBI’, ‘data.table’, ‘gtable’, ‘isoband’, ‘S7’, ‘scales’, ‘gargle’, ‘uuid’, ‘cellranger’, ‘ids’, ‘rematch2’, ‘cpp11’, ‘timechange’, ‘systemfonts’, ‘textshaping’, ‘clipr’, ‘vroom’, ‘tzdb’, ‘progress’, ‘selectr’, ‘broom’, ‘conflicted’, ‘dbplyr’, ‘dtplyr’, ‘forcats’, ‘ggplot2’, ‘googledrive’, ‘googlesheets4’, ‘haven’, ‘hms’, ‘lubridate’, ‘modelr’, ‘purrr’, ‘ragg’, ‘readr’, ‘readxl’, ‘reprex’, ‘rstudioapi’, ‘rvest’, ‘tidyr’, ‘xml2’

      В наличии есть бинарная версия, но исходники новее:
                binary source needs_compilation
    textshaping  1.0.3  1.0.4              TRUE

      Binaries will be installed
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/bit_4.6.0.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/farver_2.1.2.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/labeling_0.4.3.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/RColorBrewer_1.1-3.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/viridisLite_0.4.2.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/rematch_2.0.0.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/bit64_4.6.0-1.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/prettyunits_1.2.0.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/backports_1.5.0.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/blob_1.2.4.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/DBI_1.2.3.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/data.table_1.17.8.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/gtable_0.3.6.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/isoband_0.2.7.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/S7_0.2.0.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/scales_1.4.0.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/gargle_1.6.0.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/uuid_1.2-1.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/cellranger_1.1.0.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/ids_1.0.1.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/rematch2_2.1.2.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/cpp11_0.5.2.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/timechange_0.3.0.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/systemfonts_1.3.1.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/textshaping_1.0.3.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/clipr_0.8.0.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/vroom_1.6.6.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/tzdb_0.5.0.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/progress_1.2.3.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/selectr_0.4-2.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/broom_1.0.10.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/conflicted_1.2.0.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/dbplyr_2.5.1.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/dtplyr_1.3.2.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/forcats_1.0.1.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/ggplot2_4.0.0.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/googledrive_2.1.2.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/googlesheets4_1.1.2.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/haven_2.5.5.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/hms_1.1.3.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/lubridate_1.9.4.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/modelr_0.1.11.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/purrr_1.1.0.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/ragg_1.5.0.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/readr_2.1.5.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/readxl_1.4.5.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/reprex_2.1.1.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/rstudioapi_0.17.1.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/rvest_1.0.5.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/tidyr_1.3.1.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/xml2_1.4.0.zip'
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/tidyverse_2.0.0.zip'
    пакет ‘bit’ успешно распакован, MD5-суммы проверены
    пакет ‘farver’ успешно распакован, MD5-суммы проверены
    пакет ‘labeling’ успешно распакован, MD5-суммы проверены
    пакет ‘RColorBrewer’ успешно распакован, MD5-суммы проверены
    пакет ‘viridisLite’ успешно распакован, MD5-суммы проверены
    пакет ‘rematch’ успешно распакован, MD5-суммы проверены
    пакет ‘bit64’ успешно распакован, MD5-суммы проверены
    пакет ‘prettyunits’ успешно распакован, MD5-суммы проверены
    пакет ‘backports’ успешно распакован, MD5-суммы проверены
    пакет ‘blob’ успешно распакован, MD5-суммы проверены
    пакет ‘DBI’ успешно распакован, MD5-суммы проверены
    пакет ‘data.table’ успешно распакован, MD5-суммы проверены
    пакет ‘gtable’ успешно распакован, MD5-суммы проверены
    пакет ‘isoband’ успешно распакован, MD5-суммы проверены
    пакет ‘S7’ успешно распакован, MD5-суммы проверены
    пакет ‘scales’ успешно распакован, MD5-суммы проверены
    пакет ‘gargle’ успешно распакован, MD5-суммы проверены
    пакет ‘uuid’ успешно распакован, MD5-суммы проверены
    пакет ‘cellranger’ успешно распакован, MD5-суммы проверены
    пакет ‘ids’ успешно распакован, MD5-суммы проверены
    пакет ‘rematch2’ успешно распакован, MD5-суммы проверены
    пакет ‘cpp11’ успешно распакован, MD5-суммы проверены
    пакет ‘timechange’ успешно распакован, MD5-суммы проверены
    пакет ‘systemfonts’ успешно распакован, MD5-суммы проверены
    пакет ‘textshaping’ успешно распакован, MD5-суммы проверены
    пакет ‘clipr’ успешно распакован, MD5-суммы проверены
    пакет ‘vroom’ успешно распакован, MD5-суммы проверены
    пакет ‘tzdb’ успешно распакован, MD5-суммы проверены
    пакет ‘progress’ успешно распакован, MD5-суммы проверены
    пакет ‘selectr’ успешно распакован, MD5-суммы проверены
    пакет ‘broom’ успешно распакован, MD5-суммы проверены
    пакет ‘conflicted’ успешно распакован, MD5-суммы проверены
    пакет ‘dbplyr’ успешно распакован, MD5-суммы проверены
    пакет ‘dtplyr’ успешно распакован, MD5-суммы проверены
    пакет ‘forcats’ успешно распакован, MD5-суммы проверены
    пакет ‘ggplot2’ успешно распакован, MD5-суммы проверены
    пакет ‘googledrive’ успешно распакован, MD5-суммы проверены
    пакет ‘googlesheets4’ успешно распакован, MD5-суммы проверены
    пакет ‘haven’ успешно распакован, MD5-суммы проверены
    пакет ‘hms’ успешно распакован, MD5-суммы проверены
    пакет ‘lubridate’ успешно распакован, MD5-суммы проверены
    пакет ‘modelr’ успешно распакован, MD5-суммы проверены
    пакет ‘purrr’ успешно распакован, MD5-суммы проверены
    пакет ‘ragg’ успешно распакован, MD5-суммы проверены
    пакет ‘readr’ успешно распакован, MD5-суммы проверены
    пакет ‘readxl’ успешно распакован, MD5-суммы проверены
    пакет ‘reprex’ успешно распакован, MD5-суммы проверены
    пакет ‘rstudioapi’ успешно распакован, MD5-суммы проверены
    пакет ‘rvest’ успешно распакован, MD5-суммы проверены
    пакет ‘tidyr’ успешно распакован, MD5-суммы проверены
    пакет ‘xml2’ успешно распакован, MD5-суммы проверены
    пакет ‘tidyverse’ успешно распакован, MD5-суммы проверены

    Скачанные бинарные пакеты находятся в
        C:\Users\София\AppData\Local\Temp\RtmpCs9i8u\downloaded_packages
    > library(tidyverse)
    ── Attaching core tidyverse packages ──────────────────────────────────── tidyverse 2.0.0 ──
    ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ✔ forcats   1.0.1     ✔ stringr   1.5.2
    ✔ ggplot2   4.0.0     ✔ tibble    3.3.0
    ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ✔ purrr     1.1.0     
    ── Conflicts ────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ✖ dplyr::filter() masks stats::filter()
    ✖ dplyr::lag()    masks stats::lag()
    ℹ Use the conflicted package to force all conflicts to become errors
    > library(dplyr)
    > library(readr)
    > library(lubridate)
    > temp_file <- tempfile()
    > download.file("https://storage.yandexcloud.net/dataset.ctfsec/dns.zip", temp_file)
    пробую URL 'https://storage.yandexcloud.net/dataset.ctfsec/dns.zip'
    Content type 'application/zip' length 6407934 bytes (6.1 MB)
    downloaded 6.1 MB

    > unzip(temp_file, exdir = "dns_data")
    > dns_data <- read_tsv("dns_data/dns.log", col_names = FALSE)
    Rows: 427935 Columns: 23                                                                    
    ── Column specification ────────────────────────────────────────────────────────────────────
    Delimiter: "\t"
    chr (13): X2, X3, X5, X7, X9, X10, X11, X12, X13, X14, X15, X21, X22
    dbl  (5): X1, X4, X6, X8, X20
    lgl  (5): X16, X17, X18, X19, X23

    ℹ Use `spec()` to retrieve the full column specification for this data.
    ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
    > colnames(dns_data) <- c("ts", "uid", "id.orig_h", "id.orig_p", "id.resp_h", "id.resp_p",
    +                         "proto", "trans_id", "rtt", "query", "qclass", "qclass_name",
    +                         "qtype", "qtype_name", "rcode", "rcode_name", "AA", "TC", "RD", 
    +                         "RA", "Z", "answers", "TTLs", "rejected")
    > 
    > dns_data <- dns_data %>%
    + mutate(ts = as_datetime(ts),
    + id.orig_h = as.character(id.orig_h),
    + id.resp_h = as.character(id.resp_h),
    + query = as.character(query))
    > 
    > glimpse(dns_data)
    Rows: 427,935
    Columns: 23
    $ ts          <dttm> 2012-03-16 12:30:05, 2012-03-16 12:30:15, 2012-03-16 12:30:15, 2012-0…
    $ uid         <chr> "CWGtK431H9XuaTN4fi", "C36a282Jljz7BsbGH", "C36a282Jljz7BsbGH", "C36a2…
    $ id.orig_h   <chr> "192.168.202.100", "192.168.202.76", "192.168.202.76", "192.168.202.76…
    $ id.orig_p   <dbl> 45658, 137, 137, 137, 137, 137, 137, 137, 137, 137, 137, 137, 137, 456…
    $ id.resp_h   <chr> "192.168.27.203", "192.168.202.255", "192.168.202.255", "192.168.202.2…
    $ id.resp_p   <dbl> 137, 137, 137, 137, 137, 137, 137, 137, 137, 137, 137, 137, 137, 5353,…
    $ proto       <chr> "udp", "udp", "udp", "udp", "udp", "udp", "udp", "udp", "udp", "udp", …
    $ trans_id    <dbl> 33008, 57402, 57402, 57402, 57398, 57398, 57398, 62187, 62187, 62187, …
    $ rtt         <chr> "*\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x…
    $ query       <chr> "1", "1", "1", "1", "1", "1", "1", "1", "1", "1", "1", "1", "1", "1", …
    $ qclass      <chr> "C_INTERNET", "C_INTERNET", "C_INTERNET", "C_INTERNET", "C_INTERNET", …
    $ qclass_name <chr> "33", "32", "32", "32", "32", "32", "32", "32", "32", "32", "33", "33"…
    $ qtype       <chr> "SRV", "NB", "NB", "NB", "NB", "NB", "NB", "NB", "NB", "NB", "SRV", "S…
    $ qtype_name  <chr> "0", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", …
    $ rcode       <chr> "NOERROR", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-",…
    $ rcode_name  <lgl> FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, …
    $ AA          <lgl> FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, …
    $ TC          <lgl> FALSE, TRUE, TRUE, TRUE, TRUE, TRUE, TRUE, TRUE, TRUE, TRUE, FALSE, FA…
    $ RD          <lgl> FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, …
    $ RA          <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 1, 1, 1, 1, 0, 0, 0, 0, 0…
    $ Z           <chr> "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", …
    $ answers     <chr> "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", "-", …
    $ TTLs        <lgl> FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, …
    > 
    > summary(dns_data)
           ts                          uid             id.orig_h           id.orig_p    
     Min.   :2012-03-16 12:30:05   Length:427935      Length:427935      Min.   :  137  
     1st Qu.:2012-03-16 17:02:59   Class :character   Class :character   1st Qu.:19198  
     Median :2012-03-16 18:36:32   Mode  :character   Mode  :character   Median :47931  
     Mean   :2012-03-16 23:48:03                                         Mean   :37165  
     3rd Qu.:2012-03-17 13:00:19                                         3rd Qu.:56239  
     Max.   :2012-03-17 20:59:51                                         Max.   :65535  
      id.resp_h           id.resp_p       proto              trans_id         rtt           
     Length:427935      Min.   :  53   Length:427935      Min.   :    0   Length:427935     
     Class :character   1st Qu.:  53   Class :character   1st Qu.:11101   Class :character  
     Mode  :character   Median :  53   Mode  :character   Median :28625   Mode  :character  
                        Mean   : 301                      Mean   :29525                     
                        3rd Qu.:  53                      3rd Qu.:46913                     
                        Max.   :5355                      Max.   :65535                     
        query              qclass          qclass_name           qtype          
     Length:427935      Length:427935      Length:427935      Length:427935     
     Class :character   Class :character   Class :character   Class :character  
     Mode  :character   Mode  :character   Mode  :character   Mode  :character  
                                                                                
                                                                                
                                                                                
      qtype_name           rcode           rcode_name          AA              TC         
     Length:427935      Length:427935      Mode :logical   Mode :logical   Mode :logical  
     Class :character   Class :character   FALSE:426802    FALSE:427935    FALSE:34461    
     Mode  :character   Mode  :character   TRUE :1133                      TRUE :393474   
                                                                                          
                                                                                          
                                                                                          
         RD                RA              Z               answers             TTLs        
     Mode :logical   Min.   :0.0000   Length:427935      Length:427935      Mode :logical  
     FALSE:427106    1st Qu.:0.0000   Class :character   Class :character   FALSE:425858   
     TRUE :829       Median :0.0000   Mode  :character   Mode  :character   TRUE :2077     
                     Mean   :0.1898                                                        
                     3rd Qu.:0.0000                                                        
                     Max.   :1.0000                                                        
    > 
    > # Вопрос 4. Количество участников информационного обмена ?
    > all_ips <- unique(c(dns_data$id.orig_h, dns_data$id.resp_h))
    > total_participants <- length(all_ips)
    > print(paste("Всего участников:", total_participants))
    [1] "Всего участников: 1359"
    > # Вопрос 5. Какое соотношение участников обмена внутри
    > сети и участников обращений к внешним
    Ошибка: неожиданный символ в "сети и"

    > internal_ips <- all_ips[grepl("^(10\\.|192\\.168\\.|172\\.(1[6-9]|2[0-9]|3[0-1])\\.)", all_ips)]
    > external_ips <- setdiff(all_ips, internal_ips)
    > ratio <- length(internal_ips)/length(external_ips)
    > print(paste("Соотношение внутренних/внешних:", round(ratio, 2)))
    [1] "Соотношение внутренних/внешних: 13.77"
    > 
    > # Вопрос 6.  Найдите топ-10 участников сети, проявляющих
    > наибольшую сетевую активность.
    Ошибка: неожиданный символ в "наибольшую сетевую"

    > top_active <- dns_data %>%
    + count(id.orig_h, sort = TRUE) %>%
    + head(10)
    > print("Топ-10 активных участников:")
    [1] "Топ-10 активных участников:"
    > print(top_active)
    # A tibble: 10 × 2
       id.orig_h           n
       <chr>           <int>
     1 10.10.117.210   75943
     2 192.168.202.93  26522
     3 192.168.202.103 18121
     4 192.168.202.76  16978
     5 192.168.202.97  16176
     6 192.168.202.141 14967
     7 10.10.117.209   14222
     8 192.168.202.110 13372
     9 192.168.203.63  12148
    10 192.168.202.106 10784
    > # Вопрос 7. Найдите топ-10 доменов, к которым обращаются пользователи сети и соответственное количество обращений
    > 
    > top_domains <- dns_data %>%
    + count(query, sort = TRUE) %>%
    + head(10)
    > print("Топ-10 доменов:")
    [1] "Топ-10 доменов:"
    > print(top_domains)
    # A tibble: 4 × 2
      query      n
      <chr>  <int>
    1 1     422339
    2 -       3648
    3 3       1016
    4 32769    932
    > 
    > # Вопрос 8. Опеределите базовые статистические характеристики (функция summary() ) интервала времени между последовательными обращениями к топ-10 доменам.
    > 
    > top_domain_names <- top_domains$query
    > time_intervals <- dns_data %>%
    + filter(query %in% top_domain_names) %>%
    + arrange(query, ts) %>%
    + group_by(query) %>%
    + mutate(time_diff = as.numeric(ts - lag(ts))) %>%
    + filter(!is.na(time_diff))
    > interval_stats <- time_intervals %>%
    + group_by(query) %>%
    + summarise(
    + min = min(time_diff),
    + q1 = quantile(time_diff, 0.25),
    + median = median(time_diff),
    + mean = mean(time_diff),
    + q3 = quantile(time_diff, 0.75),
    + max = max(time_diff)
    + )
    > print("Статистика интервалов:")
    [1] "Статистика интервалов:"
    > print(interval_stats)
    # A tibble: 4 × 7
      query   min     q1  median    mean    q3    max
      <chr> <dbl>  <dbl>   <dbl>   <dbl> <dbl>  <dbl>
    1 -         0 0.0700 0.990    32.0   3.80  49787.
    2 1         0 0      0.01000   0.277 0.150 49669.
    3 3         0 0      0.0200  106.    1.99  58363.
    4 32769     0 0.115  1.12    119.    2.01  52833.
    > 
    > # Вопрос 9. Часто вредоносное программное обеспечение использует DNS канал в качестве канала управления, периодически отправляя запросы на подконтрольный злоумышленникам DNS сервер. По периодическим запросам на один и тот же домен можно выявить скрытый DNS канал. Есть ли такие IP адреса в исследуемом датасете?
    > 
    > suspicious_channels <- dns_data %>%
    + group_by(id.orig_h, query) %>%
    + summarise(
    + request_count = n(),
    + time_range = as.numeric(max(ts) - min(ts)),
    + avg_interval = time_range/(request_count - 1),
    + periodicity_score = sd(diff(as.numeric(ts)), na.rm = TRUE)
    + ) %>%
    + filter(request_count > 10, 
    + time_range > 3600,
    + periodicity_score < 300) %>%
    + arrange(periodicity_score)
    `summarise()` has grouped output by 'id.orig_h'. You can override using the `.groups`
    argument.
    > print("Подозрительные DNS-каналы:")
    [1] "Подозрительные DNS-каналы:"
    > print(suspicious_channels)
    # A tibble: 0 × 6
    # Groups:   id.orig_h [0]
    # ℹ 6 variables: id.orig_h <chr>, query <chr>, request_count <int>, time_range <dbl>,
    #   avg_interval <dbl>, periodicity_score <dbl>
    > 
    > # Вопрос 10. Определите местоположение (страну, город) и организацию-провайдера для топ-10 доменов. Для этого можно использовать сторонние сервисы, например http://ip-api.com (API-эндпоинт – http://ip-api.com/json).
    > 
    > 
    > get_ip_info <- function(ip) {
    + if (!is.na(ip)) {
    + url <- paste0("http://ip-api.com/json/", ip)
    + response <- tryCatch({
    + fromJSON(url)
    + }, error = function(e) NULL)
    + if (!is.null(response) && response$status == "success") {
    + return(data.frame(
    + ip = ip,
    + country = response$country,
    + city = response$city,
    + isp = response$isp,
    + stringsAsFactors = FALSE
    + ))
    + }
    + }
    + return(NULL)
    + }
    > domain_ips <- dns_data %>%
    + filter(query %in% top_domain_names) %>%
    + distinct(query, answers) %>%
    + filter(!is.na(answers))
    > ip_info_list <- list()
    > for (i in 1:nrow(domain_ips)) {
    + ip <- domain_ips$answers[i]
    + info <- get_ip_info(ip)
    + if (!is.null(info)) {
    + ip_info_list[[i]] <- cbind(domain = domain_ips$query[i], info)
    + }
    + Sys.sleep(0.5)
    + }
    > 
    > 
    > if (length(geo_results) > 0) {
    + 
    + 
    + о
    + 
    > geo_info <- bind_rows(ip_info_list)
    > print("Геолокация топ-доменов:")
    [1] "Геолокация топ-доменов:"
    > print(geo_info)
    # A tibble: 0 × 0
    > 
    > rm(ip_info_list)
    > if (!exists("top_domains")) {
    + top_domains <- dns_data %>%
    + count(query, sort = TRUE) %>%
    + head(10) %>%
    + rename(domain = query, request_count = n)
    + }
    > cat("Топ-10 доменов для анализа:\n")
    Топ-10 доменов для анализа:
    > print(top_domains)
    # A tibble: 4 × 2
      query      n
      <chr>  <int>
    1 1     422339
    2 -       3648
    3 3       1016
    4 32769    932
    > 
    > domain_ips <- dns_data %>%
    + filter(query %in% top_domains$domain) %>%
    + filter(!is.na(answers)) %>%
    + distinct(query, answers) %>%
    + group_by(query) %>%
    + slice(1) %>%
    + ungroup()
    Предупреждение:
    There was 1 warning in `filter()`.
    ℹ In argument: `query %in% top_domains$domain`.
    Caused by warning:
    ! Unknown or uninitialised column: `domain`. 

    > cat("IP-адреса для топ-доменов:\n")
    IP-адреса для топ-доменов:
    > print(domain_ips)
    # A tibble: 0 × 2
    # ℹ 2 variables: query <chr>, answers <chr>
    > 
    > cat("\nПроверка IP-адресов:\n")

    Проверка IP-адресов:
    > cat("Уникальные IP:", unique(domain_ips$answers), "\n")
    Уникальные IP:  
    > cat("Количество записей:", nrow(domain_ips), "\n")
    Количество записей: 0 
    > rm(list = ls(pattern = "^top_|domain_ips"))
    > top_domains <- dns_data %>%
    + count(query, sort = TRUE) %>%
    + head(10) %>%
    + rename(domain = query, request_count = n)
    > cat("Топ-10 доменов:\n")
    Топ-10 доменов:
    > print(top_domains)
    # A tibble: 4 × 2
      domain request_count
      <chr>          <int>
    1 1             422339
    2 -               3648
    3 3               1016
    4 32769            932
    > 
    > top_domain_names <- top_domains$domain
    > cat("Список доменов для анализа:", paste(top_domain_names, collapse = ", "), "\n")
    Список доменов для анализа: 1, -, 3, 32769 
    > 
    > cat("Поиск IP-адресов в столбце answers...\n")
    Поиск IP-адресов в столбце answers...
    > domain_ips1 <- dns_data %>%
    + filter(query %in% top_domain_names) %>%
    + filter(!is.na(answers)) %>%
    + distinct(query, answers) %>%
    + group_by(query) %>%
    + slice(1) %>%
    + ungroup()
    > cat("Результат поиска в answers:", nrow(domain_ips1), "записей\n")
    Результат поиска в answers: 4 записей
    > cat("Поиск реальных доменных имен в данных...\n")
    Поиск реальных доменных имен в данных...
    > is_likely_domain <- function(x) {
    + grepl("[a-zA-Z]", x) & grepl("\\.", x) & !grepl("^[0-9]+\\.[0-9]+\\.[0-9]+\\.[0-9]+$", x)
    + }
    > real_domains <- dns_data %>%
    + filter(is_likely_domain(query)) %>%
    + count(query, sort = TRUE) %>%
    + head(10) %>%
    + rename(domain = query, request_count = n)
    > cat("Топ-10 реальных доменных имен:\n")
    Топ-10 реальных доменных имен:
    > print(real_domains)
    # A tibble: 0 × 2
    # ℹ 2 variables: domain <chr>, request_count <int>
    > if (nrow(real_domains) == 0) {
    + cat("Реальных доменов не найдено, ищем строки с точками...\n")
    + real_domains <- dns_data %>%
    + filter(grepl("\\.", query)) %>%
    + count(query, sort = TRUE) %>%
    + head(10) %>%
    + rename(domain = query, request_count = n)
    + }
    Реальных доменов не найдено, ищем строки с точками...
    > cat("Финальный список для анализа:\n")
    Финальный список для анализа:
    > print(real_domains)
    # A tibble: 0 × 2
    # ℹ 2 variables: domain <chr>, request_count <int>
    > 
    > domain_ips <- dns_data %>%
    + 

## Оценка результата

В результате лабораторной работы мы закрепили знания основных функций
обработки данных экосистемы tidyverse языка R и исследования метаданных
DNS трафика

## Вывод

Таким образом, мы закрепили знания основных функций обработки данных
экосистемы tidyverse языка R и исследования метаданных DNS трафика

# Исследование информации о состоянии беспроводных сетей
iablokovasofia@yandex.ru

## Цель работы:

1.  Получить знания о методах исследования радиоэлектронной обстановки.
2.  Составить представление о механизмах работы Wi-Fi сетей на канальном
    и сетевом уровне модели OSI.
3.  Зекрепить практические навыки использования языка программирования R
    для обработки данных
4.  Закрепить знания основных функций обработки данных экосистемы
    tidyverse языка R

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


    > install.packages("dplyr")
    WARNING: Rtools is required to build R packages but is not currently installed. Please download and install the appropriate version of Rtools before proceeding:

    https://cran.rstudio.com/bin/windows/Rtools/
    Устанавливаю пакет в ‘C:/Users/София/AppData/Local/R/win-library/4.5’
    (потому что ‘lib’ не определено)
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/dplyr_1.1.4.zip'
    Content type 'application/zip' length 1593077 bytes (1.5 MB)
    downloaded 1.5 MB

    пакет ‘dplyr’ успешно распакован, MD5-суммы проверены

    Скачанные бинарные пакеты находятся в
        C:\Users\София\AppData\Local\Temp\RtmpuSf2jT\downloaded_packages
    > 
    > install.packages("tidyverse")
    WARNING: Rtools is required to build R packages but is not currently installed. Please download and install the appropriate version of Rtools before proceeding:

    https://cran.rstudio.com/bin/windows/Rtools/
    Устанавливаю пакет в ‘C:/Users/София/AppData/Local/R/win-library/4.5’
    (потому что ‘lib’ не определено)
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/tidyverse_2.0.0.zip'
    Content type 'application/zip' length 431697 bytes (421 KB)
    downloaded 421 KB

    пакет ‘tidyverse’ успешно распакован, MD5-суммы проверены

    Скачанные бинарные пакеты находятся в
        C:\Users\София\AppData\Local\Temp\RtmpuSf2jT\downloaded_packages
    > install.packages("lubridate")
    WARNING: Rtools is required to build R packages but is not currently installed. Please download and install the appropriate version of Rtools before proceeding:

    https://cran.rstudio.com/bin/windows/Rtools/
    Устанавливаю пакет в ‘C:/Users/София/AppData/Local/R/win-library/4.5’
    (потому что ‘lib’ не определено)
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/lubridate_1.9.4.zip'
    Content type 'application/zip' length 995341 bytes (972 KB)
    downloaded 972 KB

    пакет ‘lubridate’ успешно распакован, MD5-суммы проверены

    Скачанные бинарные пакеты находятся в
        C:\Users\София\AppData\Local\Temp\RtmpuSf2jT\downloaded_packages
    > install.packages("stringr")
    WARNING: Rtools is required to build R packages but is not currently installed. Please download and install the appropriate version of Rtools before proceeding:

    https://cran.rstudio.com/bin/windows/Rtools/
    Устанавливаю пакет в ‘C:/Users/София/AppData/Local/R/win-library/4.5’
    (потому что ‘lib’ не определено)
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/stringr_1.5.2.zip'
    Content type 'application/zip' length 325091 bytes (317 KB)
    downloaded 317 KB

    пакет ‘stringr’ успешно распакован, MD5-суммы проверены

    Скачанные бинарные пакеты находятся в
        C:\Users\София\AppData\Local\Temp\RtmpuSf2jT\downloaded_packages
    > install.packages("readr")
    WARNING: Rtools is required to build R packages but is not currently installed. Please download and install the appropriate version of Rtools before proceeding:

    https://cran.rstudio.com/bin/windows/Rtools/
    Устанавливаю пакет в ‘C:/Users/София/AppData/Local/R/win-library/4.5’
    (потому что ‘lib’ не определено)
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/readr_2.1.5.zip'
    Content type 'application/zip' length 1237515 bytes (1.2 MB)
    downloaded 1.2 MB

    пакет ‘readr’ успешно распакован, MD5-суммы проверены

    Скачанные бинарные пакеты находятся в
        C:\Users\София\AppData\Local\Temp\RtmpuSf2jT\downloaded_packages
    > 
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
    > library(lubridate)
    > library(stringr)
    > library(readr)
    > # импорт данных
    > data_url <- "https://storage.yandexcloud.net/dataset.ctfsec/P2_wifi_data.csv"
    > raw_data <- read_csv(data_url,
    + skip = 1, 
    + col_names = FALSE,
    + col_types = cols(.default = col_character()),
    + locale = locale(encoding = "UTF-8"))
    Предупреждение:
    One or more parsing issues, call `problems()` on your data frame for details, e.g.:
      dat <- vroom(...)
      problems(dat) 

    > cat("Структура сырых данных:\n")
    Структура сырых данных:
    > glimpse(raw_data)
    Rows: 12,250
    Columns: 15
    $ X1  <chr> "BSSID", "BE:F1:71:D5:17:8B", "6E:C7:EC:16:DA:1A", "9A:75:A8:B9:04:1E", "4A:EC…
    $ X2  <chr> "First time seen", "2023-07-28 09:13:03", "2023-07-28 09:13:03", "2023-07-28 0…
    $ X3  <chr> "Last time seen", "2023-07-28 11:50:50", "2023-07-28 11:55:12", "2023-07-28 11…
    $ X4  <chr> "channel", "1", "1", "1", "7", "6", "6", "11", "11", "11", "1", "6", "14", "11…
    $ X5  <chr> "Speed", "195", "130", "360", "360", "130", "130", "195", "130", "130", "195",…
    $ X6  <chr> "Privacy", "WPA2", "WPA2", "WPA2", "WPA2", "WPA2", "OPN", "WPA2", "WPA2", "WPA…
    $ X7  <chr> "Cipher", "CCMP", "CCMP", "CCMP", "CCMP", "CCMP", NA, "CCMP", "CCMP", "CCMP", …
    $ X8  <chr> "Authentication", "PSK", "PSK", "PSK", "PSK", "PSK", NA, "PSK", "PSK", "PSK", …
    $ X9  <chr> "Power", "-30", "-30", "-68", "-37", "-57", "-63", "-27", "-38", "-38", "-66",…
    $ X10 <chr> "# beacons", "846", "750", "694", "510", "647", "251", "1647", "1251", "704", …
    $ X11 <chr> "# IV", "504", "116", "26", "21", "6", "3430", "80", "11", "0", "0", "86", "0"…
    $ X12 <chr> "LAN IP", "0.  0.  0.  0", "0.  0.  0.  0", "0.  0.  0.  0", "0.  0.  0.  0", …
    $ X13 <chr> "ID-length", "12", "4", "2", "14", "25", "13", "12", "13", "24", "12", "10", "…
    $ X14 <chr> "ESSID", "C322U13 3965", "Cnet", "KC", "POCO X5 Pro 5G", NA, "MIREA_HOTSPOT", …
    $ X15 <chr> "Key", NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    > 
    > print(head(raw_data, 10))
    # A tibble: 10 × 15
       X1    X2    X3    X4    X5    X6    X7    X8    X9    X10   X11   X12   X13   X14   X15  
       <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr>
     1 BSSID Firs… Last… chan… Speed Priv… Ciph… Auth… Power # be… # IV  LAN … ID-l… ESSID Key  
     2 BE:F… 2023… 2023… 1     195   WPA2  CCMP  PSK   -30   846   504   0.  … 12    C322… NA   
     3 6E:C… 2023… 2023… 1     130   WPA2  CCMP  PSK   -30   750   116   0.  … 4     Cnet  NA   
     4 9A:7… 2023… 2023… 1     360   WPA2  CCMP  PSK   -68   694   26    0.  … 2     KC    NA   
     5 4A:E… 2023… 2023… 7     360   WPA2  CCMP  PSK   -37   510   21    0.  … 14    POCO… NA   
     6 D2:6… 2023… 2023… 6     130   WPA2  CCMP  PSK   -57   647   6     0.  … 25    NA    NA   
     7 E8:2… 2023… 2023… 6     130   OPN   NA    NA    -63   251   3430  172.… 13    MIRE… NA   
     8 BE:F… 2023… 2023… 11    195   WPA2  CCMP  PSK   -27   1647  80    0.  … 12    C322… NA   
     9 0A:C… 2023… 2023… 11    130   WPA2  CCMP  PSK   -38   1251  11    0.  … 13    Andr… NA   
    10 38:1… 2023… 2023… 11    130   WPA2  CCMP  PSK   -38   704   0     0.  … 24    EBFC… NA   
    > 
    > cat("\nРазмеры датасета:\n")

    Размеры датасета:
    > cat("Строк:", nrow(raw_data), "\n")
    Строк: 12250 
    > cat("Столбцов:", ncol(raw_data), "\n")
    Столбцов: 15 
    > 
    > ap_indices <- which(!is.na(raw_data$X1) &
    + str_detect(raw_data$X1, "^[0-9A-Fa-f]{2}:[0-9A-Fa-f]{2}:[0-9A-Fa-f]{2}"))
    > 
    > client_indices <- which(!is.na(raw_data$X2) &
    + str_detect(raw_data$X2, "^[0-9A-Fa-f]{2}:[0-9A-Fa-f]{2}:[0-9A-Fa-f]{2}"))
    > 
    > cat("Найдено записей точек доступа:", length(ap_indices), "\n")
    Найдено записей точек доступа: 12248 
    > cat("Найдено записей клиентов:", length(client_indices), "\n")
    Найдено записей клиентов: 0 
    > 
    > ap_data <- raw_data[ap_indices, 1:14] %>%
    + setNames(c("BSSID", "First_time_seen", "Last_time_seen", "channel","speed", "privacy", "cipher", "authentication", "power","beacons", "IV", "LAN_IP", "ID_length", "ESSID"))
    > 
    > client_data <- raw_data[client_indices, 1:6] %>%
    + setNames(c("Station_MAC", "First_time_seen", "Last_time_seen",
    + "power", "packets", "BSSID"))
    > 
    > ap_clean <- ap_data %>%
    + filter(!is.na(BSSID), BSSID != "") %>%
    + mutate(
    + channel = as.numeric(channel),
    + speed = as.numeric(speed),
    + power = as.numeric(power),
    + beacons = as.numeric(beacons),
    + IV = as.numeric(IV),
    + ID_length = as.numeric(ID_length),
    + First_time_seen = as.POSIXct(First_time_seen, format = "%Y-%m-%d %H:%M:%S"),
    + Last_time_seen = as.POSIXct(Last_time_seen, format = "%Y-%m-%d %H:%M:%S"),
    + ESSID = str_trim(ESSID)
    + ) %>%
    + distinct(BSSID, First_time_seen, .keep_all = TRUE)
    Предупреждение:
    There were 4 warnings in `mutate()`.
    The first warning was:
    ℹ In argument: `power = as.numeric(power)`.
    Caused by warning:
    ! в результате преобразования созданы NA
    ℹ Run warnings()dplyr::last_dplyr_warnings() to see the 3 remaining warnings. 

    > cat("Структура очищенных данных точек доступа:\n")
    Структура очищенных данных точек доступа:
    > glimpse(ap_clean)
    Rows: 12,248
    Columns: 14
    $ BSSID           <chr> "BE:F1:71:D5:17:8B", "6E:C7:EC:16:DA:1A", "9A:75:A8:B9:04:1E", "4A…
    $ First_time_seen <dttm> 2023-07-28 09:13:03, 2023-07-28 09:13:03, 2023-07-28 09:13:03, 20…
    $ Last_time_seen  <dttm> 2023-07-28 11:50:50, 2023-07-28 11:55:12, 2023-07-28 11:53:31, 20…
    $ channel         <dbl> 1, 1, 1, 7, 6, 6, 11, 11, 11, 1, 6, 14, 11, 11, 6, 6, 6, 6, 44, 1,…
    $ speed           <dbl> 195, 130, 360, 360, 130, 130, 195, 130, 130, 195, 180, 65, 130, 13…
    $ privacy         <chr> "WPA2", "WPA2", "WPA2", "WPA2", "WPA2", "OPN", "WPA2", "WPA2", "WP…
    $ cipher          <chr> "CCMP", "CCMP", "CCMP", "CCMP", "CCMP", NA, "CCMP", "CCMP", "CCMP"…
    $ authentication  <chr> "PSK", "PSK", "PSK", "PSK", "PSK", NA, "PSK", "PSK", "PSK", "PSK",…
    $ power           <dbl> -30, -30, -68, -37, -57, -63, -27, -38, -38, -66, -42, -62, -73, -…
    $ beacons         <dbl> 846, 750, 694, 510, 647, 251, 1647, 1251, 704, 617, 1390, 142, 28,…
    $ IV              <dbl> 504, 116, 26, 21, 6, 3430, 80, 11, 0, 0, 86, 0, 0, 0, 907, 0, 806,…
    $ LAN_IP          <chr> "0.  0.  0.  0", "0.  0.  0.  0", "0.  0.  0.  0", "0.  0.  0.  0"…
    $ ID_length       <dbl> 12, 4, 2, 14, 25, 13, 12, 13, 24, 12, 10, 0, 24, 24, 12, 0, 8, 0, …
    $ ESSID           <chr> "C322U13 3965", "Cnet", "KC", "POCO X5 Pro 5G", NA, "MIREA_HOTSPOT…
    > 
    > cat("\nСтатистика по числовым полям:\n")

    Статистика по числовым полям:
    > summary(ap_clean %>% select(channel, speed, power, beacons))
        channel           speed              power           beacons       
     Min.   :-89.00   Min.   :  -1.000   Min.   :-89.00   Min.   :   0.00  
     1st Qu.:-63.00   1st Qu.:   1.000   1st Qu.:-71.00   1st Qu.:   0.00  
     Median :-57.00   Median :   1.000   Median :-64.00   Median :   1.00  
     Mean   :-55.22   Mean   :   8.533   Mean   :-47.22   Mean   :  82.25  
     3rd Qu.:-51.00   3rd Qu.:   2.000   3rd Qu.: -1.00   3rd Qu.:  22.50  
     Max.   : 64.00   Max.   :8171.000   Max.   :  1.00   Max.   :1647.00  
                                         NA's   :12074    NA's   :12081    
    > 
    > 
    > client_clean <- client_data %>%
    + filter(!is.na(Station_MAC), Station_MAC != "") %>%
    + mutate(
    + power = as.numeric(power),
    + packets = as.numeric(packets),
    + First_time_seen = as.POSIXct(First_time_seen, format = "%Y-%m-%d %H:%M:%S"),
    + Last_time_seen = as.POSIXct(Last_time_seen, format = "%Y-%m-%d %H:%M:%S")
    + ) %>%
    + 
    + distinct(Station_MAC, First_time_seen, .keep_all = TRUE)
    > cat("Структура очищенных данных клиентов:\n")
    Структура очищенных данных клиентов:
    > glimpse(client_clean)
    Rows: 0
    Columns: 6
    $ Station_MAC     <chr> 
    $ First_time_seen <dttm> 
    $ Last_time_seen  <dttm> 
    $ power           <dbl> 
    $ packets         <dbl> 
    $ BSSID           <chr> 
    > 
    > cat("\nСтатистика по клиентам:\n")

    Статистика по клиентам:
    > summary(client_clean %>% select(power, packets))
         power        packets   
     Min.   : NA   Min.   : NA  
     1st Qu.: NA   1st Qu.: NA  
     Median : NA   Median : NA  
     Mean   :NaN   Mean   :NaN  
     3rd Qu.: NA   3rd Qu.: NA  
     Max.   : NA   Max.   : NA  
    > 
    > 
    > #Задание №1. Определить небезопасные точки доступа (без шифрования – OPN)
    > insecure_ap <- ap_clean %>%
    + filter(privacy == "OPN") %>%
    + select(BSSID, ESSID, privacy, cipher, authentication, power)
    > cat("НЕБЕЗОПАСНЫЕ ТОЧКИ ДОСТУПА (БЕЗ ШИФРОВАНИЯ):\n")
    НЕБЕЗОПАСНЫЕ ТОЧКИ ДОСТУПА (БЕЗ ШИФРОВАНИЯ):
    > cat("==========================================\n")
    ==========================================
    > print(insecure_ap)
    # A tibble: 42 × 6
       BSSID             ESSID         privacy cipher authentication power
       <chr>             <chr>         <chr>   <chr>  <chr>          <dbl>
     1 E8:28:C1:DC:B2:52 MIREA_HOTSPOT OPN     NA     NA               -63
     2 E8:28:C1:DC:B2:50 MIREA_GUESTS  OPN     NA     NA               -63
     3 E8:28:C1:DC:B2:51 NA            OPN     NA     NA               -63
     4 E8:28:C1:DC:FF:F2 NA            OPN     NA     NA                -1
     5 00:25:00:FF:94:73 NA            OPN     NA     NA                -1
     6 E8:28:C1:DD:04:52 MIREA_HOTSPOT OPN     NA     NA               -67
     7 E8:28:C1:DE:74:31 NA            OPN     NA     NA               -82
     8 E8:28:C1:DE:74:32 MIREA_HOTSPOT OPN     NA     NA               -69
     9 E8:28:C1:DC:C8:32 MIREA_HOTSPOT OPN     NA     NA               -69
    10 E8:28:C1:DD:04:50 MIREA_GUESTS  OPN     NA     NA               -78
    # ℹ 32 more rows
    # ℹ Use `print(n = ...)` to see more rows
    > 
    > cat("Всего небезопасных точек доступа:", nrow(insecure_ap), "\n\n")
    Всего небезопасных точек доступа: 42 

    > security_summary <- ap_clean %>%
    + count(privacy, name = "count") %>%
    + arrange(desc(count))
    > 
    > cat("РАСПРЕДЕЛЕНИЕ ТИПОВ БЕЗОПАСНОСТИ:\n")
    РАСПРЕДЕЛЕНИЕ ТИПОВ БЕЗОПАСНОСТИ:
    > print(security_summary)
    # A tibble: 80 × 2
       privacy           count
       <chr>             <int>
     1 (not associated)  11895
     2 WPA2                 72
     3 00:25:00:FF:94:73    45
     4 NA                   43
     5 OPN                  42
     6 E8:28:C1:DC:B2:52    12
     7 00:26:99:BA:75:80     9
     8 00:26:99:F2:7A:E2     8
     9 E8:28:C1:DC:C6:B2     8
    10 WPA3 WPA2             8
    # ℹ 70 more rows
    # ℹ Use `print(n = ...)` to see more rows
    > 
    > 
    > #Задание №2. Определить производителя для каждого обнаруженного устройства
    > get_oui <- function(mac) {
    + if (is.na(mac)) return(NA)
    + oui <- str_sub(mac, 1, 8)
    + return(oui)
    + }
    > 
    > ap_with_oui <- ap_clean %>%
    + mutate(OUI = map_chr(BSSID, get_oui))
    > client_with_oui <- client_clean %>%
    + mutate(OUI = map_chr(Station_MAC, get_oui))
    > top_manufacturers_ap <- ap_with_oui %>%
    + count(OUI, name = "count") %>%
    + arrange(desc(count)) %>%
    + head(10)
    > cat("ТОП-10 ПРОИЗВОДИТЕЛЕЙ ТОЧЕК ДОСТУПА:\n")
    ТОП-10 ПРОИЗВОДИТЕЛЕЙ ТОЧЕК ДОСТУПА:
    > print(top_manufacturers_ap)
    # A tibble: 10 × 2
       OUI      count
       <chr>    <int>
     1 BC:F1:71    52
     2 E8:28:C1    45
     3 0E:EF:92    36
     4 DA:A1:19    33
     5 FE:41:FA    32
     6 10:51:07    25
     7 5A:AB:CF    18
     8 A4:02:B9    17
     9 38:1A:52    10
    10 E2:CC:F8    10
    > 
    > top_manufacturers_client <- client_with_oui %>%
    + count(OUI, name = "count") %>%
    + arrange(desc(count)) %>%
    + head(10)
    > cat("\nТОП-10 ПРОИЗВОДИТЕЛЕЙ КЛИЕНТСКИХ УСТРОЙСТВ:\n")

    ТОП-10 ПРОИЗВОДИТЕЛЕЙ КЛИЕНТСКИХ УСТРОЙСТВ:
    > print(top_manufacturers_client)
    # A tibble: 0 × 2
    # ℹ 2 variables: OUI <chr>, count <int>
    > 
    > #Задание №3. Выявить устройства, использующие последнюю версию протокола шифрования WPA3, и названия точек доступа, реализованных на этих устройствах
    > 
    > wpa3_ap <- ap_clean %>%
    + filter(str_detect(privacy, "WPA3") | 
    + str_detect(authentication, "WPA3") |
    + str_detect(cipher, "WPA3"))
    > cat("ТОЧКИ ДОСТУПА С WPA3:\n")
    ТОЧКИ ДОСТУПА С WPA3:
    > if (nrow(wpa3_ap) > 0) {
    + print(wpa3_ap %>% select(BSSID, ESSID, privacy, authentication, cipher))
    + cat("Всего точек доступа с WPA3:", nrow(wpa3_ap), "\n")
    + } else {
    + cat("Точек доступа с WPA3 не обнаружено\n")
    + }
    # A tibble: 8 × 5
      BSSID             ESSID                                      privacy authentication cipher
      <chr>             <chr>                                      <chr>   <chr>          <chr> 
    1 26:20:53:0C:98:E8  NA                                        WPA3 W… SAE PSK        CCMP  
    2 A2:FE:FF:B8:9B:C9 "Christie’s"                               WPA3 W… SAE PSK        CCMP  
    3 96:FF:FC:91:EF:64  NA                                        WPA3 W… SAE PSK        CCMP  
    4 CE:48:E7:86:4E:33 "iPhone (Анастасия)"                       WPA3 W… SAE PSK        CCMP  
    5 8E:1F:94:96:DA:FD "iPhone (Анастасия)"                       WPA3 W… SAE PSK        CCMP  
    6 BE:FD:EF:18:92:44 "Димасик"                                  WPA3 W… SAE PSK        CCMP  
    7 3A:DA:00:F9:0C:02 "iPhone XS Max \U0001f98a\U0001f431\U0001… WPA3 W… SAE PSK        CCMP  
    8 76:C5:A0:70:08:96  NA                                        WPA3 W… SAE PSK        CCMP  
    Всего точек доступа с WPA3: 8 
    > 
    > 
    > #Задание №4. Отсортировать точки доступа по интервалу времени, в течение которого они находились на связи, по убыванию.
    > 
    > merge_sessions <- function(data) {
    + data %>%
    + arrange(BSSID, First_time_seen) %>%
    + group_by(BSSID) %>%
    + mutate(
    + time_gap = as.numeric(difftime(First_time_seen,
    + lag(Last_time_seen, default = first(First_time_seen)),
    + units = "mins")),
    + session_id = cumsum(time_gap > 45 | row_number() == 1)
    + ) %>%
    + group_by(BSSID, session_id) %>%
    + summarise(
    + session_start = min(First_time_seen),
    + session_end = max(Last_time_seen),
    + total_duration = as.numeric(difftime(max(Last_time_seen),
    + min(First_time_seen),
    + units = "mins")),
    + avg_power = mean(power, na.rm = TRUE),
    + total_beacons = sum(beacons, na.rm = TRUE),
    + .groups = "drop"
    + )
    + }
    > 
    > ap_sessions <- merge_sessions(ap_clean)
    > longest_sessions <- ap_sessions %>%
    + arrange(desc(total_duration)) %>%
    + head(20)
    > 
    > cat("ТОП-20 САМЫХ ДОЛГИХ СЕССИЙ ТОЧЕК ДОСТУПА:\n")
    ТОП-20 САМЫХ ДОЛГИХ СЕССИЙ ТОЧЕК ДОСТУПА:
    > print(longest_sessions)
    # A tibble: 20 × 7
       BSSID         session_id session_start       session_end         total_duration avg_power
       <chr>              <int> <dttm>              <dttm>                       <dbl>     <dbl>
     1 00:25:00:FF:…          1 2023-07-28 09:13:06 2023-07-28 11:56:21           163.        -1
     2 10:51:07:CB:…          1 2023-07-28 09:13:13 2023-07-28 11:56:17           163.       NaN
     3 00:95:69:E7:…          1 2023-07-28 09:13:11 2023-07-28 11:56:13           163.       NaN
     4 00:95:69:E7:…          1 2023-07-28 09:13:15 2023-07-28 11:56:17           163.       NaN
     5 10:51:07:CB:…          1 2023-07-28 09:13:05 2023-07-28 11:56:06           163.       NaN
     6 8C:55:4A:DE:…          1 2023-07-28 09:13:17 2023-07-28 11:56:16           163.       NaN
     7 00:95:69:E7:…          1 2023-07-28 09:13:11 2023-07-28 11:56:07           163.       NaN
     8 E8:28:C1:DD:…          1 2023-07-28 09:13:09 2023-07-28 11:56:05           163.       -67
     9 9E:A3:A9:D6:…          1 2023-07-28 09:13:15 2023-07-28 11:55:53           163.       -61
    10 E8:28:C1:DC:…          1 2023-07-28 09:13:03 2023-07-28 11:55:38           163.       -63
    11 BC:F1:71:D5:…          1 2023-07-28 09:13:24 2023-07-28 11:55:58           163.       NaN
    12 08:3A:2F:56:…          1 2023-07-28 09:13:27 2023-07-28 11:55:53           162.        -1
    13 10:51:07:FE:…          1 2023-07-28 09:13:27 2023-07-28 11:55:53           162.       NaN
    14 BC:F1:71:D5:…          1 2023-07-28 09:13:38 2023-07-28 11:56:02           162.       NaN
    15 70:66:55:D0:…          1 2023-07-28 09:14:09 2023-07-28 11:56:21           162.       NaN
    16 BC:F1:71:D5:…          1 2023-07-28 09:13:41 2023-07-28 11:55:53           162.       NaN
    17 6E:C7:EC:16:…          1 2023-07-28 09:13:03 2023-07-28 11:55:12           162.       -30
    18 10:51:07:FE:…          1 2023-07-28 09:13:41 2023-07-28 11:55:47           162.       NaN
    19 E8:28:C1:DC:…          1 2023-07-28 09:13:06 2023-07-28 11:55:12           162.       -63
    20 10:51:07:FF:…          1 2023-07-28 09:13:45 2023-07-28 11:55:50           162.       NaN
    # ℹ 1 more variable: total_beacons <dbl>
    > 
    > 
    > #Задание №5. Обнаружить топ-10 самых быстрых точек доступа.
    > 

## Оценка результата

В результате лабораторной работы мы получили знания о методах
исследования радиоэлектронной обстановки.

## Вывод

Таким образом, мы получили знания о методах исследования
радиоэлектронной обстановки.

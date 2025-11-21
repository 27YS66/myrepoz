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


    R version 4.5.1 (2025-06-13 ucrt) -- "Great Square Root"
    Copyright (C) 2025 The R Foundation for Statistical Computing
    Platform: x86_64-w64-mingw32/x64

    R -- это свободное ПО, и оно поставляется безо всяких гарантий.
    Вы вольны распространять его при соблюдении некоторых условий.
    Введите 'license()' для получения более подробной информации.

    R -- это проект, в котором сотрудничает множество разработчиков.
    Введите 'contributors()' для получения дополнительной информации и
    'citation()' для ознакомления с правилами упоминания R и его пакетов
    в публикациях.

    Введите 'demo()' для запуска демонстрационных программ, 'help()' -- для
    получения справки, 'help.start()' -- для доступа к справке через браузер.
    Введите 'q()', чтобы выйти из R.

    [Workspace loaded from ~/myrepoz/.RData]

    > install.packages("tidyverse")
    WARNING: Rtools is required to build R packages but is not currently installed. Please download and install the appropriate version of Rtools before proceeding:

    https://cran.rstudio.com/bin/windows/Rtools/
    Устанавливаю пакет в ‘C:/Users/София/AppData/Local/R/win-library/4.5’
    (потому что ‘lib’ не определено)
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/tidyverse_2.0.0.zip'
    Content type 'application/zip' length 431578 bytes (421 KB)
    downloaded 421 KB

    пакет ‘tidyverse’ успешно распакован, MD5-суммы проверены

    Скачанные бинарные пакеты находятся в
        C:\Users\София\AppData\Local\Temp\RtmpETv6Mp\downloaded_packages
    > install.packages("lubridate")
    WARNING: Rtools is required to build R packages but is not currently installed. Please download and install the appropriate version of Rtools before proceeding:

    https://cran.rstudio.com/bin/windows/Rtools/
    Устанавливаю пакет в ‘C:/Users/София/AppData/Local/R/win-library/4.5’
    (потому что ‘lib’ не определено)
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/lubridate_1.9.4.zip'
    Content type 'application/zip' length 995686 bytes (972 KB)
    downloaded 972 KB

    пакет ‘lubridate’ успешно распакован, MD5-суммы проверены

    Скачанные бинарные пакеты находятся в
        C:\Users\София\AppData\Local\Temp\RtmpETv6Mp\downloaded_packages
    > install.packages("readr")
    WARNING: Rtools is required to build R packages but is not currently installed. Please download and install the appropriate version of Rtools before proceeding:

    https://cran.rstudio.com/bin/windows/Rtools/
    Устанавливаю пакет в ‘C:/Users/София/AppData/Local/R/win-library/4.5’
    (потому что ‘lib’ не определено)
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/readr_2.1.6.zip'
    Content type 'application/zip' length 1237991 bytes (1.2 MB)
    downloaded 1.2 MB

    пакет ‘readr’ успешно распакован, MD5-суммы проверены

    Скачанные бинарные пакеты находятся в
        C:\Users\София\AppData\Local\Temp\RtmpETv6Mp\downloaded_packages
    > install.packages("dplyr")
    WARNING: Rtools is required to build R packages but is not currently installed. Please download and install the appropriate version of Rtools before proceeding:

    https://cran.rstudio.com/bin/windows/Rtools/
    Устанавливаю пакет в ‘C:/Users/София/AppData/Local/R/win-library/4.5’
    (потому что ‘lib’ не определено)
    пробую URL 'https://mirror.truenetwork.ru/CRAN/bin/windows/contrib/4.5/dplyr_1.1.4.zip'
    Content type 'application/zip' length 1593482 bytes (1.5 MB)
    downloaded 1.5 MB

    пакет ‘dplyr’ успешно распакован, MD5-суммы проверены

    Скачанные бинарные пакеты находятся в
        C:\Users\София\AppData\Local\Temp\RtmpETv6Mp\downloaded_packages
    > library(tidyverse)
    ── Attaching core tidyverse packages ──────────────────────────────────── tidyverse 2.0.0 ──
    ✔ dplyr     1.1.4     ✔ readr     2.1.6
    ✔ forcats   1.0.1     ✔ stringr   1.5.2
    ✔ ggplot2   4.0.0     ✔ tibble    3.3.0
    ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ✔ purrr     1.1.0     
    ── Conflicts ────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ✖ dplyr::filter() masks stats::filter()
    ✖ dplyr::lag()    masks stats::lag()
    ℹ Use the conflicted package to force all conflicts to become errors
    Предупреждения:
    1: пакет ‘tidyverse’ был собран под R версии 4.5.2 
    2: пакет ‘readr’ был собран под R версии 4.5.2 
    3: пакет ‘dplyr’ был собран под R версии 4.5.2 
    4: пакет ‘lubridate’ был собран под R версии 4.5.2 
    > library(lubridate)
    > library(readr)
    > library(dplyr)
    > library(ggplot2)
    > raw_lines <- read_lines("https://storage.yandexcloud.net/dataset.ctfsec/P2_wifi_data.csv")
    > client_start_line <- which(str_detect(raw_lines, "Station MAC"))[1]
    > ap_data <- read_csv("https://storage.yandexcloud.net/dataset.ctfsec/P2_wifi_data.csv",
    + n_max = client_start_line - 3,
    + col_names = TRUE,
    + col_types = cols(
    + BSSID = col_character(),
    + `First time seen` = col_character(),
    + `Last time seen` = col_character(),
    + `channel` = col_integer(),
    + `Speed` = col_character(),
    + `Privacy` = col_character(),
    + `Cipher` = col_character(),
    + `Authentication` = col_character(),
    + `Power` = col_integer(),
    + `# beacons` = col_integer(),
    + `# IV` = col_integer(),
    + `LAN IP` = col_character(),
    + `ID-length` = col_integer(),
    + `ESSID` = col_character()
    + ))
    Предупреждение:
    One or more parsing issues, call `problems()` on your data frame for details, e.g.:
      dat <- vroom(...)
      problems(dat) 

    > 
    > client_data <- read_csv("https://storage.yandexcloud.net/dataset.ctfsec/P2_wifi_data.csv",
    + skip = client_start_line - 1,
    + col_names = TRUE,
    + col_types = cols(
    + `Station MAC` = col_character(),
    + `First time seen` = col_character(),
    + `Last time seen` = col_character(),
    + `Power` = col_integer(),
    + `# packets` = col_integer(),
    + `BSSID` = col_character(),
    + `Probed ESSIDs` = col_character()
    + ))
    Предупреждение:
    One or more parsing issues, call `problems()` on your data frame for details, e.g.:
      dat <- vroom(...)
      problems(dat) 

    > glimpse(ap_data)
    Rows: 168
    Columns: 15
    $ BSSID             <chr> "BE:F1:71:D5:17:8B", "6E:C7:EC:16:DA:1A", "9A:75:A8:B9:04:1E", "…
    $ `First time seen` <chr> "2023-07-28 09:13:03", "2023-07-28 09:13:03", "2023-07-28 09:13:…
    $ `Last time seen`  <chr> "2023-07-28 11:50:50", "2023-07-28 11:55:12", "2023-07-28 11:53:…
    $ channel           <int> 1, 1, 1, 7, 6, 6, 11, 11, 11, 1, 6, 14, 11, 11, 6, 6, 6, 6, 44, …
    $ Speed             <chr> "195", "130", "360", "360", "130", "130", "195", "130", "130", "…
    $ Privacy           <chr> "WPA2", "WPA2", "WPA2", "WPA2", "WPA2", "OPN", "WPA2", "WPA2", "…
    $ Cipher            <chr> "CCMP", "CCMP", "CCMP", "CCMP", "CCMP", NA, "CCMP", "CCMP", "CCM…
    $ Authentication    <chr> "PSK", "PSK", "PSK", "PSK", "PSK", NA, "PSK", "PSK", "PSK", "PSK…
    $ Power             <int> -30, -30, -68, -37, -57, -63, -27, -38, -38, -66, -42, -62, -73,…
    $ `# beacons`       <int> 846, 750, 694, 510, 647, 251, 1647, 1251, 704, 617, 1390, 142, 2…
    $ `# IV`            <int> 504, 116, 26, 21, 6, 3430, 80, 11, 0, 0, 86, 0, 0, 0, 907, 0, 80…
    $ `LAN IP`          <chr> "0.  0.  0.  0", "0.  0.  0.  0", "0.  0.  0.  0", "0.  0.  0.  …
    $ `ID-length`       <int> 12, 4, 2, 14, 25, 13, 12, 13, 24, 12, 10, 0, 24, 24, 12, 0, 8, 0…
    $ ESSID             <chr> "C322U13 3965", "Cnet", "KC", "POCO X5 Pro 5G", NA, "MIREA_HOTSP…
    $ Key               <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
    > glimpse(client_data)
    Rows: 12,081
    Columns: 7
    $ `Station MAC`     <chr> "CA:66:3B:8F:56:DD", "96:35:2D:3D:85:E6", "5C:3A:45:9E:1A:7B", "…
    $ `First time seen` <chr> "2023-07-28 09:13:03", "2023-07-28 09:13:03", "2023-07-28 09:13:…
    $ `Last time seen`  <chr> "2023-07-28 10:59:44", "2023-07-28 09:13:03", "2023-07-28 11:51:…
    $ Power             <int> -33, -65, -39, -61, -53, -43, -31, -71, -74, -65, -45, -65, -49,…
    $ `# packets`       <int> 858, 4, 432, 958, 1, 344, 163, 3, 115, 437, 265, 77, 7, 71, 1, 1…
    $ BSSID             <chr> "BE:F1:71:D5:17:8B", "(not associated)", "BE:F1:71:D6:10:D7", "B…
    $ `Probed ESSIDs`   <chr> "C322U13 3965", "IT2 Wireless", "C322U21 0566", "C322U13 3965", …
    > 
    > parse_airodump_time <- function(time_str) {
    + ymd_hms(time_str)
    + }
    > ap_clean <- ap_data %>%
    + filter(!is.na(BSSID)) %>%
    + mutate(
    + `First time seen` = parse_airodump_time(`First time seen`),
    + `Last time seen` = parse_airodump_time(`Last time seen`),
    + Speed_num = as.numeric(str_extract(Speed, "\\d+")),
    + session_id = paste0(BSSID, "_", floor_date(`First time seen`, "45 minutes"))
    + ) %>%
    + group_by(session_id) %>%
    + mutate(
    + session_start = min(`First time seen`),
    + session_end = max(`Last time seen`),
    + session_duration = as.numeric(difftime(session_end, session_start, units = "mins"))
    + ) %>%
    + ungroup()
    Предупреждение:
    There were 2 warnings in `mutate()`.
    The first warning was:
    ℹ In argument: `First time seen = parse_airodump_time(`First time seen`)`.
    Caused by warning:
    !  1 failed to parse.
    ℹ Run warnings()dplyr::last_dplyr_warnings() to see the 1 remaining warning. 

    > client_clean <- client_data %>%
    + filter(!is.na(`Station MAC`)) %>%
    + mutate(
    + `First time seen` = parse_airodump_time(`First time seen`),
    + `Last time seen` = parse_airodump_time(`Last time seen`)
    + )
    > 
    > # 1. Определить небезопасные точки доступа (без шифрования – OPN)
    > insecure_ap <- ap_clean %>%
    + filter(Privacy == "OPN") %>%
    + select(BSSID, ESSID, `First time seen`, `Last time seen`, Power) %>%
    + arrange(desc(`Last time seen`))
    > print("Небезопасные точки доступа (OPN):")
    [1] "Небезопасные точки доступа (OPN):"
    > print(insecure_ap)
    # A tibble: 42 × 5
       BSSID             ESSID         `First time seen`   `Last time seen`    Power
       <chr>             <chr>         <dttm>              <dttm>              <int>
     1 00:25:00:FF:94:73 NA            2023-07-28 09:13:06 2023-07-28 11:56:21    -1
     2 E8:28:C1:DC:C6:B2 NA            2023-07-28 10:02:42 2023-07-28 11:56:21   -70
     3 E8:28:C1:DD:04:52 MIREA_HOTSPOT 2023-07-28 09:13:09 2023-07-28 11:56:05   -67
     4 E8:28:C1:DC:B2:52 MIREA_HOTSPOT 2023-07-28 09:13:03 2023-07-28 11:55:38   -63
     5 E8:28:C1:DC:B2:50 MIREA_GUESTS  2023-07-28 09:13:06 2023-07-28 11:55:12   -63
     6 E8:28:C1:DC:B2:51 NA            2023-07-28 09:13:06 2023-07-28 11:55:11   -63
     7 E8:28:C1:DE:47:D0 MIREA_GUESTS  2023-07-28 11:55:11 2023-07-28 11:55:11   -70
     8 E8:28:C1:DC:FF:F2 NA            2023-07-28 09:13:06 2023-07-28 11:55:10    -1
     9 E8:28:C1:DD:04:40 MIREA_HOTSPOT 2023-07-28 09:18:30 2023-07-28 11:55:10   -84
    10 E8:28:C1:DD:04:41 MIREA_GUESTS  2023-07-28 09:18:30 2023-07-28 11:55:10   -83
    # ℹ 32 more rows
    # ℹ Use `print(n = ...)` to see more rows
    > 
    > # 2. Определить производителя для каждого обнаруженного устройства
    > get_oui <- function(mac) {
    + str_split(mac, ":") %>% map_chr(~ paste(.x[1:3], collapse = ":"))
    + }
    > ap_with_oui <- ap_clean %>%
    + mutate(OUI = get_oui(BSSID))
    > manufacturer_db <- tribble(
    + ~OUI, ~Manufacturer,
    + "00:1A:2B", "Cisco",
    + "00:1B:44", "Apple",
    + "00:1C:B3", "TP-Link",
    + "00:1D:0F", "D-Link",
    + "00:1E:65", "Netgear",
    + "00:21:6A", "Intel",
    + "00:23:69", "Samsung",
    + "00:24:01", "ASUS",
    + "00:26:5A", "Huawei",
    + 00:50:56", "VMware"
    Ошибка: неожиданная строковая константа в:
    ""00:26:5A", "Huawei",
    00:50:56", ""

    > "00:50:56", "VMware"
    Ошибка: неожиданный ',' в ""00:50:56","

    > manufacturer_db <- tribble(
    +     + ~OUI, ~Manufacturer,
    +     + "00:1A:2B", "Cisco",
    +     + "00:1B:44", "Apple",
    +     + "00:1C:B3", "TP-Link",
    +     + "00:1D:0F", "D-Link",
    +     + "00:1E:65", "Netgear",
    +     + "00:21:6A", "Intel",
    +     + "00:23:69", "Samsung",
    +     + "00:24:01", "ASUS",
    +     + "00:26:5A", "Huawei",
    + "00:50:56", "VMware"
    + )
    Ошибка в +~OUI : неправильный аргумент для унарного оператора

    > manufacturer_db <- tribble(
    +     +     + ~OUI, ~Manufacturer,
    +     +     + "00:1A:2B", "Cisco",
    +     +     + "00:1B:44", "Apple",
    +     +     + "00:1C:B3", "TP-Link",
    +     +     + "00:1D:0F", "D-Link",
    +     +     + "00:1E:65", "Netgear",
    +     +     + "00:21:6A", "Intel",
    +     +     + "00:23:69", "Samsung",
    +     +     + "00:24:01", "ASUS",
    +     +     + "00:26:5A", "Huawei",
    +     + "00:50:56", "VMware" )
    Ошибка в +~OUI : неправильный аргумент для унарного оператора

    > 
    > 
    > manufacturer_db <- tribble(
    + ~OUI, ~Manufacturer,
    + "00:1A:2B", "Cisco",
    + "00:1B:44", "Apple",
    + "00:1C:B3", "TP-Link",
    + "00:1D:0F", "D-Link",
    + "00:1E:65", "Netgear",
    + "00:21:6A", "Intel",
    + "00:23:69", "Samsung",
    + "00:24:01", "ASUS",
    + "00:26:5A", "Huawei",
    + "00:50:56", "VMware"
    + )
    > ap_with_manufacturer <- ap_with_oui %>%
    + left_join(manufacturer_db, by = "OUI") %>%
    + mutate(Manufacturer = ifelse(is.na(Manufacturer), "Unknown", Manufacturer))
    > # 3. Выявить устройства, использующие последнюю версию протокола шифрования
    > WPA3, и названия точек доступа, реализованных на этих устройствах
    Ошибка: неожиданный ',' в "WPA3,"

    > wpa3_devices <- ap_with_manufacturer %>%
    + filter(str_detect(Authentication, "WPA3") |
    + str_detect(Privacy, "WPA3") |
    + str_detect(Cipher, "WPA3")) %>%
    + select(BSSID, ESSID, Manufacturer, Authentication, Privacy, Cipher)
    > print("Устройства с WPA3:")
    [1] "Устройства с WPA3:"
    > print(wpa3_devices)
    # A tibble: 8 × 6
      BSSID             ESSID                         Manufacturer Authentication Privacy Cipher
      <chr>             <chr>                         <chr>        <chr>          <chr>   <chr> 
    1 26:20:53:0C:98:E8  NA                           Unknown      SAE PSK        WPA3 W… CCMP  
    2 A2:FE:FF:B8:9B:C9 "Christie’s"                  Unknown      SAE PSK        WPA3 W… CCMP  
    3 96:FF:FC:91:EF:64  NA                           Unknown      SAE PSK        WPA3 W… CCMP  
    4 CE:48:E7:86:4E:33 "iPhone (Анастасия)"          Unknown      SAE PSK        WPA3 W… CCMP  
    5 8E:1F:94:96:DA:FD "iPhone (Анастасия)"          Unknown      SAE PSK        WPA3 W… CCMP  
    6 BE:FD:EF:18:92:44 "Димасик"                     Unknown      SAE PSK        WPA3 W… CCMP  
    7 3A:DA:00:F9:0C:02 "iPhone XS Max \U0001f98a\U0… Unknown      SAE PSK        WPA3 W… CCMP  
    8 76:C5:A0:70:08:96  NA                           Unknown      SAE PSK        WPA3 W… CCMP  
    > 
    > # 4. Отсортировать точки доступа по интервалу времени, в течение которого они находились на связи, по убыванию.
    > ap_by_uptime <- ap_with_manufacturer %>%
    + group_by(BSSID, ESSID) %>%
    + summarise(
    + total_uptime = as.numeric(difftime(max(`Last time seen`), 
    + min(`First time seen`), 
    + units = "hours")),
    + first_seen = min(`First time seen`),
    + last_seen = max(`Last time seen`),
    + .groups = "drop"
    + ) %>%
    + arrange(desc(total_uptime))
    > print("Точки доступа по времени на связи:")
    [1] "Точки доступа по времени на связи:"
    > print(head(ap_by_uptime, 10))
    # A tibble: 10 × 5
       BSSID             ESSID         total_uptime first_seen          last_seen          
       <chr>             <chr>                <dbl> <dttm>              <dttm>             
     1 00:25:00:FF:94:73 NA                    2.72 2023-07-28 09:13:06 2023-07-28 11:56:21
     2 E8:28:C1:DD:04:52 MIREA_HOTSPOT         2.72 2023-07-28 09:13:09 2023-07-28 11:56:05
     3 E8:28:C1:DC:B2:52 MIREA_HOTSPOT         2.71 2023-07-28 09:13:03 2023-07-28 11:55:38
     4 08:3A:2F:56:35:FE NA                    2.71 2023-07-28 09:13:27 2023-07-28 11:55:53
     5 6E:C7:EC:16:DA:1A Cnet                  2.70 2023-07-28 09:13:03 2023-07-28 11:55:12
     6 E8:28:C1:DC:B2:50 MIREA_GUESTS          2.70 2023-07-28 09:13:06 2023-07-28 11:55:12
     7 48:5B:39:F9:7A:48 NA                    2.70 2023-07-28 09:13:06 2023-07-28 11:55:11
     8 E8:28:C1:DC:B2:51 NA                    2.70 2023-07-28 09:13:06 2023-07-28 11:55:11
     9 E8:28:C1:DC:FF:F2 NA                    2.70 2023-07-28 09:13:06 2023-07-28 11:55:10
    10 8E:55:4A:85:5B:01 Vladimir              2.70 2023-07-28 09:13:06 2023-07-28 11:55:09
    > # 5. Обнаружить топ-10 самых быстрых точек доступа
    > fastest_ap <- ap_with_manufacturer %>%
    + group_by(BSSID, ESSID) %>%
    + summarise(
    + max_speed = max(Speed_num, na.rm = TRUE),
    + avg_power = mean(Power, na.rm = TRUE),
    + .groups = "drop"
    + ) %>%
    + arrange(desc(max_speed)) %>%
    + head(10)
    Предупреждение:
    There was 1 warning in `summarise()`.
    ℹ In argument: `max_speed = max(Speed_num, na.rm = TRUE)`.
    ℹ In group 168: `BSSID = "Station MAC"` `ESSID = NA`.
    Caused by warning in `max()`:
    ! у 'max' нет не пропущенных аргументов; возвращаю -Inf 

    > print("Топ-10 самых быстрых точек доступа:")
    [1] "Топ-10 самых быстрых точек доступа:"
    > print(fastest_ap)
    # A tibble: 10 × 4
       BSSID             ESSID              max_speed avg_power
       <chr>             <chr>                  <dbl>     <dbl>
     1 26:20:53:0C:98:E8 NA                       866       -85
     2 8E:1F:94:96:DA:FD iPhone (Анастасия)       866       -67
     3 96:FF:FC:91:EF:64 NA                       866       -85
     4 CE:48:E7:86:4E:33 iPhone (Анастасия)       866       -65
     5 02:B3:45:5A:05:93 HONOR 30                 360       -75
     6 14:EB:B6:6A:76:37 Gnezdo_lounge 2          360       -85
     7 4A:EC:1E:DB:BF:95 POCO X5 Pro 5G           360       -37
     8 56:C5:2B:9F:84:90 OnePlus 6T               360       -64
     9 9A:75:A8:B9:04:1E KC                       360       -68
    10 E8:28:C1:DC:B2:40 MIREA_HOTSPOT            360       -88
    > 
    > # 6. Отсортировать точки доступа по частоте отправки запросов (beacons) в единицу времени по их убыванию.
    > ap_beacon_rate <- ap_with_manufacturer %>%
    + mutate(
    + time_diff = as.numeric(difftime(`Last time seen`, `First time seen`, units = "secs")),
    + beacon_rate = `# beacons` / time_diff
    + ) %>%
    + filter(time_diff > 0) %>%
    + select(BSSID, ESSID,
    + arrange(desc(beacon_rate))
    + print("Точки доступа по частоте beacon'ов:")
    Ошибка: неожиданный символ в:
    "arrange(desc(beacon_rate))
    print"

    > print(head(ap_beacon_rate, 10))
    Ошибка: объект 'ap_beacon_rate' не найден

    > ap_beacon_rate <- ap_with_manufacturer %>%
    + mutate(
    + time_diff = as.numeric(difftime(`Last time seen`, `First time seen`, units = "secs")),
    + beacon_rate = `# beacons` / time_diff
    + ) %>%
    + filter(time_diff > 0) %>%
    + select(BSSID, ESSID,
    + arrange(desc(beacon_rate))
    + print("Точки доступа по частоте beacon'ов:")
    Ошибка: неожиданный символ в:
    "arrange(desc(beacon_rate))
    print"

    > print(head(ap_beacon_rate, 10))
    Ошибка: объект 'ap_beacon_rate' не найден

    > ap_beacon_rate <- ap_with_manufacturer %>%
    + mutate(
    + time_diff = as.numeric(difftime(`Last time seen`, `First time seen`, units = "secs")),
    + beacon_rate = `# beacons` / time_diff
    + ) %>%
    + filter(time_diff > 0) %>% 
    + select(BSSID, ESSID,
    + arrange(desc(beacon_rate))
    + print("Точки доступа по частоте beacon'ов:")
    Ошибка: неожиданный символ в:
    "arrange(desc(beacon_rate))
    print"

    > print(head(ap_beacon_rate, 10))
    Ошибка: объект 'ap_beacon_rate' не найден

    > ap_beacon_rate <- ap_with_manufacturer %>%
    + mutate(
    + time_diff = as.numeric(difftime(`Last time seen`, `First time seen`, units = "secs")),
    + beacon_rate = `# beacons` / time_diff
    + ) %>%
    + filter(time_diff > 0) %>%
    + select(BSSID, ESSID, `# beacons`, time_diff, beacon_rate) %>%
    + arrange(desc(beacon_rate))
    > print("Точки доступа по частоте beacon'ов:")
    [1] "Точки доступа по частоте beacon'ов:"
    > print(head(ap_beacon_rate, 10))
    # A tibble: 10 × 5
       BSSID             ESSID                                 `# beacons` time_diff beacon_rate
       <chr>             <chr>                                       <int>     <dbl>       <dbl>
     1 F2:30:AB:E9:03:ED "iPhone (Uliana)"                               6         7       0.857
     2 B2:CF:C0:00:4A:60 "Михаил's Galaxy M32"                           4         5       0.8  
     3 3A:DA:00:F9:0C:02 "iPhone XS Max \U0001f98a\U0001f431\…           5         9       0.556
     4 02:BC:15:7E:D5:DC "MT_FREE"                                       1         2       0.5  
     5 00:3E:1A:5D:14:45 "MT_FREE"                                       1         2       0.5  
     6 76:C5:A0:70:08:96  NA                                             1         2       0.5  
     7 D2:25:91:F6:6C:D8 "Саня"                                          5        13       0.385
     8 BE:F1:71:D6:10:D7 "C322U21 0566"                               1647      9461       0.174
     9 00:03:7A:1A:03:56 "MT_FREE"                                       1         6       0.167
    10 38:1A:52:0D:84:D7 "EBFCD57F-EE81fI_DL_1AO2T"                    704      4319       0.163
    > 
    > # Данные клиентов
    > # 1. Определить производителя для каждого обнаруженного устройства
    > client_with_oui <- client_clean %>%
    + mutate(OUI = get_oui(`Station MAC`)) %>%
    + left_join(manufacturer_db, by = "OUI") %>%
    + mutate(Manufacturer = ifelse(is.na(Manufacturer), "Unknown", Manufacturer))
    > client_manufacturer_stats <- client_with_oui %>%
    + group_by(Manufacturer) %>%
    + summarise(
    + device_count = n_distinct(`Station MAC`),
    + total_packets = sum(`# packets`, na.rm = TRUE),
    + .groups = "drop"
    + ) %>%
    + arrange(desc(device_count))
    > print("Статистика по производителям клиентов:")
    [1] "Статистика по производителям клиентов:"
    > print(client_manufacturer_stats)
    # A tibble: 1 × 3
      Manufacturer device_count total_packets
      <chr>               <int>         <int>
    1 Unknown             12081         84569
    > 
    > # 2. Обнаружить устройства, которые НЕ рандомизируют свой MAC адрес
    > non_randomized_clients <- client_with_oui %>%
    + group_by(`Station MAC`, Manufacturer) %>%
    + summarise(
    + observation_count = n(),
    + unique_networks = n_distinct(`Probed ESSIDs`),
    + total_packets = sum(`# packets`, na.rm = TRUE),
    + first_seen = min(`First time seen`),
    + last_seen = max(`Last time seen`),
    + .groups = "drop"
    + ) %>%
    + filter(observation_count > 5) %>%  
    + arrange(desc(observation_count))
    > print("Устройства без рандомизации MAC:")
    [1] "Устройства без рандомизации MAC:"
    > print(head(non_randomized_clients, 15))
    # A tibble: 0 × 7
    # ℹ 7 variables: Station MAC <chr>, Manufacturer <chr>, observation_count <int>,
    #   unique_networks <int>, total_packets <int>, first_seen <dttm>, last_seen <dttm>
    > 
    > # 3. Кластеризовать запросы от устройств к точкам доступа по их именам Определить время появления устройства в зоне радиовидимости и время выхода его из нее
    > client_clusters <- client_with_oui %>%
    + filter(!is.na(`Probed ESSIDs`) & `Probed ESSIDs` != "") %>%
    + group_by(`Station MAC`, `Probed ESSIDs`) %>%
    + summarise(
    + cluster_first_seen = min(`First time seen`),
    + cluster_last_seen = max(`Last time seen`),
    + cluster_duration = as.numeric(difftime(max(`Last time seen`), 
    + min(`First time seen`),
    + units = "mins")),
    + avg_power = mean(Power, na.rm = TRUE),
    + power_sd = sd(Power, na.rm = TRUE),
    + packet_count = sum(`# packets`, na.rm = TRUE),
    + .groups = "drop"
    + ) %>%
    + mutate(
    + power_stability = ifelse(is.na(power_sd) | power_sd == 0, 100,
    + (1 - (power_sd / abs(avg_power))) * 100)
    + )
    > print("Кластеры запросов клиентов:")
    [1] "Кластеры запросов клиентов:"
    > print(head(client_clusters, 10))
    # A tibble: 10 × 9
       `Station MAC`    `Probed ESSIDs` cluster_first_seen  cluster_last_seen   cluster_duration
       <chr>            <chr>           <dttm>              <dttm>                         <dbl>
     1 00:90:4C:E6:54:… "Redmi"         2023-07-28 09:16:59 2023-07-28 10:21:15          64.3   
     2 00:95:69:E7:7C:… "nvripcsuite"   2023-07-28 09:13:11 2023-07-28 11:56:13         163.    
     3 00:95:69:E7:7D:… "nvripcsuite"   2023-07-28 09:13:15 2023-07-28 11:56:17         163.    
     4 00:95:69:E7:7F:… "nvripcsuite"   2023-07-28 09:13:11 2023-07-28 11:56:07         163.    
     5 00:F4:8D:F7:C5:… "Redmi 12,Horn… 2023-07-28 10:45:04 2023-07-28 11:43:26          58.4   
     6 02:00:00:00:00:… "xt3 w64dtgv5c… 2023-07-28 09:54:40 2023-07-28 11:55:36         121.    
     7 02:06:2B:A5:0C:… "Avenue611"     2023-07-28 09:55:12 2023-07-28 09:55:12           0     
     8 02:1D:0F:A4:94:… "iPhone (Дима … 2023-07-28 09:57:08 2023-07-28 09:57:08           0     
     9 02:32:DC:56:5C:… "Timo Resort,M… 2023-07-28 10:58:23 2023-07-28 10:58:24           0.0167
    10 02:35:E9:C2:44:… "iPhone (Макси… 2023-07-28 10:00:55 2023-07-28 10:00:55           0     
    # ℹ 4 more variables: avg_power <dbl>, power_sd <dbl>, packet_count <int>,
    #   power_stability <dbl>
    > 
    > # 4. Оценить стабильность уровня сигнала внури кластера во времени. Выявить наиболее стабильный кластер.
    > stable_clusters <- client_clusters %>%
    + filter(!is.na(power_sd) & !is.infinite(power_sd)) %>%
    + arrange(power_sd) %>%  # Меньшее SD = более стабильный сигнал
    + select(`Station MAC`, `Probed ESSIDs`, avg_power, power_sd, power_stability, cluster_duration)
    > print("Наиболее стабильные кластеры (по уровню сигнала):")
    [1] "Наиболее стабильные кластеры (по уровню сигнала):"
    > print(head(stable_clusters, 10))
    # A tibble: 0 × 6
    # ℹ 6 variables: Station MAC <chr>, Probed ESSIDs <chr>, avg_power <dbl>, power_sd <dbl>,
    #   power_stability <dbl>, cluster_duration <dbl>
    > 
    > ggplot(stable_clusters %>% head(20), 
    + aes(x = reorder(paste(`Station MAC`, `Probed ESSIDs`), power_stability), 
    + y = power_stability)) +
    + geom_col(fill = "steelblue") +
    + coord_flip() +
    + labs(title = "Стабильность уровня сигнала в кластерах",
    + x = "Кластер (MAC + ESSID)",
    + y = "Стабильность сигнала (%)") +
    + theme_minimal()
    > 
    > stable_clusters <- client_clusters %>%
    + filter(!is.na(power_sd) & !is.infinite(power_sd)) %>%
    + arrange(power_sd) %>%  # Меньшее SD = более стабильный сигнал
    + select(`Station MAC`, `Probed ESSIDs`, avg_power, power_sd, power_stability, cluster_duration)
    > print("Наиболее стабильные кластеры (по уровню сигнала):")
    [1] "Наиболее стабильные кластеры (по уровню сигнала):"
    > print(head(stable_clusters, 10))
    # A tibble: 0 × 6
    # ℹ 6 variables: Station MAC <chr>, Probed ESSIDs <chr>, avg_power <dbl>, power_sd <dbl>,
    #   power_stability <dbl>, cluster_duration <dbl>
    > 

## Оценка результата

В результате лабораторной работы мы получили знания о методах
исследования радиоэлектронной обстановки.Составили представление о
механизмах работы Wi-Fi сетей на канальном и сетевом уровне модели OSI

## Вывод

Таким образом, мы получили знания о методах исследования
радиоэлектронной обстановки.

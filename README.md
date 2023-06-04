# Policy Proposal Project
This project entails a policy proposal to implement hydrogen cooking systems in Sichuan, China, and aims to minimize both household and general air pollution.

# Table 1: Percentage of the population exposed to household air pollution from burning solid fuels in 2019
rm(list=ls())

library(tidyr)
library(formattable)
library(dplyr)
library(data.table)

globalAir = fread("Soga_Rank.csv",
                  data.table = FALSE,
                  header = TRUE,
                  stringsAsFactors = FALSE)

head(globalAir)
attach(globalAir)

Y2019 <- globalAir %>%
  filter(`Location` %in% 
           c("India", "China", "Brazil", "Russian Federation",
             "United States of America", "Japan")) %>%
  select(c(`Location`, `Year`, `Population`, `Average`, `Median`))

formattable(Y2019, align =c("l", "c", "c", "c", "r"), 
            list(`Location` = formatter(
              "span", style = ~ style(color = "grey",font.weight = "bold")),
              `Average` = color_bar("red")
              ))

# Graph 1: Year-to-year change in primary energy consumption by source, China (2019-2021)
rm(list=ls())

library(dplyr)
library(ggplot2)

Y2019 <- c(Coal=179, Oil=381, Wind=101, Gas=245, Solar=122, "Other Renewables"=61, Nuclear=133, Hydropower=182)
Y2020 <- c(Coal=188, Oil=69, Wind=157, Gas=282, Solar=95, "Other Renewables"=73, Nuclear=41, Hydropower=117)
Y2021 <- c(Coal=1054, Oil=515, Wind=490, Gas=421, Solar=170, "Other Renewables"=110, Nuclear=100, Hydropower=-70)

energy_df <- rbind(Y2019, Y2020, Y2021)
bp <- barplot(energy_df,beside = TRUE,  main = "Year-to-year change in primary energy consumption by source, China",
              col = c("lightblue", "cornflowerblue", "deepskyblue4"),
              xlab = "Energy Sources", names = c("Coal", "Oil", "Wind", "Gas", "Solar", "Other Renewables", "Nuclear", "Hydropower"),
              ylab = "TWh", legend = c("2019", "2020", "2021"),
              cex.main = 1, cex.names = 0.75,
              args.legend = list(title = "YEARS", x = "topright", cex = 0.7, bty = "n"), ylim = c(-100, 1100))

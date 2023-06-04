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

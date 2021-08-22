
library(dplyr)
library(readr)
library(stringr)

######################### SOCIOECOCNOMICO #############################################

join01 <- read_csv2("MedianHouseholdIncome2015.csv") %>% 
  dplyr::arrange(City) %>% 
  dplyr::mutate(
    id = 1:29322
  )

join02 <- read_csv2("PercentOver25CompletedHighSchool.csv") %>% 
  dplyr::arrange(City)
  
join03 <- read_csv2("PercentagePeopleBelowPovertyLevel.csv")


union01 <- dplyr::inner_join(join01, join02, by = c("City", "Geographic"))
View(union01)

Socioeconomico <- dplyr::inner_join(union01, join03, by = c("City","Geographic")) %>% 
  dplyr::select(Geographic, City, `Median Income`, percent_completed_hs, poverty_rate) %>% 
  dplyr::rename(Median_Income = `Median Income`) %>% 
  dplyr::mutate(
    Median_Income = as.numeric(Median_Income),
    percent_completed_hs = as.numeric(percent_completed_hs),
    poverty_rate = as.numeric(poverty_rate)
  )

########################################################################################

#write.table(Socioeconomico, file ="Socioeconomico.csv", sep = ",")
#write.table(demografico, file ="demografico.csv", sep = ",")
write.table(killings, file ="killings.csv", sep = ",")

####################### KILLINGS #######################################################

killings <- read_csv2("PoliceKillingsUS.csv") %>% 
  dplyr::rename(
    City = city
  ) %>% 
  dplyr::arrange(state)

####################### DEMOGRAFICO ####################################################

demografico <- read_csv2("Demografco.csv") %>% 
  dplyr::mutate(
    share_white = as.numeric(share_white),
    share_black = as.numeric(share_black),
    share_native_american = as.numeric(share_native_american),
    share_asian = as.numeric(share_asian),
    share_hispanic = as.numeric(share_hispanic),
  ) %>% 
  dplyr::arrange(City)

########################## EXPORTANDO EN UN ARCHIVO RDS #################################
saveRDS(demografico,  file = "RDS/demografico1.rds")
saveRDS(killings,  file = "RDS/killings.rds")
saveRDS(Socioeconomico,  file = "RDS/Socioeconomico.rds")

############################################################################################
probando <- dplyr::inner_join(demografico, Socioeconomico, by = c("City","Geographic")) %>%
  dplyr::rename(state = Geographic) %>%
  dplyr::select(City)

################### IMPORTANDO #############################################################
dem_socio <- read_csv2("Union_demo_socio.csv")
muertes <- read_csv2("PoliceKillingsUS_Any.csv") %>% 
  dplyr::rename(
    City = city
  )

Data <- dplyr::inner_join(muertes, dem_socio, by = c("City", "state"))
saveRDS(Data,  file = "RDS/Data_grupo06.rds")







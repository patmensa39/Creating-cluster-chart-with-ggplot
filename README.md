# Creating-cluster-chart-with-ggplot
#Creating cluster chart  with ggplot
### make sure to install all the packages below. 
pacman::p_load(datasets, pacman, psych, rio, tidyverse)

## Using the mtcars dataset
?mtcars
view(mtcars)
glimpse(mtcars)

attach(mtcars)

data <- mtcars %>% rownames_to_column() %>% as_tibble() %>% 
  select(car = rowname, mpg:hp, wt, qsec, gear, carb) %>% 
  mutate_at(vars(-car), scale) %>%
  print()

### Analyzing data
### calculating the cluster 
hie_cluster <- data %>% dist %>% hclust()

### plotting the dendrogram
hie_cluster%>% plot(labels = data$car, cex= 0.8, hang = -1)

### drawing boxes around cluster
hie_cluster %>% rect.hclust(k = 5, border = 2.6)

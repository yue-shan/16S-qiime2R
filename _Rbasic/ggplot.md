
```
gghw1<-ggplot(hw1,aes(Ozone,Wind))
summary(gghw1)
# gghw1 is a data structure and could be used to make different plots
gghw1+geom_point()
# a simple one, can also do geom_boxplot etc.Use all defaut setting
hw1box<-gghw1+geom_boxplot
summary(hw1box)
# can see the current settings, many parameter is set as NULL. can define them in the bracket.
gghw1+geom_point(aes(color=Month), size =4, alpha=3/4)+geom_smooth()+labs(x="Oh Ozone",y="Wind ihih")+theme_bw()

#Cut continous variable to categorial
cutpoints<-quantile(hw1$Day, seq(0,1,length=4),na.rm = TRUE)
#cut Day into 3 groups 
hw1$Daycut<-cut(hw1$Day,cutpoints)
#add a new variable Daycut which is categorial
levels(hw1$Daycut)
#should show what are the options (e.g. 1-10, 10-20)
```

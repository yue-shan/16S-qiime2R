Trying to fix the graph: in a facet group

```
df1<- pd_OTU_interest %>% filter (OTU %in% OTU_in[1])
#list_OTU_in <-list ()
#list_OTU_in [1] <- pd_OTU_interest %>% filter (OTU %in% OTU_in[1])
#for (i in 1:length(OTU_in)) {list_OTU_in[i] <- pd_OTU_interest %>% filter (OTU %in% OTU_in[i])}

S24_7_OTU1 <- pd_OTU_interest %>% filter (OTU %in% OTU_in[8])
S24_7_OTU2 <- pd_OTU_interest %>% filter (OTU %in% OTU_in[9])
#ggplot(x=S24_7_OTU1$Abundance, y=S24_7_OTU2$Abundance)+geom_point


S24_7_OTU <- merge(S24_7_OTU1, S24_7_OTU2,by= c("Sample","EarTag","Group","Source","Treatment","Genotype","TreatmentWeek","WeekTreatment","Individual"), all.x=TRUE)

ggplot(S24_7_OTU,aes(x=Abundance.x, y=Abundance.y))+xlab("Abundance of S24-7_OTU1")+ylab("Abundance of S24-7_OTU2")+geom_point()+geom_smooth(method="lm") + ggtitle(cor(S24_7_OTU$Abundance.x,S24_7_OTU$Abundance.y,use="complete.obs"))


ggplot(S24_7_OTU,aes(x=Abundance.y, y=Lcn2_ug_per_mg_feces.x))+xlab("Abundance of S24-7_OTU2")+ylab("Lcn2_ug/ mg_feces2")+geom_point()+geom_smooth(method="lm") + ggtitle(cor(S24_7_OTU$Abundance.y,S24_7_OTU$Lcn2_ug_per_mg_feces.x,use="complete.obs"))

ggplot(S24_7_OTU,aes(x=Abundance.x, y=Lcn2_ug_per_mg_feces.x))+xlab("Abundance of S24-7_OTU1")+ylab("Lcn2_ug / mg_feces")+geom_point()+geom_smooth(method="lm") + ggtitle(cor(S24_7_OTU$Abundance.x,S24_7_OTU$Lcn2_ug_per_mg_feces.x,use="complete.obs"))


B_fragilis <- pd_OTU_interest %>% filter (OTU %in% OTU_in[2])
B_acidifaciens <- pd_OTU_interest %>% filter (OTU %in% OTU_in[5])
Bacteroides_OTU <- merge(B_fragilis, B_acidifaciens,by= c("Sample","EarTag","Group","Source","Treatment","Genotype","TreatmentWeek","WeekTreatment","Individual","Kindom","Order","Class","Phylum"), all.x=TRUE)
ggplot(Bacteroides_OTU,aes(x=Abundance.x, y=Abundance.y))+xlab("Abundance of B_fragilis")+ylab("Abundance of B_acidifaciens")+geom_point()+geom_smooth(method="lm") 


Lacto_1 <- pd_OTU_interest %>% filter (OTU %in% OTU_in[4])
Lacto_2 <- pd_OTU_interest %>% filter (OTU %in% OTU_in[6])
Lacto_OTU <- merge(Lacto_1, Lacto_2, by= c("Sample","EarTag","Group","Source","Treatment","Genotype","TreatmentWeek","WeekTreatment","Individual","Kingdom","Order","Class","Phylum"), all.x=TRUE)
ggplot(Lacto_OTU,aes(x=Abundance.x, y=Abundance.y))+xlab("Abundance of Lactobacillis OTU1")+ylab("Abundance of Lactobacillis OTU2")+geom_point()+geom_smooth(method="lm") + ggtitle(cor(Lacto_OTU$Abundance.x,Lacto_OTU$Abundance.y,use="complete.obs"))

Erysi_1 <- pd_OTU_interest %>% filter (OTU %in% OTU_in[3])
Erysi_2 <- pd_OTU_interest %>% filter (OTU %in% OTU_in[7])
Erysi_OTU <- merge(Erysi_1, Erysi_2, by= c("Sample","EarTag","Group","Source","Treatment","Genotype","TreatmentWeek","WeekTreatment","Individual","Kingdom","Order","Class","Phylum"), all.x=TRUE)
ggplot(Erysi_OTU,aes(x=Abundance.x, y=Abundance.y))+xlab("Abundance of Erysipelotrichaceae OTU1")+ylab("Abundance of Erysipelotrichaceae OTU2")+geom_point()+geom_smooth(method="lm") + ggtitle(cor(Erysi_OTU$Abundance.x,Erysi_OTU$Abundance.y,use="complete.obs"))
 
df_abundance <- cbind(B_fragilis$Abundance, B_acidifaciens$Abundance,Erysi_1$Abundance,Erysi_2$Abundance, Lacto_1$Abundance,Lacto_2$Abundance, S24_7_OTU1$Abundance,S24_7_OTU2$Abundance)
head(df_abundance)
colnames(df_abundance) <- c("B_fragilis", "B_acidifaciens","Erysi_1", "Erysi_2", "Lacto_1", "Lacto_2", "S24_7_OTU1","S24_7_OTU2")
df_abundance<-cbind(df_abundance,B_fragilis$Lcn2_ug_per_mg_feces,B_fragilis$Treatment)
df_abundance<-as.data.frame(df_abundance)
names(df_abundance)[9] <-"Lcn2"
df_abundance$V10<-B_fragilis$Treatment
names(df_abundance)[10] <-"Treatment"


#g1<-ggplot(df_abundance%>%filter(B_acidifaciens>0), aes(x=B_acidifaciens, y=S24_7_OTU1))+geom_point()+geom_smooth(method="lm")+xlim(0.001,30)+ ggtitle(cor(df_abundance$B_acidifaciens,df_abundance$S24_7_OTU1,use="complete.obs"))

#g2<-ggplot(df_abundance%>%filter(B_acidifaciens>0), aes(x=B_acidifaciens, y=S24_7_OTU2))+geom_point()+geom_smooth(method="lm")+ggtitle(cor(df_abundance$B_acidifaciens,df_abundance$S24_7_OTU2,use="complete.obs"))

#g3<-ggplot(df_abundance%>%filter(B_fragilis>0), aes(x=B_fragilis, y=S24_7_OTU1))+geom_point()+geom_smooth(method="lm")+ggtitle(cor(df_abundance$B_fragilis,df_abundance$S24_7_OTU1,use="complete.obs"))

#g4<-ggplot(df_abundance%>%filter(B_fragilis>0), aes(x=B_fragilis, y=S24_7_OTU2))+geom_point()+geom_smooth(method="lm")+ggtitle(cor(df_abundance$B_fragilis,df_abundance$S24_7_OTU2,use="complete.obs"))

#Wrong cor,as cor included points that's not included on the graph.

df_treat<-df_abundance%>%filter(Treatment=="IL10-SPF+BF")
df_control<-df_abundance%>%filter(Treatment=="IL10-SPF")

#g1<-ggplot(df_control, aes(x=B_acidifaciens, y=S24_7_OTU1))+geom_point()+geom_smooth(method="lm") + ggtitle(cor(df_control$B_acidifaciens,df_control$S24_7_OTU1,use="complete.obs"))

#g2<-ggplot(df_control, aes(x=B_acidifaciens, y=S24_7_OTU2))+geom_point()+geom_smooth(method="lm") + ggtitle(cor(df_control$B_acidifaciens,df_control$S24_7_OTU2,use="complete.obs"))

g3<-ggplot(df_treat, aes(x=B_fragilis, y=S24_7_OTU1))+geom_point()+geom_smooth(method="lm") + ggtitle(cor(df_treat$B_fragilis,df_treat$S24_7_OTU1,use="complete.obs"))

g4<-ggplot(df_treat, aes(x=B_fragilis, y=S24_7_OTU2))+geom_point()+geom_smooth(method="lm") + ggtitle(cor(df_treat$B_fragilis,df_treat$S24_7_OTU2,use="complete.obs"))

grid.arrange(g1,g2,g3,g4,ncol=2)

g5<- ggplot(df_treat, aes(x=B_fragilis, y=Lcn2)) +geom_point() +geom_smooth(method="lm")+ggtitle(cor(df_treat$B_fragilis,df_treat$Lcn2,use="complete.obs"))

g6<- ggplot(df_abundance, aes(x=B_acidifaciens, y=Lcn2)) +geom_point() +geom_smooth(method="lm")+ ggtitle(cor(df_abundance$B_acidifaciens,df_abundance$Lcn2,use="complete.obs"))

g7<- ggplot(df_abundance, aes(x=S24_7_OTU1, y=Lcn2))+geom_point()+geom_smooth(method="lm")+xlim(0,10)+ggtitle(cor(df_abundance$S24_7_OTU1,df_abundance$Lcn2,use="complete.obs"))

g8<- ggplot(df_abundance, aes(x=S24_7_OTU2, y=Lcn2))+geom_point()+geom_smooth(method="lm")+ggtitle(cor(df_abundance$S24_7_OTU2,df_abundance$Lcn2,use="complete.obs"))

grid.arrange(g5,g6,g7,g8,ncol=2)

#df_abundance[df_abundance$B_acidifaciens==0,]returns 0 row. Should use all data to conduct B_acid for linear regression:
g9<-ggplot(df_treat, aes(x=B_acidifaciens, y=S24_7_OTU1))+geom_point()+geom_smooth(method="lm") + ggtitle(cor(df_treat$B_acidifaciens,df_treat$S24_7_OTU1,use="complete.obs"))

g10<-ggplot(df_treat, aes(x=B_acidifaciens, y=S24_7_OTU2))+geom_point()+geom_smooth(method="lm") + ggtitle(cor(df_treat$B_acidifaciens,df_treat$S24_7_OTU2,use="complete.obs"))

g11<-ggplot(df_abundance, aes(x=B_acidifaciens, y=S24_7_OTU1))+geom_point()+ ggtitle(cor(df_abundance$B_acidifaciens,df_abundance$S24_7_OTU1,use="complete.obs"))+geom_smooth(method="lm")

g12<-ggplot(df_abundance, aes(x=B_acidifaciens, y=S24_7_OTU2))+geom_point()+ ggtitle(cor(df_abundance$B_acidifaciens,df_abundance$S24_7_OTU2,use="complete.obs"))+geom_smooth(method="lm")

g11<-ggplot(df_abundance, aes(x=B_acidifaciens, y=S24_7_OTU1,color=Treatment))+geom_point()+ ggtitle(cor(df_abundance$B_acidifaciens,df_abundance$S24_7_OTU1,use="complete.obs"))
+geom_smooth(method="lm")

ggplot(df_treat, aes(x=B_fragilis, y=Erysi_1))+geom_point()+geom_smooth(method="lm") + ggtitle(cor(df_treat$B_fragilis,df_treat$Erysi_1,use="complete.obs"))
`geom_smooth()` using formula 'y ~ x'
#no correlation
ggplot(df_treat, aes(x=B_fragilis, y=Erysi_2))+geom_point()+geom_smooth(method="lm") + ggtitle(cor(df_treat$B_fragilis,df_treat$Erysi_2,use="complete.obs"))
`geom_smooth()` using formula 'y ~ x'
#no correlation

g13<- ggplot(df_treat, aes(x=B_fragilis, y=Lacto_1))+geom_point()+geom_smooth(method="lm") + ggtitle(cor(df_treat$B_fragilis,df_treat$Lacto_1,use="complete.obs"))

g14<- ggplot(df_treat, aes(x=B_fragilis, y=Lacto_2))+geom_point()+geom_smooth(method="lm") + ggtitle(cor(df_treat$B_fragilis,df_treat$Lacto_2,use="complete.obs"))

g15<-ggplot(df_abundance, aes(x=B_acidifaciens, y=Lacto_1))+geom_point()+geom_smooth(method="lm")+ ggtitle(cor(df_abundance$B_acidifaciens,df_abundance$Lacto_1,use="complete.obs"))

g16<-ggplot(df_abundance, aes(x=B_acidifaciens, y=Lacto_2))+geom_point()+geom_smooth(method="lm")+ ggtitle(cor(df_abundance$B_acidifaciens,df_abundance$Lacto_2,use="complete.obs"))

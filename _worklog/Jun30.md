Trying to fix the graph: in a facet group 

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


g1<-ggplot(df_abundance, aes(x=B_acidifaciens, y=S24_7_OTU1))+geom_point()+geom_smooth(method="lm")+xlim(0.001,30)+ ggtitle(cor(df_abundance$B_acidifaciens,df_abundance$S24_7_OTU1,use="complete.obs"))

g2<-ggplot(df_abundance, aes(x=B_acidifaciens, y=S24_7_OTU2))+geom_point()+geom_smooth(method="lm")+ggtitle(cor(df_abundance$B_acidifaciens,df_abundance$S24_7_OTU2,use="complete.obs"))

g3<-ggplot(df_abundance, aes(x=B_fragilis, y=S24_7_OTU1))+geom_point()+geom_smooth(method="lm")+ggtitle(cor(df_abundance$B_fragilis,df_abundance$S24_7_OTU1,use="complete.obs"))

g4<-ggplot(df_abundance, aes(x=B_fragilis, y=S24_7_OTU2))+geom_point()+geom_smooth(method="lm")+ggtitle(cor(df_abundance$B_fragilis,df_abundance$S24_7_OTU2,use="complete.obs"))

g5<- ggplot(df_abundance%>%filter(B_fragilis>0), aes(x=B_fragilis, y=Lcn2))+geom_point()+geom_smooth(method="lm")+xlim(0,10)+ggtitle(cor(df_abundance$B_fragilis,df_abundance$Lcn2,use="complete.obs"))

g6<- ggplot(df_abundance%>%filter(B_acidifaciens>0), aes(x=B_acidifaciens, y=Lcn2))+geom_point()+geom_smooth(method="lm")+xlim(0,10)+ggtitle(cor(df_abundance$B_acidifaciens,df_abundance$Lcn2,use="complete.obs"))

g7<- ggplot(df_abundance, aes(x=S24_7_OTU1, y=Lcn2))+geom_point()+geom_smooth(method="lm")+xlim(0,10)+ggtitle(cor(df_abundance$S24_7_OTU1,df_abundance$Lcn2,use="complete.obs"))

g8<- ggplot(df_abundance, aes(x=S24_7_OTU2, y=Lcn2))+geom_point()+geom_smooth(method="lm")+ggtitle(cor(df_abundance$S24_7_OTU2,df_abundance$Lcn2,use="complete.obs"))


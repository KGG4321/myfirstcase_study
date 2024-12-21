# Overview

This is my first case study ( for learning R & SQL) , in this case study I am trying to find answer how differently casual members are utilizing services of cyclist company than annual members . This will help in converting casual members to annual membership program.

Dataset is from fictional cyclist company .

I have used R ,SQL & excel all three to get this answer , so that I can understand advantages for all three .

I have shown below for R only (with overview steps)  , but in uploaded Cyclist_Case_Study ppt you can find all three in more detail.

## Dataset Description


review=read_csv("Divvy_Trips_2019_Q1.csv")


![image](https://github.com/user-attachments/assets/6e1dcd82-22d8-4f4e-8dd1-19da8060863f)

## Dataset Prepare

Organizing the data to the columns which are needed and creating a new dataset out of it .

review_sorted_1<-review [, c("trip_id","start_time","end_time","usertype")]


![image](https://github.com/user-attachments/assets/3e22b34f-538b-42be-82af-06b8f39d361d)


## Dataset Cleaning 

We can see start time , end time  , trip duration  was used as character data type which should be converted to time date type .

review_sorted_4$start_time<-ymd_hms(review_sorted_4$start_time)

review_sorted_4$end_time<-ymd_hms(review_sorted_4$end_time)

review_sorted_4$ride_length<-(review_sorted_4$end_time-review_sorted_4$start_time)

## Dataset Processing
Renaming usertype name with replace function.

review_sorted_2$usertype[review_sorted_2$usertype=="Subscriber"]<-"member“
review_sorted_2$usertype[review_sorted_2$usertype=="Customer"]<-"casual“

![image](https://github.com/user-attachments/assets/1658dab6-9c71-42e9-9a10-15288d41aa9e)

## Dataset Analyze
Creating another dataframe and merging both dataframe 

review_3<-read_csv("Divvy_Trips_2020_Q1.csv")

review_sorted_3<- review_3[,c("ride_id" ,"started_at","ended_at","member_casual")]

review_final<-rbind(review_sorted_2,review_sorted_4)

## Dataset Visualization 

ggplot(data=review_final)+geom_bar(mapping=aes(x=usertype ,ride_length), stat = "summary", fun.y = "mean")+ facet_wrap(~day_of_week ,scales= 'free_x')+ ylab("Average_ride_length")

![image](https://github.com/user-attachments/assets/07ebfdf5-7f2e-4142-94e4-75ccca5dbb13)

days_of_the_week <- c("Sun", "Mon", "Tue", "Wed",  "Thu", "Fri", "Sat")
ggplot(data=review_final)+geom_bar(aes(factor(x=day_of_week,days_of_the_week), y=ride_length ,fill=day_of_week) ,stat = "summary" ,show.legend = FALSE )+ facet_wrap(~usertype ,scales= 'free_x')+ xlab("Days_of the_week")+ylab("Average_ride_length in mins")+theme(axis.text.x = element_text(angle = 45))

![image](https://github.com/user-attachments/assets/69b5e45f-3b99-4622-9519-225e5d4dac92)


## Contributing

We welcome contributions to improve the datasets and their documentation. 

Please fork the repository and submit a pull request with your changes.



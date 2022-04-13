---
title: "Designing Youtube"
date: 2022-04-12
---

### Requirements and goal of the system
#### Functional Goals
1. Users should be able to upload videos.
2. Users should be able to view and share videos.
3. Users should be able to search videos using title of the video.
4. Users should be able to view and add comments to video.
5. System should record video stats like views, likes, dislikes etc.

#### Non-Functional Goals
1. System should be highly available, consistency can take a hit in view of availability. If some users dosen't see a video for a while its fine.
2. Video streaming should be in real-time without lag.
3. System should be reliable and no data should be lost.

### Capacity Estimations and Constraints
Lets assume Youtube has 2 billion daily active users. Each user watches 5 videos a day and average size of video is 10 min.
Number of Video Views per sec = (2 * 10^9 * 5)/(24 * 60 * 60) = 10^5 videos/sec
Lets suppose video upload to video view ratio is 1:100
Number of Video uploaded per sec = 10^5/100 = 1000 videos/sec

### Storage required per sec
Lets assume for every 1 min video we need 10 MB space
New uploads = 1000 * 10min * 10MB = 100GB per sec

### Bandwidth estimation
Incoming bandwidth = 1000 Video/sec * 10MB/60 = 166 MB per sec
Outgoing bandwith = 16.6 GB per sec

##### Credits :  
1. [educative.io: Designing Youtube or Netflix](https://www.youtube.com/watch?v=ImtZgX1nmr8&list=PLhfHPmPYPPRk6yMrcbfafFGSbE2EPK_A6&index=12)

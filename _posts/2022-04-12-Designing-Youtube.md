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
  
### API Design
#### UploadVideo
uploadVideo(apiKey, videoContent, title, description, tags, categoryId, subtitles, language, location)  
apiKey : token through which user will be authenticated and throttled in case of limit accede or abuse.  
videoContent : the video file to be uploaded it could be in bytes and compressed.  
title : title of the video  
description : <optional> description of the video  
tags : <optional> tags for the video, will help to improve video rank  
categoryId : <optional> categoryId of the video  
subtitles : <optional> subtitle list for video  
language : <optional> language of the video  
location : <optional> country/region of the user  
  
Response: 202 Request Accepted If the video validations are passed. An email will be triggered to user with link to access the video once encoding is complete. Alternatively we can provide API to check video status also.
  
#### Search Video
SearchVideo(apiKey, searchQuery, cursor, location)  
apiKey: token through which user will be authenticated. User primary location and preferences can be loaded using this token.  
searchQuery: String consisting of search terms.  
cursor: A pointer to the next result-set. It will be encoded to contain info about partition and also row pointer to the next result.  
location: <optional> We want the user a option to change its location.  
  
Response: A json list containing info about video resources matching query result. Each video resource will have a title, thumbnail, creationDate, author, stats. Also it will return nextCursor, that will be passed in API to fetch next set of videos.
  
#### Stream Video
StreamVideo(apiKey, videoId, offset, codec, resolution)  
  
apiKey: token through which user will be authenticated  
videoId: An integer or string id to uniquely identify a video  
offset: Offset will be in sec from start of video. If multiple devices are supported then we will need to save offset per device to allow user to start video from where they left.  
codec & resolution: If we support different devices then we will need to support diffrent formats as different devices has different resolution and codec requirements.  
  
Response: A video stream (chunk of video)  
  
##### Credits :  
1. [educative.io: Designing Youtube or Netflix](https://www.youtube.com/watch?v=ImtZgX1nmr8&list=PLhfHPmPYPPRk6yMrcbfafFGSbE2EPK_A6&index=12)
2. [Slack Engineering: Evolving API Pagination at Slack](https://slack.engineering/evolving-api-pagination-at-slack/)
3. [Stackoverflow: How to implement cursors for pagination in an api](https://stackoverflow.com/questions/18314687/how-to-implement-cursors-for-pagination-in-an-api)
4. [API pagination design](https://solovyov.net/blog/2020/api-pagination-design/)

# Dataset

**Important Note: All of the User IDs Are Anonymized. No Personal Info Is Disclosed in the Datasets Publicized Here.**

Many of the Twitter users publicly tweet about their mental health condition on the website.
For instance, there are many tweets with the following content in it: "I'm diagnosed with depression" or "I have been diagnosed with PTSD", etc.

Many of the Twitter users also tweet about their musical taste by tweeting a link to a music streaming platform, e.g. Spotify, AppleMusic, Soundcloud,
on the website. It is a common practice and sometimes they use a hashtag with it. #np and #nowplaying are two of the widely used hashtags when Twitter users
tweet about a music they are listening to.

In order to study and analyze the musical taste of Twitter users with self-disclosed diagnosis of mental disorders, and also to study the relationship
between the musical taste and the mental disorders, I dug the public Twitter database from 01/01/2018 to 04/01/2021 (January) to retrieve a list of
such users.

To further investigate and perform comparison study, I gathered a similar dataset of tweets and musics from "control" Twitter users, i.e. Twitter users
who have never tweeted anything about mental disorders, not even once.

## Data gathering

I dug the Twitter public database (using its advanced API) with the following search terms:

1. "I am/I'm diagnosed with {disorder}"
2. "I have/I've been diagnosed with {disorder}"
3. "diagnosed me with {disorder}"
4. "I am clinically diagnosed with {disorder}"
5. "clinically diagnosed me with {disorder}"
6. "I have/I've been clinically diagnosed with {disorder}"

I performed the search (with the double quotation to make sure those exact words with those exact orders are tweeted, not a single character more or less in between)
on the entire public Twitter (at the time of retrieval, many Twitter users frequently switch between private and public mode)
from January 1st 2018 to January 4th 2021. The `{disorder}` is replaced with one of the following six mental disorders:

1. Depression
2. Anxiety
3. PTSD
4. Borderline (or "Borderline disorder")
5. Bipolar (or "Bipolar disorder")
6. Panic (or "Panic disorder")

**I tried other mental disorders as well, but there were only a handful of users who have tweeted about them. So I only retrieved the 6 most mentioned disorders.**

### Users

The following table contains the number of retrieved Twitter users who have exactly tweeted (not retweet, only native tweet by the user)
at least one of the mentioned search terms.

|  Disorder  | Retrieved Users (Number) | Retrieved Users (Percentage) |
|:----------:|:------------------------:|:----------------------------:|
| Depression |           8580           |             45.88            |
|    PTSD    |           4000           |             21.39            |
|   Anxiety  |           3907           |             20.89            |
|   Bipolar  |           1477           |             7.89             |
| Borderline |            543           |              2.9             |
|    Panic   |            272           |             1.45             |
|    Total   |           18699          |              100             |

### Tweets

As the next step, I extracted the most recent timeline of all of the retrieved users (up to ~3200 tweets according to strict Twitter API limits).
The process of extracting so many timelines take several days (given the Twitter API limits). 530 of the retrieved users either switched to the protected mode
or had their account suspended, deleted, deactivated, or in any form unaccessible through the Twitter API during the timeline extraction.
I was able to extract 18169 timelines.

The following table contains the number of tweets extracted for each disorder.

|  Disorder  | Retrieved Tweets (Number) | Retrieved Tweets (Percentage) |
|:----------:|:-------------------------:|:-----------------------------:|
| Depression |          14527850         |             45.12             |
|    PTSD    |          6854420          |             21.29             |
|   Anxiety  |          6826939          |              21.2             |
|   Bipolar  |          2546237          |              7.9              |
| Borderline |           939087          |              2.91             |
|    Panic   |           496835          |              1.54             |
|    Total   |          32191368         |              100              |

So in total I extracted 32191368 tweets associated with one of the mentioned mental disorders.

Many of the extracted timelines had only a handful of tweets while many more had full ~3200 maximum extractable tweets. The following table shows
the quartile stats for the number of tweets in each extracted timeline.

| Extracted Timelines | Mean # of tweets in each timeline |  STD  | Min | 25% Percentile |  50% |  75% |  Max |
|:-------------------:|:---------------------------------:|:-----:|:---:|:--------------:|:----:|:----:|:----:|
|        18169        |               ~1771               | ~1086 |  1  |       852      | 1852 | 2642 | 3249 |

It is noted that many of the Twitter users actively delete their past tweets either manually or automatically using software.

## The Music Dataset

As mentioned above, my goal was to study the relationship and the nature of musical taste of Twitter users with self-disclosed diagnosis of mental disorders.
In order to do so, I processed all 32191368 tweets and looked for a link to one the following three music streaming platforms:

1. Spotify
2. Apple Music
3. Soundcloud

It is noted that I inspected for other music streaming platforms and they were overwhelmingly in minority. After retrieving the name of the song and the name
of the artist, I used the Genius API, an online lyrics database, to retrieve the lyrics of the songs.

It is also noted that many of the links were actually a link to an album or a playlist, not a single track. For such cases, I retrieved all of the songs
in the album (or playlist).

Out of the 32191368 tweets, I was able to retrieve 396842 songs with their title and artist name. Out of 396842 songs, I was able to obtain
lyrics for 311568 songs through the Genius API. I manually checked some of the left out songs and realized that the Genius API is not complete
enough to cover everything. I tried other lyrics databases but they were drastically smaller and couldn't cover those left out.

### Disorders

The following table presents quartiles and some statistical information about the number of lyrics associated with each mental disorder.

|  Disorder  | Extracted Songs (Number) | Extracted Songs (Percentage) |
|:----------:|:------------------------:|:----------------------------:|
| Depression |          180386          |             45.45            |
|   Anxiety  |           97325          |             24.52            |
|    PTSD    |           66366          |             16.72            |
|   Bipolar  |           35732          |               9              |
| Borderline |           12000          |             3.02             |
|    Panic   |           5033           |             1.26             |
|    Total   |          396842          |              100             |

**It is interesting to note that even though the number of PTSD users and tweets is slightly more than those of the Anxiety, when it comes to music,
Anxiety users have much more tweeted about musics they listen to compared to PTSD users.**

### Lyrics

The following table presents quartiles and some statistical information about the number of words in retrieved lyrics, i.e. how long lyrics are.

| Extracted Lyrics | Mean # of Words in Lyrics |  STD | Min | 25% Percentile | 50% | 75% |  Max  |
|:----------------:|:-------------------------:|:----:|:---:|:--------------:|:---:|:---:|:-----:|
|      311568      |            ~347           | ~311 |  1  |       226      | 317 | 427 | 73311 |

It is clear that 1 for the minimum length of words in lyrics and 73311 for the maximum are clearly outliers and most probably due to faults in the retrieved
lyrics from Genius API. It is noted that I have not performed any text cleaning or outlier pruning on these datasets. Any observational or analytical study
require some standard cleaning on the text.

### Users

The following table presents quartiles and some statistical information about the number of songs (cumulative among albums and playlists) that disorders users
have tweeted.

| Total # of Users | Mean # of Musics Tweeted |  STD | Min | 25% | 50% | 75% |  Max |
|:----------------:|:------------------------:|:----:|:---:|:---:|:---:|:---:|:----:|
|       5009       |            ~79           | ~207 |  1  |  2  |  18 |  89 | 5028 |

It is noted that 25% of disorder users only tweeted 2 songs. There is one user who has tweeted 5028 songs, most of them are certainly albums and playlists
given the 3200 tweet cap.

### Artists

The top five most listened to artists among disorder users are:

1. BTS (14237)
2. Taylor Swift (6966)
3. Waterparks (4351)
4. Ariana Grande (3502)
5. Niall Horan (3112)

The quartile and other statistical information about the number of artists that disorder users listen to is presented in the following table.

| Total # of Artists | Mean # of Times an Artist is Listen to |  STD | Min | 25% | 50% | 75% |  Max  |
|:------------------:|:--------------------------------------:|:----:|:---:|:---:|:---:|:---:|:-----:|
|        36726       |                   ~10                  | ~102 |  1  |  1  |  2  |  5  | 14237 |

**It is very interesting to note that 50% of the artists are listened to less than twice. 75% are listened to less than 5 times. Though the average
number of times an artist is listen to is 10. The skewness is caused by the super popular artists that users listen to *A LOT* more than they do
with other artists.**

### Songs

The top five most listened to songs among disorder users are:

1. Lowkey As Hell by Waterparks (2862)
2. Nice To Meet Ya by Niall Horan (1949)
3. Dynamite by BTS (1401)
4. Life Goes On by BTS (1247)
5. Nice To Meet Ya - Stripped Version by Niall Horan (530)

The quartile and other statistical information about the number of songs that disorder users listen to is presented in the following table.

| Total # of Unique Songs | Mean # of Times a Song is Listen to |  STD  | Min | 25% | 50% | 75% |  Max |
|:-----------------------:|:-----------------------------------:|:-----:|:---:|:---:|:---:|:---:|:----:|
|          158899         |                 ~2.5                | ~11.7 |  1  |  1  |  1  |  2  | 2862 |

**It is very interesting to note that 75% of the songs are listened to less than twice. Though the average number of times a song is listen to
is ~2.5. The skewness is caused by the super popular songs that users listen to *A LOT* more than they do with other songs.**

### Music Streaming Platform

As mentioned above, I only retrieved songs from the three top music streaming platforms. Other platforms were overwhelmingly in minority. They rank as follows:

1. Spotify (320402)
2. Apple Music (74011)
3. Soundcloud (2429)

### Track, Album, or Playlist?

The streaming platforms mentioned above have dedicated sharing links for single tracks, albums, and playlists. A single link tweeted by a user might point to
a single track or might point to a playlist of 100 songs. The breakdown of all songs extracted (not unique songs, but all of them) according to
their origin is as follows:

1. Playlist (258032)
2. Album (106374)
3. Single Track (32436)



# Vpply Video Components

## Latest Stable Versions
Recorder: vpply_recorder_pv1.4.js

Player: vpply_player_pv1.6.js

Interview Recorder: vpply_interview_recorder_pv1.5

Interview_Player: vpply_interview_player_pv1.3

For staging use the script as sv_1.x

e.g https://vpply-assets.s3.ap-southeast-2.amazonaws.com/js/vpply_recorder_sv1.4.min.js

## Recorder: vpply_recorder_pv1.4.js
The recorder component records 60 second videos using the front facing camera on the users device.

place an element inside your HTML code with an id of vpply-video-element

```
<div id="vpply-video-element"></div>
```

To use the script load the recorder module and configure the recorder using your primary key: 

```
import * as recorder from 'https://vpply-assets.s3.ap-southeast-2.amazonaws.com/js/vpply_recorder_pv1.4.min.js'

recorder.configure(primary_key)
```
Add an event listener on the component to wait for the user to submit a video.
the returned result inside event.detail is the vpply_id to reference the video to watch later.

```
document.getElementById('vpply-video-element').addEventListener('videouploaded', (event) => {
    //string
    video_id = event.detail
    
})
```

use recorders destroy function to unmount the video recorder.

```
recorder.destory()
```


## Player: vpply_player_pv1.6.js
The player component will return a video element with the video loaded using the vpply_id returned from the recorder components. 

place an element inside your HTML code with an id of vpply-video-element
```
<div id="vpply-video-element"></div>
```

To use the script load the player module and configure it using your primary key and video id.
video id is the value returned from the video recorder as a reference to a video
```
import * as player from 'https://vpply-assets.s3.ap-southeast-2.amazonaws.com/js/vpply_player_pv1.6.min.js'

player.configure(primary_key, vpply_id)
 ```
to unmount the player call the destroy function
```
player.destroy()
```

## Interview Recorder: vpply_interview_recorder_pv1.5.js
The interview recorder component records multiple videos as responses to questions at a set response length in seconds. */

To start using the recorder, request a client_key using your secret key, making a get request to the vpply server. 
```
'GET' : 'https://videoapi.vpply.com/api/createckey'

//Set Request Headers //
 {
     header:    vpply_skey,
     value :    your secret key
 }
```
call the interview recorders configure function using a client key to use as reference to the bundle of videos the user saves.


Import the interview recorder module and pass in a new client key and questions array in the order the questions are set on the 
job posting to the interview recorders configure function.
```
import * as interview_recorder from 'https://vpply-assets.s3.ap-southeast-2.amazonaws.com/js/vpply_interview_recorder_pv1.5.min.js'

questions = [
    {
        question: String, 
        response_time: Number
    },
    {
        question: String, 
        response_time: Number
    },
]

interview_recorder.configure(client_key, questions)
```

Add an event listener on the component to wait for the user to submit a video.
the returned result inside event.detail is the interview_id to reference the interview to 
view all answers at once inside the interview player.
```
 document.getElementById('vpply-interview-element').addEventListener('interviewcomplete', (event) => {
    
    //string
    interview_id = event.detail
    
})
```
to close the interview_recorder call the destroy function
```
 interview_recorder.destroy()
```

## Interview Player: vpply_interview_player_pv1.3.js
The interview player component plays back a jobseekers video interview. 

place an element inside your HTML code with an id of vpply-interview-player
```
<div id="vpply-interview-player"></div>
```
call the interview players configure function using your primary key, interview id and questions 

Interview_id is the returned value of the interview recorder as a reference to a bundle of videos.
questions is an array of strings. Pass the questions in the same order they were answered in the interview_recorder.
```
import * as player from 'https://vpply-assets.s3.ap-southeast-2.amazonaws.com/js/vpply_interview_player_pv1.3.min.js'

questions = [
    {question: 'string'}, 
    {question: 'string'}
]

player.configure(primary_key, interview_id, questions)
 ```
to close the player call the destroy function
```
player.destroy()
```

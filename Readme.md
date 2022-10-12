# Vpply Recorder Docs
---

## How to integrate - Profile Videos

For Recording a profile, we configure the player to record and upload only 1 video. The response received is the video id

First, in your HTML, add a div element with the id of ‘vpply-recorder-element’

`<div id="vpply-recorder-element"></div>`

Next import the script to handle the video recording in the body of the page running the recorder. Make sure the script tag has the type="module attribute"

`<script src="recorder.js" type="module"></script>`

Import the module

`import * as recorder from <url of script>`

Next, configure the parameters of the recorder. You will need

`primary_key:string = <your primary key>`

`Recorder_config = [
    {
        allow_upload: true, 
        max_length: 60
    }
]`

`const type:string = 'profile'`

`const brand_color:string =  <your brands hex code>`

`font_family: string = <your brand font family>`

Next mount the recorder by calling the ‘mount’ function, passing in the parameters

`recorder.mount(
	primary_key,
    recorder_config,
    type,
    brand_color,
    font_family
)`

Once the recording is complete, listen for the ‘interviewcomplete’ event 

`document.getElementById('vpply-recorder-element').addEventListener('interviewcomplete', (res) => {
    let video_id = res.detail
})`

When recording is complete the element will unmount itself.

If you would like to unmount the element before a video is uploaded, you can call the unmount() function

`recorder.unmount()`

---

## How to integrate - Interviews

For Recording a profile, we configure the player to record and upload only 1 video. The response received is the video id

First, in your HTML, add a div element with the id of ‘vpply-recorder-element’

`<div id="vpply-recorder-element"></div>`

Next import the script to handle the video recording in the body of the page running the recorder. Make sure the script tag has the type="module attribute"

`<script src="recorder.js" type="module"></script>`

Next, we need to get a client key for every indivdual interview recording. To get a client key, make a http get request to the Vpply API

`'GET' : 'https://videoapi.vpply.com/api/createckey'`

`//Set Request Headers //
 {
     header:    vpply-skey,
     value :    your secret key
 }`

Import the module

`import * as recorder from <url of script>`

Next, configure the parameters of the recorder. You will need

`client_key:string = <generated client key>`

You can have as many questions here as you like structured like the objects in the array below
`recorder_config = [
    {
        allow_upload: true, 
        max_length: 60,
        text_prompt: "this is a sample question"
    },
    {
        allow_upload: true, 
        max_length: 60,
        text_prompt: "this is a sample question"
    }
]`



`const type:string = 'interview'`

`const brand_color:string =  <your brands hex code>`

`font_family: string = <your brand font family>`

Next mount the recorder by calling the ‘mount’ function, passing in the parameters

`recorder.mount(
	client_key,
    recorder_config,
    type,
    brand_color,
    font_family
)`

Once the recording is complete, listen for the ‘interviewcomplete’ event 

`document.getElementById('vpply-recorder-element').addEventListener('interviewcomplete', (res) => {
    let interview_id = res.detail
})`

When recording is complete the element will unmount itself.

If you would like to unmount the element before a video is uploaded, you can call the unmount() function

`recorder.unmount()`

## Player: vpply_player_pv1.6.js
The player component will return a video element with the video loaded using the vpply_id returned from the recorder components.

place an element inside your HTML code with an id of vpply-video-element

`<div id="vpply-video-element"></div>`
To use the script load the player module and configure it using your primary key and video id. video id is the value returned from the video recorder as a reference to a video

`import * as player from 'https://vpply-assets.s3.ap-southeast-2.amazonaws.com/js/vpply_player_pv1.6.min.js'`

`player.configure(primary_key, vpply_id)`
to unmount the player call the destroy function

`player.destroy()`


## Interview Player: vpply_interview_player_pv1.3.js
The interview player component plays back a jobseekers video interview.

place an element inside your HTML code with an id of vpply-interview-player

`<div id="vpply-interview-player"></div>`

call the interview players configure function using your primary key, interview id and questions

Interview_id is the returned value of the interview recorder as a reference to a bundle of videos. questions is an array of strings. Pass the questions in the same order they were answered in the interview_recorder.

`import * as player from 'https://vpply-assets.s3.ap-southeast-2.amazonaws.com/js/vpply_interview_player_pv1.3.min.js'`

`questions = [
    {question: 'string'}, 
    {question: 'string'}
]`

player.configure(primary_key, interview_id, questions)

to close the player call the destroy function

`player.destroy()`

# Vpply Recorder Docs
---

## How to integrate - Profile Videos

For Recording a profile, we configure the player to record and upload only 1 video. The response received is the video id

First, in your HTML, add a div element with the id of ‘vpply-recorder-element’

`<div id="vpply-recorder-element"></div>`

Next import the script to handle the video recording in the body of the page running the recorder. Make sure the script tag has the type="module attribute"

`<script src=<location of your script> type="module"`

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

`<script src=<location of your script> type="module"`

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

`recorder_config = [
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

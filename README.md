AV Presentor
====
##Control Computer
This computer would run the main application for 4 hours every day. Each
show would consists of 4 Presentation objects. The control computer is
responsible for delegating 

```
Show:[ Presentation, ... ]
```

Each Presentation would consists of an intro video, an array of
questions, and an array of survivors.

```
Presentation:{
  intro: Video,
  survivors: Array
}
```

The control computer is in charge of queueing and playing of all shows.
It needs to be aware of which show it is currently on. Since there are a
set amount of shows in sequential order. It can just play the show
incrementally.

```
// The current index which the show is on
currentIndex : 0

// The max number of shows to be played
maxIndex : 3 || Shows.length

@param showIndex - the show in the Show array which is to be played
function playShow( int ){
  // Check to see if we are on the final show.
  if ( currentIndex < 3 ) currentIndex++;
  else this.end();

  var show = shows[ currentIndex ];
  
  var intro = show.intro,
      survivors = show.survivors;

  lightManager.turnOn();
  avManager.playIntroVideo( intro );
}

```

##AV Switch
The AV Switch component would listen for end events on the intro video
to communicate to the control computer that the video has ended.

```
qaController : QAController
videoController: VideoController

AVManager = {
  playIntroVideo: function( int ){},
  playQuestionAnswer: function( question, survivor ){}
}
```

##Auditorium Lights
The Auditorium Lights component is also a simple manager class which
listens for commands to control the lights. 

```
LightsManager = {
  turnOn: function(){},
  turnOff: function(){},
  dim: function( value ){}
}
```

##Computer A
The QA Controller would provide an API for a series of commands to
enable the selection of survivors and the playback of audio

```
QAController = {
  // @param - survivor - with a series of qa questions to play
  playQASession : function( survivor ){

  }
}
```


##Computer B
The Video Controller would expose an API to allow the playback of any
intro video. It would also send an event when play back has ended.

```
IntroVideoController = {
  playVideo: function( int ){
    
  }
}
```


###Questions

Are the questions selected based on the length of the intro video
beforehand? Or is that done programmatically? When you say 'multiple
survivors to choose from' is this a user action? It will impact the
length of the session.

## Selecting Arrangements, Tracks and Motifs

To control the playback arrangement, iMusic provides a selecting feature. To make it work, you should organize your music and connect the different musical elements to a specific "select-group".

### A basic example - horizantal strategy
Add two arrangements/sections and connect them to the same select-group. In this example we use the group "theme". Assign two different values to the different sections.

```XML

<?xml version="1.0" encoding="UTF-8"?>
<imusic version="1.0" tempo="60" timeSign="4/4" audioPath="audio">
	
    <arrangement select-group="theme" select-value="A" src="themeA" selected="true" />
    <arrangement select-group="theme" select-value="B" src="themeB" />		
	
</imusic>

```

In javascript you make a select-call, specifying group and value to select theme A or B.

```javascript

iMusic.select("theme", "B");

```


### Selecting tracks - vertical strategy
You can create multiple tracks and have them muted or unmuted depending on a select-group. You can have any number of different mute-groups (select-group) and assign any track to any value or values (just use comma separated values) to make complex structures responding to your environment.

This example shows an arrangement with four tracks, all assigned to the select-group "intensity". They are responding to different values causing them to replace each other when selected.

```XML

<?xml version="1.0" encoding="UTF-8"?>
<imusic version="1.0" tempo="60" timeSign="4/4" audioPath="audio">

    <arrangement>
        <track select-group="intensity" select-value="1" src="int1" selected="true" />
        <track select-group="intensity" select-value="2" src="int2" />
        <track select-group="intensity" select-value="3" src="int3" />
	<track select-group="intensity" select-value="4" src="int4" />	
    </arrangement>
  
</imusic>

```

In javascript you control the playback (muting and unmuting) by sending a select call:

```javascript

iMusic.select("intensity", "2");

```

### Motifs and selecting
Motifs follows their parent arrangement when select. I.e. Motifs are deselected if its parent arrangement is deselected. It can also react to its own select-group (like tracks). In the case above, we could therefor have matching motifs to the different intensity levels used for the track selection. Please remember, though, that Motifs do not auto play when selected (as tracks do) but wait for play-call (refering to its tag(s)):

```XML

<?xml version="1.0" encoding="UTF-8"?>
<imusic version="1.0" tempo="60" timeSign="4/4" audioPath="audio">

    <arrangement>
        <track select-group="intensity" select-value="1" src="int1" selected="true" />
        <track select-group="intensity" select-value="2" src="int2" />
        <track select-group="intensity" select-value="3" src="int3" />
	<track select-group="intensity" select-value="4" src="int4" />	
	    
	    
	<motif tags="motif1" select-group="intensity" select-value="1" src="motif1_1" />
        <motif tags="motif1" select-group="intensity" select-value="2" src="motif1_2" />
        <motif tags="motif1" select-group="intensity" select-value="3" src="motif1_3" />
        <motif tags="motif1" select-group="intensity" select-value="4" src="motif1_4" />
    </arrangement>
  
</imusic>

```

In javascript you control the playback setting by sending a select call, but for motifs you also have to call 'play' to trigger the Motif (in this case we refer to the tag "motif" set in XML)

```javascript

iMusic.select("intensity", "2");
iMusic.play("motif1");

```
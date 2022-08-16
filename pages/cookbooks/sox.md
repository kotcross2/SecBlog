
# sox cookbook 



## extract channels 

extract just left or right channel from a stereo file
```
sox input.wav out_left.wav remix 1
sox input.wav out_right.wav remix 2
```



## mono to stereo 

from two mono file to a single stereo file 
```
sox -M -c 1 left.wav -c 1 right.wav output.mp3 
```



## batch cut and fade out

sorry, this is for the `fish` shell: 
```
for x in *.wav 
	set base ( basename $x .wav ) 
	set base $base"_cut.wav"
	echo "$base"
	sox "$x" "$base" fade 0 0:01.6 0:00.2
	trash "$x"
end
``` 



## batch strip silence 

for recorded audio
```
sox infile.wav outfile.wav silence 1 0.1 1% 1 0.1 1%
```

for digital audio 
```
sox infile.wav outfile.wav silence 1 0.0 0% 1 0.0 0%

```

batch processing to the `trimmed/` folder (`fish` shell)
```
for x in *.wav 
	mkdir -p trimmed
	sox "$x" "trimmed/$x" silence 1 0.0 0% 1 0.1 0%
end

```



## batch processing for games

trims like before, and convert to .ogg, to folder `sfx`  
```
for x in *.wav 
	set base ( basename $x .wav ) 
	mkdir -p sfx 
	sox "$x" "sfx/$base.ogg" silence 1 0.0 0% 1 0.5 0%
end
```



## automagical chop

chops a wav file with silence between different hits
```
sox input.wav chop_n.wav silence 1 0.1 1% 1 0.1 1% 
		: newfile : restart
```

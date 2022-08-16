
# imagemagick cookbook 


## generic 

convert in place, all black to transparent
```
mogrify -transparent black *
```


## mirroring

horizontal mirroring
```
mogrify -flop *.png
```

vertical mirroring
```
mogrify -flip *.png
```


## texture atlas 

append to image horizontally (left to right)
```
convert +append *.png out_01.png
```
and vertically (top to bottom)
```
convert -append out_01.png out_02.png out_03.png tilemap.png
```
this is useful for texture atlas, last argument is output

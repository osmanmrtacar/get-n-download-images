# get-n-download-images

Get and download images, delete images with the specific size

//Search in directory and save to icons.txt
```python
grep -Eorh "(https?:)?//(yourwebsite)\S+\.(jpg|png)" yourfolder youranotherfolder | sort -u > icons.txt
```

//download
```python
xargs -n 1 curl -O < icons.txt
```

//delete big images
```python
for F in *.jpg *.png; do
    identify "$F"
done | awk '{split($3,wh,/x/);} wh[1]>799 || wh[2]>799 {print $1}' | xargs rm
```

// move them
```python
for F in *.jpg *.png; do
    mv $F icons
done
```

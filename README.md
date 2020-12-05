# get-n-download-images

Get and download images, delete images with the specific size

//Search in directory and save to icons.txt
grep -Eorh "(https?:)?//(yourwebsite)\S+\.(jpg|png)" yourfolder youranotherfolder | sort -u > icons.txt

//download
xargs -n 1 curl -O < icons.txt

//delete big images
for F in *.jpg *.png; do
    identify "$F"
done | awk '{split($3,wh,/x/);} wh[1]>799 || wh[2]>799 {print $1}' | xargs rm

// move them
for F in *.jpg *.png; do
    mv $F icons
done

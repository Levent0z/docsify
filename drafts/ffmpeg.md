# FFMPEG

## Join Videos

Define the following functions and then tun `joinVideos`:

```bash
function escapeSingleQuotes() {
    echo $1 | sed "s/'/'\\\''/"
}

function joinVideos() 
{
    rm _files.tmp >/dev/null
    # For each *.MP4 file...
    for I in `find . -type f -name '*.MP4' | cut -d '/' -f 2`
    do 
        # Get creation date from the video
        declare DATE=`ffmpeg -i "$I" -hide_banner 2>&1 | grep creation_time | head -1 | cut -d ':' -f 2- | cut -d ' ' -f 2`
        declare ABSPATH=`escapeSingleQuotes "$PWD/$I"`
        # Append line that has "ISODATE file 'ABSOLUTEPATH'"
        echo "$DATE file '$ABSPATH'" >> _files.tmp
    done 
    # Sort by ISODATE, remove ISODATE for a file called join.txt acceptable to ffmpeg
    sort _files.tmp | cut -d ' ' -f 2- > join.txt
    cat join.txt

    read -p 'Continue joining files above? (y/n) ' RESP
    if [[ "$RESP" == 'y' ]]; then
        ffmpeg -safe 0 -f concat -i join.txt -c copy joined.mp4
    fi
}
```

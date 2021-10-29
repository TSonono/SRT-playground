# SRT relevant cli commands

## Listener

`./srt-live-transmit "srt://:1337?mode=listener" file://con > ./received.ts`

Will listen on port 1337 for an srt connection and dump received data to file
received.ts.

## Caller

### Source data from file

`cat <FILE> | ./srt-live-transmit file://con "srt://127.0.0.1:1337?mode=caller"`

### Source data from UDP stream

Start a UDP stream

`ffmpeg -re -stream_loop -1 -i
Big_Buck_Bunny_1080_10s_10MB.mp4 -c copy -f mpegts
'udp://0.0.0.0:12345?pkt_size=1316'`

Capture and send with SRT

`./srt-live-transmit udp://0.0.0.0:12345 "srt://127.0.0.1:1337?mode=caller"`
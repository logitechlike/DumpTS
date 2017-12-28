# What is DumpTS?
DumpTS is a simple utility tool to process TS/M2TS stream file, which will provide these kinds of features:

- Dump one elementary stream or PSI sections from m2ts/ts stream file
- Re-factor a TS/M2TS stream file in place
- Extract some elementary streams, and reconstruct a partial TS/M2TS file
- Show media information of elementary streams

# How to build?

Use VS2015 to open DumpTS.sln to build it

# How to run it?

*Usage: DumpTS.exe TSSourceFileName \[OPTION\]...*

|Option|Value|Description|
|:--|:----:|:--|
|**--output**||The output dumped file path|
|**--pid**|0Xhhhh|The PID of dumped stream|
|**--destpid**|0xhhhh|The PID of source stream will be placed with this PID|
|**--srcfmt**|ts, m2ts, tts|The source TS format, Including: ts, m2ts,if it is not specified, find the sync-word to decide it|
|**--outputfmt**|ts, m2ts, pes, es, wav, pcm|The destination dumped format, including: ts, m2ts, pes, es and so on|
|**--showpts**||Print the pts of every elementary stream packet|
|**--stream_id**|0xhh|The stream_id in PES header of dumped stream|
|**--stream_id_extension**|0xhh|The stream_id_extension in PES header of dumped stream|
|**--showinfo**||Print the media information of elementary stream, for example, stream type, audio sample rate, audio channel mapping, video resolution, frame-rate and so on|
|**--verbose**||Print more message in the intermediate process|
 
Here are some examples of command lines:  

```
DumpTS c:\\00001.m2ts --output=c:\\00001.hevc --pid=0x1011 --srcfmt=m2ts --outputfmt=es --showpts  
```
It will dump a hevc es stream with PID 0x1011 from the m2ts stream file: c:\\00001.m2ts, and print its print of every frame.

```
DumpTS C:\\test.ts --output=c:\\00001.m2ts --pid=0x100 --destpid=0x1011 --srcfmt=ts --outputfmt=m2ts  
```
It will re-factor the file: c:\\test.ts, and replace the PID 0x100 with 0x1011 in TS pack and PSI, and convert it to a m2ts

```
DumpTS C:\\00022.m2ts --output=c:\\00022.mlp --pid=0x1100 --srcfmt=m2ts --outputfmt=es 
--stream\_id\_extension=0x72  
```
It will dump a MLP sub-stream from C:\\00022.m2ts with the PID 0x1100 and stream\_id\_extension in PES: 0x72

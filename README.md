## A Light Weight Model for Active Speaker Detection

Before executing the code, you should download the arcface weight file from (https://1drv.ms/u/s!AhMqVPD44cDOhkPsOU2S_HFpY9dC) and place the weight file at: weight/model_ir_se50.pth.

How to execute:
If the video path is ./path_to_video/video.mp4, run the following command:

```
python Columbia_test.py --videoFolder ./path_to_video --videoName video
```

When you execute, the following files will be generated:

```
├── pyavi
│   ├── audio.wav (Audio from input video)
│   ├── video.avi (Copy of the input video)
│   ├── video_only.avi (Output video without audio)
│   └── video_out.avi  (Output video with audio)
├── pycrop (The detected face videos and audios)
│   ├── 000000.avi
│   ├── 000000.wav
│   ├── 000001.avi
│   ├── 000001.wav
│   └── ...
├── pyframes (All the video frames in this video)
│   ├── 000001.jpg
│   ├── 000002.jpg
│   └── ...	
└── pywork
    ├── faces.pckl (face detection result)
    ├── scene.pckl (scene detection result)
    ├── scores.pckl (ASD result)
    ├── tracks.pckl (face tracking result)
    └── identity_result.pckl (identity result)
```

scores.pckl have the following format:
```
[
  [
    # for track 1
    Talking score for frame 1,
    Talking score for frame 2, 
    …

    Talking score for frame T_1,
  ], [
    # for track 2
    Talking score for frame 1,
    Talking score for frame 2, 
    …

    Talking score for frame T_1,
  ],
  …
]

```
The talking score is between 0 and 1. The higher the score, the more likely the person is talking.

The identity_result.pckl have the following format:
```
[
  Face Id number of track 1,
  Face Id number of track 2,
  …
  Face Id number of track N,
]
```


The tracks.pckl have the following format:
```
[
  {
    # for track 1
    ‘bbox’ : [
        bbox for track 1 frame n_start,
        …
        bbox for track 1 frame n_end,
    ]
    ‘frame’: [
      track 1 frame number n_start,
      …
      track 1 frame number n_end,
    ]

  }, 
  … # track 1, …, N
]
```
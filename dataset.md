---
layout: page
title: The Dataset
description: >
  Summary of the dataset
hide_description: true
sitemap: false
---

1. this ordered seed list will be replaced by the toc
{:toc}

The HD-EPIC dataset contains diverse and dense annotations, which we detail here. 

## Recipe steps and ingredients

![Full-width image](/assets/img/dataset/prep_stepv5.jpg){:.lead width="1020" loading="lazy"}
For the "Carbonara" recipe, we visualise the prep and step time segments for three consecutive steps (left), along with sample frames with corresponding action narrations (top). The interleaving of different preps/steps is evident in the annotations 
{:.figcaption}

Our videos are distinct from short recipe videos found online, which are typically trimmed to only crucial steps, and often edited further or sped up. Videos in HD-EPIC include a wider range of recipe-relevant activities, such as fetching or prepping ingredients. To comprehensively annotate these videos, we introduce prep and step pairs. We also annotate weighing and adding temporal segments which enables monitoring the nutrition of the full dish as ingredients are incorporated.

## Fine-grained actions

![Full-width image](/assets/img/dataset/verb_noun_distribution4.png){:.lead width="1020" loading="lazy"}

Frequency of verb clusters (top) and noun clusters (bottom) in narrated sentences by category, shown on a logarithmic scale.
{:.figcaption}

### Transcriptions

We automatically transcribe and manually check and correct all audio narrations provided by participants, to obtain detailed action descriptions.

### Action boundaries

For all narrations, we label precise start and end times. In total, we obtain segments for 59,454 actions, with a mean duration of 2.0s (±3.4s).

### Parsing and clustering

We parse <span style="background-color: #dbb3ff">verbs</span>, <span style="background-color: #75d7b9">nouns</span> and <span style="background-color: #9acefe">hands</span> from open vocabulary narrations so they can be used for closed vocabulary tasks, such as action recognition. We also extract <span style="background-color: #f9a3cd">how</span> and <span style="background-color: #faad9e">why</span> clauses from 16,004 and 11,540 narrations, respectively. For example: 

> <span style="background-color: #dbb3ff">Turn</span> the <span style="background-color: #75d7b9">salt container</span> <span style="background-color: #f9a3cd">clockwise by pushing it</span> with my <span style="background-color: #9acefe">left hand</span> <span style="background-color: #faad9e">so that the lid is aligned with the container opening</span>".

### Sound annotations

We collect audio annotations. These capture start-end times of audio events along with a class name (e.g. "click", "rustle", "metal-plastic collision", "running water"). Overall, we have 50,968 audio annotations from 44 classes.

## Digital twin: Scene & Object Movements

![Full-width image](/assets/img/dataset/blender.jpg){:.lead width="1020" loading="lazy"}

Digital Twin: from point cloud (left), to surfaces (middle) and labelled fixtures (right). We show two moved objects (masks on top) at fixtures: cheese and pan.
{:.figcaption}

### Scene 

![Full-width image](/assets/img/dataset/all_fixtures.jpg){:.lead width="1020" loading="lazy"}

All kitchens with their fixture annotations (coloured randomly).
{:.figcaption}

We create digital copies of participants kitchens by reconstructing the surfaces and manually curating every fixture (e.g. cupboard, drawer), storage space (e.g. shelves, hooks) and large appliance (e.g. fridge, microwave). This is distinct from digital twins that rely on known environments with replicas. Our digital twin is created in [Blender](https://www.blender.org/) on top of the multi-video SLAM point clouds from recordings. Each kitchen contains an average of 44.9 labelled fixtures (min 32, max 58), including 11.1 counters/surfaces, 11.8 cupboards, 7.7 drawers and 3.3 appliances. We associate narrations which describe scene interactions with the annotated fixtures. 

### Hand Masks

We annotate a handful of frames per video for both hands. Frames are selected to cover various actions and kitchen locations. We use these to automatically segment, and manually correct a selected subset. In total, our dataset contains 7.7M hand masks: 3.9M right (87.2% of frames) and 3.8M left (85.6%).

### Moving Objects in 2D

To generate 3D object movement annotations, we first annotate when objects move. Annotators labelled a temporal segment each time an object is moved until it is set/put down, along with 2D bounding boxes of the object at the onset and end of motion. Tracks are annotated even for slight shifts/pushes, and thus these offer a full annotation of all object movements. Overall, we collected 19.9K object movement tracks and 36.9K bounding boxes. We label an average of 9.2 objects taken and 9.0 objects placed per minute. On average, tracks are 9.0s long, the longest is 461.5s.

### Object Masks

We obtain pixel-level segmentations from each bounding box by initialising with iterative [SAM2](https://github.com/facebookresearch/sam2) then manually correcting. Annotators corrected 74% of masks; the IoU between SAM2 and the manual masks is 0.82.

### Masks to 3D

We lift object masks to 3D using dense depth estimates and 2D-to-3D sparse correspondences provided by [MPS](https://facebookresearch.github.io/projectaria_tools/docs/ARK/mps).

### 3D Object Motion

Objects move 61.4cm (±84.5cm) on average, 27.6% move ≤ 10cm, while 7.6% move ≥ 2m.

### Object-Scene Interactions

With the 3D object locations, we associate locations with the closest fixture. We manually verify assignments and find the accuracy is 98%. On average objects move between 1.8 different fixtures per video.

### Priming Object Movement

![Full-width image](/assets/img/dataset/prime_figure.png){:.lead loading="lazy"}

Priming Object Interaction Through Gaze. Top: Camera position with projected eye-gaze and object positions in 3D. Middle: 2D gaze location. Bottom: Timeline for priming object movement e.g. the glass is primed 8.3s before taking 
{:.figcaption}

We combine eye-gaze and 3D object locations, to find when an object is primed, i.e. the moment in time when the gaze attends to the object's location before picking it up (pick-up priming) or when the gaze attends to the future location of an object before it's put down (put-down priming). We calculate the priming time for all objects, excluding those taking or placed off screen. Of those objects feasible for priming, 94.8% are primed, an average of 4.0s before being picked up, compared to 88.5% primed an average of 2.6s before being placed.

### Long Term Object Tracking

We connect object movements and form longer trajectories, i.e. object itineraries, to capture sequences of an object's movement. Our efficient pipeline utilises our lifted 3D locations and allows annotating a 1-hour long video in minute.

## Density

| Annotation Type                                                 | Total annotations | Annotations/min |
|-----------------------------------------------------------------|:-----------------:|:---------------:|
| Narrations                                                      |       59,454      |       24.0      |
| Parsing (Verbs + Nouns  + Hands + How + Why)                    |      303,968      |      122.7      |
| Recipes (Preps + Steps)                                         |       2,489       |       1.0       |
| Sound                                                           |       50,968      |       20.6      |
| Action boundaries                                               |       59,454      |       24.0      |
| Object Motion (Pick up + Put down  + Fixtures + Bboxes + Masks) |      153,480      |       62.0      |
| Object Itinerary                                                |       4,881       |       2.0       |
| Object Priming (Starts + Ends)                                  |       18,264      |       7.4       |
| Total                                                           |                   |      263.2      |

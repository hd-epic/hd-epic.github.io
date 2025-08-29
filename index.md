---
layout: plain
title: "<img src='/assets/img/hd-epic-logo-light.png' style='float: left; width: 100px; margin-right:15px'>HD-EPIC: A Highly-Detailed Egocentric Video Dataset"
no_link_title: false 
no_excerpt: false 
hide_image: false
cover: true
---

![Full-width image](/assets/img/opening_loop_cropped.gif){:.lead width="1020" loading="lazy" loop}

## News

- **June 2025**: VQA Challenge results are announced! [Check here](#vqa-challenge).
- **May 2025**: Eye-Gaze Priming data has now been released! [Annotations link](https://github.com/hd-epic/hd-epic-annotations)
- **April 2025**: VQA Challenge Benchmark is online now! [Challenge link](https://codalab.lisn.upsaclay.fr/competitions/22006).
- **April 2025**: Masks and object association annotations have now been released.
- **Feb 2025**: **[HD-EPIC](https://arxiv.org/abs/2502.04144)** accepted at **CVPR 2025**!

<br>

![Full-width image](/assets/img/dataset/diversity.png){:.lead width="1020" loading="lazy"}
Diversity in HD-EPIC, which is filmed over 3 days in-the-wild, resulting in many objects, activities and recipes.
{:.figcaption}

## Recipe steps and ingredients

![Full-width image](/assets/img/dataset/prep_stepv5.jpg){:.lead width="1020" loading="lazy"}
For the "Carbonara" recipe, we visualise the prep and step time segments for three consecutive steps (left), along with sample frames with corresponding action narrations (top). The interleaving of different preps/steps is evident in the annotations 
{:.figcaption}

Unlike typical **short recipe videos**, which are **trimmed, edited, or sped up**, HD-EPIC captures a **broader range of real-world cooking activities**, including:  

- **Fetching ingredients**  
- **Prepping ingredients**  
- **Weighing & adding ingredients** (for full nutritional tracking)  

To fully capture recipes, we introduce:  
- **Prep & Step Pairs**: Detailed segmentation of preparation and execution.  
- **Temporal Ingredient Tracking**: Enables monitoring of nutrition as ingredients are added.  


## Fine-grained actions

![Full-width image](/assets/img/dataset/verb_noun_distribution4.png){:.lead width="1020" loading="lazy"}

Frequency of verb clusters (top) and noun clusters (bottom) in narrated sentences by category, shown on a logarithmic scale.
{:.figcaption}

- **Transcriptions**: We automatically transcribe and manually check and correct all audio narrations provided by participants, to obtain detailed action descriptions.

- **Action boundaries**: For all narrations, we label precise start and end times. In total, we obtain segments for 59,454 actions, with a mean duration of 2.0s (±3.4s).

- **Parsing and clustering**: We parse verbs, nouns, and hands from open vocabulary narrations so they can be used for closed vocabulary tasks, such as action recognition. We also extract how and why clauses from 16,004 and 11,540 narrations, respectively. For example:

> Turn the salt container clockwise by pushing it with my left hand so that the lid is aligned with the container opening.

- **Sound annotations**: We collect audio annotations. These capture start-end times of audio events along with a class name (e.g. "click", "rustle", "metal-plastic collision", "running water"). Overall, we have 50,968 audio annotations from 44 classes.

## Digital twin: Scene & Object Movements

<!-- ![image](/assets/img/dataset/blender.jpg){:.lead width="125" loading="lazy"} -->
<!-- <img src="/assets/img/dataset/blender.jpg" alt="image" width="960" loading="lazy"> -->
<img src="/assets/img/dataset/blender.jpg" 
     alt="image" 
     width="800" 
     loading="lazy" 
     style="display: block; margin: auto; max-width: 100%; height: auto;">



Digital Twin: from point cloud (left), to surfaces (middle) and labelled fixtures (right). We show two moved objects (masks on top) at fixtures: cheese and pan.
{:.figcaption}

We reconstruct **digital copies of participants' kitchens**, manually curating:  

- **Surfaces**  
- **Fixtures** (e.g., cupboards, drawers)  
- **Storage spaces** (e.g., shelves, hooks)  
- **Large appliances** (e.g., fridge, microwave)

<!-- ### Key Differences   -->
Unlike digital twins based on **predefined replicas**, our reconstructions are **built from real environments** using:  

- **Multi-video SLAM point clouds** from recordings  
- **Manual curation in [Blender](https://www.blender.org/)**  

### Scene 

![Full-width image](/assets/img/dataset/all_fixtures.jpg){:.lead width="1020" loading="lazy"}

All kitchens with their fixture annotations (coloured randomly).
{:.figcaption}

Each kitchen contains an average of **44.9 labeled fixtures** (*min: 32, max: 58*):  
- **11.1** counters/surfaces  
- **11.8** cupboards  
- **7.7** drawers  
- **3.3** appliances  

We also **associate narrations** with annotated fixtures to describe scene interactions.  

**Hand Mask Annotations**:
We annotate **a subset of frames per video** for **both hands**, ensuring coverage across:  **Various actions** and **Different kitchen locations**.
Segmentation Process is **automatic** with manual correction for a selected subset. We have **7.7M total hand masks** in total.

### 3D Object Movement Annotations

We annotate **object movements** by labeling **Temporal segments** from pick-up to placement and **2D bounding boxes** at movement onset and end. Tracks include **even slight shifts/pushes**, ensuring full coverage of movements. **Every object movement is annotated**, providing a rich dataset for analysis.  

**Statistics**:<br>
- **19.9K object movement tracks**  
- **36.9K bounding boxes**  
- **9.2 objects taken per minute** *(on average)*  
- **9.0 objects placed per minute** *(on average)*  
- **Average track length**: **9.0s** *(max: 461.5s)*  

**Object Masks**:
We generate **pixel-level segmentations** from each bounding box by **Initializing with iterative [SAM2](https://github.com/facebookresearch/sam2)** and **Manually correcting the masks**. During this process, **74% of masks** were manually corrected and **IoU between SAM2 and manual masks**: **0.82**. Finally, We lift object masks to 3D using dense depth estimates and 2D-to-3D sparse correspondences provided by [MPS](https://facebookresearch.github.io/projectaria_tools/docs/ARK/mps).

**Object-Scene Interactions**:
With the 3D object locations, we associate locations with the closest fixture. We manually verify assignments and find the accuracy is 98%. On average objects move between 1.8 different fixtures per video.

### Priming Object Movement

<img src="/assets/img/dataset/prime_figure.png" 
     alt="image" 
     width="960" 
     loading="lazy" 
     style="display: block; margin: auto; max-width: 100%; height: auto;">

Priming Object Interaction Through Gaze. Top: Camera position with projected eye-gaze and object positions in 3D. Middle: 2D gaze location. Bottom: Timeline for priming object movement e.g. the glass is primed 8.3s before taking 
{:.figcaption}

We combine **eye-gaze** and **3D object locations** to detect when an object is **primed**. **Pick-up priming**: Gaze attends to an object **before picking it up**. **Put-down priming**: Gaze attends to the **future location before placement**.
This **Excludes objects taken/placed off-screen**. **94.8% of feasible objects** are **primed** **4.0s before pick-up** and **88.5% of feasible objects** are **primed** **2.6s before placement**.

**Long Term Object Tracking**:
We connect object movements and form longer trajectories, i.e. object itineraries, to capture sequences of an object's movement. Our efficient pipeline utilises our lifted 3D locations and allows annotating a 1-hour long video in minute.

## Annotation Density in HD-EPIC

| Annotation Type                                                 | Total annotations | Annotations/min |
|-----------------------------------------------------------------|:-----------------:|:---------------:|
| Narrations                                                      |       59,454      |       24.0      |
| Parsing (Verbs + Nouns  + Hands + How + Why)                    |      303,968      |      122.7      |
| Recipes (Preps + Steps)                                         |       4,052       |       1.6       |
| Sound                                                           |       50,968      |       20.6      |
| Action boundaries                                               |       59,454      |       24.0      |
| Object Motion (Pick up + Put down  + Fixtures + Bboxes + Masks) |      153,480      |       62.0      |
| Object Itinerary                                                |       4,881       |       2.0       |
| Object Priming (Starts + Ends)                                  |       18,264      |       7.4       |
| Total                                                           |                   |      263.2      |


# VQA Benchmark

**VQA Challenge @ CVPR 2025**: Challenge link: [CodaLab](https://codalab.lisn.upsaclay.fr/competitions/22006) <br> Deadline: **27th May 2025**. The deadline to submit report is **30th May** (11:55 PM AoE).<br> Results will be announced at the [Second Joint Egocentric Vision (EgoVis) Workshop](https://egovis.github.io/cvpr25) at CVPR 2025 on 12th June.

The VQA Challenge is closed now! Here are the winners of the challenge:
![Full-width image](/assets/img/dataset/hd_epic_2025_winners.png){:.lead width="1020" loading="lazy"}

### Winner Reports

| Team Number | Report Link |
|-------------|-------------|
| 1 | [Team 1](/assets/reports/2025/HD-EPIC-R1.pdf) |
| 2 | [Team 2](/assets/reports/2025/HD-EPIC-R2.pdf) |
| 3 | [Team 3](/assets/reports/2025/HD-EPIC-R3.pdf) |


## Benchmark creation

We construct a **VQA benchmark** leveraging the dense annotations in our dataset, covering **7 key annotation types**:  

### **VQA Question Types**  
1. **Recipe** – Identify, retrieve, and localize recipes and steps.  
2. **Ingredient** – Track ingredient usage, weight, timing, and order.  
3. **Nutrition** – Analyze ingredient nutrition and its evolution in recipes.  
4. **Fine-Grained Action** – Understand the **what, how, and why** of actions.  
5. **3D Perception** – Reason about object positions in **3D space**.  
6. **Object Motion** – Track object movements across **long video sequences**.  
7. **Gaze** – Estimate fixation points and anticipate future interactions.  

### **Benchmark Structure**  
- **5-way multiple choice** for each question type  
- **30 question prototypes**, generating **26,650 multiple-choice questions**  
- **Hard negatives** sampled from the dataset for increased difficulty  

### **Scalability & Impact**  
- One of the **largest VQA video benchmarks**, yet **tractable for closed-source VLMs**  
- Estimated **upper bound of 100,000 unique questions** due to annotation density  


<!-- We take the dense output of our annotation pipeline and construct a comprehensive VQA benchmark around 7 types of annotations:

1. **Recipe**. Questions on temporally localising, retrieving, or recognising recipes and their steps.
2. **Ingredient**. Questions on the ingredients used, their weight, their adding time and order.
3. **Nutrition**. Questions on nutrition of ingredients and nutritional changes as ingredients are added to recipes.
4. **Fine-grained action**. What, how, and why of actions and their temporal localisation.
5. **3D perception**. Questions that require the understanding of relative positions of objects in the 3D scene.
6. **Object motion**. Questions on where, when and how many times objects are moved across long videos.
7. **Gaze**. Questions on estimating the fixation on large landmarks and anticipating future object interactions.

For each question type, we define prototypes to sample questions, correct answers, and strong negatives from our annotations. Each question prototype is 5-way multiple choice. We generate hard negatives for prototypes by sampling within the dataset for difficult answers. In total, we have 30 prototypes, and generate 26,650 multiple-choice questions. This makes it one of the largest VQA video benchmarks, but keeps it tractable particularly to evaluate closed-source VLMs. Due to the density of our annotations, we estimate an upper bound of 100,000 possible unique questions with this set of prototypes. -->

<br>

<img src="/assets/img/dataset/q_pie_with_dist.png" 
     alt="image" 
     width="800" 
     loading="lazy" 
     style="display: block; margin: auto; max-width: 100%; height: auto;">

VQA Question Prototypes. We show our 30 question prototypes by category alongside the number of questions. Outer bars indicate the distribution over input lengths for each question.
{:.figcaption}

### **VQA Challenge**

We are hosting the **VQA Challenge** to evaluate the performance of VLMs on our benchmark. The challenge will be hosted on [CodaLab](https://codalab.lisn.upsaclay.fr/competitions/22006) and will include a leaderboard for tracking progress. The challenge will be open to all participants, and we encourage everyone to submit their results.
The challenge leaderboard closes on **27th May 2025**. The deadline to submit report is **30th May** (11:55 PM AoE).

The results with be announced in the [Second Joint Egocentric Vision (EgoVis) Workshop](https://egovis.github.io/cvpr25) at CVPR 2025 on 12th June.

The VQA Challenge is closed now! Here are the winners of the challenge:
![Full-width image](/assets/img/dataset/hd_epic_2025_winners.png){:.lead width="1020" loading="lazy"}

## VLM models

We use 4 representative models as baselines:
- [Llama 3.2 90B](https://www.llama.com/llama-downloads). We use this as a strong open-source text-only baseline, as LLMs can perform well on visual QA benchmarks without any visual input.
- [VideoLlama 2 7B](https://github.com/DAMO-NLP-SG/Video-LLaMA). Strong open-source short context model.
- [LongVA](https://github.com/EvolvingLMMs-Lab/LongVA). Longest context open-source model.
- [Gemini Pro](https://deepmind.google/technologies/gemini/pro/). Closed source, longest context of any model, and state-of-the-art on long-video.

<!-- ## Results

| Model                     | Recipe | Ingredient | Nutrition | Action |  3D  | Motion | Gaze | Avg. |
|:--------------------------|:------:|:----------:|:---------:|:------:|:----:|:------:|:----:|:----:|
| **Blind – language only** |        |            |           |        |      |        |      |      |
| Llama 3.2                 |  28.4  |    26.8    |    26.7   |  23.3  | 26.6 |   24   | 19.2 |  25  |
| Gemini Pro                |  29.5  |    31.2    |     23    |  22.1  | 30.5 |  25.3  | 22.7 | 26.3 |
| **Video-Language**        |        |            |           |        |      |        |      |      |
| VideoLlama 2              |   25   |    26.7    |     30    |  27.2  | 24.1 |  24.5  | 23.6 | 25.9 |
| LongVA                    |   22   |     30     |     31    |  28.9  | 30.4 |  24.4  | 24.1 | 27.3 |
| Gemini Pro                |  53.4  |     44     |     35    |  39.6  | 31.6 |   23   | 32.8 |  37  |
{:.stretch-table}

VQA Results per Category (% Acc.). Our VQA benchmark cannot be solved blind or by external knowledge and is a challenge for state-of-the-art video VLM models.
{:.figcaption}

The table above provides overall and per-category accuracy averaged over the prototype results. Both language-only models only achieve 25% and 26.3%, only 6.3% above random. Open-source video VLMs VideoLlama and LongVA perform similarly (25.9% and 27.3%) but have different strengths. For example, Llama is better at ordering ingredients, while the video is necessary to get above random performance on action recognition and gaze estimation. Gemini achieves the best performance, particularly for Recipe and Nutrition where external knowledge can be helpful. However, the average performance (37.0%) shows the challenge posed by our VQA benchmark.

<br> -->

![Full-width image](/assets/img/dataset/results_per_prototype.png){:.lead width="1020" loading="lazy"}

VQA Results per Question Prototype. Our benchmark contains many challenging questions for current models.
{:.figcaption}

![Full-width image](/assets/img/dataset/qual_res_v13.jpg){:.lead width="1020" loading="lazy"}

VQA Qualitative Results. We mark ground truth answers with a green background, and predictions from different models, i.e., LLaMA 3.2, VideoLLaMA 2, LongVA, Gemini Pro, with coloured dots alongside the corresponding prediction.
{:.figcaption}

<!-- ### Common Failures

In Recipe, models struggle when steps have common objects or actions. In Ingredient, models guess weights (readable from the scale by humans) poorly, also causing errors in Nutrition. Fine-grained action is hard when answers share nouns. In Gaze, models just select recently moved objects. Confusion in 3D and Object motion occurs with directions (right/left) and fixtures (counters/drawers). -->

# Download

<!-- **Early Access Data available here**: <a href="https://uob-my.sharepoint.com/:f:/g/personal/xy23932_bristol_ac_uk/Er39VjjlqKJFkNXp_tYdDaYBq-AOYKDouLM-Ph2X9M3Djw?e=v6EfVB">OneDrive</a><br> -->
**Dataset Link**: <a href="https://data.bris.ac.uk/data/dataset/3cqb5b81wk2dc2379fx1mrxh47">Link</a>.<br>

**Alternate Download Link** (without VRS files): [OneDrive](https://uob-my.sharepoint.com/:f:/g/personal/wq23021_bristol_ac_uk/EjQ8vBREuZ9Bk6X8nbnqJm0Bj-7MWvSBNdUxYJZjgxIZ3Q?e=XLveBB)

**Note**: The link above contains the following files:
- Audio-HDF5: 27 GB
- Digital-Twin: 1.35 GB
- Hands-Masks: 1.95 GB
- SLAM-and-Gaze: 349 GB
- VRS: 1.9 TB
- Videos (mp4): 115.5 GB

VRS files consume large storage space, so, you can only download the videos.
[This Github repo](https://github.com/hd-epic/hd-epic-downloader) offers a python script to download various parts of the dataset.<br>
<!-- [This Github repo](https://github.com/epic-kitchens/epic-kitchens-download-scripts) is used for EPIC-KITCHENS but can be tailored if needed to download the dataset -- we do not offer a direct download script at the moment.<br> -->
**Download Annotations**: <a href="https://github.com/hd-epic/hd-epic-annotations">GitHub</a>; [Download Tool](https://github.com/hd-epic/hd-epic-downloader)<br>
**Paper**: <a href="https://arxiv.org/abs/2502.04144">arXiv</a><br>

### ![image](/assets/img/copyright.png) Copyright

All datasets and benchmarks on this page are copyright by us and published under the [Creative Commons Attribution-NonCommercial 4.0 International](https://creativecommons.org/licenses/by-nc/4.0/) License. This means that you must give appropriate credit, provide a link to the license, and indicate if changes were made. You may do so in any reasonable manner, but not in any way that suggests the licensor endorses you or your use. You may not use the material for commercial purposes.

For commercial licenses of EPIC-KITCHENS and any of its annotations, email us at [uob-epic-kitchens@bristol.ac.uk](mailto:uob-epic-kitchens@bristol.ac.uk).

<h4>Disclaimer</h4>

HD-EPIC dataset was collected as a tool for research in computer vision. The dataset may have unintended biases (including those of a societal, gender or racial nature).

## BibTeX

Cite our paper if you find the [HD-EPIC dataset](https://arxiv.org/abs/2502.04144) useful for your research:
```{bibliography}
@InProceedings{perrett2025hdepic,
  author    = {Perrett, Toby and Darkhalil, Ahmad and Sinha, Saptarshi and Emara, Omar and Pollard, Sam and Parida, Kranti and Liu, Kaiting and Gatti, Prajwal and Bansal, Siddhant and Flanagan, Kevin and Chalk, Jacob and Zhu, Zhifan and Guerrier, Rhodri and Abdelazim, Fahd and Zhu, Bin and Moltisanti, Davide and Wray, Michael and Doughty, Hazel and Damen, Dima},
  title     = {HD-EPIC: A Highly-Detailed Egocentric Video Dataset},
  booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
  year      = {2025},
  month     = {June}
}
```

# Team

<table>
<tr>
    <td style="background:transparent; text-align:center"><img class="logo-picture" src="/assets/img/bristol_logo.jpg"></td>
    <td style="background:transparent; text-align:center"><img class="logo-picture" src="/assets/img/leiden_logo.png"></td>
    <td style="background:transparent; text-align:center"><img class="logo-picture" src="/assets/img/sing_man_logo.png"></td>
    <td style="background:transparent; text-align:center"><img class="logo-picture" src="/assets/img/bath_logo.png"></td>
</tr>
</table>
{:.stretch-table}
    
<table>
<tr>
    <td><img class="profile-picture" src="/assets/img/authors/toby.jpg"></td>
    <td><a href="https://tobyperrett.github.io/">Toby<br>Perrett</a></td>
    <td>University of Bristol</td>
    <td><img class="profile-picture" src="/assets/img/authors/ahmad.jpg"></td>
    <td><a href="https://ahmaddarkhalil.github.io">Ahmad<br>Darkhalil</a></td>
    <td>University of Bristol</td>
    <td><img class="profile-picture" src="/assets/img/authors/saptarshi.jpg"></td>
    <td><a href="https://sinhasaptarshi.github.io/">Saptarshi<br>Sinha</a></td>
    <td>University of Bristol</td>
</tr>
<tr>
    <td><img class="profile-picture" src="/assets/img/authors/omar.png"></td>
    <td><a href="https://omar-emara.github.io/">Omar<br>Emara</a></td>
    <td>University of Bristol</td>
    <td><img class="profile-picture" src="/assets/img/authors/sam.jpg"></td>
    <td><a href="https://sjpollard.github.io/">Sam<br>Pollard</a></td>
    <td>University of Bristol</td>
    <td><img class="profile-picture" src="/assets/img/authors/kranti.jpg"></td>
    <td><a href="https://krantiparida.github.io/">Kranti<br>Kumar Parida</a></td>
    <td>University of Bristol</td>
</tr>
<tr>
    <td><img class="profile-picture" src="/assets/img/authors/kaiting.jpg"></td>
    <td>Kaiting<br>Liu</td>
    <td>Leiden University</td>
    <td><img class="profile-picture" src="/assets/img/authors/prajwal.jpg"></td>
    <td><a href="https://prajwalgatti.github.io/">Prajwal<br>Gatti</a></td>
    <td>University of Bristol</td>
    <td><img class="profile-picture" src="/assets/img/authors/siddhant.jpg"></td>
    <td><a href="https://sid2697.github.io/">Siddhant<br>Bansal</a></td>
    <td>University of Bristol</td>
</tr>
<tr>
    <td><img class="profile-picture" src="/assets/img/authors/kevin.jpg"></td>
    <td><a href="https://keflanagan.github.io/">Kevin<br>Flanagan</a></td>
    <td>University of Bristol</td>
    <td><img class="profile-picture" src="/assets/img/authors/jacob.jpg"></td>
    <td><a href="https://jacobchalk.github.io/">Jacob<br>Chalk</a></td>
    <td>University of Bristol</td>
    <td><img class="profile-picture" src="/assets/img/authors/zhifan.jpg"></td>
    <td><a href="https://zhifanzhu.github.io/">Zhifan<br>Zhu</a></td>
    <td>University of Bristol</td>
</tr>
<tr>
    <td><img class="profile-picture" src="/assets/img/authors/rhodri.jpg"></td>
    <td>Rhodri<br>Guerrier</td>
    <td>University of Bristol</td>
    <td><img class="profile-picture" src="/assets/img/authors/fahd.jpg"></td>
    <td>Fahd<br>Abdelazim</td>
    <td>University of Bristol</td>
    <td><img class="profile-picture" src="/assets/img/authors/bin.jpg"></td>
    <td><a href="https://binzhubz.github.io/">Bin<br>Zhu</a></td>
    <td>Singapore Management University</td>
</tr>
<tr>
    <td><img class="profile-picture" src="/assets/img/authors/davide.jpg"></td>
    <td><a href="https://www.davidemoltisanti.com/research">Davide<br>Moltisanti</a></td>
    <td>University of Bath</td>
    <td><img class="profile-picture" src="/assets/img/authors/mike.jpg"></td>
    <td><a href="https://mwray.github.io/">Michael<br>Wray</a></td>
    <td>University of Bristol</td>
    <td><img class="profile-picture" src="/assets/img/authors/hazel.png"></td>
    <td><a href="https://hazeldoughty.github.io/">Hazel<br>Doughty</a></td>
    <td>Leiden University</td>
</tr>
<tr>
    <td></td><td></td><td></td>
    <td><img class="profile-picture" src="/assets/img/authors/dima.jpg"></td>
    <td><a href="https://dimadamen.github.io/">Dima<br>Damen</a></td>
    <td>University of Bristol</td>
</tr>
</table>
{:.stretch-table}

## Acknowledgements

The project was supported by a uncharitable donation from Meta (Aria Project Partnership) to the University of Bristol. Gemini Pro results are supported by a research credits grant from Google DeepMind. 

Research at Bristol is supported by EPSRC Fellowship UMPIRE (EP/T004991/1), EPSRC Program Grant Visual AI (EP/T028572/1) and EPSRC Doctoral Training Program. 

Research at Leiden is supported by the Dutch Research Council. (NWO) under a Veni grant (VI.Veni.222.160). 

Research at Singapore is supported by Singapore Ministry of Education (MOE) Academic Research Fund (AcRF) Tier 1 grant (No. MSS23C018).

We thank Rajan from Elancer and his team, for their huge assistance with temporal and audio annotation. We thank Srdjan Delic and his team for their assistance with mask annotations and object associations. We also thank Owen Tyley for the 3D Digital Twin of the kitchen environments using Blender. We thank David Fouhey and Evangelos Kazakos for early feedback on the project. We thank Pierre Moulon, Vijay Baiyya and Cheng Peng from the Aria team for technical assistance in using the MPS code and services. 

We acknowledge the usage of Ismbard AI Phase 1 and EPSRC Tier-2 Jade clusters.

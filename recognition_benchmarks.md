---
layout: page
title: Recognition Benchmarks
description: >
  Recognition benchmarks
hide_description: true
sitemap: false
---

1. this ordered seed list will be replaced by the toc
{:toc}

## Action Recognition

| Model           | Modality | Verb | Noun | Action | Unseen |
|:----------------|:-------- |:----:|:----:|:------:|:------:|
| Chance          |     -    | 10.9 |  1.8 |    0   |    -   |
| [SlowFast](https://openaccess.thecvf.com/content_ICCV_2019/papers/Feichtenhofer_SlowFast_Networks_for_Video_Recognition_ICCV_2019_paper.pdf)           |     Video    | 29.2 | 10.6 |   5.3  |   29   |
| [Omnivore](https://openaccess.thecvf.com/content/CVPR2022/papers/Girdhar_Omnivore_A_Single_Model_for_Many_Visual_Modalities_CVPR_2022_paper.pdf)       |     Video    | 19.5 | 17.1 |   8.7  |  28.7  |
| [MotionFormer-HR](https://proceedings.neurips.cc/paper/2021/file/67f7fb873eaf29526a11a9b7ac33bfac-Paper.pdf)                                           |     Video    | 35.7 |  20  |  10.2  |  32.2  |
| [VideoMAE-L](https://proceedings.neurips.cc/paper_files/paper/2022/file/416f9cb3276121c42eebb86352a4354a-Paper-Conference.pdf)                         |     Video    | 47.5 | 29.4 |  17.9  |  29.3  |
| [TIM](https://openaccess.thecvf.com/content/CVPR2024/papers/Chalk_TIM_A_Time_Interval_Machine_for_Audio-Visual_Action_Recognition_CVPR_2024_paper.pdf) |     Video + audio   | 51.3 | 36.1 |  23.4  |  44.6  |
| [TIM](https://openaccess.thecvf.com/content/CVPR2024/papers/Chalk_TIM_A_Time_Interval_Machine_for_Audio-Visual_Action_Recognition_CVPR_2024_paper.pdf) |     Video    | 51.2 | 36.5 |  23.9  |  44.4  |
{:.stretch-table}

Action Recognition Benchmark (% Acc.). HD-EPIC provides a significant challenge for state-of-the-art models.
{:.figcaption}

We assess 5 action recognition methods, using publicly available checkpoints fine-tuned on [EPIC-KITCHENS-100](https://epic-kitchens.github.io/). Results are shown above. Best performance on HD-EPIC is only 51% for verbs, 37% for nouns and 24% for actions leaving plenty of room for improvement.

## Sound Recognition

| Model  | Modality      | Top-1 | Top-5 | mCA  | mAP  | mAUC  |
|:-------|:--------------|:-----:|:-----:|:----:|:----:|:-----:|
| Chance | -             | 6.9   | 29.4  | 2.2  | 2.3  | 0.5   |
| [SSAST](https://cdn.aaai.org/ojs/21315/21315-13-25328-1-2-20220628.pdf)  | Audio         | 25.1  | 59.8  | 10.8 | 13.5 | 0.748 |
| [TIM](https://openaccess.thecvf.com/content/CVPR2024/papers/Chalk_TIM_A_Time_Interval_Machine_for_Audio-Visual_Action_Recognition_CVPR_2024_paper.pdf)    | Audio         | 26.9  | 56.9  | 12.4 | 11.4 | 0.689 |
| [ASF](https://arxiv.org/abs/2103.03516)    | Audio         | 27.9  | 64    | 11.9 | 14   | 0.741 |
| [TIM](https://openaccess.thecvf.com/content/CVPR2024/papers/Chalk_TIM_A_Time_Interval_Machine_for_Audio-Visual_Action_Recognition_CVPR_2024_paper.pdf)    | Audio + video | 31.9  | 61    | 14.4 | 15.7 | 0.765 |
{:.stretch-table}

Sound Recognition Benchmark. Current models struggle on HD-EPIC.
{:.figcaption}

We evaluate 3 audio models, all trained on [EPIC-Sounds](https://epic-kitchens.github.io/epic-sounds/). The table above shows a large gap in performance comparing HD-EPIC to EPIC-Sounds for SSAST (-28.4), ASF (-25.9) and TIM (-26.4). This shows audio is not as robust to new scenes as expected.

## Long-term video object segmentation

<table><thead>
  <tr>
    <th></th>
    <th colspan="3">Total</th>
    <th></th>
    <th colspan="3">Hands</th>
    <th></th>
    <th colspan="3">Objects</th>
  </tr></thead>
<tbody>
  <tr>
    <td>Model</td>
    <td style="text-align:center">J</td>
    <td style="text-align:center">F</td>
    <td style="text-align:center">J &amp; F</td>
    <td></td>
    <td style="text-align:center">J</td>
    <td style="text-align:center">F</td>
    <td style="text-align:center">J &amp; F</td>
    <td></td>
    <td style="text-align:center">J</td>
    <td style="text-align:center">F</td>
    <td style="text-align:center">J &amp; F</td>
  </tr>
  <tr>
    <td>Static</td>
    <td style="text-align:center">10.1</td>
    <td style="text-align:center">11.4</td>
    <td style="text-align:center">10.8</td>
    <td></td>
    <td style="text-align:center">15.4</td>
    <td style="text-align:center">14.7</td>
    <td style="text-align:center">15.0</td>
    <td></td>
    <td style="text-align:center">5.6</td>
    <td style="text-align:center">8.6</td>
    <td style="text-align:center">7.1</td>
  </tr>
  <tr>
    <td><a href="https://openaccess.thecvf.com/content/CVPR2024/papers/Cheng_Putting_the_Object_Back_into_Video_Object_Segmentation_CVPR_2024_paper.pdf">Cutie</a></td>
    <td style="text-align:center">45.3</td>
    <td style="text-align:center">52.4</td>
    <td style="text-align:center">48.8</td>
    <td></td>
    <td style="text-align:center">57.9</td>
    <td style="text-align:center">63.5</td>
    <td style="text-align:center">60.7</td>
    <td></td>
    <td style="text-align:center">34.5</td>
    <td style="text-align:center">42.9</td>
    <td style="text-align:center">38.7</td>
  </tr>
  <tr>
    <td><a href="https://github.com/facebookresearch/sam2">SAM2</a></td>
    <td style="text-align:center">56.9</td>
    <td style="text-align:center">61.6</td>
    <td style="text-align:center">59.2</td>
    <td style="text-align:center"></td>
    <td style="text-align:center">83.5</td>
    <td style="text-align:center">87.7</td>
    <td style="text-align:center">85.6</td>
    <td></td>
    <td style="text-align:center">34.0</td>
    <td style="text-align:center">39.2</td>
    <td style="text-align:center">36.6</td>
  </tr>
</tbody></table>
{:.stretch-table}

Long-Term VOS. Jaccard index J & contour accuracy F show Cutie and SAM2 struggle with segmenting objects.
{:.figcaption}

We construct a long-term video object segmentation benchmark using our segmentations and track associations. Our benchmark has 400 sequences each with 1-3 objects and 2 hand masks. While we have a lot more tracks, we keep it comparable to current benchmarks in size. We evaluate two models with a naive baseline where object masks are kept static. The table above shows the results. SAM2 surpasses Cutie for hands, but performs similarly poorly for objects, demonstrating the challenge of diversity in object perspective, lighting, location and occlusion

<br>

![Full-width image](/assets/img/dataset/vos_benchmark_figure_2.jpg){:.lead loading="lazy"}
Long-Term VOS. Qualitative results.
{:.figcaption}

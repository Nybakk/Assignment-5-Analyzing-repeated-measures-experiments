# Assignment 5: Analyzing repeated measures experiments

In this assignment you will analyze and report on trial investigating the effect of resistance training volume on lean mass and muscle strength. The data are part of the exscidata package and can be accessed as data("strengthvolume") and data("dxadata"). Read the instructions carefully!

Organizing the report
Your report should consist of the sections Introduction, Methods, Results and Discussion. Each part of the report should be written as a reproducible document and a link or reference to the repository containing the source document(s) should be included in the report. Below follows detailed descriptions and requirements for each section.

Introduction
This section should consist of a description of the field, resistance-training volume and muscle strength and mass. Use at least five to ten references to introduce your audience and explain why you are doing the analysis/study. A tip is to use the QALMRI method, introduced in Assignment 4 to structure the reading of background information. It is up to you how you motivate the study and how you phrase the purpose of the study. It could be a hypothesis based on previous studies, it could also be question to fill a knowledge gap that you have identified in your literature review.

Structure the introduction in paragraphs. A first paragraph could contain a general introduction to the field, why is it of interest to investigate resistance-training? A second paragraph could specifically describe the specific field of resistance-training volume, why is important to know more about how we are likely to respond to different training volumes. The second paragraph should incorporate definitions important for your report, e.g., training volume, muscle mass and strength. Try to incorporate these definition as a fluid part of the text.

A third (or last) paragraph of the introduction should contain a statement regarding the purpose of the study. The purpose could be descriptive, hypothesis-driven or guided by a question. Although it could be considered a bit backward, you should explore the data sets before you select your question/hypothesis/purpose for it to be possible to answer.

Methods
The method should give a thorough overview of the study and specific details regarding data collection. You can read about the details of this specific study in (Hammarström et al. 2020). Use your own words to describe the study based on this description. A nice way to structure the methods section is to include subheadings:

Participants and study overview: Describe the participants and give an overview of all tests/measurements. Participants should be described in the first table of the report (Table 1). The overview of the tests/measurements should be done without double presentation as details should be presented in subsequent sections.

Specific descriptions (e.g. strength tests): Describe in detail how tests/measurements that you mentioned in the overview where conducted.

Data analysis and statistics: Describe how you treated the data prior to statistical tests or procedures and what tests/procedures were used to draw inference (or more generally, to answer your purpose). Describe how you present data (e.g. descriptive data with mean (SD), inference with confidence intervals etc.).

Results
Describe the results of your analysis. This description should make use of table and figures as well as a text that guides and structures the content to the reader. Think about it this way, the text should describe when and how to read the figures and tables. This means that all aspects of the results should be covered in the text. The figures and tables should also be “self explanatory”, this means that you have to include descriptive figure captions and descriptions of tables (see below for tips).

As the main purpose of the analysis should concern the effect of training volume on muscle mass and strength, it is natural that the comparison of training outcomes between volume conditions is the main analysis in the results. You may also have questions regarding the relationship between muscle strength and mass gains, if there are differences between men and women etc. Selection of statistical/analysis techniques should reflect the study question/purpose.

Discussion
Structure the discussion with a first paragraph describing the main results of the analysis, this could be the answer to your question or a statement regarding the study hypothesis. In the following paragraphs discuss all results that you have presented in the light of previous studies. It is your job to give the reader plausible interpretations and explanations of your results. This is how single scientific results are incorporated in our collective understanding. These interpretations can later be challenged, however if you give the reader good arguments and clear descriptions, your insights will be valuable to collective reasoning even if they turn out to be wrong in light of new data.

End the discussion with a summary or conclusion. Some journals request that you state your conclusions under a specific heading in the end of the report/article.

Organizing the data analysis
Data preparation
The data is already structured in the exscidata package. To access the data, use the following code:

library(exscidata)
data("dxadata"); data("strengthvolume")

To get and overview of the variables in each data set use ?strengthvolume and ?dxadata. In the dxadata the variables of interest are organized in a more convenient way using the code below:

library(tidyverse)

dxadata %>%
  select(participant:include, lean.left_leg, lean.right_leg) %>%
  pivot_longer(names_to = "leg", 
               values_to = "lean.mass", 
               cols = lean.left_leg:lean.right_leg) %>%
  mutate(leg = if_else(leg == "lean.left_leg", "L", "R"), 
         sets = if_else(multiple == leg, "multiple", "single")) %>%
  select(participant, time, sex, include, sets, leg, lean.mass) %>%
  print()

# A tibble: 160 × 7
   participant time  sex    include sets     leg   lean.mass
   <chr>       <chr> <chr>  <chr>   <chr>    <chr>     <dbl>
 1 FP28        pre   female incl    multiple L          7059
 2 FP28        pre   female incl    single   R          7104
 3 FP40        pre   female incl    single   L          7190
 4 FP40        pre   female incl    multiple R          7506
 5 FP21        pre   male   incl    single   L         10281
 6 FP21        pre   male   incl    multiple R         10200
 7 FP34        pre   female incl    single   L          6014
 8 FP34        pre   female incl    multiple R          6009
 9 FP23        pre   male   incl    single   L          8242
10 FP23        pre   male   incl    multiple R          8685
# ℹ 150 more rows
References
Hammarström, Daniel, Sjur Øfsteng, Lise Koll, Marita Hanestadhaugen, Ivana Hollan, William Apró, Jon Elling Whist, Eva Blomstrand, Bent R. Rønnestad, and Stian Ellefsen. 2020. “Benefits of Higher Resistance-Training Volume Are Related to Ribosome Biogenesis.” Journal Article. The Journal of Physiology 598 (3): 543–65. https://doi.org/10.1113/JP278455.

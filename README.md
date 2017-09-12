## Experiment introduction

This repository consists of a basic experiment interface for conducting a copying and pasting experiment comparing two techniques: 1) AutoComPaste and 2) Traditional Copying and Pasting using keyboard shortcuts (Ctrl-C, Ctrl-V). You may view the demo at https://sailinz.github.io/


## Installation locally

You can either download as a zip file or clone this repository to get it running on your computer.

1. **Download Zip:**

Click on the **"Download Zip"** button on the right to download the repository as a zip file.

2. **Start a local web server:**

If you have Python installed, a simpler way exists. Running the following command in the root of the repository directory will start a local web server at port 8000:

```
$ python -m SimpleHTTPServer    // Python 2
$ python -m http.server         // Python 3
```

### Interface Walkthrough

There are a total of 5 screens for experiment, each corresponding to a step of the experiment. The breakdown of the screens:

1. Welcome Screen
2. Pre-experiment Questionnaire
3. Instructions
4. Experiment
5. Post-experiment Questionnaire

#### Welcome Screen

Path: `index.html`.

The welcome interface of the experiment where basic instructions are provided to your participants. Collect input from the participant/experimenter the participant ID so that the correct experiment trials and data log for a particular experiment session.


#### Pre-Experiment Questionnaire Screen

Path: `questionnaire-pre.html`.

This part of the interface collects whatever pre-experiment information which includes their personal information and their previous experience of the traditional technique.

The CSV file will be named `acp-<pid>-pre.csv`.

Some validation has been added for the form fields and a * is appended to the questions to remind the users that the answers for the questions are required.

#### Instructions Screen

Path: `instructions.html`.

This page will contain information regarding instructions on the experiment that you want your participant to read before they start on the experiment. The user need to confirm that they understand the instruction before they proceed to the experiment.

#### Experiment Screen

This screen consists 4 sessions - non-timed trail, timed block 1, break, timed block 2

Path: `experiment.html`.

This is the non-timed trail session to get the participant familiar with the ACP technique. There will be 6 trails for ACP technique which covers conditions like sentence/paragraph/phrase and single/multiple opening windows. There will be 2 trails for traditional windows to just showcase how the participant will see the highlighted stimuli in the articles.

Path: `experimentB1.html`.

This is the timed experiment of the first block. 12 conditions are assigned to each participant and each condition will have 3 consequent trails. The stimuli for the 36 trails are as distinctive as possible to minimize the learning effect on the stimuli. The conditions and corresponding trails are arranged in /data/block1/pid-B1.json for each participant.

After completing this block, the data containing the conditions and results of the trials will be generated in the form of a CSV file, `acp-<pid>-blk1-trials.csv`.

Path: `experimentBreak.html`.

A timer is set up to count down the 1 min break between the blocks.

Path: `experimentB2.html`.

This session is similar to experimentB1.html. The conditions and corresponding trails are arranged in /data/block2/pid-B2.json for each participant. The only difference is that the trails for each condition is arranged differently. This is to test the learning effect of the techniques.

After completing this block, the data containing the conditions and results of the trials will be generated in the form of a CSV file, `acp-<pid>-blk2-trials.csv`.


#### Post-Experiment Questionnaire Screen

This screen contains 2 sessions - post experiment questionnaire and an end of experiment notice.

Path: `questionnaire-post.html`.

Similar to the Pre-Experiment Questionnaire, in this screen, you will collect participants responses including personal preferences, any difficulties participants experienced in the experiment, and areas of improvement.

Upon clicking the Submit button, form responses on the page is serialized and CSV file containing the responses will be generated and available for downloading into the user's computer. The CSV file will be named `acp-<pid>-post.csv`.

Path: `endOfExperiment.html`.

A screen to notify the participant that they've finished the experiments.


## Documentation

#### ACPToolKit.js

Filename change:

The experiments results will include the blk name.

```
module.downloadTrialResults = function (data, blk) {
    var pid = ACPToolKit.getCurrentParticipantId();
    arrayToCSV(data, 'acp-' + pid + '-blk-' + blk + '-trials');
}
```

Add the third independent variable

```
$('.js-expt-technique').text(options.technique);
$('.js-expt-granularity').text(options.granularity);
$('.js-expt-articles').text(options.articles);
$('.js-expt-stimuli').text(options.stimuli);
```

#### Data Object File
Path: `data/articles`.
No changes

Path: `data/block1`.
Arrangement for the 12*3 trails of block 1 for each participant

Path: `data/block1`.
Arrangement for the 12*3 trails of block 2 for each participant

Path: `data/dataFile`.
multiWin: shows 6 windows of articles
singleWin1-6: shows 1 window which contains 1 article

Path: `experimentTrail.json`.
6+2 non-timed trail


## Credits

- Tay Yang Shun (Interface and ACPToolKit)
- Wong Yong Jie (AutoComPaste Engine)

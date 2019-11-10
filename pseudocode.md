# Experiment Description
My experiment seeks to demonstrate multiple time memory in mice through behaviour testing.

72 mice will be divided into two control groups and one experiment group. The first control group will receive conditioned place avoidance (CPA) training and the second control group will receive conditioned place preference (CPP) training, while the experiment group will receive both trainings.
Each mouse will be trained at either time 8 or 16 of the day, and will be tested at one of the timepoints. Based on the timepoint of training and testing, each group will be further divided into 4 subgroups of 6 mice:

    1st subgroup: Training - 8, Testing - 8;
    2nd subgroup: Training - 8, Testing - 16
    3rd subgroup: Training - 16, Testing - 8.
    4th subgroup: Training - 16, Testing - 16.

Because CPP and CPA involves two chambers, one of which is paired with the stimulus and the other is unpaired with the stimulus, the mice of each subgroup will be equally divided so that half will receive stimulus in one chamber and half will receive stimulus in the other chamber.


The experiment itself contains three sessions: 
    The pre-exposure session, during which the mouse will be put into the alley connecting the two chambers and allowed to explore freely for 10 minutes. The time that the mouse spent in each place will be recorded.
    The training session, which contains 8 trials. In the odd trials, each mouse will receive the assigned stimulus in their paired chamber at their assigned timepoint for 10 minutes. In the even trials, the mouse will be put into the unpaired chamber for 10 minutes without any stimulus. 
    The testing session, during which the mouse will be put into the alley connecting the two chambers at its assigned testing time and allowed to explore freely for 10 minutes. The time that the mouse spent in each place will be recorded.


# Pseudocode
## Assigning subjects to different conditions
    subjects = []
Create a new class subject to record the information of each mouse:

    class Subject:
        def __init__(self, subject_number, group=None, training_time=0, testing_time=0, paired_chamber=None, unpaired_chamber=None)
    subject = () | Input the animal number as subject number
    subjects.append(subject) | Add all animals into a list

Randomly assign subjects to groups:

    shuffle(subjects) | Randomize subjects
    for subject in subjects[0:24]:
        subject.group = "CPA_Control"
    for subject in subjects[24:48]:
        subject.group = "CPP_Control"
    for subject in subjects[48:]:
        subject.group = "Experiment"
        
Assign subjects to subgroups:             
   
    CPA_group = subjects[0:24]
    CPP_group = subject[24:48]
    Experiment_group = subject[48:]
    groups = [CPA_group, CPP_group, Experiment_group]
    for group in groups:
        for subject in group[0:6]:
            subject.training_time, subject.testing_time = 8, 8
        for subject in group[6:12]:
            subject.training_time, subject.testing_time = 8, 16
        for subject in group[12:18]:
            subject.training_time, subject.testing_time = 16, 8
        for subject in group[18:]
            subject.training_time, subject.testing_time = 16, 16

Assign paired and unpaired chambers to subject:

    if is_odd(subject.subject_number) == True:
        subject.paired_chamber, subject.unpaired_chamber = chamber_1, chamber_2
    else:
        subject.paired_chamber, subject.unpaired_chamber = chamber_2, chamber_1

## 1. Pre-exposure Session
    record_duration(subject.paired_chamber, alley, subject.unpaired_chamber)

## 2. Training Session
    trials = [1, 2, 3, 4, 5, 6, 7, 8]
    for trial in trials:
        if is_odd(trial):
            if subject.group == "CPA_Control":
                give_shock(subject, subject.paired_chamber, time = subject.training_time)
            elif subject.group == "CPP_Control":
                give_food(subject, subject.paired_chamber, time = subject.training_time)
            else:
                give_shock(subject, subject.paired_chamber, time = subject.training_time)
                give_food(subject, subject.paired_chamber, time = subject.training_time)
        else:
            no_stimulus(subject, subject.unpaired_chamber, time = subject.training_time)
        
## 3. Testing Session
    record_duration(subject.paired_chamber, alley, subject.unpaired_chamber, time = subject.testing_time)
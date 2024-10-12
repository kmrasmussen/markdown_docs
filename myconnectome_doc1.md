# Exploring Personalized Whole-Brain Models for Psychiatric Treatment

## Introduction

In recent discussions with Mario, we explored an exciting project idea focused on modeling fMRI data of psychiatric patients. The core hypothesis is that accurate modeling of fMRI data could significantly enhance treatment methods. Specifically, we are interested in developing whole-brain models that utilize anatomical information about structural connectivity between different brain regions to create dynamic models of fMRI data.

## Background

### Group-Level Modeling

Most current research concentrates on group-level modeling. Typically, researchers use an average structural connectivity matrix derived from group data, along with group-level statistics of functional recordings, to fit a general whole-brain model. Some studies also fit multiple models for different states, such as a normal state versus a meditation state, at the group level.

### Individual-Level Modeling

However, there is a growing need for individual-level, patient-specific models. These models are crucial because psychiatric conditions vary significantly among patients. While a combination of group-level and individual-level models might be ideal, focusing on the individual patient's brain is essential for personalized treatment.

## Challenges

### Data Availability

A major challenge in developing these models is the availability of data. Questions arise about how much data we can feasibly collect from a single subject and how much data is necessary to build a robust model. This issue is underexplored, even at the group level.

### Theoretical Considerations

The theoretical discussion on the amount of data required to fit a good model is also lacking. This problem is present in many research fields, suggesting that existing literature could provide valuable insights.

## Proposed Project

### The MyConnectome Project

We propose leveraging the MyConnectome Project dataset by Professor Paul Poldrack. This project involves extensive fMRI and structural imaging recordings of Poldrack himself over many days, making it the most comprehensive single-subject dataset available.

### Objectives

1. **Subject-Level Modeling**: Develop a model for a single subject and investigate the data requirements. For example, we can evaluate model performance by testing its ability to predict activity on unseen recordings.
   
2. **Pharmacological Modeling**: Incorporate pharmacological data to study the effects of substances like caffeine. Previous whole-brain models have included neurotransmitter receptor densities and other brain maps to simulate drug effects. Poldrack’s dataset includes recordings under different conditions, such as caffeinated and non-caffeinated states.

### Potential for Pharmacological Studies

We can utilize information about adenosine receptors, relevant for caffeine, from brain maps created by Justine Hansen. Although these maps are general and not specific to the subject, they offer a starting point for exploring pharmacological effects. This approach can be extended to psychiatric patients to model the effects of various medications on brain function.

## Limitations and Future Work

A key limitation is the general nature of neurotransmitter receptor density maps. Individual-specific maps would provide more accurate models, but collecting such data from psychiatric patients may be impractical. Despite this, using population-level maps remains a valuable initial step.

## Conclusion

This project aims to advance personalized whole-brain models by addressing key challenges in data availability and theoretical foundations. Utilizing the MyConnectome Project dataset offers a unique opportunity to develop and test these models, paving the way for improved psychiatric treatment through personalized brain modeling.

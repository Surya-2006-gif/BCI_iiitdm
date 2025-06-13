
# TASK - 3

## DATA CLEANING AND PRE-PROCESSING:

- ### Re-referencing:
    
      - When recording a eeg electrode reading,we basically measure voltage(microvolts).As voltage is always measured relative to a reference electrode.

      - while choosing this reference electrode ideally it shouldnt record any brain signal and noise but its not often the case.

      - There are two ways to try get a brain-activity and noise free eeg signal
          
          1.keeping electrode at less-brain activity site(ear lobes,mastoids,nose)

          2.Take reference as any electrode record eeg data and digitally(in offline) re-reference it.This allows choosing a better :reference, such as

               - Common average reference
               - Linked mastoids
               - REST (Reference Electrode Standardization Technique)
               - Laplacian (CSD) for local source estimation

          

- Most commonly we do 'common average re-referencing'

## Filtering
  
    - We filter off slowing frequency fluctuations(also known as drift) from thee eeg data which are less than 1Hz or 0.5Hz using a high pass filter

    - EEG can also be contaminated by high-frequency noise, especially above 45–50 Hz, due to:
          - Electrical line noise (50 Hz or 60 Hz depending on the country),
          - Muscle artifacts, or
          - Environmental interference.


## Epoching

    - We segemnt the eeg signal across channels based on markers.

    - most commonly 0.2s prior to the event to 1 or 2 seconds post event


## Baseline correction

    - The baseline is a short time window before the event/stimulus onset (often −200 ms to 0 ms). It's used to estimate the background brain activity that was happening just before the event.

    - By subtracting the mean of the pre-stimulus interval, we normalize the signal to a common starting point, so post-stimulus changes are clearer.


## ICA (Independent Component Analysis)
        - Independent component analysis,a blind source seperation method.
        - This method seperates the signal into multiple independent components.It is most commonly used to remove muscle artifacts,eye blink and eye movement artifacts

        
## F1_score:

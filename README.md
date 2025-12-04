# Rise Time Discrimination (English)

Three sounds are played on each trial; one is different from the other two. The odd sound is always the 1st or the 3rd, and the participant answers with `1` or `3`. Differences in rise time are scaled from `Stimuli/1.flac` upward. Practice uses stimuli 1 and 100 so the contrast is obvious.

## How to run
- Enter the participant ID and proceed to the instruction screen.
- Wait while the page shows “Loading audio...” — key stimuli are preloaded before you can start. When the message clears, **Start practice** is enabled.
- Click **Start practice** for 3 practice trials (stimuli 1 and 100). Accuracy feedback appears after each response. After practice is finished, **Start main test** becomes enabled.
- In the main test, three sounds play in sequence; once playback finishes you can press 1/3. The session ends after 75 trials or 7 reversals and automatically downloads a CSV (`<ID>_risetime_discrimination.csv`). You can re-download from the completion screen.
- Keep the audio files in `Stimuli/` (`1.flac`–`101.flac`) next to this HTML.
- If playback fails, an error message is shown; verify the `Stimuli/` files are present and reload the page.

## Key parameters (`risetime_discrimination.js`)
- `startingStep = 51`
- `maxTrials = 75`
- `numSteps = 101` (loads `Stimuli/1.flac`–`Stimuli/101.flac`)
- `targetReversals = 7`
- `stepSizes = [10, 5, 2, 1, 1, 1, 1, 1]`
- Timing: inter-stimulus 500 ms, 500 ms until buttons appear after playback, 1000 ms until next trial after a response
- Practice: `practiceConfig.trials = 3` (stimuli fixed at 1 and 100, with feedback)

## CSV columns
- `subject_id`: entered participant ID
- `trial`: trial number (1-indexed)
- `stimulus_step`: step size used (`i` for `Stimuli/i.flac`)
- `odd_position`: position of the odd sound (1 or 3)
- `correct_answer`: correct response (`'1'` or `'3'`)
- `response`: participant response (`'1'` or `'3'`)
- `correct`: 1 = correct, 0 = incorrect
- `rt_ms`: reaction time in ms (from buttons becoming active to click)
- `num_reversals_after`: cumulative reversals after this trial
- `step_before`: step value before updating
- `step_after`: step value after updating (clipped to 2–101)
- `step_size_used`: step size applied this trial
- `mean_reversal_so_far`: mean of reversal step values from the second reversal onward (blank until available)

## Staircase logic
- 1-up/2-down: consecutive correct answers make the step smaller; an error makes it larger.
- A reversal is counted when correctness flips relative to the previous trial. The threshold shown at the end is the mean of reversal step values from the second reversal onward.

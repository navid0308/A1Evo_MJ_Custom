# A1Evo_MJ_Custom

This is a custom version of the original A1Evo I created for my personal use. I have been getting excellent results with it and wanted to share it on the forum. The custom version is based on the last released version of the 1-Click A1Evo Maestro MJ solution. It works with both standard and directional bass systems. It also works on systems without a subwoofer.

Guides, Changes and FAQs - https://www.avsforum.com/threads/a1evo-mj-custom.3325897/

It's based on OCA's original work. Links below -
* YouTube - https://www.youtube.com/watch?v=lmZ5yV1-wMI
* Google Drive - https://drive.google.com/drive/folders/1rfwzbnET3wYoSSgo-4LDRpKHVXwCYoMF

## Changelogs
### Update 10/18/2026 PureEQ v7.2.0 changelog -
* Introduce a new technique for finding subwoofer IR peak
* Set min XO based on subwoofer -3dB point instead of one octave above it
* Switch to 1/48 smoothing for all things SPL calculation
* Update findNearestXO to use logarithmic distance from roll-off
* Fine tune a few parameters in roll-off detection algorithm

### Update 10/14/2026 PureEQ v7.1.0 changelog -
Going back to basics with this one - MLP for levels and delays, AVG for equalization. Using AVG for setting subwoofer trims and delays seemed like a great idea on paper, but it worsens the midbass and subwoofer to speaker handoff. This update should result in a more present bass that's anchored to the center image.
* Revert subwoofer optimization logic to use MLP for all steps except equalization
* Revert XO finalization to use MLP measurements
* Fine tune several parameters to improve alignment accuracy

### Update 9/28/2026 PureEQ v7.0.2 changelog -
* Fine tune transition from precise filters to broad filters

### Update 9/27/2026 PureEQ v7.0.1 changelog -
Minor update with bug fixes to improve transition frequency detection accuracy
* Revise the Schroder frequency detection logic to make it more robust
* Add in an upper limit of 2khz when calculating Schroder
* Minor code cleanup

### Update 9/26/2026 PureEQ v7.0.0 changelog -
This update fundamentally changes how REW filtering works and sounds. Endgame maybe?
* Introduce a 3-stage room correction approach, anchored by the detected Schroder frequency
  * Psy smoothed boosts below transition frequency
  * Var smoothed cuts below transition frequency
  * 1/1 smoothed tone control like broad filters above transition frequency
* Add in a new Schroder frequency detection logic
* Scrap dynamic fill/dynamic bass fill

### Update 9/24/2026 PureEQ v6.9.0 changelog -
Minor code change but major change in sound. Warrants a proper version bump!
* Re-introduce precise boosts - this should improve overall coherence

### Update 9/22/2026 PureEQ v6.8.1 changelog -
* Finalize XO using the frequency response instead of excess phase
* Tweak baseline + roll-off determination logic to improve accuracy
* Fine tune boost logic to better balance dips vs general trend line
* Minor bug fix for first IR peak detection algorithm
* Clean duplicates in AVR model lists

### Update 9/17/2026 PureEQ v6.8.0 changelog -
* Switch to baseline approach from v6.4/6.6
* Align AVG to target after creation
  * Better correlation with MLP
  * Fixes imaging issues in multi-channel
* Use excess phase for XO finalization and increase penalty for higher values
* SW response variation metric will now evaluate the full bandwidth
* Lots of code reorg and cleanup

### Update 8/29/2026 PureEQ v6.7.3 changelog -
* Update ACM1HB cal file to the latest version from the MultEQ app - green line should be flat!
* Move "_micCal.txt" outside of the script and remove a lot of associated logic
  * The cal file will no longer be added to the extracted .zip
  * A new "_misc" folder will host these files and import them as necessary
* Move the volume bug fix and cal file application steps later in the pipeline
  * Fixes an incompatibility where the mic cal had to be skipped for subs in certain cases

### Update 8/4/2026 PureEQ v6.7.2 changelog -
* Skip SPL alignment after generating spatial average
  * This step could introduce disconnect between MLP and AVG measurements

### Update 7/30/2026 PureEQ v6.7.1 changelog -
* Fine tune baseline and roll-off logic to improve bandwidth detection accuracy

### Update 7/27/2026 PureEQ v6.7.0 changelog -
* Simplify XO finalization to use max sum instead of RMS error from target
  * Prior logic was not very sensible when using raw measurements in AF mode
* Use 1/1 smoothing when evaluating alignments - this should improve stability
* Switch to 200-2k instead of 300-3k for aligning target curve to 75dB
  * Better focus on real world fundamentals of most instruments and voices
* Update TCx - tiny bit of fine tuning

### Update 7/7/2026 PureEQ v6.6.0 changelog -
* Re-introduce the aggressive baseline logic from v6.4.0
  * Cascading effect on roll-offs, EQ, final XO etc.
* Add in edge case handling for compatibility issues with new baseline logic
* Switch back to 1/1 smoothing for boosts to better preserve directivity
  * Produces a smoother, less fatiguing sound
  * Less impacts on phase response

### Update 6/24/2026 PureEQ v6.5.0 changelog -
* Revert the baseline generation logic to pre-v6.4.0 for better compatibility across more setups
* Revert logic to using BPF to reduce boosting at the limits
* Use the average LF/HF roll-offs for channel pairs when determining EQ limits -
  * Ensures channel pairs are EQ-ed evenly at the limits
* Fine tune XO finalization weighting to reduce XO spread
* Fine tune roll-off logic to improve accuracy

### Update 6/22/2026 PureEQ v6.4.0 changelog -
* Revamp the logic of baseline generation to make it more aggressive
  * This has a cascading effect on detected roll-offs, EQ filters etc.
  * REW Filtering should see an improvement in overall coherence and fullness
* Allow marginally more boost near roll-off points for better target tracking
* Update TCx - slightly leaner to balance out the changes from this update

### Update 6/16/2026 PureEQ v6.3.1 changelog -
This update only affects REW filtering mode, and is meant to be a refinement
* Add in an extra layer of Var smoothing to boost filters
  * Smoothes out the high frequency correction and better preserves the natural sound

### Update 6/14/2026 PureEQ v6.3.0 changelog -
Since target level offset/dynamic bass fill adjusts response level for EQ, the trim initialization step has been simplified to follow Dolby/REW standards for level matching
* Simplify the leveling logic to use Dolby/REW recommended bandwidths
  * 500-2k for speakers and 30-80hz for subwoofers
  * Android volume bug fix will also use these same ranges

### Update 6/9/2026 PureEQ v6.2.2 changelog -
* Use the widest possible SW to system overlap as evaluation range when optimizing delay
* Reduce the excessive midbass in TCx - it was becoming a bit much for my tastes

### Update 6/8/2026 PureEQ v6.2.1 changelog -
* Scrap the +15hz offset and set initial XO based on roll-off
  * This should result in lower XOs across the board
* Update TCx

### Update 6/7/2026 PureEQ v6.2.0 changelog -
* Scrap level matching non-MLP positions to MLP - better correlation with MMM
* Further reduce boost near the roll-off points
* Fine tune target level offset logic
* Streamline code to minimize dependency across functions

### Update 6/2/2026 PureEQ v6.1.3 changelog -
* Explicitly level the target curve to 75dB, irrespective of initial level
  * Results in better correlation between input signal level and output SPL
  * Improves accuracy of Dynamic EQ
* Fine tune TCx top end

### Update 5/27/2026 PureEQ v6.1.2 changelog -
* Update XO finalization logic to use RMS error against target instead of std dev of difference
  * Std dev could produce incorrect results if the difference between response and target was 'linear'
* Minor adjustment to TCx

### Update 5/25/2026 PureEQ v6.1.1 changelog -
Minor update to better handle cases where the subwoofer group delay is unusually stretched in time
* Increase negative delay headroom by 2x when aligning SW to system
* Revert SW response variation metric to report the maximum spatial variance across positions
* Update TCx

### Update 5/22/2026 PureEQ v6.1.0 changelog -
This update is primarily focused improving performance & consistency across all positions
* Use 'as is' RMS average of all positions for setting subwoofer trim(s) - improves SPL stability across positions
* Skip 'Cross corr align' when spatially averaging to preserve the phase characteristics of different positions
  * Instead, delay all non-MLP positions by the same amount as MLP - this preserves relative differences
* Use the spatial average for optimizing multi-subwoofer delays - this optimizes bass for all positions
* Use the spatial average for optimizing SW delay and crossovers for the full system - this optimizes integration for all positions
* Switch to a different metric for scoring different crossover points - shifts focus from dip removal to target tracking
* Maximize IR window anytime measurements are averaged - REW intermittently settles on a window that's too narrow
* Move SW level matching step into 'initializeSubwoofers' section for better code organization
* Move MultEQ volume bug fix to the bootup section for better code organization

### Update 5/17/2026 PureEQ v6.0.1 changelog -
* Align spatial average to target curve explicitly - should marginally improve image centering

### Update 5/15/2026 PureEQ v6.0.0 changelog -
* Precise boosts - use a combination of Psy and Var for boosts instead of 1/1
  * Improves definition and timbre matching across channels
* Aggressively taper of boosts near roll-off points - frees up dynamic headroom
* Use minimum phase whenever inversion is involved - produces the highest accuracy
* Fine tune various optimization parameters
* Update TCx

### Update 4/26/2026 PureEQ v5.8.1 changelog -
* Fine tune evaluation range that's used for aligning SW to system
  * min <-> max initial XO plus an octave on either side will be used to evaluate alignment

### Update 4/21/2026 PureEQ v5.8.0 changelog -
I wasn't 100% happy with the baseline results in a few cases. Additionally, the boost generation logic could behave in an uneven manner throughout the midrange and treble. This update is a refinement on how the baseline and REW EQ filters are calculated.
* Switch back the baseline smoothing ordering for better neutrality - logic in 5.7 could overemphasize midrange
* Fine tune boost generation logic to smooth out the filter midrange and top end - this should improve centering

### Update 4/17/2026 PureEQ v5.7.0 changelog -
This update is a refinement over the iconic v5.5.0 sound signature. Best way I can describe it - it sounds like the imaging now has anti-aliasing applied!
* Fine tune baseline response generation to better represent the midrange
* Fine tune speaker roll-off evaluation ranges to better work with the new baseline logic
* Fine tune target level offset calculation to better handle subwoofers with limited bandwidth
* Switch to using detected SW bandwidth for setting trims in REW filtering mode - works better for mismatched subwoofers
* Switch back to a wide frequency range for aligning SW to system
* Rework the XO finalization range & weighting to better balance localization vs dip reduction

### Update 4/15/2026 PureEQ v5.6.5 changelog -
This update only applies to REW filtering mode
* Revert the wideband leveling change from v5.6.3 due to worse overall performance
  * Speakers will now be level matched using 300-3000hz, similar to versions prior to v5.6.3
* Move finalize XO step after logging trims and distances for easier readability

### Update 4/13/2026 PureEQ v5.6.4 changelog -
* Switch to a maximum summation based SW alignment strategy
  * Previously this approach was used with FDW and performed worse in some cases - no FDW this time!
  * Better handles cases where subwoofers are not well matched with each other
* SW response variation metric will now be reported using the detected SW bandwidth

### Update 4/12/2026 PureEQ v5.6.3 changelog -
Experimenting with a trick from 'Movie Mode' of old. Ideally, this should improve immersion.
* Switch to using near full-bandwidth for setting speaker trims in REW filtering mode
  * Speakers will now be leveled using 250-10khz
  * Subwoofers will continue to be leveled using 20-120hz

### Update 4/11/2026 PureEQ v5.6.2 changelog -
* Do not allow extra negative delay headroom when aligning SW to system
  * This seems to better preserve time alignment

### Update 4/10/2026 PureEQ v5.6.1 changelog -
* Revert the alignment evaluation process back to the inverted cancellation approach from v5.5.0
  * This seems to be more stable across more cases
  * FDW will no longer be used as it can introduce variability
* Update TCx to add in more midbass

### Update 4/9/2026 PureEQ v5.6.0 changelog -
* Switch from using IR start times to using IR peak times when determining SW proximity
  * Excess phase responses are used for this calculation
  * The first significant peak is treated as the main peak
* Use FDW when aligning excess phase responses as an alternative to smoothing
* Switch to using Bessel slopes for bandpassing - seems to better preserve timing information
* Simplify the alignment evaluation process to find the delay for maximum summation
  * Previously it was inverting and looking for biggest cancellation - this could throw off the alignment if SW bandwidths varied a lot

### Update 4/2/2026 PureEQ v5.5.0 changelog -
This update is about...bringing that OG v4 magic back
* Switch back to complex arithmetic for filter generation - it simply sounds magical and I cannot stop listening
* Ditch full phase multi-sub alignment technique - does not consistently outperform excess phase based alignment
* Minor bug fix when converting from directional to standard bass

### Update 3/29/2026 PureEQ v5.4.0 changelog -
This update applies a new technique to extract the full phase response, and use it for various optimizations
* Introduce a new technique to extract full phase - response / magnitude of response
  * Full phase responses are used for multiple subwoofer alignment - excess phase is not reliable if impulse is not at t=0
  * Note: Excess phase responses will still be used for SW alignment to system, since speakers are time aligned to t=0
* Evaluate per speaker dip reduction when finalizing crossover - previously it would look at the RMS average for speaker pairs
* Use a marginally wider bandwidth for aligning SW to system - slight improvement in midbass
* Allow more negative delay headroom when aligning SW to system - allows greater compensation for group delay
* Ditch the usage of midrange based speaker time alignment - incompatible with upfiring speakers
* Ditch the usage of FDW, since it can be easily mislead by noise
* Disable audy2umik option when manual measurements are used

### Update 3/27/2026 PureEQ v5.3.1 changelog -
This is a minor update and it addresses a few edge cases
* Use 'Vector sum' to overcome noisy directional SW responses and better identify bandwidth
* Shift intermediate SW alignment results back to 0dB for potential subsequent alignments
* Minor code cleanup

### Update 3/26/2026 PureEQ v5.3.0 changelog -
I have been experimenting with using a wider range for level matching non-MLP positions to MLP prior to spatially averaging. The idea was to improve correlation between MLP and AVG so EQ filters benefit MLP more. In the process I found that it produced a sound that was too heavy on the fundamentals and was lacking air. To balance it out, I switched back to magnitude only arithmetic for EQ filter generation. So far, I am loving the results!
* Use 250-10khz for level matching non-MLP positions to MLP for better correlation between AVG & MLP
  * This range will also be used for the Android volume bug check and fix
* Switch back to magnitude only arithmetic - this produces highs that are exceptionally natural and spacious
* Convert EQ filter to minimum phase at a later stage to prevent sharp drop-offs in the infrasonics
* Fix an issue where directional .adys with only 1 position would crash when calculating SW bandwidth

### Update 3/24/2026 PureEQ v5.2.2 changelog -
* Reduce target level offset calculation range to ignore frequencies above 10khz - marginally improves stability
* Smooth out audy2umik top end to improve consistency between the different applications
  * Update the fixed auto-level offsets when audy2umik option is used
  * Audy2umik calibration file also updated with higher smoothing

### Update 3/22/2026 PureEQ v5.2.1 changelog -
This is a minor update and only affects REW filtering mode
* Marginally reduce filter artifacts in the high frequencies by using 'Var' smoothing for the boost generation & baseline calculation
  * Final boost filters will continue to use 1/1 smoothing for tone control-like adjustments

### Update 3/20/2026 PureEQ v5.2.0 changelog -
This one is a bit of an experiment based on lessons learned. There is a definition and weight to the sound of v4.x which I have been missing in v5.x. However, there is spaciousness and improved dialogue clarity with v5.x. Goal with this update is to find a middle ground.
* Switch to regular arithmetic for EQ filter creation - this adds higher definition & weight to the sound, similar to v4.x
* Switch to 1/1 smoothing for SPL calculation - this adds smoothness to the sound, similar to v5.x

### Update 3/19/2026 PureEQ v5.1.0 changelog -
* Update target level offset to focus only on the midrange and highs for speakers
  * This fixes an issue where it was cutting too deep and the resulting auto-leveled filter was over boosting
* Use spatial average when determining directional subwoofer bandwidth
* Fine tune boost smoothing sequence for better response shaping
* Fine tune mean SPL calculation for roll-off determination
* Lots and lots of code cleanup

### Update 3/17/2026 PureEQ v5.0.1 changelog -
* Revert back to using -6dB point for HF roll-off

### Update 3/16/2026 PureEQ v5.0.0 changelog -
The goal of this update is 3 fold - improved dialogue clarity, immersive atmos bubble & wider stereo soundstage
* Use wide frequency bands for leveling in REW filtering mode
  * Speakers will be leveled using 300-3khz
  * Subwoofers will be leveled using 20-120hz
  * Audyssey filtering and auto-level compensation will continue to use 30-80hz for subwoofers & 500-2khz for speakers
* Target level offset calculation will now use full bandwidth of response
* Reduce steps when calculating response baseline - this should speed up the script
* Update EQ logic to use magnitude only arithmetic operations as they seem to be more stable
  * This also results in smoother filters, and should produce a more natural sound
  * Filters are ultimately 'converted' to minimum phase for application purposes
* Clean up auto-leveling logic for both filtering modes
* Switch to 1/1 smoothing for SW response variation metric

### Update 3/13/2026 PureEQ v4.2.0 changelog -
This update improves the performance for both filtering modes
* Use an inverted smoothing approach to ignore peaks and infrasonic noise to extract the response baseline
  * Does a much better job of rejecting noise and ignoring peaks
* Fine tune roll-off search ranges used for mean SPL calculation & search
* Update dynamic fill to use the new baseline extraction approach
  * Performs much better in cases with lots of infrasonic noise and/or sharp narrow peaks
* Switch back to aggregate bandwidth for multiple subwoofer alignment

### Update 3/11/2026 PureEQ v4.1.1 changelog -
This update applies to both filtering modes
* Fix an issue where the response would sometimes have a leftover peak after EQ
* Simplify and reduce the boost generation steps to speed up the workflow
* Use 1/1 smoothing for roll-off determination
* Add in several clarifying comments to explain the flow of logic

### Update 3/9/2026 PureEQ v4.1.0 changelog -
Turns out dynamic bass fill and target level offset were contributing quite significantly (and positively), despite the new REW filtering approach looking like it didn't need them. As such, they are being added back in with this version. :)
* Add dynamic bass fill and target level offset logic back in
  * This better lines up the response baseline to target and prioritizes cuts over boosts
* Revert auto-level compensation logic to the prior version - this is required to properly support the other changes in this update
* Move XO finalization to after EQ generation to take advantage of any gains - this mimics the behavior of the first v4 beta

### Update 3/8/2026 PureEQ v4.0.0 changelog -
One thing I have been quietly chasing is bass that's weighty like Audyssey filtering, with a natural sounding midrange and treble like REW filtering. This was the primary motivation for v4.
* Completely rewrite REW filtering to boost using wide filters and cut using narrow filters
  * Wide boosts - uses REW arithmetic to generate boost filters using 1/1 smoothing
  * Precise cuts - uses REW arithmetic to generate cut filters using Var smoothing
  * Significantly better target curve tracking
* Move finalize XO stage prior to EQ for better evaluating raw phase interaction
  * This will also sync up final XO values between the different filtering modes
* Rewrite roll-off determination logic into more compact functions
  * Mean SPL is now calculated based on the region around roll-off
  * Use bandpassing to remove infrasonic noise for cleaner roll-off detection
* Remove all adjustments to target level offset and dynamic bass fill
  * This technique is no longer needed with the new REW filtering approach
  * Significantly simplify auto-level offset calculation
* Remove REW filtering boost sliders and all related code
* Add in subtle animation when expanding/collapsing PEQ filters section

As a general note, take it easy on the bass with this version.

### Update 3/5/2026 PureEQ v3.4.2 changelog -
This update is applicable to both REW and Audyssey filtering
* Fix an issue where SW alignment could be incorrect in certain cases
  * This update will also take into account initial XOs for SW alignment
* Simplify the roll-off determination calculation
* Simplify the target level offset calculation

### Update 3/5/2026 PureEQ v3.4.1 changelog -
* Fix an issue where the mean SPL for roll-off determination was being calculated incorrectly

### Update 3/4/2026 PureEQ v3.4.0 changelog -
* Use precise trims and distances for optimization and let the MultEQ app round the data as needed
* Fix an issue where the auto-level offset from the audy2umik option was being applied at the wrong time

### Update 2/28/2026 PureEQ v3.3.1 changelog -
* Fix an issue where the subwoofer PEQ auto-level compensation was not being applied to all subwoofers
  * This issue only affects Audyssey filtering mode
* Minor update to the fixed auto-level offsets for Audy2Umik
* Update PEQ table default frequency value to 50hz for subwoofer
* Tone down dynamic bass fill to only focus on the deeper & wider dips

### Update 2/27/2026 PureEQ v3.3.0 changelog -
* Incorporate Audy2Umik as a selectable option in the script
  * Works with both Audyssey and REW filtering
  * Optimized filename will now show "A2U" when the option is used
* Use a fixed auto-level compensation adjustment when Audy2Umik option is selected
  * This is kind of a 'Band-Aid', but works well enough for now
  * Trims are slightly different compared to using the Audy2Umik file manually
* Update Audy2Umik with marginally more smoothing and extending the frequency range to 5-24khz
  * You can use the file or the option, but don't use both as it'll overcorrect the optimization
* Minor code cleanup

### Update 2/26/2026 PureEQ v3.2.3 changelog -
* Use a wider 300-3khz midrange bandwidth for time aligning speakers instead of the narrower 500-2khz region
  * Seems to be marginally more accurate

### Update 2/23/2026 PureEQ v3.2.2 changelog -
* Fix an issue where the target level calculation was not using linear power average
* Use target curve for determining optimal target level offset (previously called dynamic bass fill)
  * This balances EQ filters based on target shape, and reduces unnecessary cuts
* Revert back to the older approach of initially compensating for MultEQ volume bug and later aligning non-MLP positions to MLP
  * Adds extra calculations, but it is more accurate for the SW response variation metric
* Minor tweak to SW mean SPL calculation for determining bandwidth
* Minor tweak to TCx

### Update 2/22/2026 PureEQ v3.2.1 changelog -
* Fix an issue where SW PEQ filters would not import correctly for directional .adys

### Update 2/22/2026 PureEQ v3.2.0 changelog -
* Use similar logic to dynamic bass fill to set target level for speakers
  * Prior method was to set target level based on FDW SPL drop, but it could be too aggressive
  * Equalized responses will now have slightly more imperfections but sound more natural
* Streamline the roll-off determination logic to speed up calculations & improve performance
* Remove the separate Android volume bug fix logic, since all non-MLP responses are level matched to MLP anyway
  * This will reduce a lot of unnecessary calculations and speed up the script
* Don't allow extra negative delay headroom when aligning SW to speakers to preserve time alignment
* Update TCx - this is my personal target curve and will be updated as I continue to tinker
* Update import filter logic to correctly populate subwoofer PEQs regardless of if the CommandID is SW1 or SWMIX
  * Previously it would ignore SW filters if the file contained SW1 but .ady contained SWMIX, or vice versa
* Reorganize the code a bit for better consistency & readability

### Update 2/20/2026 PureEQ v3.1.2 changelog -
* General improvements to roll-off determination with noisy data
  * SW roll-off evaluation frequency range reverted to the wider range used prior to 3.1.0
  * SW mean SPL calculation now no longer uses FDW - not really necessary in the low frequencies
  * Speaker roll-off determination is now relative to FDW-ed mean SPL between 300-3khz
* Switch to 1/48 smoothing for auto-level offset calculation - seems like the way to go
* Use higher granularity when checking and compensating for the Android volume bug
* Improve code consistency

### Update 2/19/2026 PureEQ v3.1.1 changelog -
* Switch from "Time Align" to "Align IR start" REW command for time aligning speakers
  * In more than one case, the "Time Align" command seemed to incorrectly time speakers when using the midrange
  * The "Align IR start" command will correctly sync midrange arrival times (thanks Michael for the bug report!)
* Improve non-MLP to MLP volume alignment precision - previously it was adjusting in 0.5dB increments
* Minor code cleanup

### Update 2/19/2026 PureEQ v3.1.0 changelog -
This update fixes a few edge cases with timing and roll-off determination, primarily with noisy data. Also, trying out 1/48 smoothing for SPL determination.
* Experiment with 1/48 smoothing for average SPL calculations - seems like linear power averaging does very well with lower smoothing
* Use frequency dependent windowing, prior to bandpassing speaker midrange, for time alignment
  * This fixes an issue where sometimes a speaker could be incorrectly timed due to noisy midrange IR
* Switch to a half octave gap detection for separating noise from response - nulls are typically 1/6 to 1/3 octaves wide
* Fine tune SW roll-off detection frequency ranges to avoid potential false positives from stacked nulls
* Leverage dynamic bass fill when converting from directional to standard bass -
  * Individual subwoofer's roll-offs will be determined by taking into account any potential gains from DBF
  * The evaluation range when aligning directional subwoofers will be based on their overlapping region instead of the aggregate

### Update 2/16/2026 PureEQ v3.0.0 changelog -
This update contains performance improvements for all filtering types, and a few fixes which should help with SW integration & overall imaging
* Switch to Var smoothing for SPL determination - more accurate for SW level, negligible difference for speakers
  * This will impact target level determination for speakers, and result in slightly different final trims with REW filtering
* Use bandpassed midrange responses of speakers for performing time alignment
  * This ignores early arriving signals from tweeters and better focuses on time aligning the critical 500-2khz region
  * Distances will vary slightly compared to what prior optimizations produced
* Use minimum phase version of the SW response for determining dynamic bass fill
  * Reduces artifacts when flipping and it's more true to the original response
* Use the precedence (Haas) effect to emphasize the center channel when dialogue enhancer is enabled
* Experiment with a different calculation for generating audy2umik - this should result in slightly better accuracy in the low bass

### Update 2/6/2026 PureEQ v2.9.7 changelog -
After the recent changes to use FDW and DBF for roll-off determination, an unwanted side effect is custom has become more sensitive to infrasonic noise. This change focuses on addressing that.
* Rework roll-off detection logic to search from high frequencies and go down to low frequencies, looking for an output gap of an octave
  * This should deal with the cases where the response rolls off early but then picks back up due to infrasonic noise
* Allow more delay headroom when aligning subwoofers and reduce granularity to speed things up
* Remove target curve dependency of dynamic bass fill and simply use SW response SPL as target SPL for flipping
* Fine tune smoothing used for dynamic bass fill to make it less aggressive
  * Fun fact: the smoothing used when flipping the SW response has a big effect on what SPL the flipped response initially settles on

### Update 2/5/2026 PureEQ v2.9.6 changelog -
* Switch to using the SW spatial average for determining dynamic bass fill, instead of SW MLP response
  * DBF is primarily a function of bandwidth and EQ, which are both determined using the spatial average
* Use the target curve for determining target level for DBF, instead of using the SW response SPL

### Update 2/4/2026 PureEQ v2.9.5 changelog -
* Use FDW-ed MLP responses to set mean SPL for determining -3dB points for both speakers and subwoofers
  * This better compensates for extra SPL from reverberations and exposes the actual roll off
* Roll in the usage of dynamic bass fill when determining SW bandwidth using the raw responses
  * This should take into account any potential bandwidth gains from EQ filters

### Update 2/1/2026 PureEQ v2.9.4 changelog -
* Move the finalize XO step after filter generation to take advantage of any EQ gains
  * This has the benefit of optimizing crossovers based on gains from EQ when using REW filtering mode
  * Crossovers will now vary between AF and RF mode, since AF still relies on the raw responses
* Optimize dynamic bass fill based the chosen target curve
* Fine tune XO finalization range & weighting

### Update 1/30/2026 PureEQ v2.9.3 changelog -
Thanks to all who tested and validated the performance of this change!
* Revamp dynamic bass fill to better handle subwoofers with lots of dips

### Update 1/28/2026 PureEQ v2.9.2 changelog -
* Fine tune XO finalization strategy

### Update 1/23/2026 PureEQ v2.9.1 changelog -
Fun fact: microphones can measure in positive or negative polarity, but there's no way to tell from the data alone. Plus, various crossover designs across different speakers make polarity detection even more challenging. What all of this means is that chasing absolute polarity detection isn't a worthwhile effort. Instead, custom will simply provide a warning if Audyssey flagged anything as being inverted during its polarity check. It's fairly reliable and serves the purpose for catching potential out of phase issues.
* Remove the experimental minimum phase based absolute polarity detection logic
* Add warnings in the log if Audyssey flagged a speaker/subwoofer for being out of phase in the .ady

### Update 1/22/2026 PureEQ v2.9.0 changelog -
* Tighten up proximity based delay range to ignore areas farther away from time alignment
* Add absolute polarity check for speakers (experimental)

### Update 1/21/2026 PureEQ v2.8.8 changelog -
This is purely a technical update and it should not affect performance
* Switch the proximity based delay range calculation to use IR start instead of first IR peak

### Update 1/16/2026 PureEQ v2.8.7 changelog -
* Removed "Align subwoofer to LCR speakers" - with the updated SW alignment logic, this should no longer be required
  * I know this may not be a popular change but I have always wanted custom to align subwoofer to the entire system, primarily because it provides better stability and predictability
* Removed delay normalization logic that is no longer needed - back when the "Align IR" command was used, min/max delays couldn't both be positive or negative. This is no longer a limitation with recent versions, and so this additional delay normalization logic is no longer required.
* Updated default high-shelf values to +/-3dB

### Update 1/14/2026 PureEQ v2.8.6 changelog -
* Experiment with using excess phase for SW integration to system
* Prior release used minimum phase for alignment, but MP does not preserve polarity and is not a viable option

### Update 1/13/2026 PureEQ v2.8.5 changelog -
* Leverage minimum phase when integrating subwoofer to the system
* Update TCx

### Update 1/2/2026 PureEQ v2.8.4 changelog -
First update of 2026! :D
* Use a progressive threshold for finalizing XO; higher XOs will require higher dip reductions, relative to target, to be considered
* Use a wider but fixed frequency band for evaluating different XOs so it is more of an apples to apples comparison
* Update log messages to actually count DOWN when cleaning up processed measurements
* Reduce a ton of clutter in the code by incorporating repeating logic into core functions
* Reorder optimization options and update the descriptions for better clarity

### Update 12/31/2025 PureEQ v2.8.3 changelog -
Happy new year all!
* (REW filtering) Use room reverberation to determine optimal target level; this will prioritize deeper cuts depending on the SPL drop from FDW
* Switch back to evaluating crossover choices between initial XO and 2x of initial XO, instead of 1.5x, to better fill in dips
* Switch back to setting minimum crossover based on 2x subwoofer low frequency extension, instead of 1.5x, to give the subwoofer more room to ramp up
* Widen the evaluation band for SW alignment to speakers to prioritize alignment over a wider frequency range
* Tighten up the evaluation range for finalizing XO to increase scrutiny on dips in the crossover region

### Update 12/30/2025 PureEQ v2.8.2 changelog -
* Revert back to the tried and true 30-80hz range for subwoofer level matching
* Move the user customizations under advanced settings for a cleaner look
* *New option to align subwoofer to LCR speakers exclusively - this should be marginally better if your focus is primarily stereo content
* Upon uploading the .ady file, the current timestamp will be saved internally and used as the unique identifier for logs/.ady/filters from that particular run
* Add countdown when cleaning up processed measurements

### Update 12/29/2025 PureEQ v2.8.1 changelog -
This change affects anyone using a directional .ady from the MultEQ app or odd.wtf
* Use excess phase responses to align multiple subwoofers - this seems to do a better job of aligning in cases where the SPL response does not do a good job of reflecting phase coherence
* Evaluation range when aligning multiple subwoofers will now be based on their aggregate bandwidth
* First IR peak calculation will now first bandpass the measurement to get rid of infrasonic or HF noise that can mask group delay

### Update 12/27/2025 PureEQ v2.8.0 changelog -
Always fun to learn new things - turns out you cannot simply average dB values like regular numbers! It has to be converted to linear power, averaged and then converted back to decibels. So, this update will have fundamental changes to SPL determination/handling and will be applicable for everyone.
* Use the correct mathematical formula for averaging dB values to determine SPL accurately
* Adjust smoothing across various places to optimize different workflows, including auto-leveling
* Crossover determination is now based on reduction of the average "dip" in the evaluation range
* Rename and reorganize a bunch of functions for easier understanding
* Switch logic to invert & optimize for maximum cancellation when aligning multiple subwoofers
* Reduce minimum delay range span to better focus on time alignment
* Improve subwoofer leveling for bandwidth-limited subwoofers

### Update 12/22/2025 PureEQ v2.7.5 changelog -
This update is applicable to both Audyssey and REW filtering. I liked how everything sounded with Psy smoothing for the various SPL calculations, but auto-leveling seems to have the highest correlation with 1/1 smoothing. So, I ended up using both where they excel.
* Revert back to Psy smoothing for all SPL related calculations except auto-leveling
* Use 1/1 smoothing ONLY for auto-level offset calculations - this seems to be the closest approximation to what auto-leveling does

### Update 12/21/2025 PureEQ v2.7.4 changelog -
This update applies to both Audyssey and REW filtering.
* Switch back to using 1/1 smoothing for SPL determination - this smoothing has the highest agreement with Audyssey's auto-leveling and also what the SPL meter would register using pink noise

### Update 12/11/2025 PureEQ v2.7.3 changelog -
This update primarily affects REW filtering.
* Use SBIR region of MLP response with FDW windowing for determining speaker EQ target level
* Revisit dynamic bass fill for settting subwoofer EQ target level
* Bug fix: in some cases the ultra high frequency filter could produce artifacts
* Add in more infrasonic points in the SW data that's pushed into the .ady

### Update 12/6/2025 PureEQ v2.7.2 changelog -
This update improves the multiple subwoofer alignment performance and stability.
* Use bandpassed individual subwoofer response for directional to standard conversion instead of the aggregate -3dB points
* Use entire bandpassed region for evaluating alignment
* Increase minimum delay span to +/-10ms with higher delay headroom for SW integration
* Bug fix: revert to using max cancellation SW integration approach instead of max sum with inverted SW
* Update TCx

### Update 12/5/2025 PureEQ v2.7.1 changelog -
Due to the way high shelf works in REW, custom has to use the lowest point after 10khz as the end frequency; otherwise, REW may avoid applying a high shelf if it sees a HF peak past 10khz. The downside was always that any UHF peaks would remain. Well, no more of those after this update!
* Add in logic to knock down any remaining ultra high frequency peaks after using high shelf for speakers

Note: This update ONLY affects REW filtering.

### Update 12/4/2025 PureEQ v2.7.0 changelog -
This update pretty much revamps how custom handles subwoofer alignments. :)
* Slopeless SW integration with speakers - this aligns SW to the system across the entire SW bandwidth
* Simplify delay range determination to +/-6ms of first peak with extra headroom for SW integration to system
* Use 1/1 smoothing for evaluating alignments to focus on the 'bigger picture'
* Tighten up the evaluation range when determining final crossovers
* Revert back to aligning directional subwoofers across their aggregate bandwidths
* Improve first IR peak detection algorithm accuracy
* Bug fix: spatial average IR window being too small and truncating the response
* Bug fix: "Remove time delay" being accidentally active in alignment tool

### Update 12/1/2025 PureEQ v2.6.7 changelog -
This is technically a bug fix - frequency range is logarithmic, so the typical "median" is not actually the midpoint of the min/max XO. It needs to be the geometric mean of min/max XO to be the correct "midpoint" of the usable XO range.
* Use geometric mean of the usable XO range for aligning SW to system
* Log alignment frequency for better transparency

### Update 11/30/2025 PureEQ v2.6.6 changelog -
Minor update to skew the preference towards lower crossovers and reduce chance of localization.
* Min XO is set based on half an octave above subwoofer's low frequency extension instead of a full octave
* Final XO is determined within initial XO and half an octave above initial XO instead of a full octave

### Update 11/28/2025 PureEQ v2.6.5 changelog -
This update is geared towards multiple subwoofer .adys, especially those where the subwoofers extend out very far into the highs. It tends to mess with the impulse response and hide the effects of group delay.
* Apply a 250hz LPF when aligning multiple subwoofers so higher end of the response does not affect delay range calculation
* Cleanup the logic a little bit

### Update 11/27/2025 PureEQ v2.6.4 changelog -
REW alignment tool's delay range needs to span negative to positive. But since custom doesn't explicitly use the "Align IR" or "Align Phase" functions, proximity based delay ranges can be tightened up around the first peak, allowing both to be either negative, positive or any combination as needed.
* Tighten up proximity based delay ranges - this will further emphasize time alignment when optimizing subwoofer delays
* Enforce a minimum of +/-3ms delay range span if first IR peak time difference is very small

### Update 11/25/2025 PureEQ v2.6.3 changelog -
A lot of times folks use the same PEQ filters for all speakers, like adding in a high shelf. This update should make the process much easier.
* Add an "All Speakers" EQ table to apply upto 15 PEQ filters globally to all speakers except subwoofers
* Update all internal functions, including import/export, to work with the "All Speakers" table

### Update 11/23/2025 PureEQ v2.6.2 changelog -
* Use midpoint of usable XO range for aligning SW to system

### Update 11/21/2025 PureEQ v2.6.1 changelog -
As everyone's seen, a lot of the recent updates have been about revisiting old approaches that didn't work as well in the past due to how custom did certain things. One such thing I have been testing today and I was blown away by the improvements - level matching non MLP positions to MLP prior to averaging. The idea was to remove SPL differences between positions, so the response trend is better isolated for EQ. After the recent fixes to auto-leveling compensation, the real benefit of this approach is really shining through. I feel like the imaging just snapped into place in a way I didn't think was possible...
* Align non-MLP positions to MLP before spatially averaging (only affects REW filtering)
* This also allows wider mic spacing measurements to have that same "close to the music" feel as tightly grouped measurements

Curious if others also notice a similar difference. This isn't a beta since the improvements were very obvious to me, so use the link in the first post to grab the latest script. Enjoy!

### Update 11/20/2025 PureEQ v2.6.0 changelog -
Alrighty, time to make it official :)
* Use the aggressive target leveling approach from 2.4.x, however -
* Psy smoothing is used to determine SPL, so it strikes a balance between the heavier cuts in 2.4.x and the lighter EQ approach of 2.5.x
* Rework the logic for auto-leveling compensation so post-EQ levels match in SPL to target much more accurately
* Improvements to XO determination and evaluation
* Initial XO is set based on nearest XO to roll-off + 15hz
* When evaluating final XO, a higher XO must provide more than 0.1dB extra output to be considered
* Updated TCx curve

Thanks to all who tested, happy listening!

### Update 11/18/2025 PureEQ v2.5.3 changelog -
* Improve average speaker/subwoofer level matching
* SW integration should now be almost completely target curve agnostic
* Revert back to an older logic where average initial XO was used to apply a singular LPF/HPF to the average speaker/subwoofer combo
* Seems to be a bit more robust than applying LPF/HPF to all channels first before averaging
* Simpler and quicker

### Update 11/18/2025 PureEQ v2.5.2 changelog -
* Use alignment tool's gain A/B to level match average speaker/subwoofer so SW integration is as target curve agnostic as possible
* Target level will be capped at 75dB
* In some cases, if a response has its bass rise starting very early, using 200-2khz could set target level above 75dB and the midrange level would be too low and no longer be level matched with other speakers
* For speakers that suffer from SBIR more in that region, custom will still correctly set their target level lower than 75dB to match the lower midrange to target without using boost headroom
* Streamline some of the logic

### Update 11/17/2025 PureEQ v2.5.1 changelog -
This is a bit of an experiment. While playing with different smoothing for determining trims, I decided to try 1/6th and really liked the results. I also generally like 1/6th because it's one step more granular than human hearing, which makes it ideal for critical listening adjustments.
* Switch to using 1/6 smoothing for determining trims

You can expect a slightly louder sound, better overall balance, and a bit fuller bass resulting from marginally higher SW trims.

### Update 11/14/2025 PureEQ v2.5.0 changelog -
Since most of the changes are going back to older tested logic that worked well, I'm happy with the shorter testing duration to make sure nothing's broken with the beta.
* Revert target leveling logic to an older approach.
* For speakers set target level similar to REW, using 200-2khz region, to get the SBIR region as close to target as possible without boost.
* For subwoofers set target level similar to REW, using bandwidth (but limit to 20-120hz), to get the dips closer to target without using boost.
* Use max possible range that's based on min/max XO to evaluate SW integration & XO optimization.
* Adjustments to TCx - this is my personal TC and will likely change over time based on my own system's response.

### Update 11/13/2025 PureEQ v2.4.5 changelog -
* Custom uses the aggregate -3dB points to establish evaluation range when aligning multiple subwoofers. This can work negatively if there is infrasonic noise or if the subwoofer plays a lot higher in the frequency range. With this update, custom will limit the evaluation range to 20-120hz when aligning multiple subwoofers if the aggregate -3dB points exceed it.
* This prioritizes alignment in the core LFE frequency range.
* Make delay search step a little smaller so it evaluates more granular delays.

### Update 11/12/2025 PureEQ v2.4.4 changelog -
* Adjust alignment tool gains when aligning multiple subwoofers so level differences do not affect delay evaluation
* Tighten up SW integration & XO determination evaluation ranges

### Update 11/10/2025 PureEQ v2.4.3 changelog -
* Minor update - Fine tune target level determination for REW filtering mode.

### Update 11/9/2025 PureEQ v2.4.2 changelog -
Trying out a change I have been thinking about for a while. The first IR peak function looks for the first +/-10% change to determine signal start time; however, in a lot of cases there can be pre-ringing that exceeds it and cause the function to settle on the wrong thing.
So, the changelog for PureEQ v2.4.2 is as follows-
* Use standard deviation of the impulse response as the threshold for determining first peak
* This makes it so that the noisier the impulse response is, the higher the threshold is for determining the first peak
* For cleaner impulse responses, it should continue to work as it did before
* Edit: Reduced high shelf default values to +/-3dB
* Edit2: Minor UI bug fix where REW filtering sliders were still active after optimization start

Lmk if you get any weird subwoofer distances with this change. Enjoy!

### Update 11/8/2025 PureEQ v2.4.1 changelog-
* SBL will get the correct enChannelType assigned based on if it's mono or stereo
* SWMIX commandIds will be fixed if they contain erroneous indexes
* Distances will be determined based on IR data instead of expecting MultEQ app to initialize variables under "channelReport" which could be hit or miss
* Absolute distances will also be scaled based on speed of sound of AVR
* New "TCx" target curve - I've been using this with my B&Ws for a while now and really like how it sounds

### Update 11/5/2025 PureEQ v2.4.0 changelog -
* Directional bass will now be converted to standard bass in Audyssey filtering mode
* Virtual subwoofer IR for each position will be injected into the ady for Audyssey to EQ
* Compatibility with the lexicographical sorting with REW beta 104
* Audyssey filtering mode is now a selectable option instead of shift + click
* Measurements will now be extracted with the correct IR delays
* The systemDelay parameter in the ady is now used to calculate the timing reference/offset of the Audyssey measurements

Thanks to all who tested, enjoy! :)

### Update 10/28/2025 PureEQ v.2.3.1 changelog -
* Fine tune delay ranges

### Update 10/27/2025 PureEQ v.2.3.0 changelog -
* Use first IR peak for subwoofers to determine proximity and establish delay range
* This prioritizes LFE time alignment when finding optimal delays
* Code cleanup

### Update 10/25/2025 PureEQ v2.2.2 changelog -
* Fix an intermittent issue where using dialogue enhancer could cause the script to crash.

### Update 10/24/2025 PureEQ v2.2.1 changelog -
You can thank @JasonCzerak for this update
Found and fixed an issue thanks to his directional ady from his brand spanking new x4800h!
* Switch to rms+p from va for creating the "average" speaker/subwoofer for SW integration.
* In some cases VA just took away so much SPL that there wasn't enough of a response left for optimizing delay and resulted in bad integration.

### Update 10/24/2025 PureEQ v2.2.0 changelog -
The additional changes to SW integration made it more of a 0.1 bump instead of a 0.0.1 bump. So here is the latest main release!
* Aggressively set target level for EQ
* Custom will now evaluate different portions of the response and level the target curve based on the weakest region
* Easier for EQ to shape the response using primarily cuts
* This will result in a fuller sound and better target tracking
* Proximity based delay range limitation for SW integration
* Prioritizes time alignment when finding the delay with max output
* Avoids edge cases where subwoofers can get assigned a distance of 0m
* Apply LPF/HPF slopes before generating the "average" speaker
* In prior versions custom would average first, apply LPF/HPF using average XO afterwards
* Now it applies LPF/HPF to subwoofer/speaker for each channel first and then averages
* Takes into account phase/impulse shifts due to different XOs much better
* This should produce more output throughout the speaker to subwoofer crossover region

### Update 10/21/2025 PureEQ v2.1.2 changelog -
* Revert partial changes from 2.1.1 - I didn't like how the EQ target levels were inconsistent based on target curves, so the logic has been reverted partially to how it was prior to 2.1.1-
* Speaker target level is set taking into account SBIR instead of full bandwidth.
* Initial XO and usable XO determination update - slight change in logic to find the next/prev available XO instead of the nearest. This ensures that initial XO and usable XO range do not fall outside speaker/subwoofer bandwidths.

### Update 10/19/2025 PureEQ v2.1.1 changelog -
* Minor adjustments to REW EQ params.

### Update 10/17/2025 PureEQ v2.1.0 changelog-
* Brute force evaluate delays instead of frequencies to find optimal alignment
* Fine tune low/high frequency roll-off determination logic
* Switch to VA when creating the "average" speaker for SW integration
* Remove timeouts on Mac - newer REW betas seem to be very stable and this should no longer be needed

### Update 10/15/2025 PureEQ v2.0.2 changelog-
* Switch to using absolute -3dB points for roll-off and initial XO determination
* XOs can be lower and SW distances may be higher as a result
* Should reduce subwoofer localization
* Less XO and SW distance variability based on target curve
* Better handling of low shelf using the slider control
* SW bandwidth will reflect any additional extension from low shelf
* Improvements to EQ accuracy
* Shift raw responses to reflect effects of AL comp

### Update 10/13/2025 PureEQ v2.0.1 changelog -
* Ability to export logs once optimization is completed
* Only .json files will be allowed when importing EQ filters
* MJC version number will now be appended to the generated ady and the log file

### Update 10/12/2025 PureEQ v2.0.0 changelog -
* Full UI support for configuring boost parameters
* Sliders only apply to REW filtering
* Full UI support for configuring custom filters per speaker
* This is applied on top of the room correction
* It works in both REW and Audyssey filtering mode
* Upto 20 filters per channel - only 3 are visible initially but additional slots will unlock as they fill up
* Import/Export function to easily save filters for future use
* If filters contain channels not in the ady, they will be ignored during import
* Users will be able to export the filters both before and after optimization

### Update 10/6/2025 PureEQ v1.5.4 changelog-
* Look for "Customization start" in the script to find the areas for user modifications
* Examples are provided in those customization sections
* Add up to 20 PEQ/LS/HS filters for each speaker as desired
* Prevent user customization filters from overwriting auto-EQ filters
* Extra safety checks when applying user customization filters
* Streamline code for Audyssey filtering

### Update 10/2/2025 PureEQ v1.5.3 changelog -
* Use pre-EQ responses for SW integration and XO optimization

### Update 9/30/2025 PureEQ v1.5.2 changelog-
* Added ease of customizability of EQ and dialogue enhancer parameters. Context - https://www.avsforum.com/posts/64229170/
* Streamlined some of the optimization logic.
* Final XO determination will prioritize maximum output.
* Dynamic bass fill swapped out for subwoofer target level adjustment prior to EQ, similar to how SBIR compensation works.
* Improvements to subwoofer abs -3dB point calculation accuracy.
* Code cleanup.

### Update 9/27/2025 PureEQ v1.5.1 changelog -
* Expand proximity based delay range calculation to allow for positive delay

### Update 9/27/2025 PureEQ v1.5.0 changelog -
* (Optional) Audyssey filtering mode - Custom will only optimize levels, crossovers and distances but will leave the EQ portion to Audyssey.
* Target curve is injected into ady and the default audyssey HF rolloff is removed.
* Multi-subwoofer alignment and integration to speakers will be done similar to how custom has always done it, except with one change -
* Officially supported directional bass adys will be preserved as directional.
* Great way to A/B audyssey filters vs REW filters, all else being kept as equal as possible.
* Press and hold shift key when clicking "Optimize Calibration" to enable this mode.
* Usage of proximity based delay range when aligning multiple subwoofers to prioritize time alignment.
* Support for standard bass adys from newer AVRs that support directional natively.
* Code cleanup.

Happy weekending all! :)

### Update 9/23/2025 PureEQ v1.4.1 changelog -
* Added support for max 18m relative distance on AVRs that support it.

### Update 9/22/2025 PureEQ v1.4.0 changelog -
* Preserve MLP measurements all the way through to the end
* MLP is now exclusively used for SW integration
* MLP is now exclusively used for XO optimization
* Custom will now show predicted MLP as well as AVG responses
* It will show how EQ filters generated from a spatial average prevent overcorrection at the MLP
* Response inconsistency between positions will show up as less correlation between MLP and AVG
* It will show how SW integration and XO optimization using MLP affects AVG
* Measurements will be organized in MLP/AVG alternating manner, so it is easy to compare
* Log the aggregate -3dB points used when optimizing multiple subwoofers
* Fine tune smoothing for different portions of the optimization

### Update 9/18/2025 PureEQ v1.3.0 changelog -
* Switch to using MLP measurements exclusively for time alignment
* Switch to using MLP measurements exclusively for multi-sub optimization
* Combined sub response for each position is generated and then used for a more accurate spatial average
* Subs are aligned in order of closest to farthest to avoid anomalies where one sub has a very irregular IR response
* Added metric to determine SW spatial variation between measurement positions
* Dialogue enhancer gain increased from 1.5dB to 3dB
* Improved EQ frequency limits handling
* Improved LF/HF roll-off detection
* Bug fixes with IR normalization

### Update 9/13/2025 PureEQ v1.2.2 changelog-
* (partial) Android volume bug fix - this is only applicable for cirrus logic models and when using the android app to take measurements
* It is a partial fix because it does not fix the issue of subwoofer trims always bottoming out at -12; you will need the version linked in the first post to properly fix that
* Support for target curves with special characters in their name
* Update to audy2umik

### Update 9/8/2025 PureEQ v1.2.1 changelog -
* Use 1/1 for leveling - this better represents real world perceived loudness using a SPL meter
* Use Var for aligning TC to response - does a better job of balancing out the level of the SBIR affected region
* Cleanup code that handles perfect speaker response assignment for cirrus logic models
* More granular leveling, especially in the bass region - this improves subwoofer target tracking for difficult responses.
* Reorganized a lot of sanity checks and initial boot up logic for better measurement checking & error handling.

### Update 9/5/2025 PureEQ v1.2.0 changelog-
* Remove step that volume aligns non-MLP positions to MLP before averaging
* Custom has volume aligned other positions to MLP before averaging for the longest time, but this is an incorrect approach
* The level differences between positions play an important role with correctly representing tonal balance when spatial averaging
* You can thank ChatGPT and Gemini for helping me figure this out!

This update should improve leveling consistency as well as imaging balance. Happy listening!

### Update 9/3/2025 PureEQ v1.1.2 changelog-
* Bug fix with delay headroom calculation - there was a little more available delay range which I missed in earlier versions.

### Update 9/1/2025 PureEQ v1.1.1 changelog-
* Improved HF consistency across channels
* Added more safety checks when using manual measurements
* Code cleanup and speedup during preprocessing stage
* Bug fix for a case where C and CH channels were being mixed up

### Update 8/29/2025 PureEQ v1.1.0 changelog -
Thanks to all who tested out dev. So far it seems to be a net positive and I am moving forward with releasing it as part of main. Changelog for PureEQ v1.1.0 -
* Better SBIR handling - custom will now level the TC to the response similar to REW before EQ; this gets the SBIR affected region better lined up with target and reduces tonal differences due to unfixable dips.
* Added flexibility for manual measurements - ady no longer needs to match exact number of measurements. As long as ady matches # of channels and model #, custom will move forward with optimizing manual measurements.
* For cirrus logic models, custom will also skip applying Audy mic cal if it detects manual measurements.
* For directional2standard conversion, use absolute -3dB points instead of -3dB points from target. This makes the multi-sub alignment process target curve agnostic and improves consistency of results.
* Allow more granular leveling, especially in the bass region - this improves subwoofer target tracking for difficult responses.
* Reorganized a lot of sanity checks and initial boot up logic for better measurement checking & error handling.

### Update 8/21/2025 PureEQ v1.0.1 changelog -
* Figured out why DE would get greyed out - if it was clicked before an ady was uploaded, it would just disable itself. This behavior is now fixed.
* The option will only get greyed out now if an ady without a center is uploaded.
* Cfinal measurement will now have "DE" in the name if dialogue enhancer is used.
* Versioning added to top right of script instead of in the logs.

### Update 8/20/2025 PureEQ v1 changelog -
PureEQ has now been merged to the main branch. Here's the changelog for PureEQ v1:
* Midrange focused leveling to improve imaging
* Reduce speaker boost headroom to preserve more of the natural sound
* Use high shelf as tone control to line up the top end across channels for immersion
* Movie mode is now deprecated in favor of PureEQ - #492
* Moved all the long variables to the bottom of the code to make it more readable
* Added versioning for future changes to main branch

### Update 8/3/2025 changelog-
Prior update started using -3dB points to better control correction range. This allowed the usage of using LPF/HPF to increase boost for subwoofers without producing any artifacts.
* Use -3dB points to establish LPF/HPF for EQ.
* Increase boost headroom for subwoofers to 6db individual and 3db overall in movie mode.
* Previously it was 3db individual, 1db overall. Boost limits for speakers are unchanged.
* Allow low shelf of +/-3db for subwoofers in movie mode.
* Speakers were already allowed a +/-3db high shelf in movie mode for better TC tracking.
* Handling for edge cases where subwoofers have very wide bandwidths.
* Improvements to leveling.

### Update 7/27/2025 changelog -
I was planning on releasing this a little later, but it has some much-needed bug fixes. Here's the changelog-
* Fixed an issue with calculating remaining delay that could cause speaker distances to exceed 6m.
* Subwoofer bandwidth is now used for setting trims - previously the subwoofer would sometimes be leveled too low or too high if the response was very choppy or had limited bandwidth.
* Auto leveling compensation is now handled in the filters - trims will no longer be adjusted to compensate for auto leveling. This will improve volume stability when switching between Full range, partial and no EQ (like pure direct).
* Code cleanup and bug fixes for REW crashes on Mac.

### Update 7/21/2025 changelog -
* Added support for systems without a subwoofer.
* Added support for 70hz crossover on models that does/will support it.
* Changed to a darker color scheme.
* Bug fixes and code cleanup.

### Update 7/6/2025 changelog -
New version uploaded today. Changelog-
* Added subwoofer bandwidth detection based on target curve (-3dB points)
* Sub bandwidth is now used to ensure sub delay is optimized based on what the sub can play
* Crossover ranges are now limited by SW bandwidth to prevent distortion
* Improve speaker roll-off detection accuracy based on target curve
* No target curve mode: Custom will now use a downward slope matching general downward trend of most speakers (instead of flat) when a TC isn't provided and enable DEQ
* Bug fixes and code cleanup

### Update 6/26/2025 changelog -
Thanks to all who tested! New version released this morning with the following changes-
* Dynamic EQ mode - run the script without a target curve selected to EQ to Flat and enable Dynamic EQ
* Improved movie mode target curve tracking in the high frequencies
* Improved general averaging, leveling and EQ performance

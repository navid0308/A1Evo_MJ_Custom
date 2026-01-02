# A1Evo_MJ_Custom

This is a custom version of the A1 evo maestro MJ script that I have built for my personal use.

It's based on OCA's original work here - https://www.youtube.com/watch?v=lmZ5yV1-wMI


Guides, Changes and FAQs - https://www.avsforum.com/threads/a1evo-mj-custom.3325897/

## Changelogs
### Update PureEQ v2.8.4 changelog -
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





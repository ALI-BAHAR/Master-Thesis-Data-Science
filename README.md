# Master-Thesis-Data-Science

Code accompanying the MSc thesis *Synthesis of Mechanistic Phytopathology Models
through Composition: the Simulation of Tuta absoluta over Tomato* — University of
Verona, Department of Computer Science, 2025–2026.

The work composes the TOMGRO tomato crop model with a stage-structured
*Tuta absoluta* population model (egg, larva, pupa, adult) through explicit
two-way interfaces: the canopy supplies the leaf resource that limits larval
recruitment, and larval feeding reduces leaf area, which then propagates through
crop growth to fruit biomass.

## This repository is for reading, not for running

The PyCrop simulation framework is not redistributed here, and the raw field
workbooks from the two farms are not published either. The notebooks therefore
cannot be executed from a clone.

They are stored with their outputs, so every figure and every number can be seen
in place: the code that produced a result sits directly above the result it
produced.

## The notebooks

| Notebook | What it does |
| --- | --- |
| `Scandola_Analysis.ipynb` | The Scandola application: calibration blocks, the retained configuration, the pest and crop results |
| `Brunelli_Analysis.ipynb` | The full Brunelli workflow: initial-state estimation, the focused parameter refinement, pest and crop results |
| `01_Original_Milan_Brunelli_SOURCE_ONLY.ipynb` | The original Milan resource–consumer formulation, reconstructed from its own published parameters |
| `02_Final_Composed_Brunelli_BENCHMARK_EXPORT.ipynb` | The composed Brunelli configuration, reduced to the run and export used by the benchmark |
| `03_Evaluate_Milan_vs_Composed_COMMON_PROTOCOL.ipynb` | Post-processing only: one scoring protocol applied to both exports |

The separation matters. The reference model is simulated only in `01`, the
composed model only in `02`, and `03` runs no simulation at all — it reads the
two exported trajectories and scores them identically. Neither model can be
favoured by its own evaluation code.

## Results

Scandola, against the untreated Testimone surveys. One configuration produces
egg, larva and adult results; there is no separate adult parameterisation.

| | Pearson r | Direction | Dominant peak |
| --- | --- | --- | --- |
| Egg | 0.806 | 7/10 | Day 69, error 0 d |
| Larva | 0.780 | 9/10 | Day 62, error 0 d |
| Adult, by trap interval | 0.998 | 5/7 | Day 62, error 0 d |

Adults are not counted on leaves. A pheromone trap accumulates catches between
inspections, so the simulated adult state is integrated over each trapping
interval before comparison. The intervals are unequal, from six to twenty days,
which is why the direction score is the more informative number in that row.

Brunelli, against the same kind of surveys, and the same observations scored
against the reconstructed reference model:

| | Original Milan | Composed |
| --- | --- | --- |
| Egg Pearson r | 0.569 | 0.784 |
| Larva Pearson r | 0.478 | 0.778 |
| Adult Pearson r | −0.242 | 0.739 |
| Egg peak-timing error | +28 d | 0 d |
| Larva peak-timing error | +28 d | 0 d |
| Adult peak-timing error | +33 d | 0 d |

Crop response against a no-pest counterfactual, under identical forcing, crop
parameters and crop initial conditions: at Day 69, Scandola loses 2.98% of leaf
area index and 1.12% of simulated fruit biomass; Brunelli loses 25.84% and
12.70%.

## How to read the comparisons

Field counts and internal model states are not on a common scale, and no
observation model links them. Nothing is normalised, amplitude-scaled, smoothed
or shifted in time, and no catchability coefficient is fitted. The evaluation is
therefore about temporal organisation — correlation, direction of change between
consecutive surveys, and the timing of the dominant peaks — not about absolute
abundance.

Two limits are worth stating plainly. Each site is calibrated separately, so this
is not a transfer test in which one parameter set is carried unchanged to a new
site. And the benchmark compares complete workflows that differ in more than the
crop representation, so the improvement belongs to the workflow as a whole rather
than to any single component.

The crop-damage percentages are model-predicted effects. No fruit was weighed in
the field.
## Image credits

The tomato photograph on the cover of the defence deck shows fruit damage by
*Tuta absoluta* larvae — Metin GULESCI, Bugwood.org, CC BY 3.0 US. The adult
moth photograph used in the thesis is by Ben Sale, CC BY 2.0.


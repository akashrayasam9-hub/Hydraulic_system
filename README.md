Why I came back to it
I wrote the report, submitted it, graduated. Two years later, working my way into data, I opened it again and noticed something uncomfortable.
The report ran to forty-odd pages and buried its main finding in two numeric tables on pages 38 and 39. Every conclusion was correct — and almost impossible to grasp without reading the whole document. The analysis existed. It just wasn't legible.
Closing that gap is what data visualisation is for. So I treated my own report as a client deliverable and rebuilt it.

The problem
A car's shock absorber has one job: stop the vehicle bouncing. It does this by forcing hydraulic fluid through small orifices, which converts the suspension's motion into heat. That heat is dumped into the atmosphere and gone forever.
Published studies put the loss through suspension dampers at roughly 200 W across four dampers on a poor road, and up to 1600 W per absorber under severe conditions. On Indian roads, which is where I was doing all this wondering, the upper figure is not hypothetical.

The question: instead of throwing that energy away as heat, can you rectify the up-and-down piston motion into one-way fluid flow, spin a hydraulic motor with it, and drive a generator?
What the system does
Six components, in sequence:
1.	Hydraulic cylinder replaces the conventional shock absorber — same dimensions, but with four side ports and no orifices in the piston
2.	Four check valves act as a hydraulic rectifier, so fluid flows one way regardless of whether the piston is compressing or extending
3.	Diaphragm accumulator smooths the pulsing flow
4.	Gerotor hydraulic motor converts fluid pressure into shaft rotation
5.	PMDC generator converts that rotation into electricity
6.	Pipelines and fittings connect it all
The design constraints I worked to: 50 mm bore, 20 mm rod, 200 mm stroke, 35 bar peak pressure, 200 bar burst limit. Those drove a required motor displacement of 10.07 cc/rev, which I matched to a commercially available Parker M4-060 at 9.8 cc/rev.


The data
There was no dataset. There was a PDF. Building one was the first real task, and the part I'd argue matters most.

I extracted four tables:
 <img width="468" height="138" alt="image" src="https://github.com/user-attachments/assets/debddd66-91d2-415d-ac9b-12cc69db2e95" />

 The one design decision worth flagging: the original report held compression and extension in two separate tables. Two tables cannot be compared in a single chart. I stacked them into one table with a Stroke column, which turned an awkward side-by-side reading exercise into a one-glance comparison. That reshape — long format instead of wide — is the whole reason the headline chart works.
I also derived flow rate in litres/min alongside the original m³/s, because nobody reads 0.0001963 as a quantity.

The model
The calculation chain runs:
piston velocity → flow rate (Q = v × A)
               → motor speed (N = Q × ηv × 60 / D)
               → angular velocity (ω = 2πN / 60)
               → EMF (E = kv × ω)
               → power (P = E² / R)
Constants: volumetric efficiency 90%, motor displacement 9.8 cc/rev, generator constant kv = 0.930, load resistance 40 Ω.
Note the squared term. That single exponent is why power behaves completely differently from speed, and it's the finding the dashboard makes obvious.

Where this model is honest about its limits: it ignores pressure losses, fluid compressibility, and the accumulator's damping effect. It's an upper bound on potential, not a prediction of delivered output. I've kept that caveat visible rather than buried, because a portfolio piece that oversells its own numbers isn't worth much.

Evaluation and observations
Four things became visible once the data was charted that were not visible in the report.
1. Power is quadratic; speed is linear. Motor speed plots as a straight line against piston velocity. Power plots as a curve. Side by side, the difference is unmissable — and it explains itself immediately once you see E² in the chain. In the report, these two facts sat forty pages apart and looked unrelated.
2. Compression consistently outperforms extension by about 30%. At 0.1 m/s: 277 W compressing versus 196 W extending. This isn't an error — the piston rod occupies part of the rod-end chamber, so the swept area is 1.649×10⁻³ m² instead of 1.963×10⁻³ m². Less displaced fluid, less flow, less power. Visible instantly as the gap between two lines; nearly invisible as two columns of numbers in separate tables.
3. The check valve is the dominant loss. 0.645 bar out of 1.136 bar total — more than half, and more than double the next-largest source. Sorted as a bar chart, this is a one-second read and an immediate engineering priority. In the report it was a calculation among calculations, with no relative weighting given.
4. The result sits credibly among published work. 235 W against Wang's 260 W and Fang's 200 W. Not an outlier in either direction, which is the reassuring answer for a theoretical model.

Outcome
At an average piston velocity of 0.1 m/s, a single absorber regenerates approximately 235 W. Four absorbers, and the figure becomes meaningful for a vehicle.
The exponential relationship carries a counterintuitive implication: worse roads generate more power. This inverts the usual assumption that rough terrain is purely a cost. For construction-site haulers, military vehicles, and off-road fleets, the conditions that damage a vehicle are also the conditions that feed it.

Business relevance
Range anxiety remains the primary obstacle to electric commercial vehicle adoption, and it's sharpest exactly where the duty cycle is roughest — mining haulage, construction logistics, agricultural fleets, defence. Those are the operators for whom this system generates the most, and they're also the ones for whom charging infrastructure is thinnest.
The economics are unusual: the system converts road quality from a pure liability into a partial asset. A fleet operating on degraded roads recovers more energy than one on smooth highway, which flips the normal relationship between terrain difficulty and operating cost.
The honest limit: this is theoretical and prototyped, the check valve alone eats over half the available pressure, and the added mass and complexity of four hydraulic circuits would need to be weighed against the recovered energy. The next step is a physical prototype and measured data — which would also give this dashboard something considerably more interesting to display.

What I took from it
The engineering was already done. What this project required was different: deciding what the data actually needed to say, reshaping it so it could say it, and choosing four views that answer four questions instead of twenty that answer none.
The two findings I'm most pleased with — the linear/quadratic contrast and the check valve's dominance — were both fully present in my original report. Neither was visible. That's the argument for this work in one sentence.
The wider thing I took from it is that the question I asked in 2020 was wrong, and asking it anyway was still the most useful thing I did that year. It didn't fix the car. It did teach me where the energy goes, and later, that knowing where the energy goes and being able to show someone where it goes are two separate skills.



# FINDING PREFERABLE MOLECULES
* QED - QED stands for quantitative estimation of drug-likeness and the concept was for the first time introduced by Richard Bickerton and coworkers. The empirical rationale of the QED measure reflects the underlying distribution of molecular properties including molecular weight, logP, topological polar surface area, number of hydrogen bond donors and acceptors, the number of aromatic rings and rotatable bonds, and the presence of unwanted chemical functionalities.

* Microsoft and Novartis developed MolSkill to find preferable drug molecules: We also show that the proposed learned scoring function can better capture the concept of drug-likeness more accurately than another widely used metric (QED).

[Pat Walters's opinion](http://practicalcheminformatics.blogspot.com/2023/04/getting-inside-mind-of-medicinal.html): In the MolSkill paper, the authors show that the two metrics are not correlated, but I wonder if MolSkill is telling me something I'm not getting from QED.  At the end of the day, I like to use tools I understand. QED is based on simple descriptors I've used for years, and I know how it works.  MolSkill is based on a neural network and is a bit of a black box)

* SA-score (synthetic accessibility (SA) score as a score between 1 (easy to make) and 10 (very difficult to make), Synthesizability score to identify odd molecules): The SA score approach begins by using rules to derive a set of molecular fragments and their frequencies from almost a million molecules randomly selected from the PubChem database.  The SA score for a new molecule can then be calculated by fragmenting the molecule according to the same set of rules and looking up the frequency of the fragments.  If a molecule contains frequently occurring fragments, people have probably made similar molecules before, and we consider the molecule synthesizable.  If the molecule contains rare fragments that haven't been seen before, it will likely be more challenging to synthesize. [LINK](https://jcheminf.biomedcentral.com/articles/10.1186/1758-2946-1-8)

# Filtering Chemical Libraries


* Lipniski's Rule of Five (RO5)
* Pat walters developed REOS (Rapid Elimination of Swill) to eliminate compounds with the sets of substructures which are likely to produce artifacts in cellular assay.
* Eli Lily develop a software with 275 rules to eliminate flase positive HIT [LINK](https://github.com/IanAWatson/Lilly-Medchem-Rules)
* StarDrop/Pipeline pilot has substructure filter to remove PAINS compounds 
* BARD: Bioassay Research database [BARD](http://bard.nih.gov)
* PAINS filters developed by Bael and Holloway (In a highly cited study, Baell and Holloway analyzed compounds that showed activity in multiple assays and
suggested that these compounds may interfere with the bioactivity detection technology. Such compounds were cleverly dubbed PAINS, or Pan-Assay INterference compoundS.)
* Pat Walters's blog about [Filtering Chemical Libraries](http://practicalcheminformatics.blogspot.com/2018/08/filtering-chemical-libraries.html)

### [PAINS alerts by Bael and Holloway ](http://medicinal-chemistry.org/files/aldrich/PAINs.pdf)
The authors then identified 480 “PAINS alerts”, i.e., substructural features frequently found in PAINS, and suggested that these alerts could be used to flag false screening hits and annotate suspect compounds in screening libraries

### [Discussion against PAINS filtering by Tropsha](https://pubs.acs.org/doi/pdf/10.1021/acs.jcim.6b00465)
The use of substructural alerts to identify Pan-Assay INterference compoundS (PAINS) has become a common component of the triage process in
biological screening campaigns. These alerts, however, were originally derived from a proprietary library tested in just six assays measuring protein−protein interaction (PPI) inhibition using the AlphaScreen detection technology only; moreover, 68% (328 out of the 480 alerts) were derived from four or fewer compounds. In an effort to assess the reliability of these alerts as indicators of pan-assay interference, we performed a large-scale analysis of the impact of PAINS alerts on compound promiscuity in bioassays using publicly available data in PubChem. We found that the majority (97%) of all compounds containing PAINS alerts were actually infrequent hitters in AlphaScreen assays measuring PPI inhibition. We also found that the presence of PAINS alerts, contrary to expectations, did not reflect any heightened assay activity trends across all assays in PubChem including AlphaScreen, luciferase, beta-lactamase, or fluorescence-based assays. In addition, 109 PAINS alerts were present in 3570 extensively assayed, but consistently inactive compounds called "Dark Chemical Matter". Finally, we observed that 87 small molecule FDA-approved drugs contained
PAINS alerts and profiled their bioassay activity. Based on this detailed analysis of PAINS alerts in nonproprietary compound libraries, we caution against the blind use of PAINS filters to detect and triage compounds with possible PAINS liabilities and recommend that such conclusions should be drawn only by conducting orthogonal experiments.

### Structure alerts ChEMBL databse

We have compiled a number of sets of publicly-available structural alerts where SMARTS were readily available and useable; these include Pfizer LINT filters, Glaxo Wellcome Hard Filters, Bristol-Myers Squibb HTS Deck Filters, NIH MLSMR Excluded Functionality Filters, University of Dundee NTD Screening Library Filters and Pan Assay Interference Compounds (PAINS) Filters. These sets of filters aim to identify compounds that could be problematic in a drug-discovery setting for various different reasons (e.g., substructural/functional group features that might be associated with toxicity or instability in in vivo info settings, compounds that might interfere with assays and for example, appear to be 'frequent hitters' in HTS). It should be noted however that some alerts/alert sets are more permissive than others and may flag a large number of compounds. Results should therefore be interpreted with care, depending on the use-case, and not treated as a blanket filter (e.g., around 50% of approved drugs have 1 or more alerts from these pooled sets). The compound report card page now provides a summary count of the number of structural alerts hits picked up.

### [Pat Walters's filtering](https://github.com/PatWalters/rd_filters)

He tried Inpharmatica structural alerts from ChEMBL against HIV dataset from DeepChem and sum up some ideas:
* Most screening collections contain a lot of molecules that probably shouldn't be there.*
* Structural alerts provide a means of identifying and potentially eliminating some of these potentially problematic molecules.
* The rd_filters.py script provides a convenient way of applying a number of different sets of structural alerts to a set of molecules. Please give it a try. 
* A lot of these filters are somewhat subjective and based on people's experience.  4 of the 8 rule sets in ChEMBL will reject the sulfonic acids shown at the beginning of this post, the other four will not.







# Case forecasting pharmacutical sales  

In partnership with Teva pharma  
![Teva pharma](/img/teva_logo.png)  

## Data description  

The file contains the following columns:  
|Column name|Explanation|
|---|---|
|Morion ID|ID of the medical product|
|ATC Code (1)|ATC classification, first level, most general; you can find the description here: [https://www.who.int/tools/atc-ddd-toolkit/atc-classification](https://www.who.int/tools/atc-ddd-toolkit/atc-classification)| 
|ATC Code (2)|ATC classification, second level|
|ATC Code (3)|ATC classification, third level|
|ATC Code (4)|ATC classification, fourth level|
|ATC Code (5)|ATC classification, fifth level, most granular|
|Brand|Anonymized code for the brand|
|INN|Molecule or molecule combination|
|NFC (1)|Form or presentation of the product|
|Description|Product description, including concentration/ strength and pack size|
|2019 01 - 2023 12|All columns with yeah-month name are containing the quantity sold (number of packs) that month, for the product ID|
	
• INN : this is the core concept of pharmaceutical products. It is the active substance, that is providing the main therapeutical effect.  
• One active substance can take many forms: oral tablets, gels, syrups, injections, etc. Each product, independent of the form, is characterized by strength and pack size.  Strength is how much active substance is in one pill/ tube/ ampoule, etc. Pack size refers to how many pills are in the package, or how large the tube is, etc.  The quantities sold largely depend on these characteristics. These are specified in the description field and NFC (1) field. They require text processing to be extracted! They might be missing, too!  
• ATC groups refer to the therapeutical group of the product. They can be found on the website specified and they aren’t very complicated. It’s a tree-based structure. ATC groups example for Metformin:  
    
![metformin example](/img/metformin.png)    

• Example: Morion ID 108746, OLANZAPINUM molecule, in the form of tablets, blister containing 28 pills, each containing 10 mg active substance. They belong to the ATC group 2: N05 PSYCHOLEPTICS.  Note that there are many other forms of Olanzapinum in the data.  

## ML/ forecasting tasks
**Level 1.** Forecasting sales for each product is an important task. Forecasting makes sense for 12 months ahead. There are relations between similar products. If one product is not available (usually observable by the 0 sales), patients will opt for a similar replacement. It is a good idea to do forecasting at Molecule (INN) level, or ATC 5, or ATC 4. It is preferable that one model forecasts together all products from one INN (one molecule). Hierarchical models can also be useful. Normalization is difficult, as presentations, strength and package sizes play a role in how much qty is bought.
**Level 2.** A model that links (strength, package size, form of administration) to quantity could be useful. In a sense, does a package of 10 tablets sell twice as much as the package of 20 tablets? Does a 200mg product sell twice less than 100mg product? Or is there a different kind of dependency?
**Level 3.** Graph ML task. Organize the products into a network / graph, linking on their strength, pack size, therapeutical class, etc. And then run graph ML, graph forecasting, to see if there’s an improvement.

## Additional information
[Presentation on Machine learning applications at Teva Pharma ](/img/MLapps_Teva_Pharma.pdf)  

## Data files
* [teva_sales.csv](/data/teva_sales.csv) - full dataset  
* [teva_sales_small.csv](/data/teva_sales_small.csv) - sampled dataset of 20 INNs to be used for development of solution  


## Contact:  

Laura-Maria Tolosi-Halacheva (Associate Director Data Science, Data Services and Emerging Technologies)

Laura-Maria.Tolosi-Halacheva01@teva.bg


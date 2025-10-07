# Project: Credit Card Fraud Analysis

**Credit Card Fraud Analysis** uses exploratory data analysis, visualisation, and predictive modelling to provide insights into the complexity of fraud and identify key factors linked to fraudulent activity.

# ![CI logo](https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png)


## Dataset Content

The dataset used is synthetic and publicly available on Kaggle: [Credit Card Fraud Dataset](https://www.kaggle.com/datasets/dhanushnarayananr/credit-card-fraud/data/code). The full dataset on Kaggle contains one million card transactions, of which approximately 8.7% are labelled as fraudulent.The dataset’s variables are designed to be relevant and aligned with real-world business concepts:
- distance_from_home: distance from the customer’s home to the location of the transaction.
- distance_from_last_transaction: distance between the current and previous transaction.
- ratio_to_median_purchase_price: The ratio between the transaction amount and the customer’s typical (median) purchase size. 
- repeat_retailer: whether the transaction occurred at the same retailer as previous purchases.
- used_chip: whether the transaction used a card chip.
- used_pin_number: whether a PIN number was used.
- fraud: target variable, indicating whether the transaction was fraudulent (1) or genuine (0). 

To keep the project lightweight and efficient, a 100,000-row stratified sample was created in advance. This sample preserved the same fraud prevalence (8.7%) and feature distributions, ensuring validity for analysis while allowing faster processing.

Sampling details, including row counts, fraud rate, and random seed, will be documented in the ETL notebook, and a small accompanying JSON file provided for transparency.

All analysis and modelling for this project will be performed on this 100k sample, with results expected to closely mirror those from the full dataset. Minor variation in statistical outcomes or model performance may occur if the full dataset were used.


## Business Rationale

**Problem Statement**

Credit card fraud is a growing global challenge. Recent reports highlight a dramatic surge in card fraud losses worldwide, with new tactics exposing gaps in current defences (FICO, 2023). Fraud has serious costs for all parties: victims suffer financial losses and stress, while banks face direct losses, higher operating costs, and reputational damage.

**Business Requirements**

To combat these evolving threats, financial institutions are increasingly turning to machine learning and AI. Industry experts emphasise that effective fraud prevention requires models that learn from global fraud patterns, analytics that adapt in real time, and platforms that deploy rapidly while amplifying human expertise (FICO, 2023).

In fraud detection, there is a crucial trade-off between catching more fraud and avoiding false alarms. Missing a fraudulent transaction (a false negative) directly causes financial loss, whereas incorrectly flagging a genuine customer (a false positive) wastes investigative effort and frustrates customers (Soto-Valero, 2023). Business success in fraud detection depends not on raw accuracy (which can be misleading on imbalanced datasets) but about balancing these outcomes.

This project explores how machine learning can identify fraudulent transactions in an imbalanced dataset and how findings can be communicated through a dashboard that supports fraud analysts and business decision-makers. The dataset used is synthetic, containing 8.7% fraudulent transactions (much higher than real-world rates of <0.5%), which provides a practical context for testing fraud detection approaches.

**Business Goals**
- Communicate insights through a dashboard that highlights trade-offs between detecting fraud and minimising false alerts.
- Evaluate how effectively machine learning models can detect fraudulent activity under these conditions.

## Hypothesis **and how to validate**
- H1: Fraud increases with greater distance from the customer’s home.
- H2: Fraud increases with greater distance from the previous transaction.
- H3: Fraud increases when the transaction amount is high relative to the customer’s usual spending.
- H4: Online transactions are more likely to be fraudulent.
- H5: Using a chip or PIN reduces the likelihood of fraud.
- H6: Fraud likelihood differs between repeat and new retailers.
- H7: Adjusting model thresholds will show how trade-offs between false positives and false negatives affect performance.
- H8: Fraud risk depends on the combination of online ordering and chip use.

## Project Plan
* Outline the high-level steps taken for the analysis.
* How was the data managed throughout the collection, processing, analysis and interpretation steps?
* Why did you choose the research methodologies you used?

## The rationale to map the business requirements to the Data Visualisations
* List your business requirements and a rationale to map them to the Data Visualisations

## Analysis techniques used
* List the data analysis methods used and explain limitations or alternative approaches.
* How did you structure the data analysis techniques. Justify your response.
* Did the data limit you, and did you use an alternative approach to meet these challenges?
* How did you use generative AI tools to help with ideation, design thinking and code optimisation?

## Ethical considerations
* Were there any data privacy, bias or fairness issues with the data?
* How did you overcome any legal or societal issues?

## Dashboard Design
* List all dashboard pages and their content, either blocks of information or widgets, like buttons, checkboxes, images, or any other item that your dashboard library supports.
* Later, during the project development, you may revisit your dashboard plan to update a given feature (for example, at the beginning of the project you were confident you would use a given plot to display an insight but subsequently you used another plot type).
* How were data insights communicated to technical and non-technical audiences?
* Explain how the dashboard was designed to communicate complex data insights to different audiences. 

## Unfixed Bugs
* Please mention unfixed bugs and why they were not fixed. This section should include shortcomings of the frameworks or technologies used. Although time can be a significant variable to consider, paucity of time and difficulty understanding implementation are not valid reasons to leave bugs unfixed.
* Did you recognise gaps in your knowledge, and how did you address them?
* If applicable, include evidence of feedback received (from peers or instructors) and how it improved your approach or understanding.

## Development Roadmap
* What challenges did you face, and what strategies were used to overcome these challenges?
* What new skills or tools do you plan to learn next based on your project experience? 

## Deployment



## Main Data Analysis Libraries
* Here you should list the libraries you used in the project and provide an example(s) of how you used these libraries.


## Credits 
**Fraud Research for Business Costs and Rationale**

The following sources were used to support the background research and help determine fraud-related business impacts, false-positive costs, and model threshold choices:
- Credit Card Fraud Detection: 2025 Trends and Interventions, FICO August 2023
- Soto-Valero, C. (2023). Evaluation Metrics for Real-Time Financial Fraud Detection ML Models – Blog.cesarsotovalero.netcesarsotovalero.netcesarsotovalero.net (Covers precision, recall, FPR/FNR business targets, and why AUC-PR is more informative than ROC in imbalanced fraud detection.)
- Alon, T. (2023). Ultimate Guide to PR-AUC: Calculations, Uses, and Limitations – Coralogix Blog.coralogix.comcoralogix.com (Explains why accuracy is misleading on imbalanced data and advocates using Precision-Recall AUC for class-imbalanced cases.)
- Sahoo et al. (2023). Data Leakage and Deceptive Performance: A Critical Examination of Credit Card Fraud Detection Methodologies (arXiv preprint) arxiv.org. (Highlights that recall is more appropriate than accuracy for fraud detection, given the high cost of false negatives.)
- NICE Actimize. (2024, November 11). Effective strategies for reducing false positives in transaction monitoring [Brochure]. Retrieved from https://www.niceactimize.com/Lists/Brochures/aml-reducing-false-positives-in-transaction-monitoring-brochure.pdf
- J.P. Morgan. (n.d.). False positives & fraud prevention tools. Retrieved from https://www.jpmorgan.com/insights/payments/analytics-and-insights/cnp-fraud-prevention-combat-chargebacks

* Notes for additional: reference where you got your content, media and extra help from. It is common practice to use code from other repositories and tutorials, however, it is important to be very specific about these sources to avoid plagiarism. 
* You can break the credits section up into Content and Media, depending on what you have included in your project. 

### Content 

- The text for the Home page was taken from Wikipedia Article A
- Instructions on how to implement form validation on the Sign-Up page was taken from [Specific YouTube Tutorial](https://www.youtube.com/)
- The icons in the footer were taken from [Font Awesome](https://fontawesome.com/)

### Media

- The photos used on the home and sign-up page are from This Open-Source site
- The images used for the gallery page were taken from this other open-source site


## Acknowledgements (optional)
* Thank the people who provided support through this project.
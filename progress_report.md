## PROJECT TITLE
**Streamlining pipeline of e-commerce customer query in chat** <br>
*by predicting product category and suggesting likely product in question*

## progress since last checkin and remaining tasks
### BERT: Predicting Product Category
Completed BERT models (weighted / unweighted `CrossEntropyLoss`)<br>
Accuracy scores on validation set:
- weighted=61.6
- unweighted=64.9

Created prediction notebook that loads model and predicts class of new input
#### todo (fri)
- Model evaluation Notebook
    - confusion matrix
    - f1-macro
    - [kappa score](https://towardsdatascience.com/multi-class-metrics-made-simple-the-kappa-score-aka-cohens-kappa-coefficient-bdea137af09c)
- Convert to flask service (sat)

### TFIDF Cosine Similarity / KNN clustering: Suggesting likely product in question (within predicted category)
Attempted Cosine similarity with acceptable results. Not sure if this is the best strategy for deployment as it requires TFIDF->CosSim entire corpus of a single category every time. KNN clustering might be more efficient in production.

#### todo (fri)
- Clustering notebook
- Pulling product names by asin using [this library](https://github.com/drawrowfly/amazon-product-api)
- postgres DB containing the tables:
    - `asin` / `combined_text` (if using cos sim) 
    - `asin` / `category` (might be redundant)
    - `asin` / `product_name`
- Flask service (sat)

### Microsite
User interface for demonstrating project. Undecided if I want to use a chat window UI or just a query page.
#### todo (sat-mon)
- react + material ui front end
    - landing page 
        - describes project
        - demo component
            - input component
            - message component
    - visualisation component
        - prediction visualisation component: D3 bar chart
        - most related words for each category
        - samples of misclassification for each category 
- Express server

### Presentation Deck
#### todo (tue)
- introduce motivation
- introduce business and DS problem
- success metric
    - prediction
    - deployability
    - usability
- snapshot of deployed site
- flow diagram
    - swimlanes: user_input - bot_response - backend(server, class_model, rec_model, db)
- describe BERT model
    - why bert? why other models were rejected
        - performance
        - deployability
    - intro to bert
    - describe model specifications and how they meet problem statement
        - 1.3m datums
        - 21 classes
        - model size
        - why weighted crossentropy only
        - why not over sampling
        - why not down sampling
        - why not over+under sampling
        - prediction values (**TO CHECK WITH CONOR MY UNDERSTANDING OF THE VALUES**)
    - evaluation
- describe suggestion model
    - explain why unsupervised instead of multiclass
    - **HOW DO I EVALUATE EFFICACY???**
- link to demo

### One useful thing you learnt from your project/teammates
- hy introduced cos sim
- huggingface library makes NLP so much easier
- considerations for deployment means I don't necessarily prioritise best scores
- SHOULD HAVE BOUGHT A LARGE INSTANCE instead of using my PC to train
- when using CUDA, you can't tell that it is maxing out your GPU capacity. but IT IS. so don't train concurrent models
- pytorch is harder than keras but easier than vanilla TF
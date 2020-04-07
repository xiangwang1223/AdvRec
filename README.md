# personalized recommendation
several algorithms for personalized recommendation


## Getting Started 
These instructions will get you a copy of the project up and running on your local machine for development and testing purpose.


### Prerequisites
You need the amazon-book/yelp2018/last-fm dataset for training and testing. To get one copy of that, take a look at [dataset](https://github.com/xiangwang1223/knowledge_graph_attention_network/tree/master/Data).
After you get the dataset, unzip the knowledge graph file.
```bash
unzip -x kg_final.txt.zip
```
Please bear in mind that this dataset directory should be put under `/Data`.
Then go to the `/Data` to prepare the test set, test sample and ground truth will be saved in pickle file.
```bash
python dump_v1.py
```
See configuration in `config/config.py` under `bprmf`, you can choose which dataset you want to dump.
Once finishing these processes, you are all set for data part.


### Installing
Just use the requirement file to prepare the environment, here we use python3.6.
```bash
pip install -r requirement.txt
```


### Train model
Currently we support three models, choose one and go to the corresponding directory.
```bash
python train.py
```
Just use this command to train a model, you can specify argument in command line, various parameters can be found at `config.py`.
I test model for every ten epochs. Both the best and the final model will be saved in `/output`. 

### Evaluate model
Typically, we saved our model under `/output`, and if you would like to test your own model, you should put your `.ckpt` file under that directory or specify the file path in command line.
```bash
python test.py --model_path output/best_model.ckpt
```
Use this command to test your model, all metric will be printed on screen.

### Result
dataset: yelp2018

|    Model    | Recall@20 | Hit ratio@20 | Precision@20 | NDCG@20 |
| :---------: | :-------: | :----------: | :----------: | :-----: |
|   BPR-MF    |  0.0488   |    0.1994    |    0.0118    | 0.0607  |
| Random walk |  0.0522   |    0.2134    |    0.0127    | 0.0643  |
|     DNS     |  0.0686   |    0.2601    |    0.0169    | 0.0839  |
|    IRGAN    |  0.0556   |    0.2203    |    0.0136    | 0.0814  |


dataset: amazon-book

|    Model    | Recall@20 | Hit ratio@20 | Precision@20 | NDCG@20 |
| :---------: | :-------: | :----------: | :----------: | :-----: |
|   BPR-MF    |  0.1214   |    0.2195    |    0.0128    | 0.0805  |
| Random walk |  0.1172   |    0.2153    |    0.0124    | 0.0772  |
|     DNS     |  0.1530   |    0.2638    |    0.0161    | 0.1047  |
|    IRGAN    |  0.1296   |    0.2311    |    0.0137    | 0.0920  |


dataset: last-fm

|    Model    | Recall@20 | Hit ratio@20 | Precision@20 | NDCG@20 |
| :---------: | :-------: | :----------: | :----------: | :-----: |
|   BPR-MF    |  0.0660   |    0.3065    |    0.0270    | 0.1056  |
| Random walk |  0.0670   |    0.3053    |    0.0275    | 0.1082  |
|     DNS     |  0.0876   |    0.3694    |    0.0361    | 0.1385  |
|    IRGAN    |  0.0615   |    0.3103    |    0.0268    | 0.1238  |

### Note
In this repo, we actually provide five types of sampling strategies for negative item sampling, you can using this by specifying parameters in dataset preparation
1. Random Sampling
2. Random walk in knowledge graph
3. Popularity based sampling
4. Dynamic sampling strategy
5. Adversarial sampling strategy

### Reference
[1] Rendle, Steffen, et al. "BPR: Bayesian personalized ranking from implicit feedback." Proceedings of the twenty-fifth conference on uncertainty in artificial intelligence. AUAI Press, 2009.

[2] Zhang, Weinan et al. “Optimizing top-n collaborative filtering via dynamic negative item sampling.” SIGIR (2013).

[3] Wang, Jun et al. “IRGAN.” Proceedings of the 40th International ACM SIGIR Conference on Research and Development in Information Retrieval - SIGIR  ’17 (2017): n. pag. Crossref. Web.

## Funding Source Acknowledgement

This research is supported by the National Research Foundation, Singapore under its International Research Centres in Singapore Funding Initiative. Any opinions, findings and conclusions or recommendations expressed in this material are those of the author(s) and do not reflect the views of National Research Foundation, Singapore.

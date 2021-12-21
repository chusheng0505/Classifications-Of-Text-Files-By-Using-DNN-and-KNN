# Classifications-Of-Chinese-Text-Files-By-Using-DNN-and-KNN
Try to use methods of KNN and DNN to classify categories of text files
I am trying to classify Chinese Text Files into specified categories(total 7 categories).

## Steps of Processing:
1. Feature_Extractions : TF-IDF is used as features of each texts
  1.1 Jieba module is used to split text in files
    1.1.1 Jieba.cut_for_search() is well performance in this trial
    1.1.2 Stopping_Words Dictionary is built by own
    1.1.3 Select top-K TF-IDF results (here, K = 10)
2. Word2Vec model is used 
3. Classifiers : KNN & DNN model

## Data:
1. Total 6804 files and split into training / validation / testing datasets with ratio 0.75:0.25
  1.1 Samples of files(here, category : 2社會):
![image](https://user-images.githubusercontent.com/55430748/146853940-b5ec018c-f22d-4c7a-bac8-9374068032d6.png)
  1.2 Categories of files :  ['0體育', '1房產', '2社會', '3星座', '4科技', '5娛樂', '6時尚']
  
## Parameters used:
1. KNN --> n = 5
2. DNN --> { epochs : 100 , batch_size : 16 , optimizer : Adam(lr = 1e-4) , loss_fn : category_crossentropy }
  2.1 Early_Stopping : { monitor : val_loss , patience : 5 }
  2.2 ReduceOnLr : { monitor : val_loss , patience : 5 , factor : 0.1 , min_lr : 1e-8 }

## Results:
1. DNN -- with training accuracy : 1.0
  ![image](https://user-images.githubusercontent.com/55430748/146854945-8054095e-0981-4fcb-b632-ea51f16f72d5.png)

 1.1 accuracy for testing sets : ~ 66.7 %
 Problems : For those failed to be classied,the word vectors results are worst and found that the TF-IDF results
            are strange too.
            
            For example , we get ['寧波', '志願', '願者', '志願者', '交通', '記者', '市民', '活動', '交通規則', '一邊'] TF-IDF 
            result and this file is belong to 0體育.But we can found that none of the elements in features are related to this category!
 ## In future,we may consider to modify a specified dictionary for each categories but not for common files.

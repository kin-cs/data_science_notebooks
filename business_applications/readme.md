Medicial
========

### applications
- diagnosis
- interpreting patient medical records
- drug discovery (e.g. AtomNet, ChemGAN)

#### Examples
- https://www.viz.ai/
  - medicial images diagnosis
- http://paigeai.com/
  - cancer detection

### Knowledge
- using adversarial autoencoder (AAE)
  - learn latent representation
- using Tensorflow Serving for deployment

Marketing
=========

### applications:
- content creation
  - real-time optimization content
- audience targeting (analyzing data and scoring them)

### example companies:
- appier
- insidesales
- **persado**: help you find the phrases and words which drive the better action for the audience
  - identify the language and emotions that resonate with consumers to increase engagement and build 

### Methods:
- Recommendation System for Audience Targeting
  - use LightFM
  - use TensorRec
- Content Creation
  - use LSTM
- Chatbot
  - using it in FB Messager, Telegram


Finance
=======

Ref
- Stock Price Prediction | AI in Finance - https://www.youtube.com/watch?v=7vunJlqLZok&list=PL2-dafEMk2A6oABirZ1Ug805Ag-8W54rN&index=3
  - [**IMPORTANT**] AI in Finance Notebook:  https://github.com/llSourcell/AI_in_Finance/blob/master/Market%20Prediction.ipyn

### applications
- fraud detection
- algo trade
  - e.g. platform https://numer.ai
- credit lending
  - e.g. https://www.zestfinance.com/zaml
- portfolio advisor


### example application - price prediction

Data Points to Use:
- Tweets about a company (good/bad)
- Reddit Posts (good/bad)
- News headlines about a company (good/bad)
- Past Prices
- All sorts of social media, blog posts
- All sorts of financial metadata (dividends, financial reports, etc)

### Possible Methods:
- linear regression
- SVM
- NN
- RL
  - https://doctorj.gitlab.io/sairen/
  
Fraud Prevention
----------------
ref: https://www.youtube.com/watch?v=UNgdIkuVC6g&list=PL2-dafEMk2A6oABirZ1Ug805Ag-8W54rN&index=4
[**important**] - https://medium.com/@curiousily/credit-card-fraud-detection-using-autoencoders-in-keras-tensorflow-for-hackers-part-vii-20e0c85301bd

### Using autoencoder for fraud detection
The concept is to train a good autoencoder for normal transaction, make the reconstruction error as low as possible. Then try to put the fradulent transactions into this autoencoder, this time the reconstruction error would be high, so that we can set a threshold to determine the fradulent transactions from the normal ones.

### examples companies:
- Jumio: face verification
- BioCatch: e.g. auto detect the machine input



### knowledge
- **TextBlob**: NLP tool, based on NLTK
  - https://www.analyticsvidhya.com/blog/2018/02/natural-language-processing-for-beginners-using-textblob/
  - language translation and detection which is powered by Google Translate
  - Sentiment Analysis
- **Sairen** - OpenAI Gym Reinforcement Learning Environment for the Stock Market (real-time)
- Quandl
- Numerai
  - data science competition in Finance

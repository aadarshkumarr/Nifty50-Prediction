# Nifty50-Prediction
Nifty50 Prediction is the act of trying to determine the future value of a Nifty50 companies stock or other financial instrument traded on a financial exchange. Just select the company name and click on Predict. You will get a graph of prediction for your selected company. We does not provide financial advice or personal investment to individuals, or act as personal financial, legal, or instututional investment advisors, or individually advocate the purchase or sale of any security or investment or the use of any particular financial strategies. Information is provided 'as-is' and solely for informational purposes and is not advice. We does not bear any responsibility for any losses or damage that may occur as a result of reliance on this data.

Stock Price Prediction of Nifty 50 Companies
Developer
Aadarsh Kumar
Content
Main Directory
Nifty-Prediction  

└───Nifty-50-Prediction
└───models
└───Screenshots
1. Documents Folder
Contains Reports, PPT and Project diaries of 7th and 8th semester.

Documents Directory

1. Nifty-50-Prediction Folder
Contains following Django Project files and folders.

Nifty-50-Prediction Directory

Nifty-50-Prediction
└───Stock_Prediction
└───lstm
└───stock
|   db.sqlite3
|   manage.py
|   nifty50Companies.csv 
Stock_Prediction
The Django project holds some configurations that apply to the project as a whole, such as project settings, URLs, shared templates and static files. Each application can have its own database and has its own functions to control how the data is displayed to the user in HTML templates.
Stock_Prediction Directory

Stock_Prediction
|   __init__.py
|   asgi.py
|   settings.py
|   urls.py
|   wsgi.py
lstm
It is special kind of recurrent neural network that is capable of learning long term dependencies in data. This is achieved because the recurring module of the model has a combination of four layers interacting with each other.
lstm Directory

lstm
|   RunModel.py
|   TrainModel.py
|   lstmModel_final.json
|   weights_final.h5
Our LSTM model
following code is from TrainModel.py

model = Sequential()
model.add(LSTM(64, activation='relu', return_sequences=True,input_shape=(n_steps, n_features)))
model.add(LSTM(64, activation='relu'))
model.add(Dense(1))
model.compile(optimizer='adam', loss='mse',)
model.fit(X, y, epochs=30, verbose=1)
Prediction for 30 days
following code is from RunModel.py

def getNext30Days(self):
        self.__inputHandler()
        dataset = self.data
        dataset = dataset['Close'].values
        dataset = dataset[len(dataset)-30:]
        n_features = 1
        n_steps = 30
        past_days = 30
        # demonstrate prediction for next 30 days
        x_input = np.array(dataset.tolist())
        temp_input = list(x_input)
        lst_output = []
        i = 0
        while(i < 30):

            if(len(temp_input) > past_days):
                x_input = np.array(temp_input[1:])
                x_input = x_input.reshape((1, n_steps, n_features))
                yhat = self.model.predict(x_input, verbose=0)
                temp_input.append(yhat[0][0])
                temp_input = temp_input[1:]
                lst_output.append(yhat[0][0])
                i = i+1
            else:
                x_input = x_input.reshape((1, n_steps, n_features))
                yhat = self.model.predict(x_input, verbose=0)
                temp_input.append(yhat[0][0])
                lst_output.append(yhat[0][0])
                i = i+1
        print(lst_output)
        predictions = lst_output
        return predictions
stock
A Django application is a Python package that is specifically intended for use in a Django project. An application may use common Django conventions, such as having models , tests , urls , and views submodules.
stock Directory

stock
└───migrations
└───templates
|   |   base.html
|   |   home.html
|   |   signup.html
|   __init__.py
|   admin.py
|   apps.py
|   forms.py
|   models.py
|   tests.py
|   views.py
db.sqlite3
SQLite3 is a software library that provides a relational database management system. The lite in SQLite means lightweight in terms of setup, database administration, and required resources. SQLite has the following noticeable features: self-contained, serverless, zero-configuration, transactional.
We are using sqlite3 for manageing User Authentication 

manage.py
A command-line utility that lets you interact with this Django project in various ways. You can read all the details about manage.py in django-admin and manage.py. The inner mysite/ directory is the actual Python package for your project.

nifty50Companies.csv
Csv file containing the list of nifty 50 companies with their respective symbol

2. models Folder
Contains experiments with models

models Directory

models
|   NiftyPrediction.ipynb
|   NiftyPrediction.ipynb
3. Screenshots Folder
Contains screenshots of the UI Home/Login Page | Signup Page :---:|:---:  | 

Prediction	News Section
	
Required Libraries
django Django is a high-level Python Web framework that encourages rapid development and clean, pragmatic design.
nsepy NSEpy is a library to extract historical and realtime data from NSE’s website.
sklearn Simple and efficient tools for predictive data analysis
tenserflow TensorFlow is an end-to-end open source platform for machine learning.
keras Keras is a deep learning API written in Python, running on top of the machine learning platform TensorFlow.
datetime The datetime module supplies classes for manipulating dates and times.

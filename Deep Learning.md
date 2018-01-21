# Neural Networks

## Single Layer Neural Networks

![Single Layer](http://neuroph.sourceforge.net/tutorials/images/perceptron.jpg)

![Perseptrons](https://codesachin.files.wordpress.com/2015/12/actfn001.jpg)

## Multi Layer Neural Networks

![Multi Layer](http://www.mdpi.com/sensors/sensors-09-02586/article_deploy/html/images/sensors-09-02586f6-1024.png)

![Function](https://www.analyticsvidhya.com/wp-content/uploads/2016/07/SLP.png)

## Aktivasyon Fonksiyonları

![Atiactivation Function](http://www.turingfinance.com/wp-content/uploads/2014/04/Activations-Functions.png)

![Relu](https://www.learnopencv.com/wp-content/uploads/2017/10/relu-activation-function-1.png)

# Keras ile Deep Learning

## Kanser Tespiti

https://archive.ics.uci.edu/ml/machine-learning-databases/breast-cancer-wisconsin/ 

Sitesinden 	*breast-cancer-wisconsin.data* dataset'imizi indiriyoruz.

    #-*-coding: cp1254-*-

    from keras.models import Sequential
    from keras.layers import Dense, Dropout, Activation
    import keras
    from keras.layers import Input, Dense
    from keras.optimizers import SGD

    from sklearn.preprocessing import Imputer
    import numpy as np
    import pandas as pd

    veri=pd.read_csv("breast-cancer-wisconsin.data") #Dataset'imizi okuduk.

    veri.replace('?', -99999, inplace=True)

    veriyeni=veri.drop(['1000025'],axis=1)

    imp=Imputer(missing_values=-99999,strategy="mean",axis=0)
    veriyeni=imp.fit_transform(veriyeni)

    giris=veriyeni[:,0:8] #input matrisi
    cikis=veriyeni[:,9] #output matrisi

    print giris.shape
    print cikis.shape

    model = Sequential() #Ardışık Model oluşturduk.
    #1. hiden Layer
    model.add(Dense(128,input_dim=8)) #Dense(Node Sayısı, input_dim=input sayısı)
    model.add(Activation('relu')) #Aktivasyon fonksiyonunu belirledik.
    #2. hiden Layer
    model.add(Dense(64))
    model.add(Activation('relu'))
    #Output Layer
    model.add(Dense(32))
    model.add(Activation('softmax')) #Output aktivasyon fonksiyonu "softmax" 'dir.

    model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])
    #ilk olarak optimizasyon fonksiyonumuzu belirledik, loss kayıp fonksiyonumuzu belirledik, metrics algoritmanın doğru yada yanlış yaptığını anlamasını sağlayacak yöntemi belirledik.

    model.fit(giris,cikis,epochs=5,batch_size=32,validation_split=0.13)
    #fit ile oluşturduğumuz modeli çalıştırma parametrelerini girdik.
    #epochs kaç defa sistemin eğitileceği
    #batch_size Tek seferde ne kadar verimizin ağdan geçeğini belirtir.
    #validation_split data setimizin % kaçını test için ayıracağımızı belirtiriz.

    #Eğitim çıktıları 
    #loss: Train verisi üzerindeki hata oranı
    #acc: Train verisi üzerindeki doğruluk oranı 
    #val_loss: test datasına göre hata oranı
    #val_acc: test datasına göre doğruluk oranı

    tahmin1=np.array([6,1,1,1,2,1,3,1]).reshape(1,8) #tahmin datası oluşturduk.
    print model.predict_classes(tahmin1) #oluşturduğumuz tahmin hatrisini modelimize verdik.

    tahmin2=np.array([10,5,5,3,6,7,7,10]).reshape(1,8)
    print model.predict_classes(tahmin2)
 
## Neural Network modeli Oluşturma

    model = Sequential() #Ardışık Model oluşturduk.
    
    model.add(Dense(128,input_dim=8)) #Dense(Node Sayısı, input_dim=input sayısı)
    model.add(Activation('relu')) #Aktivasyon fonksiyonunu belirledik.
    
    model.add(Dense(128,input_dim=8,activation='relu')) #Dense(Node Sayısı, input_dim=input sayısı, activation=Aktivasyon fonksiyonu) şeklinde tek satırda da oluşturulabilir.
    
## Aktivasyon Fonksiyonları

Bazı Aktivasyon fonksiyonları;

    model.add(Activation('relu'))
    model.add(Activation('sigmoid'))
    model.add(Activation('tanh'))
    model.add(Activation('linear'))
    model.add(Activation('softmax'))
    
Referans link: [Keras Aktivation Function](https://keras.io/activations/)  
    
## Hata(Loss) Fonsiyonları 
    
Bazı Hata Fonksiyonları;

mean_squared_error

![MSE](https://cdn-images-1.medium.com/max/1600/1*5B-_uIK9ULfzx5sV-aBmiA@2x.png)

mean_absolute_error

![MAE](http://www.statisticshowto.com/wp-content/uploads/2016/10/MAE.png)

root_mean_square_error

![RMSE](http://file.scirp.org/Html/htmlimages/5-2601289x/fcdba7fc-a40e-4019-9e95-aca3dc2db149.png)

Referans link: [Keras Loss Function](https://keras.io/losses/)
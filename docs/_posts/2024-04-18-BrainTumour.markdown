---
layout: post
title:  "Skin Lesion Classifier"
date:   2024-04-18 16:01:51 +0000       
categories: jekyll update
---
I have recently begun working on a Brain tumour segmentation task, the data for which can be found here.

Having researched the topic, I have decided to implement a U-net architecture, as it has been shown to work well on Biomedical data, due to its contracting and expanding layers joined together by skip connections. 

The relatively small dataset that I am working with (images), as well as computational limitations, have led me to decide that I will initially focus on scans with non-empty masks. The below pie chart shows that these make up less than half of the dataset, meaning data augmentation techniques were of paramount importance to stop overfitting. As such, I chose to randomly flip training images and their masks either horizontally or vertically (or both).

![PieChart](/assets/ScanDist.png)

Overall, this worked very effectively, with the test images below highlighting the performance of the model

![FinalImages](/assets/FinalImages.png)

My next step shall be to train a classifier, determining whether or not a scan contains a tumour and only passing it through the above model if the scan is classified as having a tumour. As ever, the performance of the model could be significantly improved with more training examples, although more computing power would almost certainly be necessary to avoid extreme training times. 

Another interesting step to take would be to introduce metadata about the scans which could improve the performance of the classifier especially. This could be introduced before the 


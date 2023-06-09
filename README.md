# DETR_model
I carried out the global wheat detection competition: https://github.com/marieGD00/DETR_model/edit/main/README.md where I used and then fine tuned Facebook's pre-trained resnet 50 DETR model to improve accuracy results from 69% to 75%. 
Fine tuning method:  

Realizing that loss weights were an effective way to control how the model performed I came across a paper named “Focal and Efficient IOU Loss for Accurate Bounding Box Regression” by Yi-Fan Zhang Weiqiang Renc, Zhang Zhang, Zhen Jiaa , Liang Wang, and Tieniu Tana. The FEIOU loss combines two components: the Focal loss and the IOU loss. The Focal loss is a modification of the cross-entropy loss function that down-weights the contribution of easy examples to the loss. 

It is defined as:

FL(pt) = - (1 - pt)^γ log(pt)
where pt is the predicted probability of the correct class, γ is a tunable parameter that controls the degree of down-weighting, and log denotes the natural logarithm. By using the Focal loss, the model can focus on hard examples and suppress the effect of easy examples, which can be useful in the presence of imbalanced data. To combine the Focal loss and the IOU loss, the authors propose a weighted sum of the two losses, where the Focal loss is multiplied by a factor λ that controls the balance between the two losses. The resulting FEIOU loss is defined as:
FEIOU(pt, p, t) = λ * FL(pt) + (1 - λ) * IOU(p, t). By implementing focal loss function for the “labels’,’boxes’ and cardinality losses with the addition of the class balance factor alpha and focusing parameter gamma for the boxes loss. We trained 8 epochs and reached a model accuracy of 0.75 which significantly beats our initial score of 0.69 with no fine tuning.


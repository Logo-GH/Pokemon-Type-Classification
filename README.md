# Pokemon-Type-Classification
Using CNN machine learning models to attempt to predict a pokemon's type just based off their image/sprite.

This project focuses on non-mutually exclusive multi-class labeling, as there are both monotypes and dual-types in pokemon.
This project pulls pokemon sprites from PokeAPI, separates them into test and training based on generation. In this instance the only generation used as the test set was generation 9. Augmentations are made on the sprites in order to fix a major issue with class imbalance. 

There are two .ipynb files included:
  - PyTorch_Pokemon_Project_github
  - Pytorch_Pokemon_Project_Shinies_github
Both files work independently of one another. The second one is just an expansion of this project where I added shiny sprites as well to be included in training. Important to note that these were kept and ran in separate folders. It is recommended to keep them in separate folders as there is overlap in terms of the file names they create. Can be kept in the same folder if that is addressed though. Make sure that in each folder you include the Typing_sprites folder. That contains images for all the different types, and is used for visuals within the code.

There are three major models used. A basic custom CNN, Resnet 18, and Resnet 50. In the Shinies file there is Resnet18, Resnet50, and custom Resnet 50 that has been fine tuned. They all used BCE with Logit Loss as their loss function.
Each model outputs 18 scores whose position is tied to a specific pokemon typing. A custom accuracy method is used due to the non-mutually exclusive multi-class labeling nature of predicting pokemon types. Exact:
  -For monotypes, exact accuracy comapares the true label to the highest probability prediction. If it is correct it assigns 2 points, if not 0
  -For dual-types, exact accuraces compare the top 2 predictions to the true label that will contain two values. For every match 1 point is awarded, for a maximum of 2 and minimum of 0.
  
Top K:
  -For monotypes, top k accuracy takes the top 3 predictions, and sees if the true label falls within those 3. The only requirement is that the predictions in the top 3 must be above 10% confidence, apart         from the top 1 selection as at least 1 type needs to be predicted for a monotype. If the true label falls within the predicted 3, 2 points are awarded
  -For dualtypes, top k accuracy takes the top 4 predictions, and sees if either of the values in the true label fall within those 4. The only requirement is that the predictions in the top 4 must be above       10% confidence, apart from the the top 2 selections as at least 2 types need to be predicted for a dual-type. 2 points awarded if both fall within the top 4, 1 point if 1 does, 0 if neither do.

Enjoy :)

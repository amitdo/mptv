# mptv
Tools necessary to perform a multi-fold pretrained voting approach utlizing OCRopus in order to significantly improve the achievable OCR error rate.  
Please note that this code was only used to provide a proof of concept for the publications listed below including the output of several (unnecessary) intermediate results.
In order to implement the concepts into an OCR workflow I **highly** recommend to use Christoph Wick's (@chwick) [Calamari](https://github.com/Calamari-OCR/calamari) which now natively supports cross fold training, confidence voting and pretraining.

## Installing

#### Clone Repository
`git clone https://github.com/chreul/mptv.git`

#### Setup and Activate Virtual Enviroment
`python -m pip install --user virtualenv`

`python -m virtualenv path/to/venv`

`source path/to/venv/bin/activate`

#### Install Requirements and Run MPTV Setup
`pip install -r requirements.txt`

`python setup.py install`


## Usage

### mptv-setup_folds
Input: image list (\*.png, \*.bin.png, \*.nrm.png, + corresponding GT (\*.gt.txt))  
Output: folder (--output, default: ./Data) with n (--folds, default = 5) sub folders which contain #lines/n lines  

The folder id gets placed in front of the line name in order to prevent overwriting of lines with the same name.

### mptv-run_multi_train
Input: folder containing the "Folds" sub folder.  
Output: "Models" folder which containes the trained models for each fold.

--models: "LH,LH,FRK,ENG,ENG" means that the first two folds starts training from LH fold 3 from ENG, and fold 4 and 5 from FRK with LH, ENG,  
and FRK being different mixed models from the pretraining folder.
"LH,,,,LH" starts the training of fold 1 and 5 from LH and trains the rest from scratch.

### mptv-find_best_model
Input: folder containing "Folds" and "Models" sub folders.  
Output: the best model of each fold stored in "Models/BestModels".

### mptv-recognize_lines
Input: folder(s) containing the to-be-predicted lines.  
Output: folder "Voting" in each input folder which contains the results (\*.txt and \*.extLlocs) for each fold.

### mptv-conf_vote  
Input: "Voting" folder(s) resulting from the preceding step.  
Output: "Voting/Voted" folders containing voted \*.txts.

## Corresponding Publications

### Cross Fold Training and Confidence Voting
[1] Reul, Springmann, Wick, Puppe. (2017). Improving OCR Accuracy on Early Printed Books by Utilizing Cross Fold Training and Voting. Accepted for the 13th IAPR International Workshop on Document Analysis Systems, [DAS2018](https://das2018.cvl.tuwien.ac.at/en/). Preprint available at [ArXiv e-prints](https://arxiv.org/abs/1711.09670).

```
@article{reul2017voting,
  title = {Improving {OCR} Accuracy on Early Printed Books by Utilizing Cross Fold Training and Voting},
  author = {Reul, Christian and Springmann, Uwe and Wick, Christoph and Puppe, Frank},
  journal = {ArXiv e-prints},
  url = {https://arxiv.org/abs/1711.09670},
  year = {2017}
}
```
### PreTraining/Transfer Learning
[2] Reul, Wick, Springmann, Puppe. (2017). Transfer Learning for {OCR}opus Model Training on Early Printed Books. 
027.7, Journal for Library Culture. Available [online](http://0277.ch/ojs/index.php/cdrs_0277/article/view/169).

```
@article{reul2017transfer,
  author = {Reul, Christian and Wick, Christoph and Springmann, Uwe and Puppe, Frank},
  title = {Transfer Learning for {OCR}opus Model Training on Early
		  Printed Books},
  journal = {027.7 Zeitschrift für Bibliothekskultur / Journal for
		  Library Culture},
  volume = {5},
  number = {1},
  year = {2017},
  pages = {38-51},
  url = {http://dx.doi.org/10.12685/027.7-5-1-169}
}

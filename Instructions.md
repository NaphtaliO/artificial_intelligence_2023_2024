Create a folder called images. Inside the folder, create subfolders, one per class. For example, a folder called cat and another called dog.
Obtain about 100 JPG images of each class and store them in the subfolders. How? One way is as follows:
In Chrome, install the Imageye extension.
In Chrome, do a Google image search for each class. E.g. first, an image search for "cat" and, later, an image search for "dog".
Run the Imageye extension. It will allow you to select which images you wish to download. You can click on Tools to make the menu bar appear; then, you can filter by Size (e.g. choose just the medium and large ones, to avoid downloading thumbnails) and by Type (e.g. choose just JPGs). Having applied these filters, you then click on Select all and then Download.
Clean your dataset.
Some ideas for doing this:

On a Mac, make sure you don't have any of those stupid .DS files or __MACOS folders.
Manually delete any of the downloaded images that are not JPGs.
Scan through the images manually and delete any that you think are not great examples. In my case, I would delete images that aren't good examples of cats or dogs.
Corrupted exif values may cause problems during training. Clean them using ExifTool by Phil Harvey.
To install:

Download it from https://github.com/exiftool/exiftool
Unzip it.
To run it:

Type:
$ ./exiftool-master/exiftool -r -all= -ext JPG -ext JPEG ./images
Look at the messages it spews out. If it complains about any of the images, then manually delete those images from your dataset.
ExifTool saves copies of the original images. Delete them by typing:
$ find ./images -type f -name '*jp*g_original*' -delete
If necessary, either supplement your dataset (i.e. manually download a few extra images to compensate for the ones that didn't download and the ones that you deleted) or prune your dataset (i.e. delete some). When you finish you should have 100 images of each class.
I have made available a program called partition_images.py on Canvas. Use it to split your dataset into three.
To install:

Remember to activate your virtual environment first.
Then install an extra library as follows:
$ pip install split-folders
To run, type (e.g.):

$ python3 partition_images.py images 0.5 0.25
In this CA, I recommend a 50%-25%-25% split, as above.

It creates three new folders: train, val and test.

Afterwards, when you're sure you're done, delete the images folder (or move it somewhere). You can also de-install the Chrome extension.

Create a Jupyter notebook called ai2_training.ipynb. In this Jupyter notebook, use transfer learning to build one or more neural network classifiers for your dataset. Your different classifiers may differ in their architectures (i.e. their layers), their learning rates, their use of data augmentation, and so on. (Of course, it is better if one classifier is motivated by failings of the previous one, e.g. if the previous one overfits, then the next one can try to remedy the overfitting.) Make sure your notebook includes markdown cells to explain what you are doing/why you are doing it/how you are doing it/etc. In the grading, this is just as important as the code.
The final cell of your notebook should save your best classifier to a file. If your best model is called best_network, for example, then the last cell of your notebook will contain the following:

best_network.save("best_network.h5")
Create a folder called examples. Into this folder, place up to 6 images. They might be copies of test set images; or they might be new images that you've downloaded from the web or that you've taken yourself; or a mixture. Either way, they should be carefully selected for use in step 8.
Create a Jupyter notebook called ai2_demo.ipynb. In this Jupyter notebook, use the images that you selected in step 7 to highlight some strengths and weaknesses of the classifier that you saved in step 6. Again use markdown cells to give me some narrative: why do you think it gets things right/why do you think it gets things wrong/etc.
Obviously one of the earliest cells of this notebook will need to load the classifier:

best_network = load_model("best_network.h5")
And another will need to load the images from the examples folder, e.g.:

path = "examples"
pathnames = [os.path.join(path, filename) for filename in sorted(os.listdir(path))]

imgs = [load_img(img_path, target_size=(224, 224)) for img_path in pathnames]
for img in imgs:
    plt.figure()
    plt.imshow(img)
On completion, you should have a folder that contains the following files:
ai2_training.ipynb
ai2_demo.ipynb
best_network.h5
and the following folders:

train
val
test
examples
and nothing else.
Zip this folder.

Before 11am on Monday 29th January 2024, submit your zip file using Canvas.

Notes:

You may use the Python libraries that I advised you to install at the start of the CS4618 module. If you want to install additional modules, they must be ones that can be installed using pip and you must list them in a cell at the start of your notebook(s).
All other code should be included in your notebook. No other files can be submitted.
I shall interrupt each of your notebooks if they haven't completed after 30 minutes on Google Colab using a GPU. Thirty minutes is an enormously generous limit. Do not feel compelled to fill 30 minutes. Thirty minutes of mindless experiments will get a lower grade than a faster piece of insightful work. You can comment-out things that you tried but which proved less fruitful.
You may borrow freely from the lecture handouts but otherwise the work must be your own. If you borrow snippets of code from elsewhere on the web, include a citation to the original source.
The work must be your own. All parties to collusion will be penalized; plagiarism (both deliberate and inadvertent) will meet with severe penalties, which may include exclusion from the University, as will fabrication and falsification of results. You may be called to discuss your submission with me and this will inform the grading, any penalties and any disciplinary actions.
Be aware that the use of ChatGPT or Copilot or similar tools to generate text, code or diagrams without clear attribution will be considered an academic offence equivalent to plagiarism.
Late submissions are not permitted.
To obtain higher grades, everything should be well-reasoned.
To obtain higher grades, you should attempt to 'push the envelope' - go beyond the bog-standard stuff from the lectures. E.g. do not expect a high grade if all you do is copy from lecture 22 of AI1.
Do not get stressed if the things you try do not improve the accuracy. The key to a good grade is to show me all the interesting things that you tried plus your reasoning.
And, to repeat: work on your own; do not share ideas or code; don't let others look at your solution. Everyone will have a unique solution.

G'luck,

Derek
